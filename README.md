<div align="center">
<h1>JsHook</h1>

[![Xposed](https://img.shields.io/badge/-Xposed-3DDC84?style=flat&logo=Android&logoColor=white)](#)
[![GitHub release](https://img.shields.io/github/release/Xposed-Modules-Repo/me.jsonet.jshook.svg)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases/latest)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Channel&color=0088cc)](https://t.me/jshookapp)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Chat&color=0088cc)](https://t.me/jshookgroup)
[![GitHub Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/me.jsonet.jshook/total?label=GitHub%20Downloads&logo=github&color=0088cc)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases)
[![LSPosed Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/me.jsonet.jshook/total?label=LSPosed%20Downloads&logo=Android&labelColor=F48FB1&logoColor=ffffff&color=0088cc)](https://modules.lsposed.org/module/me.jsonet.jshook)

android中hook神器 支持java层和native层

[README of English](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/blob/main/README.US.md)
</div>

## 关于模块

Xposed是一个模块框架，可以在不接触任何APK的情况下更改系统和应用程序的行为。这意味着模块可以在不同版本甚至ROM上工作而无需任何更改。

JsHook是使用Xposed框架对任意APP的初始化进行注入Frida，Xposed模块开发需要一定的Java语法基础，技术门槛高，hook只支持java层，而JsHook注入的Frida很棒，只需要会简短的Js语法基础，即可用手机快速制作属于自己的hook插件，并且hook支持java层和native层。

## 模块兼容

1. Xposed api 82
2. Android 7 - 12

## 如何使用该模块

### 如何启用脚本

启用脚本前请确认选择的应用已开启hook服务选项，如果是LSPosed非全局作用域在激活模块时除了勾选系统还需勾选对应脚本生效的应用，每次更改脚本内容都需要重启一下被hook的app。

### 启用脚本的应用为什么会闪退

JsHook做的事情很简单，帮助开发者将Frida注入到app，如果注入的app打开闪退那就是Frida不兼容当前机型，可以点击下方技术框架链接去github提交issues反馈给Frida作者，JsHook也会第一时间跟进Frida版本。
