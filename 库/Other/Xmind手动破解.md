# Xmind手动破解

1. 从Xmind官网下载最新版软件，并且完成安装，登录账号。

2. 屏蔽Hosts，防止软件联网校验是否正版。

   ```
   127.0.0.1  www.xmind.app
   127.0.0.1 www.xmind.net
   127.0.0.1 www.xmind.cn
   ```

3. 修改软件配置文件，Win + E 打开资源管理器，地址栏粘贴 `%Appdata%\XMind\Electron v3\vana\state\`

4. 打开文件`account.json`编辑里面的内容

5. 将里面的`"rawSubscriptionData"`换成下面的激活内容，保存文件。

   ```
   WUnYY8kQKgX3kjftuV3gnl+b7lLsBaQjZv1C8AbQBBIn9RiEkGiJGlk/9EAsI5E6uuxGTkhnf5D5Si2buztQGEaLXzVXzFzsMmdXw5fzb+Oo6I78/xNPCRfOKSOlrtOveGdYX+GZJKXJSG77/hb93Tgst5/v1BqS+PdKHwd3dMg=
   ```

6. `account.json`文件属性选择只读，保存。

7. 激活码有效期到2022-11-25，因此需要使用RunAsDate修改软件所在的时间。

   [https://www.nirsoft.net/utils/run_as_date.html](https://www.nirsoft.net/utils/run_as_date.html)

   选择Xmind安装目录，勾选立即模式，时间选择2022年11月之前的时间即可。
