<div align="center">
<h1>JsHook</h1>

[![Xposed](https://img.shields.io/badge/-Xposed-3DDC84?style=flat&logo=Android&logoColor=white)](#)
[![GitHub release](https://img.shields.io/github/release/Xposed-Modules-Repo/me.jsonet.jshook.svg)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases/latest)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Channel&color=0088cc)](https://t.me/jshookapp)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Chat&color=0088cc)](https://t.me/jshookgroup)
[![GitHub Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/me.jsonet.jshook/total?label=GitHub%20Downloads&logo=github&color=0088cc)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases)
[![LSPosed Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/me.jsonet.jshook/total?label=LSPosed%20Downloads&logo=Android&labelColor=F48FB1&logoColor=ffffff&color=0088cc)](https://modules.lsposed.org/module/me.jsonet.jshook)

hook artifact in android support java layer and native layer

[中文的README](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/blob/main/README.md)
</div>

## About the module

Xposed is a module framework that can change the behavior of your system and applications without touching any APK. This means that modules can work on different versions and even ROMs without any changes.

JsHook is the use of Xposed framework for the initialization of any APP to inject Frida, Xposed module development requires a certain base of Java syntax, high technical threshold, hook only supports the java layer, while JsHook injection of Frida is great, only need to be a short Js syntax base, you can use the phone to quickly make their own hook plug-in, and hook support java layer and native layer.

## Module compatibility

1. Xposed api 82
2. Android 7 - 12

## How to use the module

### How to enable scripts

Before enabling the script, please make sure the selected application has enabled the hook service option, if it is LSPosed non-global scope in addition to check the system when activating the module also need to check the corresponding script effective application, each time you change the script content need to restart the app being hooked.

### Why does the script enabled application flash back

JsHook do things very simple, to help developers inject Frida into the app, if the injected app open flashback that is Frida is not compatible with the current model, you can click the technical framework link below to github submit issues feedback to Frida author, JsHook will also be the first time to follow up Frida version.
