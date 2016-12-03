---
title: Vonic简明教程（一）：起步
date: 2016-12-03 14:52:10
tags: 
  - Vue
  - Vonic
---

<blockquote class="blockquote-center">
  [Vonic](https://github.com/wangdahoo/vonic) 是一个基于Vue.js和ionic样式的UI框架，用于方便快速地搭建单页应用。
</blockquote>

<p align="center">
  [查看Vonic组件列表](https://wangdahoo.github.io/vonic/docs/)
</p>

### 如何利用Vonic快速搭建一个单页应用脚手架
写几个页面组件，配下路由。对，就这样。

#### 准备
Vonic依赖于vue.js、vue-router.js、axios.js这三个基础库及ionic样式文件。
在本地创建一个html文件，如：index.html，然后你可以这样引入它们和Vonic框架的核心js文件vonic.js：
```html
<!-- ionic 样式文件 -->
<link rel="stylesheet" href="https://unpkg.com/vonic@0.5.1/dist/ionic/css/ionic.css">

<!-- axios/vue/vue-router -->
<script src="https://unpkg.com/axios@0.15.3/dist/axios.min.js"></script>
<script src="https://unpkg.com/vue@1.0.28/dist/vue.min.js"></script>
<script src="https://unpkg.com/vue-router@0.7.13/dist/vue-router.min.js"></script>

<!-- vonic核心文件 -->
<script src="https://unpkg.com/vonic@0.5.1/dist/vonic.min.js"></script>
```

#### 添加应用挂载点
在body中添加von-app标签，作为vonic单页应用的挂载点
```html
<body>
  <von-app></von-app>
</body>
```

#### 编写页面组件
这里，我们采用编写vue options对象的方式来编写页面组件，代码如下：

```js
const Index = { template: `
  <div class="page has-navbar" v-nav="{title: '首页', showBackButton: false}">
    <div class="page-content">
      <p>Hell,Vonic!</p>
      <a v-link="{path: '/about'}">
      	about
      </a>
    </div>
  </div>
`}
```
> Vonic单页应用的页面组件均用一个带有.page类的div进行包括，并通过v-nav指定来控制全局的navbar行为，v-nav的值可以直接用字面量字符串表示。而页面组件内容，则都编写在.page-content这个容器中

v-nav指令属性列表

| 属性名 | 属性描述 | 类型 | 必选 | 默认 |
|-----|-----|-----|-----|-----|
| title  | 导航栏标题 | String | No | 空字符串 |
| showBackButton  | 是否显示（左边的）返回按钮 | Boolean | No | false |
| onBackButtonClick  | 返回按钮点击回调函数 默认调用history.go(-1) | Function | No | undefind |
| showMenuButton  | 是否显示（右边的）菜单按钮 | Boolean | No | false |
| onMenuButtonClick  | 菜单按钮点击回调函数 | Function | No | undefind |
| backButtonText  | 返回按钮文字（图标） | String | No | 见备注 |
| menuButtonText  | 菜单按钮文字（图标） | String | No | 见备注 |
> backButtonText和menuButtonText两个选项默认值按平台不同给定不同的html字符串，以backButtonText为例，iOS下默认值为：&lt;a class="button button-icon icon ion-ios-arrow-back"&gt;&lt;/a&gt;。你可以通过这个属性来定制自己的返回按钮。

按同样的方法，我们编写第二个页面组件，代码如下：
```js
const About = { template: `
  <div class="page has-navbar" v-nav="{title: '关于我们', showBackButton: true}">
    <div class="page-content">
      <p>Nothing here.</p>
    </div>
  </div>
`}
```

#### 配置路由信息
接下来，我们把刚才写的两个页面组件按不同的路由进行配置，配置方式同VueRouter
```js
const routers = {
  '/': { component: Index },
  '/about': { component: About }
}
```

#### 启动应用
最后，以安装Vue插件的方式，启动Vonic应用
```js
Vue.use(Vonic.app, {
  routers: routers,
  defaultRouterUrl: '/'
})
```

完整代码和运行效果请查看 [https://jsfiddle.net/wangdahoo/rn7ypwvn/](https://jsfiddle.net/wangdahoo/rn7ypwvn/)

#### 整合webpack
如果你喜欢用es6 + babel + webpack + vue-loader的方式来开发vue组件（*.vue），那你可以这样：
```bash
$ vue init wangdahoo/vonic-template my-project
$ cd my-project
$ npm install
$ npm run dev
```
嗯，就这么简单。
