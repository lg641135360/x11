> 在你的程序可以**使用一个显示器之前**，你必须建立一个**与X服务器的连接**
>
> 建立连接之后，才能使用`xlib`宏和函数来返回有关显示的信息

* [打开一个**连接**到显示器](./display/open_display.md)
* [获取关于显示器、图像格式和屏幕的信息](./display/obtain_info.md)
* [释放客户端创建的数据](./display/free_client_data/free_data.md)
* [关闭（断开）一个显示器](./display/close_display/close.md)

最后对关闭与X服务器的连接时发生的情况进行讨论

[生成一个`NoOperation`协议请求](./XNoOp.md)

[在线程中使用`Xlib`](./Xlib_in_thread.md)

---

除了与X服务器的连接外，`Xlib`的实现还可能需要与其他类型的服务器的连接（例如，与输入法服务器的连接，如 "地域和国际化文本函数 "中所述）

* 使用多个显示器的工具箱和客户端，或者使用显示器与其他输入相结合的工具箱和客户端，需要获得这些**额外的连接**，以正确地阻止直到输入可用，并需要在输入可用时处理该输入
* 在`Xlib`事件函数中使用**单个显示器**并阻止输入的简单客户端**不需要使用这些设施**

> * 跟踪一个显示器的内部连接，使用[`XAddConnectionWatch()`](/display/internal_conn/addconnectwatch.md)
> * 要停止跟踪一个显示器的内部连接，使用[`XRemoveConnectionWatch()`](/display/internal_conn/removeconnectwatch.md)
> * 要处理一个内部连接上的输入，使用[`XProcessInternalConnection()`](./display/internal_conn/processinternalconn.md)
> * 要获得一个显示器的所有当前内部连接，使用[`XInternalConnectionNumbers()`](/display/internal_conn/internalconnnum.md)

