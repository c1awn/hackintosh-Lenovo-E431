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

#### 小于 4k 的屏幕（2k 或 1080p）开启 HiDPI
```
 此脚本的目的是为中低分辨率的屏幕开启 HiDPI 选项，并且具有原生的 HiDPI 设置，不需要 RDM 软件即可在系统显示器设置中设置
macOS 的 DPI 机制和 Windows 下不一样，比如 1080p 的屏幕在 Windows 下有 125%、150% 这样的缩放选项，而同样的屏幕在 macOS 下，缩放选项里只是单纯的调节分辨率，这就使得在默认分辨率下字体和UI看起来很小，降低分辨率又显得模糊
```
- 脚本`bash -c "$(curl -fsSL https://raw.githubusercontent.com/xzhih/one-key-hidpi/master/hidpi.sh)"`  
- 分辨率建议填写2560x1440 1920x1080 1680x945 1536x864 1488x837 1440x810 1280x720，其中1680x945HiDPI和1488x837HiDPI是推荐项，而
1488x837HiDPI基本解决了字体太小显示发虚的问题，但是比1680x945HiDPI的图标看着大些。


#### updated in 20200425
-  发现睡眠差不多每小时自动唤醒，醒后自动重新睡眠，不确定未升级前是否也这样，平时没注意。`log show --last 6h | grep "Wake reason"`查看唤醒原因，主要是`AppleACPIPlatformPower Wake reason: RTC (Alarm)`，~~atched新增SSDT-RTC0.aml后解决，当晚直到第二天未发现RTC唤醒记录。~~ 还是会有RTC唤醒，就这样吧。
-  发现登录时的桌面壁纸黑屏没有了，但是开机第二阶段出现花屏，注销未发现花屏。开机时间25S左右。
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
```
EFI\CLOVER\kexts\Other\VoodooPS2Controller.kext (v.1.9.2)
EFI\CLOVER\kexts\Other\VirtualSMC.kext (v.1.1.2)
EFI\CLOVER\kexts\Other\USBInjectAll.kext (v.0.7.5)
EFI\CLOVER\kexts\Other\SMCSuperIO.kext (v.1.1.2)
EFI\CLOVER\kexts\Other\SMCProcessor.kext (v.1.1.2)
EFI\CLOVER\kexts\Other\SMCLightSensor.kext (v.1)
EFI\CLOVER\kexts\Other\SMCBatteryManager.kext (v.1)
EFI\CLOVER\kexts\Other\RealtekRTL8111.kext (v.2.2.2)
EFI\CLOVER\kexts\Other\Lilu.kext (v.1.4.3)
EFI\CLOVER\kexts\Other\IntelMausiEthernet.kext (v.2.2.1d1)
EFI\CLOVER\kexts\Other\FakePCIID_XHCIMux.kext (v.1.3.9)
EFI\CLOVER\kexts\Other\FakePCIID.kext (v.1.3.9)
EFI\CLOVER\kexts\Other\BlueTooth_Injector.kext (v.1.0.0)
EFI\CLOVER\kexts\Other\AppleBacklightInjector.kext (v.0.9.0)
EFI\CLOVER\kexts\Other\AppleALC.kext (v.1.4.8)
EFI\CLOVER\kexts\Other\ACPIPoller.kext (v.0.8.1)
```
  - ACPI用的hotpatch
  - 显卡，核心显卡HD4000，启动项屏蔽独显
  - 亮度调节正常，电池识别正常
  - 声卡，AppleAlc。如果重启或者开机时插着耳机、音箱，会有1秒左右的爆音。
  - 使用VirtualSMC而不是fakesmc
  - CPU i5-3230M侦测7档变频
  - 睡眠、唤醒正常
  - 其他：无线网卡无解，另外，如果外接HDMI显示器且开启HiDPI，10.14和10.12系统启动或者注销时会花屏或者8苹果，不外接显示器没遇到花屏，不影响使用。~~而10.15系统不存在此问题，但是开机时间比之前长20s左右，登陆后桌面背景会黑几秒再恢复。~~

