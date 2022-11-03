C++程序的完整编译过程：预编译->编译->汇编->链接

![image-20221103104852785](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221103104852785.png)

![image-20221103111923730](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221103111923730.png)

CMake的所有指令，都会生成Makefile，而Makefile的所有指令，都会转换成gcc/g++的每一条指令。

编译过程：

编译结束后，.o可以生成可执行文件(g++ -o，cmake: add_exe)、静态库static(ar ...，cmake: add_lib)、动态库shared(g++ ...，cmake: add_lib)。

链接过程：

gcc: ld连接器，cmake: target_link(target: 可执行/static/shared link:static/shared)



特例：main.cpp->main可执行。这个过程仍然是main.cpp->temp->main.o->main。最后一步是链接么？链接了什么？是系统的默认库么？

答：最后一步本身是生成可执行文件，可以在此过程中链接.a静态库，.so动态库，但此处是直接生成，不进行额外链接。



- 链接器ld是一个命令，来源可能是“Loader”or “Link editor”。

- ld命令：GNU链接器，将目标文件与库链接为可执行程序或库文件；格式为” ld [opt] <objfile...>”;

- -g：生成调试信息。
- -o：指定输出文件名。
- -E：只输出预编译结果→即生成.i文件
- -S：输出汇编代码。
- -c：只编译不链接，生成可重定位文件。
- -O：指定编译优化级。O0→O3，优化程度逐渐增强。
- -Wall：显示所有警告信息(Warning all)。
- 注：.o是目标文件、.a是静态库(理解为若干.o的打包)、.so是动态库(共享库)。
- -fPIC：(Position Independent Code)编译生成与位置无关代码——使.so文件的代码段变为真正意义上的共享。
- -shared：如果想创建动态链接库可以使用此选项结合上面的fPIC。
- 注：上面两个选项是创建动态链接库时候用的(编译可执行文件的时候不用)。
- -w：关闭所有警告，一般不建议使用。
- -Wl：是为了将后面的option传递给链接器。
- soname：影响一个可执行文件在链接器ld加载动态链接库时实际查找的动态库文件名。

- C/C++：GCC/G++ -Wl,-soname 链接选项作用_test1280-CSDN博客

- “-I”（大写i），“-L”（大写l），“-l”（小写l）及其区别：

- -I(大写的i)：将后面的路径作为第一个寻找头文件的目录；
- -L：指定链接的动态库/静态库路径（一般和下面的小写l共用）,-L.表示当前目录；
- 比如把libtest.so放在/aaa/bbb/ccc目录下，那链接参数就是-L /aaa/bbb/ccc -ltest

- -l(小写的l)：指定需要链接的库的名字，-l参数紧接着就是库名(一般和上面的-L共用)。
  库名和库文件名不是一个东西。对静态库来说其库名为”zstest”,则库文件名就为libzstest.a。动态库的命令规则与静态库相同，不过其后缀名为”.so”。即库文件名称为”libzstest.so”,就可以知道库名称为“zstest”。（注：库名就是我们写编译语句g++时候所要引用的库的名称；库文件名就是这个库所对应的实实在在的文件的文件名）
- 在实际使用中libxxx.so大多情况只是一个链接，它链接到一个具体的包含版本信息的库文件libxxx.so.xx，例如”cd /usr/lib”可以看到很多这种例子。当然我们也可以自己使用ln命令来制作链接“ln -s libxxxx.so.xx libxxxx.so”。

- 动态链接库路径。系统默认在/usr/lib和/usr/local/lib两个库目录搜索。自己定义的库先把要额外指定路径或者拷贝到这两个目录下。自己额外指定路径总共有三种方式：

- 将当前路径添加到/etc/ld.so.conf文件中或者/etc/ld.so.conf.d目录下的一个文件(推荐)；

- 通过设置“LD_LIBRARY_PATH”环境变量。这个变量是告诉loader在哪些目录中可以找到共享库。例如在.bashrc或.cshrc增加：export LD_LIBRARY_PATH = /usr/local/gcc9/lib64:$LD_LIBRARY_PATH

- 通过编译选项-Wl，-rpath执行动态搜索的路径。

