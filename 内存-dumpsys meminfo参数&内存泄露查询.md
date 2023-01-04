## dumpsys命令查看内存情况

- 仍然使用之前ps –A所使用的程序，然后执行`dumpsys meminfo pid`可以查询到的下述图片中的结果。
- rss和pss在增长，说明此时内存占用的情况一直都在升高。

## 参数详解

- Java heap：从 Java 或 Kotlin 代码分配的heap内存。
- Native heap：从 C 或 C++ 代码分配的heap内存。
- Code：程序中用于处理代码和资源（如经过优化或编译的 dex 代码、.so 库等）的内存。
- Stack：程序中的native栈和 Java 栈使用的内存。
- Dalvik heap：程序中 Dalvik 分配占用的内存。
- Graphics：EGL mtrack + GL mtrack。渲染相关的所有内存之和。
- EGL mtrack主要为Android的图像显示系统SurfaceView/TextureView等内存开销的总和。（android surface、egl相关）
- GL mtrack主要为GL texture size、GL command buffer等内存开销的总和。(gl相关)
- Heap Size， Heap Alloc， Heap Free等统计在Android app程序中有效。



- USER为用户，PID为进程号，PPID为父进程进程号。
- VSZ即（Virtual Memory Size/ Virtual memory usage ）表示进程分配的虚拟内存。包括进程可以访问的所有内存，包括进入交换分区的内容，以及共享库占用的内存。
- RSS（Resident Set Size）为实际使用物理内存（包含共享库占用的内存）。表示一个进程在RAM中实际使用的空间地址大小，包括了全部共享库占用的内存。
- PSS （Proportional Set Size）为实际使用物理内存（按比例分配共享库占用的内存）。表示一个进程在RAM中实际使用的空间地址大小，它按比例包含了共享库占用的内存。

![image-20230104140813453](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20230104140813453.png)

## swap增加的情况

- rss和pss不断增长，到一定程度的时候会导致swap开始增加的情况。此时有一定概率出现swap快速增加导致的rss值短暂下降的情况。不能因此认为实际总的内存消耗是在下降的。最后判断的依据仍然为总体趋势。
- 总内存= 物理内存 + 交换分区 。直接从物理内存读写数据比硬盘读写数据要快的多，但是内存是有限的，所以当物理内存不足时，计算机会利用磁盘空间虚拟出的逻辑内存，用作虚拟内存的磁盘空间，被称为交换空间（swap space）。