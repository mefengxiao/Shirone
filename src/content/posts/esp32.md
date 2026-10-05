---
title: 灵车，用 ESP32S3 做硬件通行密钥
published: 2026-10-05
publishedAt: 2026-10-05T16:07:28+08:00
description: 'ESP32 改通行密钥的方法'
image: ''
tags: [esp32]
category: '硬件'
draft: false 
lang: ''
---

最近入手了一个立创的 ESP32S3 开发板，但是面包板还没有到。所以，看了一下有没有什么项目可以做下，就有了这个文章

## 刷写

打开 [picokeys 刷写](https://www.picokeys.com/esp32-flasher/) 网站

1. 在下方选择 **Pico Fido** ，然后 **Connect** 再将ESP32连接电脑（一定要用数据线）连接

2. 电脑上会出现 ESP32 所在的串口，将它连接

3. 网页会弹出一个选项框，在网页上选择 **Install Pico Fido** 等待它写入固件
    - 如果 ESP32 内有项目它会提示清除，请选择清除

## 写 VIDPID

再来到网页下面，可以看见超链接 [Pico Commissioner](https://www.picokeys.com/pico-commissioner/)

但是，Pico Commissioner 已经被开发者下线并替换成收费项目 那怎么办呢？

vtumi 大佬给出了解决方案 [pico-fido](https://github.com/vtumi/pico-fido/)

也可以使用大佬给的网站配置 [phphy](https://passkey.phphy.com/)

在网站内有些配置，我介绍一下需要更改的内容

**产品名称** ：可以随便填，我这里填写 `esp32yubikey`

**USB VID:PID 预设** ；选择 **Yubikey 4/5**

**硬件参数** ：可以根据你的 ESP32 硬件配置，其他可根据自己要求选择

点击 **Webusb 写入**，选择你的 ESP32 设备

写入成功后，再点击 **WebAuthn 写入** 选择外部安全密钥并配置密码

> [!IMPORTANT]
> 写入似乎不支持 Firefox 内核的浏览器，请使用 Chromium 内核的浏览器