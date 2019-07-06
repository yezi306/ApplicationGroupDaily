### 什么是AlarmManager
1. AlarmManager是安卓中的一个==系统级别==的提示服务，他的功能是在==特定的时间==为我们广播一个指定的Intent
==注意这里的Intent内的东西要注册==
2. 我们需要为AlarmManager设置一个Intent，当时间到的时候就会执行这个Intent动作。我们通常使用==PendingIntent==，因为它为Intent封装了startActivity、startService、sendBroadcast方法。
### AlarmManager常用的3个方法
> 1. **set(int type, long startTime, PendingIntent pi);**

用于设置一次性闹钟，第一个参数表示闹钟类型， 第二个参数表示闹钟执行时间， 第三个参数表示闹钟响应的动作。

其中==int type==有5个参数值：
---
（1）AlarmManager.ELAPSED_REALTIME表示闹钟在手机睡眠状态下不可用，该状态下闹钟使用相对时间（相对于系统启动开始），状态值为3；

（2）AlarmManager.ELAPSED_REALTIME_WAKEUP表示闹钟在睡眠状态下会唤醒系统并执行提示功能，该状态下闹钟也使用相对时间，状态值为2；

（3）AlarmManager.RTC表示闹钟在睡眠状态下不可用，该状态下闹钟使用绝对时间，即当前系统时间，状态值为1；

（4）AlarmManager.RTC_WAKEUP表示闹钟在睡眠状态下会唤醒系统并执行提示功能，该状态下闹钟使用绝对时间，状态值为0；

（5）AlarmManager.POWER_OFF_WAKEUP表示闹钟在手机关机状态下也能正常进行提示功能，所以是5个状态中用的最多的状态之一，该状态下闹钟也是用绝对时间，状态值为4；不过本状态好像受SDK版本影响，某些版本并不支持；

**相对时间的获取：SystemClock.elapsedRealtime()**

**绝对时间的获取：System.currentTimeMillis()**

---

PendingIntent有==3种构造方法==：
---
（1） 如果通过启用**服务**来实现闹钟的话，就需要用PendingIntent.getService(Context x, int i, Intent intent, int j);

（2） 如果通过发送**广播**来实现闹钟的话，就需要用PendingIntent.getBroadcast(Context x, int i, Intent intent, int j);

（3） 如果通过切换**Activity**的方式来实现闹钟的话，使用PendingIntent.getActivity(Context x, int i,  Intent intent, int j);

---

> 2. **setRepeating(int type, long startTime, long intervalTime, PendingIntent pi);**

> 3. **setInexactRepeating(int type, long startTime, long IntervalTime, PendingIntent pi);**
