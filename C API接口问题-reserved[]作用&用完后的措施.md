# C API接口问题-reserved[]作用&用完后的措施

### 问题描述

void* reserved[2]，在C风格的接口头文件中，结构体经常可见保留指针数组，用来维持一定范围内的兼容性。

![image-20220809135522438](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220809135522438.png)

### 问题描述

每次新使用一个指针，reserved[num]的num就会减一，如果用完了怎么办呢？答案是可以使用extend_info扩展，在reserved用完之前，extend_info去指向一个新的结构体，其内可以扩展之前结构体的信息，并且可以继续加reserved[]。

![image-20220809140415402](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220809140415402.png)

![image-20220809140339986](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220809140339986.png)