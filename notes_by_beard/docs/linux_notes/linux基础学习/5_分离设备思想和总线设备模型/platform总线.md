###### 虚拟总线platform
这是系统提供的一条总线，因为一个驱动程序总是有两部分，一部分是driver——驱动，device——设备相关，所以说这条总线就分出了两部分，一部分是前者，一部分是后者，分别使用链表进行管理，而这两者又可以是相互对应的。
当我们注册一个driver的时候，他会与所有的device链表成员一一使用匹配规则进行匹配，如果匹配成功，就会注册字符驱动设备。同样的，我们也可以先注册device，这样的话，device就会与driver一一进行匹配了，直到匹配成功就会进行注册字符驱动设备操作。其中的注册字符驱动设备操作是通过.probe函数进行的。
###### platform并不是唯一的总线
在linux上面，还有usb_bus、i2c_bus、spi_bus。
###### 这种driver和device的设计思想并不是独属于platform的
理论上，任何可以分出一些固定不变代码和设备相关的情况都可以使用这套设计思想来实现。
###### driver和device的对应关系
一个driver是可以对应多个device的，但是一个device只对应一个driver（只是说device对应多个driver是不合理的，实际上能不能这样做我还不知道）。
###### 这样分层的好处
在device里面可以定义那些设备相关的变量，这样就使得模块更加抽象化，另外对于这种抽象化模块的作用对象的修改变得十分容易，不像原来学习的那种写驱动方式，只能够写死（当然那种写法可以通过一些手段来避免这样的事情，比如说应用程序输入参数来的方式，但是这在一般场合是不会这样使用的，因为写应用程序的人不一定懂这些参数具体该怎么写），大大提高了驱动程序的灵活性。
举个例子，原来的写法就是将uart0抽象为一个模块，但是像uart1我就必须再为他写一个驱动了，这样十分的不方便，而总线的这种写法就是将所以操作相似的uart外设全部抽象为一个模块，把这个抽象出来的东西写到上面所说的driver里面去，而在device里面决定具体使用哪个串口以及一些其他的特殊信息。device里面就抽象了一些模块相似的东西为一个模块，device就抽象了这些模块之间的不同的东西，当出现这种情况的时候，就可以采用这种总线分层的思想来写，不一定是驱动。
###### 匹配方法（match）
默认使用的就是对两个结构体的name成员进行比较的匹配方法，如果说想要多个device匹配同一个driver的话，这种匹配方式肯定不行（因为在这种匹配过程中，会根据这个name创建一些文件夹或者文件，如果两个device一样的话，就会导致同名文件的创立，这种情况显然是不允许的），所以说我们需要深入研究这两者之间的匹配方法。
```c
struct bus_type platform_bus_type = {
	.name		= "platform",
	.dev_groups	= platform_dev_groups,
	.match		= platform_match,
	.uevent		= platform_uevent,
	.pm		= &platform_dev_pm_ops,
};

//下面是match函数
static int platform_match(struct device *dev, struct device_driver *drv)
{
	struct platform_device *pdev = to_platform_device(dev);
	struct platform_driver *pdrv = to_platform_driver(drv);

	/* When driver_override is set, only bind to the matching driver */
	//第一种办法：这里就说明了只要设置driver_override的值就可以强制绑定到固定的driver上去。
	//也就是说强制使用这个名字来看跟driver匹配不匹配
	if (pdev->driver_override)
		return !strcmp(pdev->driver_override, drv->name);

	/* Attempt an OF style match first */
	//第二种办法：设备树
	if (of_driver_match_device(dev, drv))
		return 1;

	/* Then try ACPI style match */
	//第三种方法：比较老了，不常用
	if (acpi_driver_match_device(dev, drv))
		return 1;

	/* Then try to match against the id table */
/*第四种方法：这种方法就是提前在id_table成员里面存储能匹配的name，只要devic
的name和这些设置的name值其中的一个相等就能够匹配成功。*/
	if (pdrv->id_table)
		return platform_match_id(pdrv->id_table, pdev) != NULL;

	/* fall-back to driver name match */
/*第五种方法：使用他们两个的名称来进行匹配，也就是默认的方法，如果上面的情况都不满足的话就会进入到这里来。*/
	return (strcmp(pdev->name, drv->name) == 0);
}

```
如果一个设备已经匹配了驱动的话，再次匹配会失败。










