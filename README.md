<div align="center">
<h1>JsHook</h1>

[![Xposed](https://img.shields.io/badge/-Xposed-3DDC84?style=flat&logo=Android&logoColor=white)](#)
[![GitHub release](https://img.shields.io/github/release/Xposed-Modules-Repo/me.jsonet.jshook.svg)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases/latest)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Channel&color=0088cc)](https://t.me/jshookapp)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Chat&color=0088cc)](https://t.me/jshookgroup)
[![LSPosed Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/me.jsonet.jshook/total?label=LSPosed%20Downloads&logo=Android&labelColor=F48FB1&logoColor=ffffff&color=0088cc)](https://modules.lsposed.org/module/me.jsonet.jshook)

android中hook神器 支持java层和native层

[README of English](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/blob/main/README.en.md)
</div>

## 关于模块

Xposed是一个模块框架，可以在不接触任何APK的情况下更改系统和应用程序的行为。这意味着模块可以在不同版本甚至ROM上工作而无需任何更改。

JsHook是使用Xposed框架对任意app的初始化进行注入Rhino/Frida，Xposed模块开发需要一定的Java语法基础，技术门槛高，而JsHook注入的Rhino/Frida很棒，只需要会简短的Js语法基础，即可用手机快速制作属于自己的hook插件，并且hook支持java层和native层。

## 模块兼容

1. Xposed api 82
2. Android 7 - 12

## 如何使用该模块

### 如何启用脚本

启用脚本前请确认选择的应用已开启hook服务选项，如果是LSPosed非全局作用域在激活模块时除了勾选系统还需勾选对应脚本生效的应用，每次更改脚本内容都需要重启一下被hook的app。

### 如何选择注入框架

如果你对Xposed的hook方法比较熟，推荐Rhino，使用js调用Xposed框架的方法，且兼容性高；而Frida属于另一个hook框架，需要对Frida有一定的了解，上手较难，且不支持部分机型和app。

## 注意事项

版本1.0.2之前默认是frida注入，所以之前使用frida的需要在框架管理中将全局默认设置为frida，导入框架目前只支持frida-gadget。

## 脚本说明

### 通用

日志打印：

```js
common.log('...');
```

消息提示：

```js
common.toast('...');
```

获取Context：

```js
common.getcontext();
```

### rhino

hook构造函数

<table>
<thead>
<tr>
<td colspan="4" align="center">hookAllConstructors</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>类名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>构造函数执行前</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>构造函数执行后</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>替换构造函数执行过程</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

示例：

```js
common.hookAllConstructors('com.test.test', function (param) {
    //构造函数执行前
    //打印构造函数接收到的第一个参数
    common.log(param.args[0]);
    //修改这个参数的值
    param.args[0] = 'fuck';
}, function (param) {
    //构造函数执行后
    //...
});
```

hook指定参数的构造函数

<table>
<thead>
<tr>
<td colspan="4" align="center">hookConstructor</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>类名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>参数类型</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>构造函数执行前</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>构造函数执行后</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>替换构造函数执行过程</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

示例：

```js
common.hookConstructor('com.test.test', ['java.lang.String', 'int'], function (param) {
    //...
}, function (param) {
    //...
});
```

hook类方法

<table>
<thead>
<tr>
<td colspan="4" align="center">hookAllMethods</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>类名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>构造函数执行前</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>构造函数执行后</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>替换构造函数执行过程</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

示例：

```js
common.hookAllMethods('com.test.test', 'methodname', function (param) {
    //...
}, function (param) {
    //...
}, function (param) {
    //调用原方法返回
    return common.thisMethod(param);
});
```

hook指定参数的类方法

<table>
<thead>
<tr>
<td colspan="4" align="center">hookMethod</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>类名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>参数类型</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>构造函数执行前</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>构造函数执行后</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>替换构造函数执行过程</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

示例：

```js
common.hookMethod('com.test.test', 'methodname', ['java.lang.String', 'int'], function (param) {
    //...
    //修改返回值
    param.setResult('fuck');
}, function (param) {
    //...
    //获取类方法的返回值并打印
    common.log(param.getResult());
});
```

修改静态变量值

<table>
<thead>
<tr>
<td colspan="4" align="center">setStaticObjectField</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>类名</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>变量名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>fieldValue</td>
<td>Object</td>
<td>变量值</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
common.setStaticObjectField('com.test.test', '变量名', '变量值');
```

修改动态变量值

<table>
<thead>
<tr>
<td colspan="4" align="center">setObjectField</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>类名或者当前实例</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>变量名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>fieldValue</td>
<td>Object</td>
<td>变量值</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
common.setObjectField('com.test.test', '变量名', '变量值');
//或者
//param.thisObject 在hook回调方法中获取
common.setObjectField(param.thisObject, '变量名', '变量值');
```

获取静态变量值

<table>
<thead>
<tr>
<td colspan="4" align="center">getStaticObjectField</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>类名</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>变量名</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
common.getStaticObjectField('com.test.test', '变量名');
```

获取动态变量值

<table>
<thead>
<tr>
<td colspan="4" align="center">getObjectField</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>类名或者当前实例</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>变量名</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
common.getObjectField('com.test.test', '变量名');
```

主动调用动态方法

<table>
<thead>
<tr>
<td colspan="4" align="center">callMethod</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>类名或者当前实例</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>methodMame</td>
<td>String</td>
<td>方法名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>参数值</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
common.callMethod('com.test.test', 'methodname', ['a', 1]);
```

主动调用静态方法

<table>
<thead>
<tr>
<td colspan="4" align="center">callStaticMethod</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>类名</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>methodMame</td>
<td>String</td>
<td>方法名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>参数值</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
common.callStaticMethod('com.test.test', 'methodname', ['a', 1]);
```

`replaceHookedMethod`中调用原方法

<table>
<thead>
<tr>
<td colspan="4" align="center">thisMethod</td>
</tr>
<tr>
<td>参数</td>
<td>参数类型</td>
<td>参数说明</td>
<td>是否必填</td>
</tr>
</thead>
<tbody>
<tr>
<td>param</td>
<td>Object</td>
<td>参数</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
//param在replaceHookedMethod中获取
common.thisMethod(param);
```

[查看更多](https://p-bakker.github.io/rhino/tutorials/scripting_java/)

### frida

[查看更多](https://frida.re/docs/javascript-api/)
