### trace的几种抓取方式

#### 通过systrace抓取，需要python 2和systrace.py（当前测试抓取时间最多不能超过2s）

./python /d/Adb/platform-tools_r31.0.3-windows/platform-tools/systrace/systrace.py -o mynewtrace.html sched freq idle am wm gfx view binder_driver hal dalvik camera input res

#### 通过开启手机QCOM/MTK自带trace跟踪工具，到相应路径取出（当前测试较稳）

adb shell setprop persist.traced.enable 1   Android P和Q需要手动开启
adb reboot
确认相关服务是否正常启动

> ps -A | grep -iE "traced"
> nobody 1016 1 45620 2444 0
> nobody 1017 1 45620 2624 0

#### 通过perfetto网页抓取（当前测试偶尔抓取结果较少）

![image-20221103101612020](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221103101612020.png)

