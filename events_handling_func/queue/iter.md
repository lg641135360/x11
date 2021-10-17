> 这里的每个函数都要求传递一个**谓词过程**，用来确定一个事件是否符合想要的东西
>
> * 谓词过程必须在不调用任何`Xlib`函数的情况下决定该事件是否有用
> * 如果`Xlib`已经为线程进行了初始化，那么在调用predicate的时候会锁定显示器，并且除非调用者首先调用`XLockDisplay()`，否则predicate对任何锁定显示器的`Xlib`函数的调用结果不会被定义

##### 函数定义

```c
Bool (*predicate)(display, event, arg)
     Display *display;
     XEvent *event;
     XPointer arg;
```

##### 参数

* display 指定与X服务器的连接
* event 指定`XEvent`结构
* `arg` 指定从`XIfEvent()`、`XCheckIfEvent()`或`XPeekIfEvent()`函数传入的参数

##### 调用规则

* 谓词程序对队列中的**每个事件都要调用一次**，直到**找到一个匹配的事件**
  * 找到一个匹配后，谓词程序必须返回True
  * 如果没有找到匹配，则必须返回False
* 使用`XIfEvent()`来检查事件队列中是否有匹配的事件，如果**找到**，则从**队列中删除该事件**
* 使用`XCheckIfEvent()`来检查事件队列中是否有匹配的事件，而不进行阻塞
* 检查事件队列中的匹配事件而不从队列中移除事件，使用`XPeekIfEvent()`



#### 使用窗口或事件掩码选择事件

> 允许不按顺序处理事件

* 移除同时符合窗口和事件掩码的下一个事件，请使用 `XWindowEvent()`
* 删除下一个与窗口和事件掩码（如果有的话）相匹配的事件，请使用`XCheckWindowEvent()`
* 移除与事件掩码相匹配的下一个事件，使用`XMaskEvent()`
* 返回并移除与事件掩码相匹配的下一个事件（如果有的话），使用`XCheckMaskEvent()`
* 返回和删除队列中与事件类型相匹配的下一个事件，使用`XCheckTypedEvent()`
* 返回并删除队列中与事件类型和窗口相匹配的下一个事件，请使用`XCheckTypedWindowEvent()`

#### 将事件放回队列

* 把一个事件推回到事件队列中，请使用`XPutBackEvent()`

##### 发送事件到其他应用程序

* 使用`XSendEvent()`来发送一个事件到**指定的窗口**
  * 被用于选择处理
  * 例如，当一个选择被转换并存储为一个属性时，选择的所有者应该使用`XSendEvent()`向请求者发送一个`SelectionNotify`事件

