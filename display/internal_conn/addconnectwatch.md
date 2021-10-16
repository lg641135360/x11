##### 语法

```c
typedef void (*XConnectionWatchProc)(display, client_data, fd, opening, watch_data)
      Display *display;
      XPointer client_data;
      int fd;
      Bool opening;
      XPointer *watch_data;

Status XAddConnectionWatch(display, procedure, client_data)
      Display *display;
      XWatchProc procedure;
      XPointer client_data;
```

##### 参数

* display 指定与X服务器的连接。
  procedure 指定要被调用的过程。
  client_data 指定额外的客户端数据。

##### 描述

* 注册了一个**过程**，当`Xlib`为指定的显示器打开或关闭内部连接时，该过程将被调用
* 该过程会被传递给显示器
  * 指定`client_data`，连接的文件描述符，一个指示连接是否被打开或关闭的布尔值，以及一个指向私有监视数据位置的指针
* 如果`Opening`为`True`，这个存储过程可以在`watch_data`所指向的位置存储一个指向私有数据的指针
* 当这个存储过程后来被调用，并且`Opening`为`False`时，`watch_data`所指向的位置将保持这个相同的私有数据指针
* 函数可以在一个显示被打开后的任何时候被调用
  * 如果内部连接已经存在，在`XAddConnectionWatch()`返回之前，将立即为每个连接调用注册的程序
  * 如果程序成功注册，`XAddConnectionWatch()`返回一个非零状态
  * 否则，它返回零
* 注册的过程不应该调用任何`Xlib`函数
  * 如果该过程直接或间接地导致内部连接或监视程序的状态改变，其结果将不被定义
  * 如果`Xlib`已经为线程进行了初始化，那么在调用该过程时将锁定显示器，并且该过程对任何锁定显示器的`Xlib`函数的调用结果不会被定义，除非执行线程已经使用`XLockDisplay()`在外部锁定了显示器

