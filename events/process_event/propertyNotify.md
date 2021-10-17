> X服务器可以将`PropertyNotify`事件报告给**想要了解**指定**窗口的属性变化信息**的客户
>
> * 接收`PropertyNotify`事件，在窗口的事件掩码属性中设置`PropertyChangeMask`位

##### 事件结构

```c
typedef struct {
	int type;		/* PropertyNotify */
	unsigned long serial;	/* # 服务器处理的最后一个请求的数量 */
	Bool send_event;	/* 如果这是来自SendEvent请求，则为true  */
	Display *display;	/* 事件是从哪个显示器读取的 */
	Window window;
	Atom atom;
	Time time;
	int state;		/* PropertyNewValue or PropertyDelete */
} XPropertyEvent;
```

* 窗口成员被设置为其相关属性被改变的窗口

* atom成员被设置为属性的atom，并指出哪个属性被改变或需要
* 时间成员被设置为该属性被改变时的服务器时间
* 状态成员被设置为指示该属性是否被改变为新值或被删除，可以是`PropertyNewValue`或`PropertyDelete`
  * 当使用`XChangeProperty()`或`XRotateWindowProperties()`改变窗口的一个属性时（甚至当使用`XChangeProperty()`添加零长度的数据时），以及使用`XChangeProperty()`或`XRotateWindowProperties()`用相同的数据替换一个属性的全部或部分时，状态成员被设置为`PropertyNewValue`。
* 当使用`XDeleteProperty()`或（如果删除参数为True）`XGetWindowProperty()`删除窗口的一个属性时，状态成员被设置为`PropertyDelete`

