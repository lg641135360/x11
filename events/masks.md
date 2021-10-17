> 客户端选择报告一个窗口的大多数事件
>
> 要做到这一点，需要将一个事件掩码传递给`Xlib`事件处理函数，该函数需要一个event_mask参数

* 定义在`X11/X.h`中
* 掩码中的**每个位**都映射到**一个事件掩码名称**，它描述了你**希望X服务器返回**给客户端应用程序的事件
  * 除非客户端特别要求它们，否则大多数事件在产生时不会报告给客户端
  * 通过将`GC`中的图形曝光设置为False来抑制它们，否则`GraphicsExpose`和`NoExpose`默认会作为`XCopyPlane()`和`XCopyArea()`的结果报告
* `SelectionClear`, `SelectionRequest`, `SelectionNotify`或`ClientMessage`不能被屏蔽
* 与选择有关的事件只发送给与选择合作的客户端（见 "选择 "一节）
* 当键盘或指针映射被改变时，`MappingNotify`总是被发送到客户端

##### 常用掩码

| 事件掩码                   | 情况                                       |
| -------------------------- | ------------------------------------------ |
| `NoEventMask`              | 不需要事件                                 |
| `KeyPressMask`             | 键盘向下的事件                             |
| `KeyReleaseMask`           | 键盘向上事件                               |
| `ButtonPressMask`          | 指针式按钮向下事件                         |
| `ButtonReleaseMask`        | 指针式按钮上升事件                         |
| `EnterWindowMask`          | 指针式窗口进入事件                         |
| `LeaveWindowMask`          | 指针式窗口离开事件                         |
| `PointerMotionMask`        | 指针运动事件                               |
| `PointerMotionHintMask`    | 指针式运动提示                             |
| `Button1MotionMask`        | 按钮1向下时的指针运动                      |
| `Button2MotionMask`        | 按钮2向下时的指针运动                      |
| `Button3MotionMask`        | 按钮3向下时的指针式运动                    |
| `Button4MotionMask`        | 按钮4向下时的指针运动                      |
| `Button5MotionMask`        | 按钮5向下时的指针运动                      |
| `ButtonMotionMask`         | 任何一个按钮向下时的指针运动               |
| `KeymapStateMask`          | 窗口进入和聚焦时需要的键盘状态             |
| `ExposureMask`             | 任何需要的曝光                             |
| `VisibilityChangeMask`     | 任何需要的可见性变化                       |
| `StructureNotifyMask`      | 窗口结构的任何变化                         |
| `ResizeRedirectMask`       | 重定向调整此窗口的大小                     |
| `SubstructureNotifyMask`   | 结构通知                                   |
| `SubstructureRedirectMask` | 重定向对子结构的请求                       |
| `FocusChangeMask`          | 输入焦点变化                               |
| `PropertyChangeMask`       | 属性变化                                   |
| `ColormapChangeMask`       | 颜色图的任何变化                           |
| `OwnerGrabButtonMask`      | 当owner_events设置为True时，自动抓取被激活 |

