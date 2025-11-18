uboot是一款优秀的开源软件，我们学习uboot就是想shell那样，能够使用里面的一些基本命令就行了。

#### print

打印已经继承好了的环境变量，环境变量显示为：变量名=变量值

#### setenv，saveenv

设置环境变量（或者修改已有的环境变量，删除已有的环境变量），保存环境变量。

```shell
setenv abc 100 200	#在变量名abc后面一个空格后的所有字符串组成了abc这个变量
setenv abc 200 300	#修改已有的abc环境变量
setenv abc	#后面什么都不跟，删除abc环境变量

#上面的过程修改的环境变量都是放在内存中的，没有能够保存
saveenv		#把本次的设置的环境变量写回存储器
```

#### 网络搭建

uboot的网络层的设置与ipaddr变量名有关。

```shell
setenv ipaddr 192.169.100.110		#设置了本机的ip地址
ping		#一般都是开发板ping主机，uboot的ping功能不够完善（能够发出去，但是接受不到）
```

#### 网络传输层

uboot没有装载tcp协议，只有udp协议，也就是tftp协议。

在Windows或者linux创建一个服务端。Windows可以下载一个tftpd的服务包（一个可执行程序，执行即可）。

linux下，也是下载那个tftp包。32bit:`sudo apt-get isntall tftp-hpa`;	64bit:`sudo apt-get install tftp openbsc-xinetd`。可以使用`netstat -ua`来检查是否连接tftp成功。

==vi编辑文件的时候，会自动在末尾添加一个换行符==

`./client server_ip port xxxx`其中server_ip变成了通过环境变量serverip来获得。

```shell
setenv serverip 192.168.xxx.xxx		#设置服务端的ip地址
#端口不用设置，因为tftp已经默认了端口

#abc：表示要从 TFTP 服务器下载的文件名，即服务器上存在名为 abc 的文件，指令执行后会将该文件传输到设备的 20008000 内存地址处。
tftp 20008000 abc		
```

使用tftp可以把操作系统镜像等文件从服务端下载内核到开发板中，然后再启动内核即可。

#### nand

使用这个命令能够烧写，修改nanflash的命令的集合。

使用格式：`nand [动词] [内存地址] [nandflash的内部地址] [搬移大小]`。其中内存地址是源还是目的，要依据动词来判断，动词可以是read，write，erase。

```shell
#将nandflash中读取第5M数据写到内存的21000000中，数据量为1k
nand read 21000000 500000 1024

#flash的特性就是写之前必须先擦除，所以说在write之前要做一个擦除操作
nand erase 500000 1024		#注意指令格式
```

#### bootm、go

bootm用于启动内核（多用与uImage）。go命令可以将pc指针指向一个指定的地方。

内核的名称:

1. uImage（包含内核也包含和uboot相关的东西），Image，bzImage。他们都是一块数据，只是数据压缩的格式不一样。

先利用tftp将内核文件下载到开发板，然后再使用命令。在使用命令之前有一些内核启动的前提条件。

#### 内核启动条件

需要一个环境变量来衔接内核与uboot，这个环境变量是bootargs。

需要设置设备信息，比如Ram，NFS，flash。指定根文件在哪里，即指定root。

所有的进程组成的是一个树状关系。这些进程最后对应了一个根节点，即init进程。有了这个进程之后，只要fork就可以在这个进程下创建新的进程。

设置控制台，即console。

```shell
root=		#还需要设置，启动的根文件系统在哪儿
inti=		#内核启动后，第一个可执行文件，即init进程从哪里来
console=		#内核启动时，使用哪个设备作为控制台
setenv bootargs root=/dev/mtdblock2 init=/linuxrc console=ttySAC0,115200
saveenv bootargs		#保存设置
```

#### 文件系统的烧写

1. NFS，映射到内存中，在开发过程中这种方法居多。这种方法实际上是在服务器中存储了实际的数据，当客户端访问的时候，就会从服务器下拉文件，即按量访问。

   服务端安装和配置nfs服务：

   ```shell
   #安装
   sudo apt-cache search nfs-		#搜索nfs服务
   sudo apt-get install nfs-kernel-server		#安装nfs服务
   
   #配置:		/etc/exports
   sudo vi /etc/exports
   	#修改里面的文件，第一列填写需要共享的目录，第二列填写
   	#文件内容如下示例：
   #*号代表任意ip可访问，rw代表权限，sync表示同步，最后一个是安全机制，我们不需要，所以no_check
   /home/rocky/work/rootfs		*(rw,sync,no_subtree_check)
   
   #重启服务生效
   sudo etc/init.d/nfs-kernel-server restart
   ```

   客户端配置：

   1. 先设置nfsroot，他为服务端的ip地址，还有后面的目录是主机共享出的目录路径。

   2. 因为在uboot启动之后，uboot下设置的环境变量中的ip自然是失效了，所有我们需要重新设置客户端的ip，也就是ip。
   3. 然后设置init和console。

   ```shell
   
   setenv bootargs root=/dev/nfs nfsroot=192.168.10.110:/home/rocky/work/rootfs ip=192.168.10.122 init=/linuxrc console=ttySAC0,115200
   
   saveenv
   
   tftp 20008000 uImage		#下载内核
   
   bootm 20008000
   ```

2. Ramdisk，利用网线，在产上线的时候多使用这种方法。内存磁盘，把文件系统的内容在ram上运行起来。

   需要提前将根文件系统的压缩包放到initrd指定的地址上。

   ```shell
   root=/dev/ram
   initrd=0x21000000,8M		#设置ram设备的设备信息，也就是指定根文件系统的位置还有大小
   init=/linuxrc
   console=ttySAC0
   
   setenv bootargs roto=/dev/ram initrd=0x21000000,8M init=/linuxrc console=ttySAC0,115200		#设置环境变量
   saveenv
   bootm 20008000		#开启内核，专用于uImage
   ```

#### 系统上电自运行



 ```shell
 setenv bootdelay		#删掉这个变量，系统上电之后就不会傻傻地等待了
 setenv bootcmd			#只要将这个变量设置为uboot开启内核的那些命令，uboot就会上电自己运行那些程序了，也就是达到了系统上电自运行的效果
 saveenv
 ```



























