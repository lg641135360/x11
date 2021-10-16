##### 语法

```c
void XLockDisplay(display)
      Display *display;
```

##### 参数

* display 指定与X服务器的连接

##### 说明

* 锁定了所有其他线程对指定显示器的使用
  * 试图使用该显示器的其他线程将被阻止，直到该显示器被该线程解锁
* 可以嵌套使用该函数
* 当`XUnlockDisplay()`被调用的次数与`XLockDisplay()`相同时，显示器才会**真正被解锁**
* 使用`XInitThreads()`成功地初始化了`Xlib`的线程，否则这个函数没有作用

