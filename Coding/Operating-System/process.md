---
tags: []
---

# 进程 _Process_



## 进程状态与转化

如下图,以Linux为例

![进程状态转化图](/assets/process-states-in-operating-system.gif)

Linux里面进程有五种运行状态：R、S、T、D、Z

- 运行状态（TASK_RUNNING）
指正在被CPU运行或者就绪的状态。这样的进程被成为runnning进程。运行态的进程可以分为3种情况：内核运行态、用户运行态、就绪态。

- 可中断睡眠状态（TASK_INTERRUPTIBLE）
处于等待状态中的进程，一旦被该进程等待的资源被释放，那么该进程就会进入运行状态。

- 不可中断睡眠状态（TASK_UNINTERRUPTIBLE）
该状态的进程只能用wake_up()函数唤醒。

- 暂停状态（TASK_STOPPED）
当进程收到信号SIGSTOP、SIGTSTP、SIGTTIN或SIGTTOU时就会进入暂停状态。可向其发送SIGCONT信号让进程转换到可运行状态。

- 僵死状态（TASK_ZOMBIE）
当进程已经终止运行，但是父进程还没有询问其状态的情况。


注意：

只有当进程从“内核运行态”转移到“睡眠状态”时，内核才会进行进程切换操作。在内核态下运行的进程不能被其它进程抢占，而且一个进程不能改变另一个进程的状态。为了避免进程切换时造成内核数据错误，内核在执行临界区代码时会禁止一切中断。 