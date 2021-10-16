> 应用程序不应直接修改显示和屏幕结构的任何部分。
>
> 这些**成员**应该被认为是**只读**的，尽管它们可能**因为对显示的其他操作而发生变化**

* `AllPlanes == unsigned long XAllPlanes() `

  * 返回一个所有位都设置为1的值，适合作为程序的平面参数使用

* `BlackPixel WhitePixel`

  * `BlackPixel() and WhitePixel()`

  * 实现单色的应用程序

  * 这些像素值是为默认颜色映射中永久分配的条目

  * 实际的`RGB`（红、绿、蓝）值在某些屏幕上是可以设置的，而且在任何情况下，实际上可能不是黑色或白色

  * 这些名称是为了传达预期的颜色的相对强度

  * ```c
    BlackPixel(display, screen_number)
    
    unsigned long XBlackPixel(display, screen_number)
          Display *display;
          int screen_number;
    ```

    * display 指定与X服务器的连接
    * screen_number 指定主机服务器上适当的屏幕号
    * 两者返回指定屏幕的黑色像素值

  * ```c
    WhitePixel(display, screen_number)
    
    unsigned long XWhitePixel(display, screen_number)
          Display *display;
          int screen_number;
    ```

    * 同上

* `ConnectionNumber`

  * `ConnectionNumber(display)`

  * ```c
    int XConnectionNumber(display)
          Display *display;
    ```

    * display 指定与X服务器的连接
    * 两者都返回指定显示器的连接号，Linux下是连接的文件描述符

* `DefaultColormap`

  * `DefaultColormap(display, screen_number)`

  * ```c
    Colormap XDefaultColormap(display, screen_number)
          Display *display;
          int screen_number;
    ```

    * display 指定与X服务器的连接
    * screen_number 指定主机服务器上适当的屏幕号
    * 两者都返回默认的`colormap ID`，用于在指定的屏幕上分配
    * 大多数常规的颜色分配都应该从这个颜色映射中进行

