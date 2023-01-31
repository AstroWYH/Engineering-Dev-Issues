## malloc_debug简介

malloc_debug是**Android平台自带**的调试工具，与其他内存检测工具原理类似，使用调试函数替换标准c库中的malloc/free等内存操作相关函数，每次申请释放内存的时候都对内存做标记，当内存泄漏或越界的时候，会记录相关信息。

## malloc_debug使用介绍

在adb shell中需要去设置的属性

- adb shell setprop libc.debug.malloc.options "backtrace guard leak_track verbose backtrace_dump_on_exit backtrace_dump_prefix=/sdcard/heap"
- adb shell setprop libc.debug.malloc.program xxx(程序名)

### 参数介绍

- backtrace: 代表开启堆栈记录。
- guard: 开启内存越界检测。
- leak_track: 程序在退出时，如有内存泄漏，而不产生abort。
- backtrace_dump_on_exit: 程序退出时dump堆栈和内存信息。
- backtrace_dump_prefix: dump文件存放的路径和文件名的开头字符。如本处生成的文件放在/sdcard/目录下，文件名开头为heap字样。
- libc.debug.malloc.program: 用于设置检测的程序，不设置则检测所有的运行的程序。程序名为可执行文件名称即可。

运行程序之后会生成如下以heap开头的报告文件

![image-20230104145049611](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20230104145049611.png)

## 解析heap.xxx文件

- 这里需要使用带symbol库文件来进行dump文件解析。解析命令：python3 native_heapdump_viewer.py --symbols aaa(symbol库的路径) bbb(dump的heap文件路径) --html > ccc.html(生成html文件的路径)
- 执行解析命令后，便在指定的路径中生成解析后的html文件，该文件可以直接用浏览器打开。例如：python3 D:\symbols\native_heapdump_viewer.py --symbols ./ ./sdcard/heap.28465.exit.txt --html > heap_infoj14.html
- 注意：本地要有一个symbols文件夹里面要用so和可执行文件摆放和当初在手机上面的摆放一致。然后这里—symbols指定本地的symbols目录，即相当于手机的根目录。比如手机内文件放在/data/local/tmp/xxx中，本地文件则放在symbols/data/local/tmp/xxx中。

## 解析结果分析

- 尽管log中会出现大量的malloc_debug内存泄漏打印信息，但部分可能是常驻内存，只能依靠以下报告进行动态分析，看是否有内存不断升高的项。

- 报告解析完成之后如下图所示。如果有内存泄漏，某一个部分的比例会不断升高。然后可以点击查看其栈信息。

- 一边展开堆栈，一边继续查看内存升高的项。

- 展开至上图之后，最终依次排查疑似项之后定位为

  libxxxxxxso xxx::FacexxxCalculator::Process(fsp::CalculatorContext*) D:\myCode\xxx\xxx\sdk\.cxx\cmake\release\arm64-v8a/../../../../features/xxx/src/calculators/face_xxx_calculator.cc:137

![image-20230104150301869](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20230104150301869.png)