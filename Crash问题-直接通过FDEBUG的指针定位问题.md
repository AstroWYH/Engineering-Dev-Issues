# Crash问题-直接通过F DEBUG的指针定位问题

### 问题描述

集成侧传入frame，正常拍照crash，addr2line定位为SDK内部代码模块，但带有集成侧传入的output_frame指针。

### 解决方法

如果对SDK内部代码模块有信心，则可直接排查该output_frame指针是否为F DEBUG中crash的地址，即可直接确定错误位置，如下图所示。

```c
LOG: ..., output_data addr:0xffffffff
F DEBUG: ..., fault addr 0xffffffff
```

