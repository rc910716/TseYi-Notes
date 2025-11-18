# input子系统框架

###### input子系统仍然是一个字符设备驱动程序
input子系统将一个驱动分为三层：handler,core,device。这种关系仍然可以像设备树那样分出两层，一个设备相关层，一个处理层用来处理各种事件，使用core（核心）层来注册这些结构体。
输入子系统的设备相关信息和处理层相匹配，就相当于总线里面的device和driver相匹配，而这个子系统又做了许多的封装。同样的，注册device的时候，device也会对handler一一查找并试图进行匹配。
也就是说在input子系统里面对于字符设备和总线进行了一层抽象。
大概步骤：
	1. 先进行匹配，并创建句柄，input_handle,这个结构体存储了device和handler，device和handler的结构体都有一个链表存储了input_handler，也就是说device和handler可以通过input_handle桥接找到对方。（这里所说的存储指的是能够通过这个结构体找到那两个东西，并非物理意义上的存储）。注意与总线的不同，这里可以多个device对应多个handler，并非总线里面的一对多，而是多对多的关系，在双方的结构体里面都使用链表存储了所有的“多”。如果匹配成功就会使用connect函数。
	2.匹配成功，就会使用handler里面的函数处理事件，优先使用filter函数来处理事件。如果提供event或者events，就使用他们来处理事件。  


