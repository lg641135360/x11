##### 两种方式选择想要报告给客户程序的事件

* 在调用`XCreateWindow()`和`XChangeWindowAttributes()`时设置`XSetWindowAttributes`结构的`event_mask`成员
* 使用`XSelectInput()`

