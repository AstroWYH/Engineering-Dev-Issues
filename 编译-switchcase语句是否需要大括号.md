# 编译问题-switchcase语句是否需要大括号

```c
// 有时遇到switch case，直接编译会报错，加大括号就没问题，到底是怎么回事呢？

int a = 2;
switch (a)
{
    case 1:
        int c = 10; // 编译会报错，case里不能定义局部变量，C++不能明确其作用范围
        break;
    case 2:
        break;
    default:
        break;
}

switch (a)
{
    case 1:
        {
            int c = 10; // 编译成功，因为有语句块限定范围
            break;
        }
    case 2:
        break;
    default:
        break;
}
```

