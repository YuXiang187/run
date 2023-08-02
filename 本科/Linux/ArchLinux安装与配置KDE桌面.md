<div align="right"><a href="https://github.com/YuXiang187/run"><img src="./assets/run.png"></a></div>
<p align="right">当前所在位置：<strong>run > 本科 > Linux</strong></p>

# ArchLinux安装与配置KDE桌面

## 1.更新系统

```bash
pacman -Syyu
```

## 2.创建新用户

```bash
useradd -m -g users -G wheel -s /bin/bash yuxiang
```

设置密码：

```bash
passwd yuxiang
```

## 3.编辑新用户权限

```bash
EDITOR=vim visudo
```

按下<kbd>/</kbd>搜索`wheel`，然后<kbd>Enter</kbd>

定位到`# %wheel ALL=(ALL:ALL) ALL`，在`#`号下按**2**次<kbd>X</kbd>删除注释

按<kbd>Esc</kbd>输入`:wq`退出Vim

## 4.安装KDE桌面环境

```bash
pacman -S plasma-meta konsole dolphin bash-completion
```

将SDDM设置为开机自启

```bash
systemctl enable sddm
```

开启32位支持库以及ArchLinuxCN支持库

```bash
vim /etc/pacman.conf
```

按下<kbd>Shift</kbd>+<kbd>G</kbd>到达文档末

光标往上，定位到下面一行，然后删除下面文字前面的`#`号注释

```bash
[multilib]
Include = /etc/pacman.d/mirrorlist
```

再把下面文字的注释去掉，如：

```bash
[custom]
SigLevel = Optional TrustAll
Server = file:///home/custompkgs
```

再把`[custom]`改成`[archlinuxcn]`，删除`SigLevel`一行，并更换为中科大的源

```bash
[archlinuxcn]
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```

按下<kbd>Esc</kbd>输入`:wq`保存退出

退出后再更新一下新添加的内容

```bash
pacman -Syyu
```

好了，输入`reboot`重启！

## 5.进入桌面的配置

安装ntfs-3g

```bash
sudo pacman -S ntfs-3g
```

安装开源字体

```bash
sudo pacman -S adobe-source-han-serif-cn-fonts wqy-zenhei
```

```bash
sudo pacman -S noto-fonts noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
```

安装基本环境

```bash
sudo pacman -S git base-devel
```

安装Chrome

```bash
sudo pacman -S archlinuxcn-keyring
```

```bash
sudo pacman -S yay
```

```bash
yay -S google-chrome
```

编辑`~/.bashrc`

```bash
alias N='export https_proxy=http://127.0.0.1:7890;export http_proxy=http://127.0.0.1:7890;export all_proxy=socks5://127.0.0.1:7890'
alias O='unset http_proxy;unset https_proxy'
alias G='google-chrome-stable --proxy-server="http://127.0.0.1:7890"'
```

将Windows下的字体文件`msyh.ttf`、`msyhbd.ttf`复制到`/usr/share/fonts/`目录下

再将系统设置为中文

注销重新登录即可看到效果

## 6.配置中文输入法

安装fcitx输入法

```bash
sudo pacman -S fcitx5-im
```

安装fcitx提供的中文输入包

```bash
sudo pacman -S fcitx5-chinese-addons
```

安装主题皮肤

```bash
sudo pacman -S fcitx5-material-color
```

在系统输入法设置中添加拼音输入法，并启用云拼音

配置附加组件中设置经典用户界面，选择一个你喜欢的输入法主题

设置环境变量，让其它程序也能使用这个中文输入法

```bash
sudo vim /etc/environment
```

按<kbd>I</kbd>输入：

```bash
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
GLFW_IM_MODULE=ibus
```

按下<kbd>Esc</kbd>输入`:wq`保存退出

在系统设置中设置`Fcitx 5`开机自启

注销重新登录即可看到效果，按下<kbd>Ctrl</kbd>+<kbd>空格</kbd>来切换输入法

## 7.安装显卡驱动

如果你不知道显卡情况，可运行以下命令获知：

```bash
lspci -k | grep -A 2 -E "(VGA|3D)"
```

### Intel核心显卡

```bash
sudo pacman -S xf86-video-intel lib32-mesa vulkan-intel lib32-vulkan-intel
```

**Intel显卡驱动导致部分录屏软件花屏的解决办法**：

