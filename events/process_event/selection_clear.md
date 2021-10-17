> X服务器向失去选择所有权的客户端报告`SelectionClear`事件
>
> 当**另一个客户端**通过调用`XSetSelectionOwner()`宣称对选择的所有权时，X服务器会产生这种事件类型

##### 事件结构

```c
typedef struct {
	int type;		/* SelectionClear */
	unsigned long serial;	/* # of last request processed by server */
	Bool send_event;	/* true if this came from a SendEvent request */
	Display *display;	/* Display the event was read from */
	Window window;
	Atom selection;
	Time time;
} XSelectionClearEvent;
```



* 选择成员被设置为选择原子。
* 时间成员被设置为选择所记录的最后一次改变时间。
* window成员是当前所有者（失去选择的所有者）在其`XSetSelectionOwner()`调用中指定的窗口

