# C API接口问题-create_handle时传入handle一级指针获取失败

### 问题场景

集成侧create时传入handle的一级指针，想在接口获取handle的内容失败。

### 解法

集成侧应该传handle的二级指针，或handle一级指针的引用（如果接口要求C风格，则不允许引用）。

### 详细描述

![image-20220809133337615](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220809133337615.png)

```cpp
如果接口外部调用方，想传入一个handle_impl的m_handle （一级指针），让接口内部给其赋值，即让m_handle指向new handle_impl()。该场景下，如果直接传入m_handle（一级指针）是做不到的，因为接口内部函数会拷贝一个新的指针*p_handle，p_handle会指向new handle_impl()，但这跟m_handle没关系，出了接口内部函数后，m_handle仍然一无所有。

因此采取在接口外部传入m_handle的地址（即&m_handle ，二级指针），这样在接口内部函数采用**p_handle作为形参，再对*p_handle=new handle_impl()，（此时*p_handle就接管着m_handle），这样离开接口内部函数后，m_handle就获得了handle_impl。此外，其实上述场景在接口外部传入m_handle，在接口内部函数形参用引用接住，也是没有问题的，只不过接口需要保持C风格。
```

![image-20220809132841358](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220809132841358.png)