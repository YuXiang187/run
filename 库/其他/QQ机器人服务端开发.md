# QQ机器人服务端开发

记得屏蔽`/echo`功能防止机器人被发现！

* `on_keyword`：创建消息关键词匹配事件响应器

```python
from nonebot import on_keyword
from nonebot.adapters.onebot.v11 import Event
from nonebot.adapters.onebot.v11 import Message

catch_str = on_keyword({'今日', '今天'})


@catch_str.handle()
async def send_msg(event: Event):
    get_msg = str(event.get_message())
    msg = "[CQ:at,qq={}]".format(event.get_user_id()) + get_msg
    await catch_str.finish(Message(f'{msg}'))
```

```python
import threading
import time

from nonebot import on_message
from nonebot.adapters.onebot.v11 import Event
from nonebot.adapters.onebot.v11 import Message

timer = 0
times = 0

reply_msg = on_message()


@reply_msg.handle()
async def send_msg(event: Event):
    global timer
    global times
    if timer < 7:
        times = (times + 1)
    else:
        times = 0
    timer = 0
    if (times >= 5) and (timer < 7):
        times = 0
        await reply_msg.finish(Message(f"{str(event.get_message())}"))


def while_thread():
    global timer
    while True:
        timer = (timer + 1)
        if timer > 12:
            timer = 7
        time.sleep(1)


LongtimeThread = threading.Thread(target=while_thread)
LongtimeThread.start()
```

如何安装nonebot插件？定位到你的bot目录，输入：

```bash
nb plugin install <name>
```

插件配置会自动添加至配置文件

更多内容参见[NoneBot开发文档](https://v2.nonebot.dev)