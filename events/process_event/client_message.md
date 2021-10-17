> **X服务器**只有在**客户端调用`XSendEvent()`函数**时才会**产生`ClientMessage`事件**

##### 事件结构

```c
typedef struct {
	int type;			/* ClientMessage */
	unsigned long serial;		/* # of last request processed by server */
	Bool send_event;		/* 如果这是来自SendEvent请求，则为true */
	Display *display;		/* 事件是从哪个显示器上读取的 */
	Window window;
	Atom message_type;
	int format;
	union {
		char b[20];
		short s[10];
		long l[5];
	        } data;
} XClientMessageEvent;
```

* `message_type`成员被设置为一个原子，表示接收客户端应该如何解释数据。

* `format`成员被设置为8、16或32，并指定数据是否应被看作是字节、短线或长线的列表
* 数据成员是一个联合体，包含成员b、s和l。
  * b、s和l成员代表20个8位数值、10个16位数值和5个32位数值的数据。
  * 特定的消息类型可能不会使用所有这些值。
* X服务器不会对`window`、`message_type`或`data`成员中的值进行解释

