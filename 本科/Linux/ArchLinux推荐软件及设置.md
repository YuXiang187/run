<div align="right"><a href="https://github.com/YuXiang187/run"><img src="./assets/run_logo.svg" alt="SVG Image" height="50"></a></div>
<p align="right">当前所在位置：<strong>run > 本科 > Linux</strong></p>

# ArchLinux推荐软件及设置

## 1.基本软件

```bash
sudo pacman -S gwenview krita
```

```bash
sudo pacman -S bleachbit scrcpy gimp
```

```bash
sudo pacman -S kdenlive obs-studio
```

```bash
sudo pacman -S pandoc-cli
yay -S typora
```

```bash
yay -S sublime-text-4
```

```bash
yay -S wps-office-cn wps-office-mui-zh-cn ttf-wps-fonts libtiff5
```

```bash
sudo pacman -S steam
yay -S proton
```

## 2.炫技软件

### 终端小火车

```bash
sudo pacman -S sl
```

使用：`sl <option>`

* `-a`：火车上的人们会呼救
* `-l`：显示小一点的火车
* `-F`：会飞的火车
* `-e`：允许按下<kbd>Ctrl</kbd>+<kbd>C</kbd>中断火车

无限小火车：`while true;do sl;done`

### 终端代码雨

```bash
sudo pacman -S cmatrix
```

使用：`cmatrix <option>`

- `-b`：随机粗体

- `-B`：全部粗体

- `-o`：使用旧风格滚动（不好看）

- `-x`：显示不一样的符号

- `-u`：滚动的快慢，0-9任意选

- `-C`：显示的颜色，默认`green`

  可选：`red`、`blue`、`white`、`yellow`、`cyan`、`magenta`、`black`

按下<kbd>Ctrl</kbd>+<kbd>C</kbd>或者<kbd>Q</kbd>退出

### 终端自动炫技

```bash
yay -S hollywood
```

使用：`hollywood`

### 终端会说话的牛

```bash
sudo pacman -S cowsay
```

使用：`cowsay "Hello"`（终端输出`Hello`）

* `-l`：查动物
* `-f <name>`：换动物

### 终端打效果字

```bash
yay -S toilet
```

例如：

```bash
toilet -f mono12 -F metal OpenSkill
```

* `-f <name>`：设置字体
* `-w <width>`：设置输出宽度
* `-t`：适应终端宽度
* `-F <option>`：
  * `crop`：纯白色
  * `rainbow`：彩虹
  * `metal:`：金属
  * `flip`：镜像水平反转
  * `flop`：镜像垂直反转
  * `180`：旋转180度
  * `left`：左垂直显示
  * `right`：右垂直显示
  * `border`：加边框
* `-E html`：导出为HTML

### 终端打大字

```bash
sudo pacman -S figlet
```

使用`figlet <text>`即可输出大字

## 3.系统设置

### 调节鼠标灵敏度

安装`xorg-xinput`：

```bash
sudo pacman -S xorg-xinput
```

查看鼠标ID：

```bash
xinput list
```

设置鼠标灵敏度：

```bash
xinput --set-prop 8 'libinput Accel Speed' -0.6
```

注意：“-0.6”是要设置的鼠标灵敏度（范围为[-1,1]），“8”要修改为你自己鼠标的ID！

### 添加HP打印机

```bash
sudo pacman -S cups hplip
yay -S hplip-plugin
```

```bash
sudo systemctl start cups.service
sudo systemctl enable cups.service
```

浏览器进入127.0.0.1:631，（用户名和密码输入当前用户的）选择Administration > Add Printers，选中你要添加的打印机，然后继续完成设置

### 全局热键

#### 模拟按键

安装模拟按键软件xdotool

```bash
sudo pacman -S xdotool
```

模拟两个按键<kbd>Alt</kbd>+<kbd>Tab</kbd>

```bash
xdotool key alt+Tab
```

自动输入`word`

```bash
xdotool type 'word'
```

模拟鼠标点击：移动到`(x,y)`，然后点击鼠标左键（1左，2中，3右）

```bash
xdotool mousemove 655 320 click 1
```

重复点击鼠标右键1次

```bash
xdotool click -repeat 1 3
```

获取鼠标位置

```bash
xdotool getmouselocation
```

#### 全局热键

安装全局热键设置软件xbindkeys

```bash
sudo pacman -S xbindkeys
```

生成默认配置文件

```bash
xbindkeys --defaults > ~/.xbindkeysrc
```

辅助按键显示

```bash
xbindkeys -k
```

重启xbindkeys

```bash
killall xbindkeys
xbindkeys
```

#### 示例配置

认识/下一个（/）

```bash
xdotool mousemove 91 712 click 1
```

模糊（*）

```bash
xdotool mousemove 205 712 click 1
```

不认识/记错了（-）

```bash
xdotool mousemove 316 712 click 1
```

拼写（+）

```bash
xdotool mousemove 306 63 click 1
```

