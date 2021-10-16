```c
XFree(data)
     void *data; 
```

* data 指定要被释放的数据
* 通用的`Xlib`例程，释放指定的数据
* 用它来释放任何由`Xlib`分配的对象，除非为该对象明确指定了一个替代的函数
* 不能传NULL参数