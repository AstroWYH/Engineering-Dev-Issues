# C API接口问题-reserved[]作用&用完后的措施

### 问题描述

void* reserved[2]，在C风格的接口头文件中，结构体经常可见保留指针数组，用来维持一定范围内的兼容性。

```c
typedef struct SomeConfig {
    bool           a = true;
    const char     *path_a = nullptr;
    const char     *path_b = nullptr;
    bool           b = true;
    // ...
    void           *reserved[2] = {0}; // 结构体经常可见保留指针数组，用来维持一定范围内的兼容性
}
```

### 问题描述

每次新使用一个指针，reserved[num]的num就会减一，如果用完了怎么办呢？答案是可以使用extend_info扩展，在reserved用完之前，extend_info去指向一个新的结构体，其内可以扩展之前结构体的信息，并且可以继续加reserved[]。

```c
typedef struct SomeExtendInfo {
    bool           c = true;
    // ...
    void           *reserved[2] = {0};
}

typedef struct SomeConfig {
    bool           a = true;
    const char     *path_a = nullptr;
    const char     *path_b = nullptr;
    bool           b = true;
    // ...
    SomeExtendInfo extend_info = nullptr;
    void           *reserved[1] = {0}; // 结构体经常可见保留指针数组，用来维持一定范围内的兼容性
}
```


