---
title: Vonic简明教程（二）：组件与服务
date: 2016-12-04 11:33:14
tags: 
  - Vue
  - Vonic
categories: 前端  
---

<blockquote class="blockquote-center">
  [Vonic](https://wangdahoo.github.io/vonic/docs/) 是一个基于Vue.js和ionic样式的UI框架，用于方便快速地搭建单页应用。
</blockquote>

<p align="center">
  [GitHub 地址](https://github.com/wangdahoo/vonic)
</p>

### 概述
这里主要介绍如何使用Vonic提供的组件与服务，并给出一个登录页范例

### 组件
Vonic核心js文件加载完成后，会在window上暴露一个全局变量Vonic，你可以通过该对象来引入Vonic组件，像这样：
```js
new Vue({
  components: {
    'von-input': Vonic.VonInput,
    'md-button': Vonic.MdButton
  },

  // ...
})
```

如果你采用的是es6 + babel + webpack方式进行开发，先在webpack配置文件中添加：
```js
resolve: {
  alias: {
    'vonic': 'vonic/src/vonic.js'
  }
}
```
然后，像这样在*.vue文件的script标签中引入Vonic组件：
```js
import {VonInput, MdButton} from 'vonic'

export default {
  components: {
    VonInput, 
    MdButton
  },

  // ...
}
```

> webpack.config.js 文件配置请参考：
[https://github.com/wangdahoo/vonic-template/blob/master/template/webpack.config.js](https://github.com/wangdahoo/vonic-template/blob/master/template/webpack.config.js)

### 服务
Vonic还提供了一些服务类的组件(Service)。你只需要通过服务代理对象提供的Api方法来调用它们，而并不需要关心和维护它们的生命周期及状态。如：
```js
  $loading.toast('这是一个提示')
```

下面列出常用的Vonic服务：

| 服务 | 服务描述 |
|-----|-----|
| $router  | 路由服务，VueRouter对象代理，额外提供了控制页面transition方向的forward方法和back方法 |
| $loading  | 加载（preloader)提示服务 |
| $alert  | 警告对话框服务 |
| $confirm  | 警告对话框服务 |
| $alert_ios  | 警告对话框服务，iOS风格样式 |
| $confirm_ios  | 警告对话框服务，iOS风格样式 |
| $storage  | localStorage存储服务 |
| $popup  | 弹层服务 |
| $sidebar  | 侧边栏服务 |
| $actionSheet  | ActionSheet服务 |
| $vonicModal  | 模态窗服务 |

### 组件文档
> 未完整，持续更新中
[https://github.com/wangdahoo/vonic/blob/master/COMPONENTS.md](https://github.com/wangdahoo/vonic/blob/master/COMPONENTS.md)

### 范例：登录页面
> 该范例中，使用到的组件有：VonInput、MdButton；使用到的服务有：$router、$loading、$confirm

完整代码及运行效果：[https://jsfiddle.net/wangdahoo/n00L0c2a/](https://jsfiddle.net/wangdahoo/n00L0c2a/)