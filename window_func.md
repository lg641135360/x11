> 在X窗口系统中，一个**窗口**是屏幕上的一个**矩形区域**，可以让你**查看图形输出**
>
> 客户端程序可以在一个或多个屏幕上显示重叠和嵌套的窗口，这些**窗口**由一台或多台机器上的**X服务器驱动**
>
> 想要创建窗口的客户端必须首先通过调用`XOpenDisplay()`将他们的程序**连接到X服务器**

##### 基础知识

* [视觉类型](./window/Basic_knowledge/Visual_Types.md)
* [窗口属性](./window/Basic_knowledge/window_attr.md)

##### `API` `todo` 暂时不需要

* [创建窗口](./window/create.md)
* [销毁窗口](./window/destory.md)
* [映射窗口](./window/map.md)
* [取消映射窗口](./window/unmap.md)
* [配置窗口](./window/conf.md)
* [改变堆叠顺序](./window/change_the_stacking_order.md)
* [改变窗口属性](./window/change_win_attrs.md)

指出一些可能产生事件的窗口操作

* 应用程序必须符合**与窗口管理器**进行**通信的既定惯例**，这样它才能与使用中的各种窗口管理器很好地工作（见 "客户端与窗口管理器的通信 "一节）
* 工具包通常为你遵守这些惯例，减轻了你的负担

