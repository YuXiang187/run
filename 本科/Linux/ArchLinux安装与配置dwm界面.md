# ArchLinux安装与配置dwm界面

## 0.自定义suckless软件

### 1.克隆源代码

```bash
git clone https://git.suckless.org/dwm
git clone https://git.suckless.org/st
git clone https://git.suckless.org/dmenu
git clone https://git.suckless.org/slstatus
```

### 2.安装补丁

dwm必装补丁（1个）：**systray**

st必装补丁（3个）：

* **alpha**（自行修改透明度：0.75）
* **anysize**
* **scrollback**

安装补丁：

```bash
patch -p1 < xx.diff
```

### 3.编辑源代码

> dwm

config.h

```bash
static const unsigned int borderpx  = 0;
static const int topbar             = 0;
static const char col_gray4[]       = "#f4606c";
static const char col_cyan[]        = "#222222";
```

```bash
static const char *fonts[]          = { "Microsoft Yahei:size=14:antialias=true:autohint=true","Symbols Nerd Font:pixelsize=22:antialias=true:autohint=true" };
static const char dmenufont[]       = "Microsoft Yahei:size=14:antialias=true:autohint=true";
```

```bash
static const Rule rules[] = {
	/* xprop(1):
	 *	WM_CLASS(STRING) = instance, class
	 *	WM_NAME(STRING) = title
	 */
	/* class      instance    title       tags mask     isfloating   monitor */
	{ "Pcmanfm",  NULL,       NULL,       0,            1,           -1 },
	{ "flameshot",NULL,       NULL,       0,            1,           -1 },
};
```

```bash
static const Layout layouts[] = {
	/* symbol     arrange function */
	{ "Tile",     tile },    /* first entry is default */
	{ "Null",     NULL },    /* no layout function means floating behavior */
	{ "[M]",      monocle },
};
```

```bash
#define MODKEY Mod4Mask
```

* 启动器的快捷键改为<kbd>Super</kbd>+<kbd>A</kbd>
* 关闭窗口的快捷键改为<kbd>Super</kbd>+<kbd>Shift</kbd>+<kbd>Q</kbd>
* 退出dwm的快捷键改为<kbd>Super</kbd>+<kbd>Shift</kbd>+<kbd>E</kbd>
* 打开终端的快捷键改为<kbd>Super</kbd>+<kbd>Enter</kbd>
* 提升窗口的快捷键改为<kbd>Super</kbd>+<kbd>Shift</kbd>+<kbd>Enter</kbd>

~/.upvol.sh

```bash
amixer set Master 5%+
```

~/.downvol.sh

```bash
amixer set Master 5%-
```

加权：

```bash
chmod +x ~/.upvol.sh
chmod +x ~/.downvol.sh
```

---

```bash
static const char *webcmd[]   = { "google-chrome-stable", NULL };
static const char *vpncmd[]   = { "google-chrome-stable --proxy-server=\"http://127.0.0.1:7890\"", NULL };
static const char *filecmd[]  = { "pcmanfm", NULL };
static const char *upvol[]    = { "/home/yuxiang/.upvol.sh", NULL };
static const char *downvol[]  = { "/home/yuxiang/.downvol.sh", NULL };
```

* 打开Chrome的快捷键改为<kbd>Super</kbd>+<kbd>S</kbd>
* 打开代理Chrome的快捷键改为<kbd>Super</kbd>+<kbd>G</kbd>
* 打开PCManFM的快捷键改为<kbd>Super</kbd>+<kbd>C</kbd>
* 调高音量快捷键改为<kbd>Super</kbd>+<kbd>Z</kbd>
* 调低音量快捷键改为<kbd>Super</kbd>+<kbd>Shift</kbd>+<kbd>Z</kbd>

> dmenu

config.h

```bash
static int topbar = 0;
```

```bash
static const char *fonts[] = {
	"Microsoft Yahei:size=14:antialias=true:autohint=true"
};
```

> slstatus

config.h

