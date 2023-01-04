## ASAN简介

- ASAN，全称 AddressSanitizer，是一种结合编译器插桩和run-time lib的一种快速内存检测工具，主要用于检测代码中的部分内存安全问题，例如缓冲区溢出或对悬空指针的非法访问等。
- ASAN 已经在 chromium 项目上检测出了300多个潜在的未知bug。对程序性能损耗较小，检测可能导致**性能降低2倍**左右，比Valgrind（官方给的数据大概是**降低10-50倍**）**快了一个数量级**。
- Valgrind只能检查到堆内存的越界访问和悬空指针的访问，ASAN 不仅可以检测到堆内存的越界和悬空指针的访问，还能检测到栈和全局对象的越界访问。这也是 ASAN 在众多内存检测工具的比较上出类拔萃的重要原因，基本上现在 C/C++ 项目都会使用ASAN来保证产品质量，尤其是大项目中更为需要。

## ASAN在Android平台上支持检测以下内存问题

- 堆栈和堆缓冲区上溢/下溢
- 释放之后的堆使用情况
- 超出范围的堆栈使用情况
- 重复释放/错误释放
- 部分平台可支持内存泄漏检测，目前有 x86_64 Linux / OS X
- android平台asan无法检测内存泄漏，其他内存问题可以正常使用，内存泄漏使用malloc_debug工具

## ASAN Linux上配置和使用示例

这里是Linux系统上以gcc为例的一个简单的内存泄漏检测例子

-  gcc -g test_asan.c -o tt -Lasan -fsanitize=address -fsanitize-recover=address -fno-omit-frame-pointer
- -Lasan链接asan的动态库
- -fsanitize=address开启内存越界检测，加-g定位到代码行号
- -fsanitize-recover=address 采用该选项支持内存出错之后程序继续运行，并且必须运行环境下配置export ASAN_OPTIONS=halt_on_error=0才会生效。

![image-20230104143132510](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20230104143132510.png)

## Asan内存检测类型

```c
// 基本命令
-fsanitize=address

检测内存泄漏：       ==1621572==ERROR: LeakSanitizer: detected memory leaks …
检测空悬指针访问：    ==1624341==ERROR: AddressSanitizer: heap-use-after-free on address 0x60b0000000f0 …
检测堆溢出：         ==2172878==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000001c …
C++中的new/delete不匹配：==2180936==ERROR: AddressSanitizer: alloc-dealloc-mismatch (operator new [] vs operator delete) on 0x60b0000000f0 …
检测栈溢出：         ==2196928==ERROR: AddressSanitizer: stack-buffer-overflow on address 0x7ffc33777f24 …
检测全局缓冲区溢出：  ==2213117==ERROR: AddressSanitizer: global-buffer-overflow on address 0x558855e231b4 …

```

## ASAN和Valgrind综合对比

![image-20230104144630869](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20230104144630869.png)