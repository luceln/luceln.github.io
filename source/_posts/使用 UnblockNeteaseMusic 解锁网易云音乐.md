---
title: 使用 UnblockNeteaseMusic 解锁网易云音乐
tags:
- 网易云音乐
- 软件食用
categories:
- 软件食用
abbrlink: 9be0780d
---

## 前言

本文基于 Windows10，记录使用 UnblockNeteaseMusic 解锁网易云音乐的步骤，仅作参考使用。

<!-- more -->

## 安装 nodejs

可以前往 [Node.js](https://nodejs.org/en/download/ "Node.js官网") 官网下载，也可以去 [淘宝 Node.js 镜像](https://npm.taobao.org/mirrors/node "淘宝 Node.js 镜像") 下载。



## 下载 UnblockNeteaseMusic

GitHub 地址：https://github.com/nondanee/UnblockNeteaseMusic

下载后解压。



## 获取网易云音乐的 ip 地址

打开 cmd，输出

```
ping music.163.com
```

例如我的是 `59.111.181.60` ，复制这个 ip 地址。



## 新建 bat 文件

在 UnblockNeteaseMusic 解压的目录里，新建一个文本文档，然后修改为 `xx.bat`。右键编辑，在 bat 文件里输入

```
@echo off
node app.js -p 2333 -f 59.111.181.60
```

`2333` 是端口号，可以自定义。

`59.111.181.60` 是刚复制好的网易云的 ip 地址。



## 设置网易云客户端

点击`设置 -> 工具 -> 代理`，选择自定义代理。

``` 
服务器：127.0.0.1
端口：2333
```

服务器是本机地址，端口号输入自定义的端口，点击确定即可。

此时，运行 bat 文件，在重启网易云客户端即可正常使用。



## 隐藏运行窗口

由于 bat 文件运行时会有一个 cmd 窗口，并且也不能把它关掉，否则代理会使用不了。这时我们就需要让它在后台运行。

同样在 UnblockNeteaseMusic 解压的目录里新建一个 vbs 文件，名字叫 xx.vbs，然后在 vbs 文件里输入

```
Set ws = CreateObject("Wscript.Shell")
ws.run "cmd /c xx.bat",vbhide
```

以后只要双击这个 vbs 文件即可在后台运行 bat 文件。



## 开机启动 vbs 文件

由于每次启动网易云客户端之前，都要运行 bat 文件，所以我们干脆开机启动 vbs 文件。

使用快捷键 `Win + r` 启动运行，然后输入以下代码打开开机启动项的目录。

```
Shell:startup
```

然后，右键 vbs 文件新建一个快捷方式，然后把这个快捷方式剪切放入开机启动项的目录，以后开机后就会自动在后台运行 bat 文件了。



## 运行网易云客户端的同时运行 bat 文件

如果不想每次都开机启动，而想只在我们使用网易云时才打开的可以用这种方法。

### 找到 `cloudmusic.exe` 所在的路径

可以右键网易云音乐的快捷方式，点击属性。然后复制 `目标(T)` 里的内容。如：

```
C:\Software\Install\CloudMusic\cloudmusic.exe
```



### 修改 xx.vbs 文件

右键编辑 xx.vbs 文件，里面修改成：

```
Dim ws,MusicPath

MusicPath="C:\Software\Install\CloudMusic\cloudmusic.exe"
path = Chr(34) & MusicPath & Chr(34)

Set ws = CreateObject("Wscript.Shell")
ws.run "cmd /c xx.bat",vbhide
ws.Run path,1
```



### 替换快捷方式

执行之前的操作后，每次都要点击 vbs 文件才会同时启动网易云客户端和 bat 文件，直接点之前的网易云客户端的快捷方式并不能启动 bat 文件，所以我们可以把 vbs 文件的快捷方式替换掉网易云的快捷方式。

1. 右键 vbs 文件，新建快捷方式。
2. 右键快捷方式，点击`属性 -> 更改图标 -> 浏览`。
3. 然后找到 `cloudmusic.exe` 所在的位置，把图标换成网易云的图标。
4. 重命名快捷方式为网易云音乐，替换之前的快捷方式。



## 移动端共用

**电脑运行 bat 文件后，让电脑和手机处于同一个局域网内。**

1. 打开 cmd，然后输入 `ipconfig`，复制 ipv4 内网地址 。
2. 打开手机连接的 WiFi 的网络详情，然后选择代理为 `代理自动配置`。
3. 然后在 `PAC 网址` 里输入

```
http://192.168.2.181:2333/proxy.pac
```

`192.168.2.181` 是电脑的 内网 IP 地址，2333 是之前设置的端口。

然后就可以解锁手机端的网易云。



## 参考

[使用 UnblockNeteaseMusic 解锁网易云音乐](https://www.coolapk.com/feed/17372371?shareKey=ODI1NTliMjk3MDUzNWVhMjQ3YTA~&shareUid=1167987&shareFrom=com.coolapk.market_10.1)