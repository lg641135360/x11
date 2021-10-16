##### 语法

```c
void XProcessInternalConnection(display, fd)
      Display *display;
      int fd;
```

##### 参数

* display 指定与X服务器的连接。
  `fd` 指定文件描述符

##### 说明

* 处理一个内部连接上的可用输入
* 只有在操作系统设施（例如，选择或轮询）表明输入是可用的之后，才能为内部连接调用该函数
* 否则，其效果就无法定义

