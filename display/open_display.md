##### 语法

* `Display *XOpenDisplay(display_name)`
  * `char *display_name`

##### 参数

* 在符合`POSIX`标准的系统中，若`display_name`为`NULL`，则默认为`DISPLAY`环境变量的值
* `hostname:number.screen_number`
  * `hostname` 指定显示器物理连接的主机的名称。可以在主机名后面加上单冒号（:）或双冒号（::）
  * `number` 指定该主机上的显示服务器的编号。可以选择在这个显示器号码后面加上一个句号(.)
    * 一个CPU可以有一个以上的显示器。多个显示器的编号通常从0开始
  * `screen_number` 指定该服务器上要使用的屏幕。多个屏幕可以由一个X服务器控制
    * 设置了一个内部变量，可以通过使用`DefaultScreen()`宏或`XDefaultScreen()`函数（使用的是C语言以外的语言）进行访问（见 "显示宏"）
* `dual-headed:0.1`
  * 在名为 "dual-headed "的机器上显示0的屏幕1

##### 描述

* `XOpenDisplay`函数返回一个Display结构，该结构作为与X服务器的连接，包含关于该X服务器的所有信息。`XOpenDisplay()`通过TCP或DECnet通信协议，或通过一些本地进程间通信协议，将你的应用程序连接到X服务器
* 如果主机名是一个主机名，并且用一个冒号（:）来分隔主机名和显示号，`XOpenDisplay()`就会使用TCP流进行连接。如果没有指定主机名，`Xlib`使用它认为最快的传输方式
* 如果主机名是一个主机名，并且用双冒号（::）分开主机名和显示号，`XOpenDisplay()`使用DECnet连接
* 一台X服务器可以同时支持任何或所有这些传输机制。一个特定的`Xlib`实现可以支持这些传输机制中的许多种

##### 返回值

* 如果成功，`XOpenDisplay()`返回一个指向Display结构的指针，该结构在`X11/Xlib.h`中定义
  * 显示器中的所有屏幕都可以被客户端使用
  * display_name参数中指定的屏幕编号由`DefaultScreen()`宏（或`XDefaultScreen()`函数）返回
  * 只能通过使用信息宏或函数来访问显示和屏幕结构的元素
* 不成功，它返回NULL
* X服务器可以实现各种类型的访问控制机制（见 "控制主机访问"）

