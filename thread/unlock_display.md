##### 语法

```c
void XUnlockDisplay(display)
      Display *display;
```

##### 参数

* display 指定与X服务器的连接

##### 说明

* 允许其他线程再次使用指定的显示器
* 如果`XLockDisplay()`被一个线程调用了多次，那么在显示器真正被解锁之前，`XUnlockDisplay`必须被调用同等次数
* 只有使用了`XInitThreads()`成功地初始化了Xlib的线程，该函数才有效

