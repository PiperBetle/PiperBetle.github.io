---
layout: post
title: "Electron 软件简单修改——去除全屏化"
tags: 逆向
---

最近在上网课，软件（有道领世）一打开就直接全屏化了，右上角只有最小化和关闭两个按钮，非常不方便，决定想个办法去除全屏化。  
> 以下均默认安装 scoop 环境，每条指令都使用管理员权限在 pwsh 中运行。若不是，请按照你的 shell 进行修改。

首先打开软件，一股 Electron 的风味，来验证一下？打开安装目录，文件夹 resources 里面有 app.asar 文件，看到这个，可以确定是 Electron 编写的。只有 Electron 会用 .asar 文件来运行，而这个文件就是 Electron 运行时的主要文件。  
.asar 文件并没有加密或压缩而是只简单进行了打包来减少小文件数量减少寻址，所以只需要解包就行了。
```ps1
scoop install nodejs # 安装 nodejs
npm install -g asar # 安装 asar
cp app.asar app.asar.old # 复制一份原文件防炸
asar extract app.asar.old ydls # 把 app.asar 解包到 ydls 文件夹
```
这样就实现了 .asar 文件的解包。  
接下来打开 ydls/dist/main/main.js，这个 main.js 就是 Electron 程序启动的入口。  
这个 main.js 可能写的比较混乱，进行了压缩或混淆，只需要格式化或反混淆就可以了。  
由于想要去除全屏化，所以搜索 fullscreen 试试看。
```js
g=new c.BrowserWindow({show:!1,width:1440,height:1086,resizable:!0,fullscreen:!0,icon:((...t)=>a.default.join(e,...t))("icon.png"),webPreferences:{contextIsolation:!0,webSecurity:!1,preload:a.default.join(__dirname,"preload.js"),webviewTag:!0}})
```
容易猜到，这个 g 就是新建的窗口，后面那些是初始化。`fullscreen:!0` 是什么意思？默认 `fullscreen` 不为 $0$？默认全屏！那我把 `fullscreen:!0` 改成 `fullscreen:0` 是不是就好了……
进行修改后，还需要再次打包。
```ps1
asar pack ydls app.asar # 把文件夹 ydls 打包为 app.asar（若已存在 app.asar 会进行替换）
```
这个时候再次打开软件，发现全屏化没了。原来他的最小化和关闭按钮只是皮套啊，真正的最小化最大化关闭是被全屏隐藏起来了。