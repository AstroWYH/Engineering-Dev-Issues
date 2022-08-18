# 链接问题-用dlopen时链接dl库而非-shared选项

```cmake
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC ...") # -fPIC链接地址重定位，否则编译不过
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ...")

TARGET_LINK_LIBRARIES(${Some_Target}
  dl # 链接dl库来dlopen
)

# .cpp使用dlopen前需要包含头文件
#include <dlfcn.h>

# 注：网上方法有用-shared选项，但在aarch64-linux实测发现执行main()函数前直接segmentation错误
```

