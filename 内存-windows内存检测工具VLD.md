## VLD（visual leak detector）

- Windows系统的vs、qt上都可以使用（qt上要选择MSVC编译器，不可用MinGW编译器）。
- 其支持上VS远好于qt，对于qt的qml支持更弱。

## Vld的特点

- 1.能够得到显示泄露位置所在的文件名及行号以及拿到其调用的堆栈信息。
- 2.源码使用GPL发布，免费且开源。
- 3.操作简单。有已经准备好的lib，只需要安装相应插件之后，包含头文件vld.h，即可直接在vs/qt的tool中进行操作。
- 4.只支持vs2009~2015。

![image-20230104141447640](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20230104141447640.png)

## Windows其它内存泄漏检测工具

- 最简单的为vs自带的CRT内存泄漏检测，其还可以检测MFC工程。开启debug模式，添加相关宏定义即可。
- Dr Memory。类似于vld一样像插件安装，在visual studio在vs上用tool打开。
- LeakDiag。微软开发的一款内存泄漏检测工具。