* `DefaultDepth`

  * ```c
    DefaultDepth(display, screen_number)
    
    int XDefaultDepth(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * display 指定与X服务器的连接

  * screen_number 指定主机服务器上适当的屏幕编号

  * 两者都返回指定屏幕的默认根窗口的深度（平面的数量）

  * 这个屏幕上也可能支持其他深度（见`.PN XMatchVisualInfo `）

* `XListDepths`

  * 确定给定屏幕上可用的深度数

  * ```c
    int *XListDepths(display, screen_number, count_return)
          Display *display;
          int screen_number;
          int *count_return;
    ```

    * display 指定与X服务器的连接
    * screen_number 指定主机服务器上适当的屏幕编号
    * count_return 返回深度的数量

  * 函数返回指定屏幕上可用的深度数组

    * 如果指定的screen_number是有效的，并且可以为该数组分配足够的内存，`XListDepths()`将count_return设置为可用深度的数量
    * 否则，它不设置count_return并返回NULL。要释放分配给深度数组的内存，请使用`XFree()`

* `DefaultGC`

  * ```c
    DefaultGC(display, screen_number)
    
    GC XDefaultGC(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回**指定屏幕的根窗口**的**默认图形上下文**

    * `GC`是为了方便简单的应用而创建的，它包含默认的`GC`组件，前景和背景像素值分别初始化为屏幕的黑色和白色像素
    * 可以自由地修改它的内容，因为它没有被用于任何`Xlib`函数

  * `GC`不应该被释放

* `DefaultRootWindow`

  * ```c
    DefaultRootWindow(display)
    
    Window XDefaultRootWindow(display)
          Display *display;
    ```

  * 返回默认屏幕的根窗口

* `DefaultScreenOfDisplay`

  * ```c
    DefaultScreenOfDisplay(display)
    
    Screen *XDefaultScreenOfDisplay(display)
          Display *display;
    ```

  * 返回一个**指向默认屏幕**的**指针**

* `ScreenOfDisplay`

  * ```c
    ScreenOfDisplay(display, screen_number)
    
    Screen *XScreenOfDisplay(display, screen_number)
          Display *display;
    ```

  * 返回一个指向指定屏幕的指针

* `DefaultScreen`

  * ```c
    DefaultScreen(display)
    
    int XDefaultScreen(display)
          Display *display;
    ```

  * 返回由`XOpenDisplay()`函数引用的**默认屏幕号**

  * 这个宏或函数应该被用来在只使用一个屏幕的应用程序中检索屏幕号

* `DefaultVisual`

  * ```c
    DefaultVisual(display, screen_number)
    
    Visual *XDefaultVisual(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回指定屏幕的**默认视觉类型**

* `DisplayCells`

  * ```c
    DisplayCells(display, screen_number)
    
    int XDisplayCells(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回默认颜色映射中的条目数

* `DisplayPlanes`

  * ```c
    DisplayPlanes(display, screen_number)
    
    int XDisplayPlanes(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回**指定屏幕**的**根窗口的深度**

* `DisplayString`

  * ```c
    DisplayString(display)
    
    char *XDisplayString(display)
          Display *display;
    ```

  * 返回当前显示被打开时传递给`XOpenDisplay()`的字符串

  * 如果传递的字符串是NULL，这些返回当前显示被打开时DISPLAY环境变量的值

  * 对于调用fork系统调用并希望从子进程打开一个新的连接到同一个显示器的应用程序是很有用的，也可以用于打印错误信息

* `XExtendedMaxRequestSize`

  * ```c
    long XExtendedMaxRequestSize(display)
    	Display *display;
    ```

  * 如果指定的显示器不支持扩展长度的协议编码，`XExtendedMaxRequestSize()`函数返回0

  * 否则，它返回服务器使用扩展长度编码支持的最大请求大小（以4字节为单位）

    * `Xlib`函数`XDrawLines()`, `XDrawArcs()`, `XFillPolygon()`, `XChangeProperty()`, `XSetClipRectangles()`, 和`XSetRegion()`将根据需要使用扩展长度编码，如果服务器支持
    * 其他`Xlib`函数（例如`XDrawPoints()`, `XDrawRectangles()`, `XDrawSegments()`, `XFillArcs()`, `XFillRectangles()`, `XPutImage()`）中使用扩展长度编码是允许的，但不是必须的

  * `Xlib`实现可以选择**将数据分成多个小请求**来代替

* `XMaxRequestSize`

  * ```c
    long XMaxRequestSize(display)
    	Display *display;
    ```

  * 返回服务器支持的**最大请求大小**（以4字节为单位），而不使用扩展长度的协议编码

  * 除非服务器支持扩展长度的协议编码，否则对服务器的单一协议请求不能大于这个大小

  * 协议保证该大小不小于4096个单位（16384字节）

  * Xlib会根据以下函数的需要自动将数据分解成多个协议请求

    * `XDrawPoints()`, `XDrawRectangles()`, `XDrawSegments()`, `XFillArcs()`, `XFillRectangles()`, and `XPutImage()`

* `LastKnownRequestProcessed`

  * ```c
    LastKnownRequestProcessed(display)
    
    unsigned long XLastKnownRequestProcessed(display)
         Display *display;
    ```

  * 提取`Xlib`已知的被X服务器处理的最后一个请求的完整序列号

    * 当收到回复、事件和错误时，`Xlib`会自动设置这个数字

* `NextRequest`

  * ```c
    NextRequest(display)
    
    unsigned long XNextRequest(display)
         Display *display;
    ```

  * 提取将用于下一次请求的完整序列号

  * 序列号为每个显示器连接单独维护

* `ProtocolVersion`

  * ```c
    ProtocolVersion(display)
    
    int XProtocolVersion(display)
          Display *display;
    ```

  * 返回与连接的显示器相关的X协议的主要版本号（11）

* `ProtocolRevision`

  * ```c
    ProtocolRevision(display)
    
    int XProtocolRevision(display)
          Display *display;
    ```

  * 返回X服务器的次要协议修订号

* `QLength`

  * ```c
    QLength(display)
    
    int XQLength(display)
          Display *display;
    ```

  * 返回连接的显示器的事件队列的长度

  * 可能有更多的事件还没有被读入队列（见`XEventsQueued()`）

* `RootWindow`

  * ```c
    RootWindow(display, screen_number)
    
    Window XRootWindow(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回根窗口

    * 对于需要特定屏幕的drawable的函数和创建顶层窗口很有用

* `ScreenCount`

  * ```c
    ScreenCount(display)
    
    int XScreenCount(display)
          Display *display;
    ```

  * 返回可用屏幕的数量

* `ServerVendor`

  * ```c
    ServerVendor(display)
    
    char *XServerVendor(display)
          Display *display;
    ```

  * 返回一个指向空头字符串的指针，该字符串提供了对X服务器实现的所有者的一些标识

  * 如果服务器返回的数据是拉丁文可移植字符编码，那么这个字符串就是主机可移植字符编码。

  * 否则，该字符串的内容取决于实现

* `VendorRelease`

  * ```c
    VendorRelease(display)
    
    int XVendorRelease(display)
          Display *display;
    ```

  * 返回一个与供应商发布的X服务器有关的数字

