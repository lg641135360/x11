##### 语法

```c
Status XRemoveConnectionWatch(display, procedure, client_data)
      Display *display;
      XWatchProc procedure;
      XPointer client_data;
```

##### 参数

* display 指定与X服务器的连接
  procedure 指定要被调用的过程
  client_data 指定额外的客户端数据

##### 描述

* 删除了一个先前注册的连接监视过程
* `client_data`必须与该存储过程最初注册时使用的`client_data`一致

