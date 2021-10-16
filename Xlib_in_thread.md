> 在有线程的系统中，可以提供支持以允许多个线程同时使用`Xlib`

* 初始化对并发线程的支持，[`XInitThreads`](./thread/init.md)
* 在多个`Xlib`调用中锁定一个显示，[`XLockDisplay`](./thread/lock_display.md)
* 解锁之，[`XUnlockDisplay`](./thread/unlock_display.md)

