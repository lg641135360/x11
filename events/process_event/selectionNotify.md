> 当选择没有所有者时，这个事件由X服务器响应`ConvertSelection`协议请求而产生
>
> 当有一个所有者时，它应该由选择的所有者通过使用`XSendEvent()`来产生
>
> 当一个选择被转换并存储为一个属性时，或者当一个选择转换不能被执行时（通过将属性成员设置为None表示），选择的所有者应该向请求者发送这个事件
>
> 如果在`ConvertSelection`协议请求中指定None作为属性，所有者应该选择一个属性名称，将结果作为该属性存储在请求者窗口中，然后发送一个`SelectionNotify`，给出该实际属性名称

##### 事件结构

```c
typedef struct {
	int type;		/* SelectionNotify */
	unsigned long serial;	/* # of last request processed by server */
	Bool send_event;	/* true if this came from a SendEvent request */
	Display *display;	/* Display the event was read from */
	Window requestor;
	Atom selection;
	Atom target;
	Atom property;		/* atom or None */
	Time time;
} XSelectionEvent;
```

* 请求者成员被设置为与选择的请求者相关的窗口。
* 选择成员被设置为表示选择的原子。
  * 例如，PRIMARY用于主要选择。
* 目标成员被设置为表示转换类型的原子。
  * 例如，PIXMAP用于像素图。
* 属性成员被设置为表示结果被存储在哪个属性上的原子。
  * 如果转换失败，属性成员被设置为无。
* 时间成员被设置为转换发生的时间，可以是一个时间戳或`CurrentTime`。

