<div align="center">
<h1>JsHook</h1>

[![Xposed](https://img.shields.io/badge/-Xposed-3DDC84?style=flat&logo=Android&logoColor=white)](#)
[![GitHub release](https://img.shields.io/github/release/Xposed-Modules-Repo/me.jsonet.jshook.svg)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases/latest)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Channel&color=0088cc)](https://t.me/jshookapp)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Chat&color=0088cc)](https://t.me/jshookgroup)
[![LSPosed Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/me.jsonet.jshook/total?label=LSPosed%20Downloads&logo=Android&labelColor=F48FB1&logoColor=ffffff&color=0088cc)](https://modules.lsposed.org/module/me.jsonet.jshook)

hook artifact in android support java layer and native layer

[中文的README](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/blob/main/README.md)
</div>

## About the module

Xposed is a module framework that can change the behavior of your system and applications without touching any APK. This
means that modules can work on different versions and even ROMs without any changes.

JsHook is the use of Xposed framework for the initialization of any app to inject Rhino/Frida, Xposed module development
requires a certain Java syntax base, the technical threshold is high, while JsHook injected Rhino/Frida is great, only
need to know a short Js syntax base, you can use the phone to quickly make their own hook plug-ins, and hook support
java layer and native layer.

## Module compatibility

1. Xposed api 82
2. Android 7 - 12

## How to use the module

### How to enable scripts

Before enabling the script, please make sure the selected application has enabled the hook service option, if it is
LSPosed non-global scope in addition to check the system when activating the module also need to check the corresponding
script effective application, each time you change the script content need to restart the app being hooked.

### How to choose an hook framework

If you are familiar with Xposed hook method, Rhino is recommended, using js call Xposed framework methods, and high
compatibility; and Frida belongs to another hook framework, need to have some understanding of Frida, it is difficult to
get started, and does not support some models and apps.

## Cautions

Version 1.0.2 before the default is frida hook, so the previous use of frida need to use the framework management will
be set to frida global default , import framework currently only supports frida-gadget.

## Script Description

### Universal

Log Printing：

```js
common.log('...');
```

Message Tips：

```js
common.toast('...');
```

Get Context：

```js
common.getcontext();
```

### rhino

hook constructor

<table>
<thead>
<tr>
<td colspan="4" align="center">hookAllConstructors</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace the constructor execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookAllConstructors('com.test.test', function (param) {
    //Before the execution of the constructor
    //Print the first argument received by the constructor
    common.log(param.args[0]);
    //Modify the value of this parameter
    param.args[0] = 'fuck';
}, function (param) {
    //After the execution of the constructor
    //...
});
```

hook constructor with specified parameters

<table>
<thead>
<tr>
<td colspan="4" align="center">hookConstructor</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>Parameter Type</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace the constructor execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookConstructor('com.test.test', ['java.lang.String', 'int'], function (param) {
    //...
}, function (param) {
    //...
});
```

hook class method

<table>
<thead>
<tr>
<td colspan="4" align="center">hookAllMethods</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace the constructor execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookAllMethods('com.test.test', 'methodname', function (param) {
    //...
}, function (param) {
    //...
}, function (param) {
    //The call to the original method returns
    return common.thisMethod(param);
});
```

hook the class method with the specified parameters

<table>
<thead>
<tr>
<td colspan="4" align="center">hookMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>Parameter Type</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace the constructor execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookMethod('com.test.test', 'methodname', ['java.lang.String', 'int'], function (param) {
    //...
    //Modify return value
    param.setResult('fuck');
}, function (param) {
    //...
    //Get the return value of the class method and print it
    common.log(param.getResult());
});
```

Modifying static variable values

<table>
<thead>
<tr>
<td colspan="4" align="center">setStaticObjectField</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>Variable Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>fieldValue</td>
<td>Object</td>
<td>Variable Value</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.setStaticObjectField('com.test.test', 'Variable Name', 'Variable Value');
```

Modifying dynamic variable values

<table>
<thead>
<tr>
<td colspan="4" align="center">setObjectField</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class name or current instance</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>Variable Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>fieldValue</td>
<td>Object</td>
<td>Variable Value</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.setObjectField('com.test.test', 'Variable Name', 'Variable Value');
//or
//param.thisObject Get in the hook callback method
common.setObjectField(param.thisObject, 'Variable Name', 'Variable Value');
```

Get static variable values

<table>
<thead>
<tr>
<td colspan="4" align="center">getStaticObjectField</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>Variable Name</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.getStaticObjectField('com.test.test', 'Variable Name');
```

Get dynamic variable values

<table>
<thead>
<tr>
<td colspan="4" align="center">getObjectField</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class name or current instance</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>Variable Name</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.getObjectField('com.test.test', 'Variable Name');
```

Active invocation of dynamic methods

<table>
<thead>
<tr>
<td colspan="4" align="center">callMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class name or current instance</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>methodMame</td>
<td>String</td>
<td>Method name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>Parameter Value</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.callMethod('com.test.test', 'methodname', ['a', 1]);
```

Active invocation of static methods

<table>
<thead>
<tr>
<td colspan="4" align="center">callStaticMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>methodMame</td>
<td>String</td>
<td>Method name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>Parameter Value</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.callStaticMethod('com.test.test', 'methodname', ['a', 1]);
```

Calling the original method in `replaceHookedMethod`

<table>
<thead>
<tr>
<td colspan="4" align="center">thisMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>param</td>
<td>Object</td>
<td>Parameters</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
//param is retrieved in the replaceHookedMethod
common.thisMethod(param);
```

[View more](https://p-bakker.github.io/rhino/tutorials/scripting_java/)

### frida

[View more](https://frida.re/docs/javascript-api/)
