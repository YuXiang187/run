<div align="right"><a href="https://github.com/YuXiang187/run"><img src="./assets/run_logo.svg" alt="SVG Image" height="50"></a></div>
<p align="right">当前所在位置：<strong>run > 本科 > 其他</strong></p>

# Git使用

## 基本使用

前往[Git官网](https://git-scm.com/)下载安装包，ArchLinux用户可直接使用pacman安装

配置用户和邮箱：

```bash
git config --global user.name YuXiang
git config --global user.email yuxiang@gmail.com
```

初始化：

```bash
git config --global http.sslVerify "false"
```

* `git clone <url>`：克隆项目
* `git init`：在项目的文件夹下进行git初始化

提交代码：

1. 让git把当前文件夹内的所有文件提交到暂存区

   ```bash
   git add .
   ```

   下面是只提交一个文件到暂存区

   ```bash
   git add main.py
   ```

2. 提交代码到仓库

   ```bash
   git commit -m "task_1 were completed"
   ```

查看提交历史记录（包括作者、时间、备注）

```bash
git log
```

---

回退到某一版本

```bash
git reset --hard <commit ID>
```

注意：--hard参数会删除回退点之前的所有信息，谨慎使用

打上标签

```bash
git tag -a <tag> <commit ID>
```

查看标签

```bash
git tag
```

## 分支

创建分支：

```bash
git branch <branchname>
```

切换分支：

```bash
git checkout <branchname>
```

合并分支：

```bash
git merge <branchname>
```

删除分支：

```bash
git branch -d <branchname>
```

列出所有分支：

```bash
git branch
```

## 添加远程仓库

这里以Github为例

指定一个简单的名字，以便用来引用：

```bash
git remote add origin <url>
```

生成SSH Key：

```bash
ssh-keygen -t rsa -C "yuxiang@gmail.com"
```

如果提示没有此命令需要添加环境变量`..\Git\usr\bin\ssh-keygen.exe`

这里的邮箱改为你在Github上注册的邮箱

成功的话会在`~/`下生成`.ssh`文件夹，进去，打开`id_rsa.pub`，复制里面的`key`

---

回到Github上，进入 Account => Settings（账户配置）

左边选择`SSH and GPG keys`，然后点击`New SSH key`按钮，title设置标题，可以随便填，粘贴在你电脑上生成的`key`

完成后验证是否成功：`ssh -T git@github.com`

```bash
mkdir test
cd test
#echo "hello" >> README.md
git init
git add README.md
git commit -m "添加README.md文件"
```

提交到Github

```bash
git remote add origin git@github.com:YuXiang187/test.git
git push -u origin master
```

---

查看所有远程仓库

```bash
git remote -v
```

删除远程仓库

```bash
git remote rm <name>
```

## 提取远程仓库

从远程仓库下载新分支与数据：

```bash
git fetch origin
```

从远端仓库提取数据并尝试合并到当前分支：

```bash
git merge origin/master
```

## 推送远程仓库

```bash
#echo "hello" >> test.md
git add test.md
git commit -m "add hello"
```

```bash
git push origin master
```