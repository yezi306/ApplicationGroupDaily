### 什么是ADB
ADB就是连接手机和电脑的纽带，通过ADB可以用电脑来操作手机
- **adb version**：查看当前ADB的版本号
- **adb shell**:进入Shell，进入以后可以使用很多的Linux的Shell命令
- 下载APK：**adb install -r 应用程序名.apk** : 将APK安装在data/data目录下，作为普通的用户程序
- 下载APK（向手机中写入文件）：**adb push <local><remote>** ：不是安装命令，是将一个文件写入手机存储系统，需要相应的权限
- 获取文件：**adb pull <remote><local>**
- 查看Log:
```
adb shell
logcat|grep "abc"
```
- 删除应用
```
adb remount
adb shell
cd system/app
rm *.apk
```
- 查看系统盘符：adb shell df
- 输出所有已经安装应用：adb shell pm list packages -f
- 模拟按键输入：adb shell input ketevent （code，可以上网查）
- 模拟滑动输入：adb shell input touchscreen <x1> <y1> <x2> <y2>