隐藏输入法（`）

```bash
xdotool mousemove 354 520 click 1
```

选项一（1）

```bash
xdotool mousemove 199 329 click 1
```

选项二（2）

```bash
xdotool mousemove 199 410 click 1
```

选项三（3）

```bash
xdotool mousemove 199 487 click 1
```

选项四（4）

```bash
xdotool mousemove 199 569 click 1
```

开始拼写（9）

```bash
xdotool mousemove 278 555 click 1
```

继续复习（0）

```bash
xdotool mousemove 287 700 click 1
```

## 4.软件设置

### Minecraft我的世界

存储Minecraft启动器账户登录信息需要先安装`gnome-keyring`

```bash
sudo pacman -S gnome-keyring
```

使用Vim编辑`~/.xinitrc`，添加：

```bash
eval $(/usr/bin/gnome-keyring-daemon --start --components=pkcs11,secrets,ssh)
export SSH_AUTH_SOCK
```

最后安装Minecraft：

```bash
yay -S minecraft-launcher
```

安装Forge，请前往[https://files.minecraftforge.net](https://files.minecraftforge.net)下载文件，然后使用`java -jar <file>`启动下载的文件

安装Optifine，请前往[https://optifine.net](https://optifine.net)下载文件，然后放到`.minecraft`下的`mods`文件夹

---

PVP玩家可以选择：

Lunar客户端：

```bash
yay -S lunar-client
```

Badlion客户端：

```bash
yay -S badlion-client
```

---

解决Minecraft旧版本无法输入中文的问题：

**1.安装软件包**

```bash
sudo pacman -S zenity xbindkeys xdotool
```

**2.设置脚本**

```bash
vim ~/.mcinput.sh
```

下面的脚本来自依云's Blog，链接：[https://blog.lilydjwg.me/2015/5/17/input-chinese-to-minecraft-in-linux.93167.html](https://blog.lilydjwg.me/2015/5/17/input-chinese-to-minecraft-in-linux.93167.html)，非常感谢他解决了我的问题

```bash
chars=$(zenity --title 中文输入 --text 中文输入 --width 500 --entry 2>/dev/null)
sleep 0.1
xdotool key --delay 150 Escape t
sleep 0.2
xdotool type --delay 150 "$chars"
xdotool key Return
```

**3.设置全局热键F12**

生成默认配置文件

```bash
xbindkeys --defaults > ~/.xbindkeysrc
```

辅助按键显示，在空白窗口弹出后按下F12

```bash
xbindkeys -k
```

接着把终端输出的内容复制到`~/.xbindkeysrc`，再编辑一下该按键要执行的命令，如：

```bash
vim ~/.xbindkeysrc
```

```bash
"sh ~/.mcinput.sh"
    m:0x0 + c:96
    F12
```

最后启动Xbindkeys

```bash
xbindkeys
```

设置进入桌面自动启动Xbindkeys

```bash
vim ~/.xinitrc
```

```bash
# 添加到exec命令之前
xbindkeys &
exec your_window_manager
```

完成了，以后在打开MC时按下F12输入你想输入的内容，然后按下回车就可以直接输入中文了

### XP-Pen数位板驱动

```bash
yay -S xp-pen-tablet
```

需要以root账户运行的解决办法：

```bash
sudo chown $(whoami) /usr/lib/pentablet
sudo chmod +x /usr/lib/pentablet/pentablet
```

Chrome手写输入插件：**Google 输入工具**

如果你有电子白板的需求，可以安装OpenBoard

```bash
yay -S openboard
```

### Android Studio安卓开发

```bash
yay -S android-studio
```

修复启动时空白界面的问题：

```bash
sudo vim /etc/environment
```

```bash
_JAVA_AWT_WM_NONREPARENTING=1
```

Git图形界面管理器：

```bash
yay -S gitkraken
```

### Vim终端文本编辑器

> 无插件版

```bash
syntax on
set relativenumber
set cursorline
set wrap
set showcmd
set wildmenu
set hlsearch
set incsearch
set ignorecase
set nocompatible
set fileencodings=utf-8,gbk,utf-16le,cp1252,iso-8859-15,ucs-bom
set termencoding=utf-8
set encoding=utf-8
set scrolloff=4
set clipboard=unnamedplus

let mapleader = " "

vnoremap <LEADER>p "+p
vnoremap <LEADER>y "+y

map Q :q<CR>
map W :w<CR>
map ro :set relativenumber<CR>
map rf :set norelativenumber<CR>

map sl :set splitright<CR>:vsp<CR>
map sh :set nosplitright<CR>:vsp<CR>
map sk :set nosplitbelow<CR>:sp<CR>
map sj :set splitbelow<CR>:sp<CR>

map wl <C-w>l
map wk <C-w>k
map wh <C-w>h
map wj <C-w>j

map tn :tabe<CR>
map tl :tabn<CR>
map th :tabp<CR>

