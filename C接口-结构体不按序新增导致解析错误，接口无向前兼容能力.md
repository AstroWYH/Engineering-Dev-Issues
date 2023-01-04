# C API接口问题-结构体不按序新增导致解析错误，接口无向前兼容能力

### 问题描述

Config需要新添加write_dir，直接添加到working_dir后面看似同类（都是path）放在一起比较好看，但很容易造成问题，如果集成侧不更新C接口头文件.h，则很容易传入方和接收方的内容不一致，导致解析错误。

正确的做法是，在靠近reserved[]上面挨个添加需要新增的结构指针，这样即使集成侧不更新头文件，也不会造成问题，因为大不了就是不传值，SDK内部会当做默认reserved处理，保证了**接口的向前兼容**能力。

```c
typedef struct SomeConfig {
    bool           a = true;
    const char     *path_a = nullptr;
    const char     *path_b = nullptr; // path_b为新增，直接写在path_a后面好看，但兼容性不好，容易出错
    bool           b = true;
    void           *reserved[2] = {0};
}

typedef struct SomeConfig {
    bool           a = true;
    const char     *path_a = nullptr;
    bool           b = true;
    const char     *path_b = nullptr; // 正确做法为，按序新增到最后，reserved的前面，保证良好的接口兼容性
    void           *reserved[2] = {0};
}
```

