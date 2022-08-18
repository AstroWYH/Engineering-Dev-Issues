# 链接问题-通过dlerror()打印dlopen失败原因

```c
void *handle = nullptr;
STATUS ret = STATUS_OK;
handle = dlopen("libxxx.so", RTLD_LAZY);

if (!handle)
{
    // 通过dlerror()打印dlopen失败的原因，如还需要依赖其他的库等
    fprintf(stderr, "dlerror:%s ", dlerror());  
    printf("dlopen failed! \n");
    return -1;
}
```

