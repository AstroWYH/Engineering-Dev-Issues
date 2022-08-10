# Crash崩库问题-char*字符串打印错误导致crash，且addr2line定位不准

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

CATEGORY_STR本身就是指针，直接用%s打印就是字符串，如果用*CATEGORY_STR打印，则可能造成意料之外的后果。

本次错误为：无论怎么加log，灰色两行addr2line的结果始终不变，定位到固定的cpp行数（错误的），影响误判。

![image-20220808222705301](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220808222705301.png)

