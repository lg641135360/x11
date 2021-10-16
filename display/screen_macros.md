> 需要一个指向相应屏幕结构的指针

* `BlackPixelOfScreen`

  * ```c
    BlackPixelOfScreen(screen)
    
    unsigned long XBlackPixelOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的黑色像素值

* `WhitePixelOfScreen`

  * ```c
    WhitePixelOfScreen(screen)
    
    unsigned long XWhitePixelOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的白色像素值

* `CellsOfScreen`

  * ```c
    CellsOfScreen(screen)
    
    int XCellsOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的默认颜色贴图中的颜色贴图单元的数量

* `DefaultColormapOfScreen`

  * ```c
    DefaultColormapOfScreen(screen)
    
    Colormap XDefaultColormapOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的默认`Colormap`

* `DefaultDepthOfScreen`

  * ```c
    DefaultDepthOfScreen(screen)
    
    int XDefaultDepthOfScreen(screen)
          Screen *screen;
    ```

  * 返回根窗口的深度

* `DefaultGCOfScreen`

  * ```c
    DefaultGCOfScreen(screen)
    
    GC XDefaultGCOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的默认图形上下文（`GC`），它的深度与屏幕的根窗口相同

  * `GC`决不能被释放

* `DefaultVisualOfScreen`

  * ```c
    DefaultVisualOfScreen(screen)
    
    Visual *XDefaultVisualOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的默认视觉

* `DoesBackingStore`

  * ```c
    DoesBackingStore(screen)
    
    int XDoesBackingStore(screen)
          Screen *screen;
    ```

  * 返回一个值，表明该屏幕是否支持背部存储

  * 返回的值可以是`WhenMapped`、`NotUseful`或`Always`中的一个（见 "Backing Store Attribute"）

* `DoesSaveUnders`

  * ```c
    DoesSaveUnders(screen)
    
    Bool XDoesSaveUnders(screen)
          Screen *screen;
    ```

  * 返回一个布尔值，表明该屏幕是否支持保存下划线

* `DisplayOfScreen`

  * ```c
    DisplayOfScreen(screen)
    
    Display *XDisplayOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的显示

* `XScreenNumberOfScreen`

  * ```
    XScreenNumberOfScreen()
    
    int XScreenNumberOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的屏幕索引号

* `EventMaskOfScreen`

  * ```c
    EventMaskOfScreen(screen)
    
    long XEventMaskOfScreen(screen)
          Screen *screen;
    ```

  * 连接设置时返回指定屏幕的根窗口的事件掩码

* `WidthOfScreen`

  * ```c
    WidthOfScreen(screen)
    
    int XWidthOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的宽度，单位是像素

* `HeightOfScreen`

  * ```c
    HeightOfScreen(screen)
    
    int XHeightOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的高度，单位是像素

* `WidthMMOfScreen`

  * ```c
    WidthMMOfScreen(screen)
    
    int XWidthMMOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的宽度，单位是毫米

* `HeightMMOfScreen`

  * ```c
    HeightMMOfScreen(screen)
    
    int XHeightMMOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的高度，单位是毫米

* `MaxCmapsOfScreen`

  * ```c
    MaxCmapsOfScreen(screen)
    
    int XMaxCmapsOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕所支持的最大的已安装的颜色贴图数量（见 "管理已安装的颜色贴图"）

* `MinCmapsOfScreen`

  * ```c
    MinCmapsOfScreen(screen)
    
    int XMinCmapsOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕所支持的最小的已安装的颜色贴图的数量（见 "管理已安装的颜色贴图"）

* `PlanesOfScreen`

  * ```c
    PlanesOfScreen(screen)
    
    int XPlanesOfScreen(screen)
          Screen *screen;
    ```

  * 返回根窗口的深度

* `RootWindowOfScreen`

  * ```c
    RootWindowOfScreen(screen)
    
    Window XRootWindowOfScreen(screen)
          Screen *screen;
    ```

  * 返回指定屏幕的根窗口

