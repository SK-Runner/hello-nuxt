#  Nuxt

## 一、概述

### 1、Nuxt.js 简单定义

​		Nuxt.js 一个基于 Vue.js 的通用应用框架，通过对客户端/服务端基础架构的抽象组织，Nuxt.js 主要关注的是应用的 **UI渲染**。

​		Vue.js原来是开发SPA（单页应用）的，但是随着技术的普及，很多人想用Vue开发多页应用，并在服务端完成渲染。这时候就出现了Nuxt.js这个框架，她简化了SSR（服务端渲染）的开发难度。还可以直接用命令把我们制作的vue项目生成为静态html。

### 2、服务端渲染的优点

​		SPA（单页应用）**不利于搜索引擎的SEO**操作。比如做一个新闻网站，需要通过百度、谷歌、bing这些搜索引擎搜索到我们开发的项目，但是这些引擎对SPA的抓取并不好，特别是百度根本没法抓取到SPA的内容页面，所以我们必须**把应用在服务端渲染成适合搜索引擎抓取的页面**，再下载到客户端。那Nuxt.js适合做新闻、博客、电影、咨询这样的需要搜索引擎提供流量的项目。

### 3、SSR（服务端渲染）

​		服务器渲染，就是在服务器端将对Vue页面进行渲染生成html文件，将html页面传递给浏览器。

#### 3.1 服务端渲染的优点

1. SPA的HTML只有一个无实际内容的HTML和一个app.js，SSR生成的HTML是有内容的，这让搜索引擎能够索引到页面内容。
2. 更快内容到达时间 传统的SPA应用是将bundle.js从服务器获取，然后在客户端解析并挂载到dom。而SSR直接将HTML字符串传递给浏览器。大大加快了首屏加载时间。


### 3.2 Nuxt.js 的特点（或优势）：

- 基于 Vue.js
- 自动代码分层
- 服务端渲染
- 强大的路由功能，支持异步数据
- 静态文件服务
- ES6/ES7 语法支持
- 打包和压缩 JS 和 CSS
- HTML头部标签管理
- 本地开发支持热加载
- 集成ESLint
- 支持各种样式预处理器： SASS、LESS、 Stylus等等

## 二、项目安装

### 1、安装

```
npx create-nuxt-app <项目名>
```

### 2、目录结构

- |-- .nuxt                 // Nuxt自动生成，临时的用于编辑的文件，build 
- |-- assets              // 用于组织未编译的静态资源入LESS、SASS 或 JavaScript 
- |-- components     // 用于自己编写的Vue组件，比如滚动组件，日历组件，分页组件 
- |-- layouts             // 布局目录，用于组织应用的布局组件，不可更改。 
- |-- middleware      // 用于存放中间件 
- |-- pages              // 用于存放写的页面，我们主要的工作区域 
- |-- plugins            // 用于存放JavaScript插件的地方 
- |-- static               // 用于存放静态资源文件，比如图片 
- |-- store               // 用于组织应用的Vuex 状态管理。 
- |-- .editorconfig   // 开发工具格式配置 
- |-- .eslintrc.js      // ESLint的配置文件，用于检查代码格式 
- |-- .gitignore       // 配置git不上传的文件 
- |-- nuxt.config.json         // 用于组织Nuxt.js应用的个性化配置，已覆盖默认配置 
- |-- package-lock.json     // npm自动生成，用于帮助package的统一性设置的，yarn也有相同的操作
- |-- package.json           // npm包管理配置文件

#### 3、常用配置项

##### 3.1 配置 IP 和端口

在 /package.json中添加：

```json
  "config": {
    "nuxt":{
      "host":"127.0.0.1",
      "port":"8080"
    }
  },
```

##### 3.2 配置全局CSS

在 nuxt.config.js 中：

```javascript
  //添加了css初始化文件，normailze.css
  css: [
    'element-ui/lib/theme-chalk/index.css',
    "~assets/css/normailze.css"
  ],
```

##### 3.3 配置webpack的loader

​		在nuxt.config.js里是可以对webpack的基本配置进行覆盖的，比如现在我们要配置一个url-loader来进行小图片的64位打包。就可以在nuxt.config.js的build选项里进行配置。

```javascript
loaders:[
    {
        test:/\.(png|jpe?g|gif|svg)$/,
        loader:"url-loader",
        query:{
            limit:10000,
            name:'img/[name].[hash].[ext]'
        }
    }
],
```

## 三、  Nuxt.js 路由

### 1、路由配置和参数传递

#### 1.1  nuxt-link 标签

​		Nuxt.js并不推荐<a>标签的作法，它为我们准备了<nuxt-link>标签（vue中叫组件）。我们先把<a>标签替换成<nuxt-link>，在实际开发中尽量使用<nuxt-link>标签的方法跳转路由。

```javascript
<template>
  <div>
    <ul>
      <li><nuxt-link :to="{name:'index'}">HOME</nuxt-link></li>
      <li><nuxt-link :to="{name:'about'}">ABOUT</nuxt-link></li>
      <li><nuxt-link :to="{name:'news'}">NEWS</nuxt-link></li>
    </ul>
  </div>
</template>
```

#### 1.2 params传递参数

传递参数：

```vue
<li><nuxt-link :to="{name:'news',params:{newsId:10010}}">NEWS</nuxt-link></li>
```

接收参数：

```vue
<p>新闻ID：{{$route.params.newsId}}</p>
```

### 2、Nuxt 动态路由和参数校验

#### 2.1 动态路由

​		动态路由就是带参数的路由，以下划线为前缀的Vue文件就是动态路由，然后在文件里边有 $route.params.id来接收参数。

在 url 中添加传递的动态值

```vue
<a href="/news/新闻内容1">进入News-1</a>
<a href="/news/新闻内容2">进入News-2</a>
```

获取url中的动态值

```vue
<p>{{$route.params.id}}</p>
```

#### 2.2 动态参数校验

​		进入一个页面，对参数传递的正确性校验是必须的，Nuxt.js也贴心的为我们准备了校验方法validate( )。

_id.vue中：

```vue
export default {
    validate({params}){
        // 判断动态路由内容是否以数字结尾
        return /\d$/.test(params.id)
    }
}
```

如果动态路由中不符合验证条件（href="/news/新闻内容"），则不会找到_id.vue这个页面（进入404页面）

### 3、Nuxt 的路由动画效果





