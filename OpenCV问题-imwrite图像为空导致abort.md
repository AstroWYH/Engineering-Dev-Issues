# OpenCV问题-imwrite图像为空导致abort

OpenCV问题多出现于其源码的Assert()，然后导致强制终止crash。遇到该类问题时，首先检查图像是否为空，这种是最常见的。该问题就是在imwrite时图像为空导致的abort。

![image-20220809132115960](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220809132115960.png)

