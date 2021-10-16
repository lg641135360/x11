> 应用程序需要以服务器要求的格式向X服务器**提交数据**
>
> 为了帮助简化应用程序，大部分**转换数据**的工作由`Xlib`提供（见 "在客户端和服务器之间传输图像 "和 "操纵图像"）

##### 各种满足X服务器要求的结构体

* `XPixmapFormatValues`

  * ```c
    typedef struct {
    	int depth;
    	int bits_per_pixel;
    	int scanline_pad;
    } XPixmapFormatValues;
    ```

  * 连接设置时返回的像素图格式信息

* `XListPixmapFormats`

  * 获得一个给定显示器的像素图格式信息

  * ```c
    XPixmapFormatValues *XListPixmapFormats(display, count_return)
          Display *display;
          int *count_return;
    ```

    * display 指定与X服务器的连接
    * count_return 返回显示器所支持的像素图格式的数量

  * 返回一个`XPixmapFormatValues`结构数组，描述指定显示器支持的**Z格式图像的类型**

  * 如果可用的内存不足，`XListPixmapFormats`返回NULL

  * 要释放分配给`XPixmapFormatValues`结构的存储，请使用`XFree()`

---

##### C语言的宏，对应函数是为其他语言绑定的，都为指定的服务器和屏幕返回什么数据，经常作为工具包以及简单的应用程序所利用

* `ImageByteOrder`

  * ```c
    ImageByteOrder(display)
    
    int XImageByteOrder(display)
          Display *display;
    ```

  * `XY`格式（位图）的每个扫描线单元或Z格式的每个像素值的图像指定所需的字节顺序

  * 该宏或函数可以返回`LSBFirst`或`MSBFirst`

* `BitmapUnit`

  * ```c
    BitmapUnit(display)
    
    int XBitmapUnit(display)
          Display *display;
    ```

  * 返回位图的扫描线单位的大小，单位是比特

  * 扫描线是以这个值的倍数计算的

* `BitmapBitOrder`

  * ```c
    BitmapBitOrder(display)
    
    int XBitmapBitOrder(display)
          Display *display;
    ```

  * 在每个位图单元内，屏幕上显示的位图中最左边的位是该单元中最不重要的位或最重要的位
  * 可以返回`LSBFirst`或`MSBFirst`

* `BitmapPad`

  * ```c
    BitmapPad(display)
    
    int XBitmapPad(display)
          Display *display;
    ```

  * 每个扫描线必须被填充到这个宏或函数返回的比特的倍数

* `DisplayHeight`

  * ```c
    DisplayHeight(display, screen_number)
    
    int XDisplayHeight(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回一个整数，描述屏幕的高度，单位是像素

* `DisplayHeightMM`

  * ```c
    DisplayHeightMM(display, screen_number)
    
    int XDisplayHeightMM(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回指定屏幕的高度，单位是毫米

* `DisplayWidth`

  * ```c
    DisplayWidth(display, screen_number)
    
    int XDisplayWidth(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回屏幕的宽度，单位是像素

* `DisplayWidthMM`

  * ```c
    DisplayWidthMM(display, screen_number)
    
    int XDisplayWidthMM(display, screen_number)
          Display *display;
          int screen_number;
    ```

  * 返回指定屏幕的宽度，单位是毫米

