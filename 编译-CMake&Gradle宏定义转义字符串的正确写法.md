# 编译问题-CMake&Gradle宏定义转义字符串的正确写法

### 问题描述

CMake进行宏定义，宏定义内容为字符串，字符串中包括了分号，想传入.cpp文件，以下为正确的转义方式：

```cmake
target_compile_definitions(some_module PUBLIC "-Dxxx_STRING=\"A\;B"")
```

Gradle中的CMake的正确转义方式为：

```cmake
cppFlags '-Dxxx_STRING=\'"' + xxx_string + '"\''
```

