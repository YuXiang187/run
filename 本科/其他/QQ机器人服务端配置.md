<div align="right"><a href="https://github.com/YuXiang187/run"><img src="./assets/run_logo.svg" alt="SVG Image" height="50"></a></div>
<p align="right">当前所在位置：<strong>run > 本科 > 其他</strong></p>

# QQ机器人服务端配置

在PyCharm上创建一个项目，然后在PyCharm中打开终端

安装库：

```bash
pip install nb-cli
```

安装驱动器：

```bash
nb driver
```

选择`Install a Builtin Driver`安装

输入`httpx`回车

---

安装OneBot协议适配器：

```bash
nb adapter
```

选择`Install a Published Adapter`

输入`OneBot`回车

---

创建项目：

```bash
nb create
```

1. 名字自己输
2. 选择`In a "src" folder`
3. 选择`echo`，按下<kbd>空格</kbd>确认，然后回车
4. 选择`OneBot V11`，按下<kbd>空格</kbd>确认，然后回车

---

配置项目：

`.env`文件修改为：

```
ENVIRONMENT=prod
```

如果在Linux环境，则`.env.dev`需要设置`FASTAPI_RELOAD=false`，Windows不用

修改`.env.dev`的端口号为10800

修改`.env.prod`的端口号为10800

---

下载[cqhttp](https://github.com/Mrs4s/go-cqhttp)库的`go-cqhttp_windows_amd64.exe`

Pycharm项目根目录下创建`cqhttp`文件夹，将上诉文件复制到该文件夹内并重命名为`cqhttp.exe`

不要通过双击运行程序，使用shell运行！

输入3（反向Websocket通信）回车

修改`config.yml`：

```
  - ws-reverse:
      # 反向WS Universal 地址
      # 注意 设置了此项地址后下面两项将会被忽略
      universal: ws://127.0.0.1:10800/onebot/v11/ws/
      # 反向WS API 地址
```

设置完成QQ号后，首先运行`bot.py`，再运行`cqhttp.exe`，QQ扫码登录

需要私聊或者群内@机器人才可以使用`/echo`命令

这样服务端就搭建完成了