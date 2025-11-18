# dispatch
## delay
###### mdelay
这个是直接卡在那里，直接延时。
###### schdule_timeout
使用这个函数进行延迟之前要设置模式，使用set_current_state()，参数输入一些宏能够设置延时模式。这个设置函数设置的是线程的状态，而非某个函数的状态，可以设置为运行状态，可打断，不可打断等等。
不使用这个设置函数的情况下，是处于运行状态的，也就是说其他线程无法打算这个线程，也就无法进行调度。
参数输入HZ为延时一秒。
###### set_current_state
1. 函数意义：
	1Linux 内核中用于一个关键函数，用于设置当前进程的运行状态。进程状态决定了进程是否可被调度、是否能被信号唤醒等核心行为，是内核进程管理和调度的基础。

2. 下面是输入参数及其含义：
	TASK_RUNNING	运行状态：进程可被调度执行（正在运行或在运行队列中等待 CPU）。
	TASK_INTERRUPTIBLE	可中断休眠：进程暂停运行，等待某个事件（如 I/O 完成、信号），可被信号唤醒。
	TASK_UNINTERRUPTIBLE	不可中断休眠：进程暂停运行，等待某个事件，但不能被信号唤醒（用于必须等待的场景，如磁盘 I/O）。
	TASK_KILLABLE	可杀死的休眠：类似 TASK_UNINTERRUPTIBLE，但可被致命信号（如 SIGKILL）唤醒。
	TASK_STOPPED	停止状态：进程被信号（如 SIGSTOP）暂停，需 SIGCONT 恢复。
	EXIT_ZOMBIE	僵尸状态：进程已终止，但父进程未回收其资源（仅保留 PID 和退出状态）。
3. 作用：
	控制进程调度：除 TASK_RUNNING 外，其他状态的进程会被移出运行队列，不再参与 CPU 调度，直到状态被改变。
	配合休眠 / 唤醒机制：进程进入休眠前必须设置状态（如 TASK_INTERRUPTIBLE），再通过 schedule() 或 schedule_timeout() 主动放弃 CPU。
###### kthread_stop
这个函数会设置一个标志位来告诉内核线程该退出了
所以我们在创建的内核线程里面要加一个判断kthread_should_stop()，使用这个函数就能够判断内核线程是否应该返回了，当函数的返回值为真的时候，就代表创建的内核线程应该返回了。
## sleep
# thread
## thread
## kthread
