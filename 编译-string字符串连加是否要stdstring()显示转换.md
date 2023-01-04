# 编译问题-string字符串连加是否要std::string()显示转换

```c
#include <iostream>
#include <string>
int main() {
    std::string path = std::string("/dump/tex/") + std::to_string(666) + std::string(".jpg");
    std::cout << path;
}
// 正常打印结果
/dump/tex/666.jpg

int main() {
    std::string path = "/sdcard/dump/tex/" + std::to_string(666) + ".jpg";
    std::cout << path;
}
// 正常打印结果
/dump/tex/666.jpg

int main() {
    std::string path = "/sdcard/dump/tex/" + "pic" + std::to_string(666) + ".jpg";
    std::cout << path;
}
// 异常报错。在string连加时，"/sdcard/dump/tex/" + "pic"这样的操作是通不过的。
// 1）通过std::string()显示转换；2）避免上述相加
tempCodeRunnerFile.cpp: In function 'int main()':
tempCodeRunnerFile.cpp:4:44: error: invalid operands of types 'const char [18]' and 'const char [4]' to binary 'operator+'
     std::string path = "/sdcard/dump/tex/" + "pic" + std::to_string(666) + ".jpg";
                        ~~~~~~~~~~~~~~~~~~~~^~~~~~~
```

