<div align="center">
<h1>JsHook</h1>

[![Xposed](https://img.shields.io/badge/-Xposed-3DDC84?style=flat&logo=Android&logoColor=white)](#)
[![GitHub release](https://img.shields.io/github/release/Xposed-Modules-Repo/me.jsonet.jshook.svg)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases/latest)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Channel&color=0088cc)](https://t.me/jshookapp)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Chat&color=0088cc)](https://t.me/jshookgroup)

android中hook神器 支持java层和native层

[README of English](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/blob/main/README.en.md)
</div>

## 关于

xposed是一个模块框架，可以在不接触任何apk的情况下更改系统和应用程序的行为。这意味着模块可以在不同版本甚至rom上工作而无需任何更改。

jshook是对app注入rhino/frida，xposed模块开发需要一定的java语法基础，技术门槛高，而jshook注入的rhino/frida只需要会简短的js，即可用手机快速实现hook，并且hook支持java层和native层。

## 兼容

1. Xposed api 82
2. Android 5 - 13

## 如何使用

### 如何启用脚本

启用脚本前请确认选择的应用已开启hook服务选项，如果是lsposed非全局作用域在激活时除了勾选系统还需勾选对应脚本生效的应用，每次更改脚本内容都需要重启一下被hook的app。

### 如何选择注入框架

如果你对xposed的hook方法比较熟，推荐rhino，使用js调用xposed框架的api，且兼容性高；而frida属于另一个hook框架，需要对frida有一定的了解，上手较难，且不支持部分机型和app。

## 脚本说明

### 通用

日志打印：

```js
common.log('...');
console.log('...');
```

消息提示：

```js
common.toast('...');
```

弹窗提示：

```js
common.dialog('...');
```

获取Context：

```js
common.getcontext();
```

mod菜单：

<table>
<thead>
<tr>
<td colspan="4" align="center">modmenu</td>
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
<td>title</td>
<td>String</td>
<td>标题</td>
<td align="center">N</td>
</tr>
<tr>
<td>item</td>
<td>Array</td>
<td>菜单项</td>
<td align="center">Y</td>
</tr>
<tr>
<td>title</td>
<td>String</td>
<td>标题</td>
<td align="center">N</td>
</tr>
<tr>
<td>change</td>
<td>Function</td>
<td>回调</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

示例：

```js
common.modmenu('test mod', [
    {
        'id': '1',
        'type': 'category',
        'title': 'category title'
    },
    {
        'id': '2',
        'type': 'switch',
        'title': 'switch1 title',
        'enable': true
    },
    {
        'id': '3',
        'type': 'switch',
        'title': 'switch2 title'
    },
    {
        'id': '4',
        'type': 'webview',
        'data': '<font color="red"><b>text</b></font>',
        //or
        //'url': 'http://xxxxx.com'
    },
    {
        'id': '5',
        'type': 'button',
        'title': 'button title'
    },
    {
        'id': '6',
        'type': 'input',
        'title': 'input title',
        'val': 'default value'
    },
    {
        'type': 'collapse',
        'title': 'collapse title',
        'item': [
            {
                'id': '7',
                'type': 'switch',
                'title': 'switch title'
            }
        ],
        'enable': true
    },
    {
        'id': '8',
        'type': 'slider',
        'title': 'slider title',
        'val': 88,
        'min': 1,
        'max': 100
    },
    {
        'id': '9',
        'type': 'checkbox',
        'title': 'checkbox title',
        'enable': true
    },
    {
        'type': 'checkboxs',
        'item': [
            {
                'id': '10',
                'type': 'checkbox',
                'title': '1 title'
            },
            {
                'id': '11',
                'type': 'checkbox',
                'title': '2 title'
            },
            {
                'id': '12',
                'type': 'checkbox',
                'title': '33333333 title'
            }
        ]
    },
    {
        'id': '13',
        'type': 'radio',
        'title': 'radio title',
        'item': ['test', 'test2', 'test3']
    }
], function (data) {
    common.toast(JSON.stringify(data));
});
```

带tab选项卡的示例：

```js
common.modmenu('test mod', [
    {
        'type': 'tab',
        'title': 'tab1 title',
        'item': [
            {
                'id': '1',
                'type': 'switch',
                'title': 'switch1 title'
            }
        ],
        'enable': true
    },
    {
        'type': 'tab',
        'title': 'tab2 title',
        'item': [
            {
                'id': '2',
                'type': 'switch',
                'title': 'switch2 title'
            }
        ]
    }
], function (data) {
    common.toast(JSON.stringify(data));
});
```

注意：使用mod菜单需要让jshook保持运行状态且授权悬浮窗权限，关闭jshook会导致菜单关闭，不影响hook服务

### rhino

获取LoadPackageParam

<table>
<thead>
<tr>
<td colspan="4" align="center">getlpparam</td>
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
<td colspan="4" align="center">无</td>
</tr>
</tbody>
</table>

示例：

```js
common.getlpparam();
```

获取类实例

<table>
<thead>
<tr>
<td colspan="4" align="center">findClass</td>
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
<td>classLoader</td>
<td>ClassLoader</td>
<td>类加载器</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
common.findClass('com.test.test', classLoader);
```

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
<td>Object</td>
<td>类实例或类名</td>
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
<td>Object</td>
<td>类实例或类名</td>
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
<td>Object</td>
<td>类实例或类名</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>函数执行前</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>函数执行后</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>替换函数执行过程</td>
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

hook指定的类方法

<table>
<thead>
<tr>
<td colspan="4" align="center">hookByMethod</td>
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
<td>method</td>
<td>Method</td>
<td>方法对象</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>函数执行前</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>函数执行后</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>替换函数执行过程</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

示例：

```js
common.hookByMethod(method, function (param) {
    //...
    //修改返回值
    param.setResult('fuck');
}, function (param) {
    //...
    //获取类方法的返回值并打印
    common.log(param.getResult());
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
<td>函数执行前</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>函数执行后</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>替换函数执行过程</td>
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
<td>Object</td>
<td>类实例或类名</td>
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
<td>Object</td>
<td>类实例或类名</td>
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
<td align="center">N</td>
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
<td>Object</td>
<td>类实例或类名</td>
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
<td align="center">N</td>
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

#### fridamod

curl

<table>
<thead>
<tr>
<td colspan="4" align="center">curl</td>
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
<td>url</td>
<td>String</td>
<td>地址</td>
<td align="center">Y</td>
</tr>
<tr>
<td>method</td>
<td>String</td>
<td>请求类型</td>
<td align="center">N</td>
</tr>
<tr>
<td>header</td>
<td>Array</td>
<td>头部信息</td>
<td align="center">N</td>
</tr>
<tr>
<td>data</td>
<td>Object</td>
<td>提交数据</td>
<td align="center">N</td>
</tr>
<tr>
<td>callback</td>
<td>Function</td>
<td>回调</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

示例：

```js
common.curl('https://xxxxx.com', 'post', ['token: sssss'], {data: '111'}, function (data) {
    common.log(data);
});
```

shell

<table>
<thead>
<tr>
<td colspan="4" align="center">shell</td>
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
<td>content</td>
<td>String</td>
<td>内容</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

示例：

```js
common.shell('curl https://xxxxx.com', function (data) {
    common.log(data);
});
```
