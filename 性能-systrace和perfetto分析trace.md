### 以perfetto官方提供 example_android_trace为例

找到进程pid，找到线程tid，wasd放大缩小切换到想要观察的线程的具体执行细节，鼠标框选可得知运行时间。可见当前框选为33ms左右，处理2次，即约每秒60次处理。

![image-20221103102902459](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221103102902459.png)

找到相应线程，某次某个具体函数，进行双击，下方弹出信息框，可观察其执行耗时，可观察其执行在哪个CPU核上。左侧和上方可观察该线程的Running、Runnale具体状态，根据Runnale占比判断线程具体执行了多久， 被抢占了多久等信息。

![image-20221103103148214](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221103103148214.png)

观察线程在哪个CPU核上运行，以及其运行情况。通过0123为小核、4567为大核，7为超大核，一般不启用，否则功耗明显较高，应用于较大场景。分析当前线程在CPU某个核上的频率，是否明显较低导致性能较差等，如800KHz和1.7GHz的区别等。

![image-20221103103617816](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221103103617816.png)