<div align="right"><a href="https://github.com/YuXiang187/run"><img src="./assets/run.png"></a></div>
<p align="right">当前所在位置：<strong>run > 本科 > 其他</strong></p>

# Python自动化代码

安装所需库

```bash
pip install opencv-contrib-python==4.5.5.62
pip install opencv-python==4.5.5.62
pip install pyautogui
pip install Pillow
```

模拟键盘鼠标点击

```python
import os
import pyautogui

os.startfile('C:\Windows\System32\win32calc.exe')
pyautogui.moveTo(166, 258, duration=1)  # 延迟1秒移动鼠标
pyautogui.click()  # 点击
pyautogui.doubleClick()  # 双击
# pyautogui.click(button='right')  # 按下鼠标右键

pyautogui.keyDown('6')  # 按下“6”
pyautogui.keyUp('6')  # 抬起“6”
```

点击图片所在坐标

```python
def click_img(img_path):
    """
    点击图片所在坐标
    :param img_path:图片路径
    """
    pyautogui.screenshot().save("./pic/screenshot.png")  # 保存截图
    img_screenshot = cv2.imread("./pic/screenshot.png")  # 载入截图
    img_model = cv2.imread(img_path)  # 图像模板
    height, width, channel = img_model.shape  # 读取模板宽高
    result = cv2.matchTemplate(img_screenshot, img_model, cv2.TM_SQDIFF_NORMED)  # 进行模板匹配
    upper_left = cv2.minMaxLoc(result)[2]  # 解析出匹配区域的左上角坐标
    lower_right = (upper_left[0] + width, upper_left[1] + height)  # 计算匹配区域右下角的坐标
    x = int((upper_left[0] + lower_right[0]) / 2)  # 获取x坐标
    y = int((upper_left[1] + lower_right[1]) / 2)  # 获取y坐标
    pyautogui.click(x, y, duration=1, button='left')  # 点击指定坐标
```

返回进程PID

```python
def return_pid(process_name):
    """
    返回进程pid
    :param process_name: 进程名
    :return: 进程pid
    """
    pl = psutil.pids()
    for pid in pl:
        if psutil.Process(pid).name() == process_name:
            return pid


os.startfile('C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe')
while isinstance(return_pid('chrome.exe'), int):
    print('正在等待浏览器关闭……')
    time.sleep(2)
```

QQ自动回复机器人

```python
from collections import deque
from nonebot import on_message
from nonebot.adapters.onebot.v11 import GroupMessageEvent
from nonebot.adapters.onebot.v11 import Message

is_reply = True
msgs = deque([], 6)


def write_log(msg):
    with open('../lesson_log.txt', 'a') as f:
        f.write(msg + '\n')


def check_num(num, msg):
    global is_reply
    if num == 123456:
        is_reply = True
        write_log("语文老师：" + msg)
    elif num == 123456:
        is_reply = True
        write_log("数学老师：" + msg)


reply_msg = on_message()


@reply_msg.handle()
async def send_msg(event: GroupMessageEvent):
    global is_reply
    global msgs
    if event.group_id == 123456:
        if not str(event.get_message()).startswith("[CQ:image"):
            check_num(int(event.get_user_id()), str(event.get_message()))
            msgs.append(str(event.get_message()))
        if len(set(msgs)) == 2 and is_reply:
            is_reply = False
            await reply_msg.finish(Message(msgs[4]))
```