map <LEADER>fd /\(\<\w\+\>\)\_s*\1
map <LEADER>sc :set spell!<CR>
map <LEADER><LEADER> <Esc>/<++><CR>:nohlsearch<CR>c4l
map <LEADER>se :g/^\s*$/d<CR>:nohlsearch<CR>
map <LEADER>a ggvG$
map <LEADER>ns :nohlsearch<CR>
map <LEADER>d Vyp
map <LEADER>da <Esc>:r !echo `date "+\%Y-\%m-\%d \%H:\%M:\%S"`<CR>

inoremap jj <Esc>
```

> 插件版

```bash
syntax on
set relativenumber
set cursorline
set wrap
set showcmd
set wildmenu
set hlsearch
set incsearch
set ignorecase
set nocompatible
set fileencodings=utf-8,gbk,utf-16le,cp1252,iso-8859-15,ucs-bom
set termencoding=utf-8
set encoding=utf-8
set scrolloff=4
set clipboard=unnamedplus

let mapleader = " "
let &t_SI = "\<Esc>]50;CursorShape=1\x7"
let &t_SR = "\<Esc>]50;CursorShape=2\x7"
let &t_EI = "\<Esc>]50;CursorShape=0\x7"

vnoremap <LEADER>p "+p
vnoremap <LEADER>y "+y

map Q :q<CR>
map W :w<CR>
map ro :set relativenumber<CR>
map rf :set norelativenumber<CR>

map sl :set splitright<CR>:vsp<CR>
map sh :set nosplitright<CR>:vsp<CR>
map sk :set nosplitbelow<CR>:sp<CR>
map sj :set splitbelow<CR>:sp<CR>

map wl <C-w>l
map wk <C-w>k
map wh <C-w>h
map wj <C-w>j

map tn :tabe<CR>
map tl :tabn<CR>
map th :tabp<CR>

map <up> :res-1<CR>
map <down> :res+1<CR>
map <left> :vertical resize-1<CR>
map <right> :vertical resize+1<CR>

map <LEADER>fd /\(\<\w\+\>\)\_s*\1
map <LEADER>sc :set spell!<CR>
map <LEADER><LEADER> <Esc>/<++><CR>:nohlsearch<CR>c4l
map <LEADER>se :g/^\s*$/d<CR>:nohlsearch<CR>
map <LEADER>a ggvG$
map <LEADER>ns :nohlsearch<CR>
map <LEADER>d Vyp
map <LEADER>da <Esc>:r !echo `date "+\%Y-\%m-\%d \%H:\%M:\%S"`<CR>

inoremap jj <Esc>

call plug#begin('~/.vim/plugged')
Plug 'vim-airline/vim-airline'
Plug 'connorholyday/vim-snazzy'
Plug 'preservim/nerdtree'
Plug 'mg979/vim-visual-multi'
Plug 'tpope/vim-speeddating'
call plug#end()

map tt :NERDTreeToggle<CR>
let NERDTreeMapOpenExpl = ""
let NERDTreeMapUpdir = ""
let NERDTreeMapUpdirKeepOpen = "l"
let NERDTreeMapOpenSplit = ""
let NERDTreeOpenVSplit = ""
let NERDTreeMapActivateNode = "i"
let NERDTreeMapOpenInTab = "o"
let NERDTreeMapPreview = ""
let NERDTreeMapCloseDir = "n"
let NERDTreeMapChangeRoot = "y"

let g:SnazzyTransparent = 1

color snazzy
```

**安装插件**

* `vim-airline/vim-airline`
* `connorholyday/vim-snazzy`
* `preservim/nerdtree`
* `vim-visual-multi`
* `tpope/vim-speeddating`

**安装示例**

1. 前往[https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug)下载`plug.vim`插件

2. 安装插件

   ```bash
   mkdir -p  ~/.vim/autoload/
   cp plug.vim  ~/.vim/autoload
   ```

3. 添加或删除插件

   编辑 ~/.vimrc 文件中的内容

   ```bash
   call plug#begin('~/.vim/plugged')
   Plug 'vim-airline/vim-airline'
   Plug 'connorholyday/vim-snazzy'
   Plug 'preservim/nerdtree'
   Plug 'mg979/vim-visual-multi'
   Plug 'tpope/vim-speeddating'
   call plug#end()
   ```

   运行命令重新加载：

   ```bash
   :source ~/.vimrc
   ```

4. 安装或卸载插件（需要先安装`git`）

   打开 vim 使用命令：`PlugInstall`
   打开 vim 使用命令：`PlugClean`

### Sublime Text文本编辑器

记得安装`Theme-Soda`主题

```bash
{
    "color_scheme": "Packages/Color Scheme - Default/Monokai.sublime-color-scheme",
    "font_face": "Microsoft Yahei",
    "font_size": 16,
    "caret_style": "smooth",
    "soda_classic_tabs": true,
    "theme": "Soda Dark 3.sublime-theme",
    "ignored_packages": [
        "Vintage",
    ],
    "update_check": false,
    "tab_size": 4,
    "translate_tabs_to_spaces": true,
    "expand_tabs_on_save": true,
}
```

推荐插件：

* **ConvertToUTF8**：其他编码转换成UTF8编码
* **DeleteBlankLines**：去除空段插件