> X服务器向选区的所有者报告`SelectionRequest`事件
>
> 每当客户端通过调用`XConvertSelection()`来请求**转换所拥有的选择**时，X服务器就会生成这个事件

##### 事件结构

```c
typedef struct {
	int type;		/* SelectionRequest */
	unsigned long serial;	/* # of last request processed by server */
	Bool send_event;	/* true if this came from a SendEvent request */
	Display *display;	/* Display the event was read from */
	Window owner;
	Window requestor;
	Atom selection;
	Atom target;
	Atom property;
	Time time;
} XSelectionRequestEvent;
```

* owner成员被设置为当前所有者在其`XSetSelectionOwner()`调用中指定的窗口。
* 请求者成员被设置为请求选择的窗口。
* 选择成员被设置为命名该选择的原子。
  * 例如，PRIMARY被用来表示主要的选择。
* 目标成员被设置为表示希望选择的类型的原子。
* 属性成员可以是一个属性名称或无。
* 时间成员被设置为来自`ConvertSelection`请求的时间戳或`CurrentTime`值。 
* 所有者应该根据指定的目标类型转换选择，并向请求者发送一个`SelectionNotify`事件。
  * 关于使用选择的完整规范在X Consortium标准的客户间通信约定手册中给出

