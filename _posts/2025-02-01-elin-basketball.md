---
layout: post
title: "Elin 投篮 脚本"
tags: 游戏
---

毫无疑问得先安装 keyboard 库和 pyautogui 库。

```bash
pip install -i https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple keyboard
pip install -i https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple pyautogui
```

代码来自于 [BV1f2DrYJEvH](https://www.bilibili.com/video/BV1f2DrYJEvH/)。

`sec` 表示蓄力时长，得按照自己机子的卡顿情况按需调整，$0.63\sim0.66$ 都有可能。

```py
import keyboard
import pyautogui
flag=2
def start():
	global flag
	flag=1
	print("开始")
def end():
	global flag
	flag=2
	print("暂停")
def quit():
	global flag
	flag=0
if __name__=="__main__":
	sec=0.65
	print("按下1开始，按下2暂停，按下0退出")
	keyboard.add_hotkey("1",start)
	keyboard.add_hotkey("2",end)
	keyboard.add_hotkey("0",quit)
	while True:
		if flag==1:
			pyautogui.mouseDown()
			pyautogui.sleep(sec)
			pyautogui.mouseUp()
		elif flag==0:
			break
		else:
			pyautogui.sleep(3)
```