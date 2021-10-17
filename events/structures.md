对于每个事件类型，在`X11/Xlib.h`中都声明了一个相应的结构。所有的事件结构都有以下共同的成员。

```c
typedef struct {
	int type;
	unsigned long serial;	/* # of last request processed by server */
	Bool send_event;	/* true if this came from a SendEvent request */
	Display *display;	/* Display the event was read from */
	Window window;
} XAnyEvent;
```

##### 成员

* 类型成员被设置为**唯一标识**的事件类型常量名称
  * 例如，当X服务器向客户端应用程序报告一个`GraphicsExpose`事件时，它会发送一个`XGraphicsExposeEvent`结构，其类型成员被设置为`GraphicsExpose`
* `display`成员被设置为指向**事件被读取的显示器的指针**
  * 如果事件来自`SendEvent`协议请求，`send_event`成员将被设置为`True`
* `serial`成员被设置为协议中报告的序列号，但从16位的最小有效位扩展为完整的32位值
* 窗口成员被设置为对工具包调度员最有用的窗口

##### 发送事件时机

* X服务器可以在**输入流的任何时候**发送事件
* `Xlib`将在等待回复时收到的任何事件存储在一个事件队列中，供以后使用
* `Xlib`还提供了一些函数，允许你**检查事件队列中的事件**（见 "事件队列管理 "一节）

##### `XEvent union`

* 所有定义事件的联合体

* 使用`XEvent union`来访问每个事件的成员

```c
typedef union _XEvent {
	int type;	/* must not be changed */
	XAnyEvent xany;
	XKeyEvent xkey;
	XButtonEvent xbutton;
	XMotionEvent xmotion;
	XCrossingEvent xcrossing;
	XFocusChangeEvent xfocus;
	XExposeEvent xexpose;
	XGraphicsExposeEvent xgraphicsexpose;
	XNoExposeEvent xnoexpose;
	XVisibilityEvent xvisibility;
	XCreateWindowEvent xcreatewindow;
	XDestroyWindowEvent xdestroywindow;
	XUnmapEvent xunmap;
	XMapEvent xmap;
	XMapRequestEvent xmaprequest;
	XReparentEvent xreparent;
	XConfigureEvent xconfigure;
	XGravityEvent xgravity;
	XResizeRequestEvent xresizerequest;
	XConfigureRequestEvent xconfigurerequest;
	XCirculateEvent xcirculate;
	XCirculateRequestEvent xcirculaterequest;
	XPropertyEvent xproperty;
	XSelectionClearEvent xselectionclear;
	XSelectionRequestEvent xselectionrequest;
	XSelectionEvent xselection;
	XColormapEvent xcolormap;
	XClientMessageEvent xclient;
	XMappingEvent xmapping;
	XErrorEvent xerror;
	XKeymapEvent xkeymap;
	long pad[24];
} XEvent;
```

* 联合体第一个成员是**类型成员**，被设置成**事件类型**
* 第二个成员总是产生该事件的协议**请求的序列号**
* 第三个成员总是`send_event`，它是一个`Bool`，表示该事件是否**由不同的客户端发送**
* 第四个成员总是一个显示器，它是**事件被读取的显示器**
* 除了`keymap`事件，第五个成员总是一个窗口，这是经过精心挑选的，对工具包调度员有用

> 前五个的顺序不能改变

* 大多事件还包含一个**时间成员**，代表事件**发生的时间**

* 此外，在用于访问结构中的任何其他信息之前，必须对通用事件的指针进行投递