```bash
sudo vim /etc/X11/xorg.conf.d/00-modesetting.conf
```

添加以下内容：

```bash
Section "Device"
   Identifier "Intel"
   Driver "modesetting"
EndSection
```

注销或重启即可生效

### NVIDIA独立显卡

构建NVIDIA内核需要`linux-headers`，请先安装：

```bash
sudo pacman -S linux-headers
```

安装驱动：

```bash
sudo pacman -S nvidia # GeForce 920以上
yay -S nvidia-470xx-dkms lib32-nvidia-utils # GeForce 630-920
yay -S nvidia-390xx-dkms lib32-nvidia-utils # GeForce 400/500/600
yay -S nvidia-340xx-dkms lib32-nvidia-utils # GeForce 8/9
```

完成后重启系统（因为要屏蔽nouveau内核模块）

---

手动创建配置文件（如果你安装的是`nvidia`包，则不需要执行此步骤）

```bash
sudo vim /etc/X11/xorg.conf.d/20-nvidia.conf
```

```bash
Section "Device"
   Identifier     "Device0"
   Driver         "nvidia"
   VendorName     "NVIDIA Corporation"
EndSection
```

完成后重启系统即可

### AMD独立显卡

安装驱动：

```bash
sudo pacman -S lib32-mesa xf86-video-amdgpu vulkan-radeon amdvlk # HD 6000以上
sudo pacman -S lib32-mesa xf86-video-ati # HD 6000以下
```

* HD 6000以上

  使用Vim编辑`/etc/X11/xorg.conf.d/20-amdgpu.conf`文件

  ```bash
  Section "Device"
       Identifier "AMD"
       Driver "amdgpu"
  EndSection
  ```

* HD 6000以下

  使用Vim编辑`/etc/X11/xorg.conf.d/20-radeon.conf`文件

  ```bash
  Section "Device"
      Identifier "Radeon"
      Driver "radeon"
  EndSection
  ```

注销或重启即可生效

## 8.配置KDE

### 1.安装软件及其配置

```bash
sudo pacman -S latte-dock flameshot kdeconnect ark
```

Latte栏的大小为`56`像素

科学上网：

```bash
yay -S clash-for-windows-bin
```

配置代理：

1. 打开Clash，将`Port`（端口号）设置为`7890`
2. 在`Profiles`导入机场（订阅地址），然后在`Proxies`设置源即可

通过sudo保持代理：

```bash
sudo vim /etc/sudoers.d/05_proxy
```

```bash
Defaults env_keep += "*_proxy *_PROXY"
```

Google Chrome启用代理：

```bash
google-chrome-stable --proxy-server="http://127.0.0.1:7890"
```

### 2.系统主题及面板配置

> 主题设置

* 安装全局主题：Breeze 微风深色
* 应用程序风格：Breeze 微风
* Plasma 视觉风格：Layan
* 窗口装饰元素：Layan-solid
* 颜色：Layan
* 图标：Tela blue Dark
* 光标：Breeze 微风
* 欢迎屏幕：Layan
* SDDM：Layan

> 桌面特效

* 对话框显隐过度
* 窗口惯性晃动
* 窗口粉碎动画
* 最小化过渡动画：神灯
* 虚拟桌面3D切换动效

> 虚拟桌面

* 主桌面
* 副桌面

> 锁屏

* 自动锁定屏幕：如果空闲`10`分钟
* 外观配置：Your Name

> 快捷键

* KWin：切换下一个桌面<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Tab</kbd>

> 终端配置

* 透明度设置为40%

> 顶部菜单栏面板从左到右如下布局

* 应用程序菜单：设置为Arch Linux图标
* Window Title Applet：无窗口时设置显示文本“Arch Linux”
* 全局菜单
* 面板间距
* 便利贴：设置半透明白字便利贴
* 系统托盘
* 数字时钟：仅显示时钟
* 锁定/注销：仅显示关机键

> 可选Plasma插件：Simple System Monitor、Smart Video Wallpaper（仅支持mpg格式视频）、Netspeed Widget

Smart Video Wallpaper应用后桌面会黑屏，解决办法如下：

```bash
sudo pacman -S mpv gst-plugins-ugly gst-libav gst-plugins-bad
```

Simple Monitor无法显示信息的解决办法如下：

```bash
sudo pacman -S ksysguard
```

以上设置重启系统后生效