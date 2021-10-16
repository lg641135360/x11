##### 语法

```c
Status XInternalConnectionNumbers(display, fd_return, count_return)
      Display *display;
      int **fd_return;
      int *count_return;
```

##### 参数

* display 指定与X服务器的连接
* `fd_return` 返回文件描述符
* `count_return` 返回文件描述符的数量

##### 描述

* 返回当前为指定显示器**打开的**所有内部连接的**文件描述符的列表**
* 当不再需要分配的列表时，用`XFree()`释放它
* 如果列表被成功分配，该函数返回一个非零状态；否则，它返回零

