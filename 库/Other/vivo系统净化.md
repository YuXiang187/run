# vivo系统净化

自备安装包：

* **文件管理器+**（必需）
* **v2rayNG**或者**ClashForAndroid**
* **Google三件套**

---

操作步骤：

- [ ] 拔手机卡
- [ ] 还原系统
- [ ] 初始设置
  - [ ] 卸载可以卸载的app
  - [ ] 系统初步设置
  - [ ] 连接电脑，传输init安装包，安装文件管理器+
  - [ ] 使用adb卸载系统预装
  - [ ] 重启
  - [ ] 整顿系统控制面板、系统最终设置
  - [ ] 设置相册、搜狗输入法的通知权限
- [ ] 连接WiFi
- [ ] 连接电脑，传输全部数据
- [ ] 安装v2rayNG
- [ ] 安装Google三件套
  - [ ] 安装POCO启动器，卸载系统自带启动器
  - [ ] 安装国外软件
- [ ] 插手机卡
- [ ] 安装国内软件
  - [ ] 微信
  - [ ] QQ
  - [ ] 其他


---

附录：vivo Y5s系统预装卸载名单（放在`.bat`文件快速执行）

```bash
@echo off
adb shell pm uninstall --user 0 com.android.backupconfirm
adb shell pm uninstall --user 0 com.android.BBKCrontab
adb shell pm uninstall --user 0 com.android.bbklog
adb shell pm uninstall --user 0 com.android.bbkmusic
adb shell pm uninstall --user 0 com.android.bips
adb shell pm uninstall --user 0 com.android.browser
adb shell pm uninstall --user 0 com.android.dreams.alwaysondisplay
adb shell pm uninstall --user 0 com.android.filemanager
adb shell pm uninstall --user 0 com.android.htmlviewer
adb shell pm uninstall --user 0 com.android.managedprovisioning
adb shell pm uninstall --user 0 com.android.printservice.recommendation
adb shell pm uninstall --user 0 com.android.printspooler
adb shell pm uninstall --user 0 com.android.statementservice
adb shell pm uninstall --user 0 com.android.VideoPlayer
adb shell pm uninstall --user 0 com.android.vivo.tws.vivotws
adb shell pm uninstall --user 0 com.android.wallpaperbackup
adb shell pm uninstall --user 0 com.android.wallpapercropper
adb shell pm uninstall --user 0 com.bbk.account
adb shell pm uninstall --user 0 com.bbk.appstore
adb shell pm uninstall --user 0 com.bbk.calendar
adb shell pm uninstall --user 0 com.bbk.cloud
adb shell pm uninstall --user 0 com.bbk.facewake
adb shell pm uninstall --user 0 com.bbk.iqoo.logsystem
adb shell pm uninstall --user 0 com.bbk.photoframewidget
adb shell pm uninstall --user 0 com.bbk.scene.launcher.theme
adb shell pm uninstall --user 0 com.bbk.SuperPowerSave
adb shell pm uninstall --user 0 com.bbk.theme
adb shell pm uninstall --user 0 com.bbk.theme.resources
adb shell pm uninstall --user 0 com.bbk.updater
adb shell pm uninstall --user 0 com.focaltouchscreen.sensortest
adb shell pm uninstall --user 0 com.google.android.marvin.talkback
adb shell pm uninstall --user 0 com.iqoo.engineermode
adb shell pm uninstall --user 0 com.iqoo.powersaving
adb shell pm uninstall --user 0 com.iqoo.secure
adb shell pm uninstall --user 0 com.mediatek.atci.service
adb shell pm uninstall --user 0 com.mediatek.atmwifimeta
adb shell pm uninstall --user 0 com.mediatek.gnssdebugreport
adb shell pm uninstall --user 0 com.mediatek.mtklogger
adb shell pm uninstall --user 0 com.mobiletools.systemhelper
adb shell pm uninstall --user 0 com.nttouchscreen.mptest
adb shell pm uninstall --user 0 com.tencent.soter.soterserver
adb shell pm uninstall --user 0 com.vivo.abe
adb shell pm uninstall --user 0 com.vivo.agent
adb shell pm uninstall --user 0 com.vivo.aiengine
adb shell pm uninstall --user 0 com.vivo.aiservice
adb shell pm uninstall --user 0 com.vivo.appfilter
adb shell pm uninstall --user 0 com.vivo.assistant
adb shell pm uninstall --user 0 com.vivo.audiofx
adb shell pm uninstall --user 0 com.vivo.browser
adb shell pm uninstall --user 0 com.vivo.bsptest
adb shell pm uninstall --user 0 com.vivo.contentcatcher
adb shell pm uninstall --user 0 com.vivo.daemonService
adb shell pm uninstall --user 0 com.vivo.devicereg
adb shell pm uninstall --user 0 com.vivo.doubleinstance
adb shell pm uninstall --user 0 com.vivo.easyshare
adb shell pm uninstall --user 0 com.vivo.epm
adb shell pm uninstall --user 0 com.vivo.ewarranty
adb shell pm uninstall --user 0 com.vivo.faceunlock
adb shell pm uninstall --user 0 com.vivo.favorite
adb shell pm uninstall --user 0 com.vivo.findphone
adb shell pm uninstall --user 0 com.vivo.floatingball
adb shell pm uninstall --user 0 com.vivo.fuelsummary
adb shell pm uninstall --user 0 com.vivo.gamecube
adb shell pm uninstall --user 0 com.vivo.gamewatch
adb shell pm uninstall --user 0 com.vivo.globalanimation
adb shell pm uninstall --user 0 com.vivo.globalsearch
adb shell pm uninstall --user 0 com.vivo.hiboard
adb shell pm uninstall --user 0 com.vivo.hybrid
adb shell pm uninstall --user 0 com.vivo.livewallpaper.brilliant
adb shell pm uninstall --user 0 com.vivo.magazine
adb shell pm uninstall --user 0 com.vivo.mediatune
adb shell pm uninstall --user 0 com.vivo.minscreen
adb shell pm uninstall --user 0 com.vivo.motionrecognition
adb shell pm uninstall --user 0 com.vivo.numbermark
adb shell pm uninstall --user 0 com.vivo.pem
adb shell pm uninstall --user 0 com.vivo.pushservice
adb shell pm uninstall --user 0 com.vivo.quickpay
adb shell pm uninstall --user 0 com.vivo.safecenter
adb shell pm uninstall --user 0 com.vivo.sdkplugin
adb shell pm uninstall --user 0 com.vivo.secime.service
adb shell pm uninstall --user 0 com.vivo.setupwizard
adb shell pm uninstall --user 0 com.vivo.shortcutcenter
adb shell pm uninstall --user 0 com.vivo.singularity
adb shell pm uninstall --user 0 com.vivo.SmartKey
adb shell pm uninstall --user 0 com.vivo.smartmultiwindow
adb shell pm uninstall --user 0 com.vivo.smartunlock
adb shell pm uninstall --user 0 com.vivo.sos
adb shell pm uninstall --user 0 com.vivo.space
adb shell pm uninstall --user 0 com.vivo.upnpserver
adb shell pm uninstall --user 0 com.vivo.vhomeguide
adb shell pm uninstall --user 0 com.vivo.vivokaraoke
adb shell pm uninstall --user 0 com.vivo.vms
adb shell pm uninstall --user 0 com.vivo.vtouch
adb shell pm uninstall --user 0 com.vivo.wallet
adb shell pm uninstall --user 0 com.vivo.weather.provider
adb shell pm uninstall --user 0 com.vivo.widget.calendar
adb shell pm uninstall --user 0 com.vlife.vivo.wallpaper
adb shell pm uninstall --user 0 com.vivo.livewallpaper.glaze
pause
```

安装完POCO桌面后卸载：

```bash
adb shell pm uninstall --user 0 com.bbk.launcher2
```
