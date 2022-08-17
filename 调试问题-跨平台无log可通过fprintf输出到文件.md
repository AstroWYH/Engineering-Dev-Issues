# 调试问题-跨平台无log可通过fprintf输出到文件

在非android平台运行时，如aarch64-linux等平台，可通过如下方式打印log

```c
#include<stdio.h>
FILE *stream;

int main() {
    int i = 10;
    double fp = 1.5;
    char s[] = "this is a string";
    char c = '\n';
    stream = fopen( "fprintf.out", "w" );
    fprintf(stream, "%s%c", s, c); // 既会打印终端，又会打印到文件
    fprintf(stream, "%d\n", i);
    fprintf(stream, "%f\n", fp);
    fprintf(stderr, "%d\n", i); // 直接打印终端
    fclose(stream);
    system("type fprintf.out");
}

// fprintf.out
this is a string
10
1.500000
```

