# Crash问题-char*字符串打印crash导致addr2line定位不准

```cpp
// ...
constexpr char const *STR = "a,b,c";
// 或
const char* STR = nullptr;
// ...

// 错误写法：
// LOG("wyh STR:%s", *STR);

// 正确写法(不需要解引用)：
LOG("wyh STR:%s", STR);
```

STR本身就是指针，直接用%s打印就是字符串，如果用*STR打印，则可能造成意料之外的后果。

本次错误为：无论怎么加log，调用栈最深的几行addr2line的结果始终不变，定位到固定的cpp行数（错误的），影响误判。但浅层的可能没问题。

```c
	行 229: 08-08 18:23:59.255 13833 13833 F DEBUG   :       #04 pc 0000000000000000  /data/local/tmp/libx.so (Some::somefun1(char const*, std::__va_list)+184) (BuildId: xxxxxxxxxxxxx)
	行 230: 08-08 18:23:59.255 13833 13833 F DEBUG   :       #05 pc 0000000000000001  /data/local/tmp/libx.so (Some::__log__(somefun2, char const*, ...)+232) (BuildId: xxxxxxxxxxxxx)
	行 231: 08-08 18:23:59.255 13833 13833 F DEBUG   :       #06 pc 0000000000000002  /data/local/tmp/libx.so (Some::Handler::somefun3()+184) (BuildId: xxxxxxxxxxxxx)
```