```bash
static const struct arg args[] = {
	/* function format          argument */
	{ run_command,	"\uf303 %s | ",	"uname -r | awk -F \"-\" ' { print $1 } '" },
	{ cpu_perc,	"\ufb19 %s%% | ",	NULL },
	{ ram_perc,	"\uf2db %s%% | ",	NULL },
	{ run_command,	"\uf028 %s | ",	"amixer sget Master | awk -F \"[][]\" ' /Mono:/ { print $2 }'" },
	{ datetime, "%s",           "%F %T" },
};
```

> st

config.mk

```bash
X11INC = /usr/include/X11
X11LIB = /usr/include/X11
```

config.h

```bash
static char *font = "monospace:pixelsize=14:antialias=true:autohint=true";
```

### 4.编译源代码

```bash
make
make clean
```

编译顺序：`dwm` - `dmenu` - `slstatus` - `st`

## 1.使用ArchLinuxCN源

> 以root用户登录

```bash
pacman -Syyu
vim /etc/pacman.conf
```

按下<kbd>/</kbd>输入Color，定位到`#Color`，**删掉**前面的`#`号

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

安装密钥

```bash
pacman -S archlinuxcn-keyring
```

---

如果在安装密钥的过程中报错`could not be locally signed`，可以先执行下面的命令：

```bash
pacman -Syu haveged
systemctl start haveged
systemctl enable haveged

rm -rf /etc/pacman.d/gnupg
pacman-key --init
pacman-key --populate archlinux
```

再安装archlinuxcn密钥：

```bash
pacman -S archlinuxcn-keyring
```

## 2.安装X窗系统、字体

X窗系统及其他：

```bash
pacman -S xorg-server xorg-xinit
pacman -S base-devel feh picom libxft polkit
pacman -S git unzip
pacman -S alsa-utils
pacman -S yay
```

字体：

```bash
pacman -S noto-fonts noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
pacman -S ttf-nerd-fonts-symbols
```

## 3.创建新用户

创建用户：

```bash
useradd -m -g users -G wheel -s /bin/bash yuxiang
```

设置密码：

```bash
passwd yuxiang
```

编辑新用户权限：

```bash
EDITOR=vim visudo
```

按下<kbd>/</kbd>搜索`wheel`，然后<kbd>Enter</kbd>

定位到`# %wheel ALL=(ALL) ALL`，在`#`号下按**2**次<kbd>X</kbd>删除注释

按<kbd>Esc</kbd>输入`:wq`退出Vim

输入`exit`返回登录界面，使用刚创建的账户登录

## 4.安装dwm并配置工作环境

这里要连接外部U盘复制一些东西

将Windows下的`msyh.ttf`、`msyhbd.ttf`、`simhei.ttf`字体文件复制到`/usr/share/fonts`目录下

终端输入`alsamixer`进入调音台，在“Master”选项卡下按下<kbd>↑</kbd>键调节音量，然后按下<kbd>M</kbd>键取消静音

将已经写好的suckless系列软件的源代码复制到Downloads目录下，然后切换到源代码目录执行下面的命令安装：

```bash
make && sudo make clean install
```

安装顺序为`dwm` > `dmenu` > `slstatus` > `st`

复制一份xinitrc配置文件到家目录并编辑：

```bash
cp /etc/X11/xinit/xinitrc ~/.xinitrc
vim ~/.xinitrc
```

在最后显示`fi`段后插入（`fi`后面还有东西就删掉）：

```bash
......
	unset f
fi # 下面插入！如果下面有东西就删掉！

exec picom -CGb &
exec slstatus &
exec dwm
```

输入`reboot`重启

启动dwm：

```bash
startx
```

安装浏览器：

```bash
yay -S google-chrome
```

配置~/.bashrc：

```bash
vim ~/.bashrc
```

```bash
echo -e "\e[31m DO NOT USE \"sudo rm -rf /*\" ON THIS PC. \e[0m"
alias l='lsblk'
alias n='neofetch'
alias e='exit'
alias u='sudo umount -R /mnt'
alias P='poweroff'
alias R='reboot'
alias S='systemctl hybrid-sleep'
alias U='sudo pacman -Syyu'
alias N='export https_proxy=http://127.0.0.1:7890;export http_proxy=http://127.0.0.1:7890;export all_proxy=socks5://127.0.0.1:7890'
alias O='unset http_proxy;unset https_proxy'
```

安装fcitx输入法：

