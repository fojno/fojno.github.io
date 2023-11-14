作者：XiNGRZ　2019年06月14日 03:36

### 写在前面
1. 该手机的厂商不提供刷机保修，意味着刷机后你将失去保修资格，且需要自己承担失手造成故障的风险；
2. 该手机首次刷机需要特殊的工具和极强的动手能力，请先充分阅读本帖再决定是否继续刷机；
3. 魔趣是原生系统，不包含（也不会加入）一步、大爆炸等 Smartisan OS 特色功能。如果你离不开他们，不建议你尝试魔趣；
### 准备工具
1. 高通 EDL 线（也称为 9008 线、救砖线、工程线），自行上淘宝购买（10几块的就够了，反正就用一次。淘宝上有些卖家会写着「小米工程线」，其实是同一个东西，通用的）；
2. QPST 线刷工具、TWRP 线刷包、底包、魔趣 ROM 等相关资源，详见：[坚果手机 Pro (odin) 底包、TWRP 及相关工具](https://web.archive.org/web/20221030101045/https://bbs.mokeedev.com/t/topic/14504)
3. adb 及 fastboot 命令行工具请自行安装
考虑到大家的动手能力，不建议自己 DIY 刷机线。能买就买吧。
**再次警告：坚果 Pro 刷机会丧失保修资格；且需要极强的动手能力，稍有失误可能会使你的手机永久损坏。如果你没有 100% 的把握，请放弃！**
### 一、刷入 TWRP
1. 安装 QPST 工具包中的线刷工具和驱动，打开 Qfil 软件；
2. 进 Configuration，确保 Device Type 选了 eMMC；
3. 拔掉数据线， 关机。等待手机彻底关机、屏幕不亮为止；
4. 把 EDL 线插到电脑上，按住手机的音量增和音量减、按住 EDL 线上的小开关把另一头插入手机。等待大概 3 秒松手，此时电脑上的 Qfil 应该会识别到 Qualcomm HS-USB QDLoader 设备；
5. 在 Qfil 里选择 Flat Build；
6. 点击 Programmer 的那个 Browse，选择线刷包中的 prog_ 开头的文件；
7. 点击 Load XML，选择线刷包中的 rawprogram_unsparse.xml；
8. 它会再次弹出选择框，点取消；
9. 深呼吸；
10. 点击 Download 按钮，稍等片刻，TWRP 刷入完成；
11. 同时按住音量增、音量减、Home和电源四个按键。直到你看到白色锤子的时候松开电源键（继续按住其它三个键）；直到你看到 TWRP 的时候才松开所有按键，进入 TWRP，继续进行下面的步骤。
如果刷机失败，或打算中途放弃，你可以按住音量加和电源键退出 EDL 模式，回到正常系统。
### 二、刷入魔趣
1. 进 Wipe（清除），把下面那个条条拖住向右划一下（不需要高级清除，不需要勾选任何东西，不要自作聪明）；
2. 返回上一层，进 Install（安装），刷入底包（RADIO- 开头的那个）；
3. 返回上一层（不要重启），再次进安装，刷入魔趣（MK 开头的那个）；
4. 刷完重启，完成。
### 可选步骤：Bootloader 解锁及刷入 Magisk
如果你不打算刷 Magisk、不打算彻底解锁 Bootloader，你可以忽略这一部分，照常使用。
如果你需要 Magisk，你必须按照这里的步骤彻底解锁 Bootloader，否则下次更新可能无法开机。
1. 开启开发者模式；
2. `adb shell setprop ro.oem_unlock_supported 1`
3. 在开发者模式中打开「OEM 解锁」；
4. `fastboot oem unlock`
`fastboot oem unlock-go`
5. 重启进 TWRP，双清（否则锁屏无法解锁）。
### 如何刷回原厂 Smartisan OS 系统
1. 下载官方卡刷包放到内置存储根目录；
2. 在 TWRP 里 Wipe，然后刷入卡刷包。

——————

### 出现Sahara Fail是因为没禁用驱动签名，这里是禁用教程：
在管理员权限的命令行输入
bcdedit -set testsigning on
重启电脑，然后重新安装驱动，进QFIL就能成功download了

完成后可以用
bcdedit -set testsigning off
还原以前的配置。

注意如果启用了系统盘 BitLocker， 启用和关闭test mode后重启会需要Recovery key。

——————

[原链接](https://web.archive.org/web/20221101010510/https://bbs.mokeedev.com/t/topic/14503/1)
<!-- ##{"timestamp":1698812955}## -->