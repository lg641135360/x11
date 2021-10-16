> 获得有关显示器、图像格式或屏幕的信息

* 提供一些宏和相应函数，从`Display`结构中返回数据
  * [显示宏](./display_macros.md)
  * [图像格式宏](./image_format_macros.md)
  * [屏幕宏](./screen_macros.md)

* `Display`结构的所有其他成员（也就是那些没有定义宏的成员）都是`Xlib`的私有成员，不得使用。
  * 应用程序决不能直接修改或检查`Display`结构的这些私有成员



