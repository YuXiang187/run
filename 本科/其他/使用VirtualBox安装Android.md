# 使用VirtualBox安装Android

## 1.下载最新Android镜像

前往[android-x86.org](https://www.android-x86.org/)下载最新的Android镜像（iso）

## 2.打开VirtualBox安装Android

在VirtualBox中新建一个虚拟机

* 类型选择Linux
* 版本选择Other Linux (64-bit)

内存最好给4096MB以上

存储最好给20GB以上

---

在“设置”中

* 系统>处理器(P)中设置处理器数量为2个
* 系统>硬件加速(l)中设置半虚拟化接口为KVM
* 显示>屏幕(S)中设置显存大小为128MB
* 显示>屏幕(S)中设置显卡控制器为VBoxSVGA（请无视无效设置的提示）
* 存储>设置虚拟盘片（导入刚刚下载好的Android镜像）

完成，启动虚拟机，然后选择Advanced options...>Auto_Installation>Yes

在安装向导进行到WiFi设置时，请选择跳过，然后再设置

安装完成后，尽情享用吧！