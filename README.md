# 倾听者K5刷机教程

说明：
1. 以下内容请自行测试，如有不足欢迎提交is或pr。
2. 如果有人有时间，欢迎补充。
3. 以下带 \[\*\] 的只是思路，并未测试，不确定是否可用，可以删除或补充

## 基础

### 进入安卓原生设置
1. 开机，进入“系统设置”（默认倒数第二个图标）
2. 向下进入“关于本机”（倒数第二行）
3. 长按“关于本机”（顶部）
4. 输入以下暗码（四选一）（理论上软件版本在3.3.0及以下的都可以用）即可进入
- 803145
- 202309
- 202403
- 504202  
p.s. 803146可以进入系统更新，不过没什么用

若暗码更新，可以看[这个方法](https://b23.tv/BV1ZvKQeZEvB)

### 打开开发者模式
1. 进入原生设置，找到最后一行的“关于手机”，进入
2. 连续点击倒数第二行的“版本号”多次，直到提示已打开开发者模式
3. 返回前一页面，倒数第二行已出现“开发者模式”
4. 详见[启用开发者选项](https://developer.android.google.cn/studio/debug/dev-options?hl=zh-cn#enable)

### 安装apk
1. 参考[下载 ADB](https://source.android.google.cn/docs/setup/build/adb?hl=zh-cn#download-adb)下载好adb
2. 参考[在设备上启用 adb 调试](https://developer.android.google.cn/tools/adb?hl=zh-cn#Enabling)，连接倾听者，并执行以下命令
```sh
$ adb devices
* daemon not running; starting now at tcp:5037
* daemon started successfully
List of devices attached
xxxxxxxxxxxxx   device
```
出现```xxxxxxxxxxxxx   device```字样即为成功  
若倾听者有如下弹窗，点```确定```即可
```
允许USB调试吗？

这台计算机的 RSA 秘钥指纹如
下：
xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:
xx:xx:xx:xx:xx:xx
[ ] 一律允许使用这台计算机进行调试
                   取消     确定
```
3. 执行`adb install [apk文件名]`，例如安装`example.apk`就执行以下命令
```sh
$ adb install example.apk
Performing Push Install
example.apk: 1 file pushed, 0 skipped. xxx MB/s (xxx bytes in xxxs)
        pkg: /data/local/tmp/example.apk
Success
```
出现`Success`字样即为成功，若失败多是apk问题，检查是否支持安卓5.1

4. 现在可以进入“应用/已下载”，点开安装的应用，点击最下面的按钮“启动”即可启动。你可以下载一个启动器代替`com.listeneer.k5`，再安装一个文件管理器，这样就不用那么麻烦了

**警告：K5有高达0.5GB内存（bushi），所以某些应用可能无法正常使用**



## 进阶

**警告：刷机有风险，请先备份**

### 卡刷（recovery）
0. 可以用 `adb reboot recovery` 跳到第4步
1. 长按 *音量+* 和 *电源* ，开机（没有动画，不要放）
2. 屏幕上会出现以下字样
```
Select Boot Mode:
[VOLUME_UP to select. VOLUME_DOWN is OK.]

[Recovery    Mode]        <<==
[Fastboot    Mode]
[Normal      Boot]
```
3. 按 *音量+* 移动 `<<==` 到 `[Recovery    Mode]` 前，按 *音量-* 进入
4. 现在屏幕上会出现躺着的机器人与 `无命令。`
5. 同时按下 *电源* 与 *音量-* 不放， 再按下 *音量+*
6. 不出意外的话就进入了rec，*电源* 进入、 *音量-* 下移、 *音量+* 上移，\[\*可以愉快地用 `adb sideload [zip线刷包名]` 或emmc上的包卡刷了（magisk只能刷25.*或更早版本，详见[v26.0更新记录第一条](https://github.com/topjohnwu/Magisk/releases/tag/v26.0)）\]


### 线刷（fastboot）
1. 打开“开发者模式/OEM解锁”
2. 与[上面1~3](#卡刷)类似，选`[Fastboot    Mode]`；也可以用 `adb reboot bootloader`
3. 执行 `fastboot oem unlock`
4. 按屏幕上的提示操作，**注意：该操作会清除emmc，但不会清除tf卡；由于tf卡挂载在/sdcard，所以一般文件（下载或用电脑拷的）都在tf卡上，而应用配置（如听单等）在emmc上，请自行备份**
5. \[\*解完bl锁后再次进入fastboot，即可用`fastboot [分区名] [img镜像文件名]`线刷\]

### 工厂模式（假rec？）
1. 长按 *音量-* 和 *电源* ，开机即可
2. 用 */\\* 和 *\\/* 上下移动， *复读* 进入
3. 若不慎进入“按键”测试，多次按 *电源* 键退出