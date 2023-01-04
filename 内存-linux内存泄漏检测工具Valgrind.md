一般使用 –g –O0 对代码进行编译，如：g++ -g -O0 segfault.cpp -o segfault

使用valgrind对编译好的程序进行检测，如：

- valgrind --tool=memcheck --leak-check=full --log-file=reportleak ./segfault
- --tool 指定检测工具，valgrind默认使用工具为memcheck，还支持callgrind，cachegrind，helgrind，massif，extension等工具。
- --leak-check 打开内存泄漏检测开关，full表示给出每个确定或者可能丢失的内存块的详细信息，包含分配位置。
- --log-file 指定log输出文件, 这里指定为reportleak。

![image-20230104142318434](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20230104142318434.png)