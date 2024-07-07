# 倾听者K5隐藏操作

## 进入安卓原生设置
1. 开机，进入“系统设置”
2. 进入“关于本机”
3. 长按“关于本机”
4. 输入以下数字（四选一）
- 803145（K3可用）
- 202309
- 202403
- 504202
- 记得打开usb调试，更新后可以用adb把 ```k5启动器的apk``` pull出来反编译
5. 即可进入
6. 其他操作与安卓设置相同（毕竟这是安卓5.1的设置）

## 卡刷（recovery）
0. 可以打开usb调试，用 ```adb reboot recovery``` 跳到第4步
1. 长按 *音量+* 和 *电源* ，开机（没有动画，不要放）
2. 屏幕上会出现以下字样

```
Select Boot Mode:
[VOLUME_UP to select. VOLUME_DOWN is OK.]

[Recovery    Mode]        <<==
[Fastboot    Mode]
[Normal      Boot]
```
3. 按 *音量+* 移动 ```<<==``` 到 ```[Recovery    Mode]``` 前，按 *音量-* 进入
4. 现在屏幕上会出现躺着的机器人与 ```无命令。```
5. 同时按下 *电源* 与 *音量-* 不放， 再按下 *音量+*
6. 不出意外的话就进入了rec，*电源* 进入、 *音量-* 下移、 *音量+* 上移，可以愉快的卡刷了


## 线刷（fastboot）
1. 打开OEM解锁
2. 与[上面1~3](#卡刷)类似，选```[Fastboot    Mode]```；也可以用 ```adb reboot bootloader```
3. 执行 ```fastboot oem unlock``` （如果Windows找不到设备可能是驱动问题，用Linux）
4. 按屏幕上的提示操作，**注意：会清除emmc，但不会清除tf卡，一般文件（下载或用电脑拷的）都在tf卡上，无需担心**
5. 解完bl锁后再次进入fastboot，即可线刷

## 工厂模式（假rec？）
1. 长按 *音量-* 和 *电源* ，开机即可
2. 用 */\\* 和 *\\/* 上下移动， *复读* 进入
3. 若不慎进入“按键”测试，多次按 *电源* 键退出