```bash
sudo pacman -S fcitx5-im fcitx5-configtool
```

安装fcitx提供的中文输入包：

```bash
sudo pacman -S fcitx5-chinese-addons
```

安装主题皮肤：

```bash
sudo pacman -S fcitx5-material-color
```

设置环境变量，让其它程序也能使用这个中文输入法：

```bash
vim ~/.pam_environment
```

按<kbd>I</kbd>输入：

```bash
INPUT_METHOD DEFAULT=fcitx5
GTK_IM_MODULE DEFAULT=fcitx5
QT_IM_MODULE DEFAULT=fcitx5
XMODIFIERS DEFAULT=\@im=fcitx5
```

按下<kbd>Esc</kbd>输入`:wq`保存退出

先运行`fcitx5`，再打开`fcitx5-configtool`配置输入法（后面按下<kbd>Ctrl</kbd>+<kbd>空格</kbd>来切换输入法），还可以设置一下皮肤、是否启用云拼音等

```bash
feh --randomize --bg-fill ~/Downloads/demo.jpg
```

设置开机自动启用数字键：

```bash
sudo pacman -S numlockx
```

编辑.xinitrc：

```bash
vim ~/.xinitrc
```

在文档末`fi`下面插入（注意还有一个`&`符号！）：

```bash
......
	unset f
fi # 下面插入！如果下面有东西就删掉！

numlockx &
exec feh --randomize --bg-fill ~/Downloads/demo.jpg &
exec picom -CGb &
exec fcitx5 &
exec slstatus &
exec dwm
```

注意，`numlockx &`必须添加在`exec`命令之前

接着重新启动dwm即可

## 5.安装显卡驱动

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

完成后重启系统（因为要屏蔽nouveau内核模块），接着手动创建配置文件：

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

**NVIDIA显卡驱动导致部分录屏软件花屏的解决办法**：

1. 修改配置文件

   ```bash
   sudo vim /etc/X11/xorg.conf.d/20-nvidia.conf
   ```

2. 如果配置文件中存在DRI，请把它注释掉

   ```bash
   #    Load        "dri"
   ```

3. 修改`Section "Device"`选项，修改`Option "NoFlip" "false"`为`Option "NoFlip" "true"`

   ```bash
   Section "Device"
      Identifier     "Device0"
      Driver         "nvidia"
      VendorName     "NVIDIA Corporation"
      Option "NoFlip" "true"
   EndSection
   ```

4. 重启系统后生效

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

## 6.安装软件

**安装conky**

```bash
sudo pacman -S conky
```

创建conky配置文件：

```bash
vim ~/.conkyrc
```

并在里面输入：

```bash
background no
use_xft yes
xftfont Microsoft Yahei:size=14
xftalpha 0.75
update_interval 5.0
total_run_times 0
own_window yes
own_window_type override
own_window_transparent yes
own_window_hints undecorated,below,skip_taskbar,sticky,skip_pager
double_buffer yes
default_color grey
alignment middle_right
no_buffers yes
uppercase no
cpu_avg_samples 2
net_avg_samples 2
override_utf8_locale no

TEXT
${color #f4606c}${alignc}${nodename} ${uptime_short}

${color #f4606c}CPU: ${color grey}$cpu%
${color #f4606c} ${cpugraph 16,140 000000 7f8ed3}
${color #f4606c}RAM: $color$mem/$memmax
${color #f4606c} ${membar 6,140}

${color #f4606c}File Systems:
${color #f4606c}/ $color${fs_free /}
${color #f4606c} ${fs_bar 6,140 /}

${color grey}In: ${tcp_portmon 1 32767 count}  Out: ${tcp_portmon 32768 61000 count}${alignr}
```

保存退出后，编辑`~/.xinitrc`文件，在`exec dwm`前面插入`exec conky &`，如：

```bash
exec feh --randomize --bg-fill ~/Pictures/Wallpapers/sky.png &
exec picom -CGb &
exec fcitx5 &
exec slstatus &
exec conky &
exec dwm
```

---

**安装文件管理器**

```bash
sudo pacman -S gvfs pcmanfm
```

---

**安装火焰截图**

```bash
sudo pacman -S flameshot
```

---

**安装Clash**

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