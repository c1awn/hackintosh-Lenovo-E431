# hackintosh
```
                                      MacBook
                                      ----------------------------------------------
                                      Model   : Hackintosh (SMBIOS: MacBookAir5,2)
                 ###                  OS      : macOS Catalina 10.15.4 19E287
               ####                   Kernel  : Darwin 19.4.0
               ###                    Uptime  : 15 hours, 19 minutes
       #######    #######             Shell   : /bin/bash
     ######################           Time    : 
    #####################             CPU     : Intel Core i5-3230M 2.60GHz x (4)
    ####################              Memory  : 2062MB(Avai) / 8192MB(Total)
    ####################              Disk    : 95GB(Avai) / 118GB(Total)
    #####################             IP Addr : Public *********** / Intranet 192.168.**
     ######################           Battery : 96.80%  /  charged
      ####################            Terminal: xterm-256color by Apple Terminal
        ################              Graphics: Intel HD Graphics 4000 (1536 MB), 3360 x 1890
         ####     #####               Display : 3360 x 1890
```
> 这是老机器ThinkPad E431（62771U0）的EFI  
每次想到还有小瑕疵，“又不是不能用”的箴言可以缓解心情  
ps.E431配置落后，不管是window还是macOS都卡顿，已更新内存条、固态  

#### updated in 20200425
-  发现睡眠自动唤醒，不确定未升级前是否也这样，平时没注意。`log show --last 6h | grep "Wake reason"`查看唤醒原因，主要是`AppleACPIPlatformPower Wake reason: RTC (Alarm)`，暂时未能解决。
```
2020-04-25 05:16:44.042603+0800 0x119d3    Default     0x0                  73     0    powerd: [powerd:sleepWake] Wake reason: "<private>"  identity: "<private>"
2020-04-25 05:17:04.055124+0800 0x74       Default     0x0                  0      0    kernel: (AppleACPIPlatform) AppleACPIPlatformPower Wake reason: RTC (Alarm)
2020-04-25 05:17:04.055125+0800 0x74       Default     0x0                  0      0    kernel: (AppleACPIPlatform) AppleACPIPlatformPower Wake reason: RTC (Alarm)
2020-04-25 06:19:00.651086+0800 0x74       Default     0x0                  0      0    kernel: (AppleACPIPlatform) AppleACPIPlatformPower Wake reason: RTC (Alarm)
2020-04-25 06:19:00.651087+0800 0x74       Default     0x0                  0      0    kernel: (AppleACPIPlatform) AppleACPIPlatformPower Wake reason: RTC (Alarm)
2020-04-25 07:26:31.797015+0800 0x74       Default     0x0                  0      0    kernel: (AppleACPIPlatform) AppleACPIPlatformPower Wake reason: RTC (Alarm)
2020-04-25 07:26:31.797016+0800 0x74       Default     0x0                  0      0    kernel: (AppleACPIPlatform) AppleACPIPlatformPower Wake reason: RTC (Alarm)
```


#### updated in 20200423
1. 10.14和10.12系统版本用的黑果小兵镜像，10.15系统用的远景镜像
2. clover版本5113，EFI可用于引导10.12.6、10.14.6、10.15.4
3. 安装完10.14.6不要在设置里更新1.6G左右的安装包，会导致卡顿严重。不要使用搜狗输入法，卡顿严重。远景10.5.2镜像安装成功后设置直接更新10.5.4，未发现异常。
4. 驱动情况，基本已更新至最新版
  - ACPI用的hotpatch
  - 显卡，核心显卡HD4000，启动项屏蔽独显
  - 亮度调节正常，电池识别正常
  - 声卡，AppleAlc。如果重启或者开机时插着耳机、音箱，会有1秒左右的爆音。
  - 使用VirtualSMC而不是fakesmc
  - CPU i5-3230M侦测7档变频
  - 睡眠、唤醒正常
  - 其他：无线网卡无解，另外，如果外接HDMI显示器且开启HiDPI，10.14和10.12系统启动或者注销时会花屏或者8苹果，不外接显示器没遇到花屏，不影响使用。而10.15系统不存在此问题，但是开机时间比之前长20s左右，登陆后桌面背景会黑几秒再恢复。

