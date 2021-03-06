> 关闭一个显示器或断开与X服务器的连接

* `XCloseDisplay()`
* `Xlib`允许客户端所拥有的**资源**在客户端的**连接关闭后继续存在**
  * 要改变客户端的关闭模式，使用`XSetCloseDownMode()`

---

##### 关闭连接时X服务器的操作

* 取消了客户端拥有的所有选择（见`XSetSelectionOwner()`）
* 如果客户端主动抓取指针或键盘，它将执行`XUngrabPointer()`和`XUngrabKeyboard()`
* 如果客户端抓取了服务器，它将执行`XUngrabServer()`
* 释放所有由客户端进行的被动抓取
* 根据关闭模式是`RetainPermanent`还是`RetainTemporary`，它将客户端分配的所有资源（包括`colormap`条目）标记为永久或临时
  * 并不妨碍其他客户端应用程序明确地销毁这些资源（见`XSetCloseDownMode()`)

##### 关闭模式是`DestroyAll`时，X服务器销毁资源的方式

* 检查客户端保存集中的每个窗口，以确定它是否是**客户端创建的窗口的下级（子窗口）**
  * (保存集是一个其他客户的窗口列表，被称为保存集窗口)
  * 如果是这样，X服务器会将保存的窗口重新parent到最接近的祖先，这样保存的窗口就不会是客户端创建的窗口的下级
  * 重置后，保存窗口的左上角的绝对坐标（相对于根窗口）保持不变
* 如果保存设置的窗口没有被映射，它将对保存设置的窗口执行`MapWindow`请求
  * 即使保存设置的窗口不是由客户创建的窗口的下级，X服务器也会这样做
* 销毁了所有由客户创建的窗口
* 对客户端在服务器中创建的每个非窗口资源（例如，字体、Pixmap、游标、`Colormap`和`GContext`）执行适当的释放请求
* 释放所有由客户端应用程序分配的颜色和颜色表项
* 当最后一个与X服务器的连接关闭时，会有额外的处理
  * 一个X服务器会经历一个没有连接和有一些连接的周期

当与X服务器的最后一个连接因关闭`close_mode`为`DestroyAll`的连接而关闭时，X服务器会做以下工作

* 重置其状态，就像它刚刚被启动一样
  * X服务器开始销毁所有在`RetainPermanent`或`RetainTemporary`模式下终止的客户端的残留资源
* 除了预定义的原子标识符外，它删除了所有的原子标识符
* 删除了所有根窗口的所有属性（见 "属性和原子 "一节）
* 重设所有设备映射和属性（例如，按键、铃声和加速）以及访问控制列表
* 恢复了标准的根标示和光标
* 恢复了默认的字体路径
* 将输入焦点恢复到`PointerRoot`状态

如果你在关闭模式设置为`RetainPermanent`或`RetainTemporary`的情况下关闭一个连接，X服务器不会重置

