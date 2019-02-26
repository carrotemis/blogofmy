---
title: Vue 全家桶学习总结
date: 2019-02-26 23:32:17
tags:
---
# Vue

## Vue.js 特性：

1.轻量级
2.双向数据绑定
3.指令
4.组件化

## 什么是 MVVM

```
MVC => MVP => MVVM
// 视图层和数据层的双向绑定
View <=> ViewModel <=> Model
```
1. MVVM是一种设计思想， 是 Model-View-ViewModel 的缩写。Model 层代表数据模型，也可以在 Model 中定义数据修改和操作的业务逻辑；View 代表 UI 组件，它负责将数据模型转化成 UI 展现出来，ViewModel 是一个同步 View 和 Model 的对象。

2. 在 MVVM 架构下，View 和 Model 之间并没有直接的联系，而是通过 ViewModel 进行交互，Model 和 ViewModel 之间的交互是双向的， 因此 View 数据的变化会同步到Model 中，而 Model 数据的变化也会立即反应到 View 上。

3. ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而 View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作 DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

## Vue.js 的优点

1. 低耦合。视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的"View"上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。
2. 可重用性。你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。
3. 独立开发。开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计。
4. 可测试。界面素来是比较难于测试的，而现在测试可以针对ViewModel来写
5. 易用灵活高效

## Vue 组件是什么

组件 (Component) 是 Vue.js 最强大的功能之一。组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素，Vue.js 的编译器为它添加特殊功能。在有些情况下，组件也可以表现为用 is 特性进行了扩展的原生 HTML 元素。所有的 Vue 组件同时也都是 Vue 的实例，所以可接受相同的选项对象 (除了一些根级特有的选项) 并提供相同的生命周期钩子。

# Vue-cli
Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统，致力于将 Vue 生态中的工具基础标准化。

## Vue 脚手架 3.x 以上版本使用

全局安装
```
yarn global add @vue/cli
```
快速原型开发
```
npm install -g @vue/cli-service-global
```
创建项目
```
vue create hello-world
// 如果是在 Windows 上通过 minTTY 使用 Git Bash，交互提示符并不工作，需要执行下面命令
winpty vue.cmd create hello-world
```
```
cd hello-world
```
Project setup
```
yarn install
```
（以下命令 run 可以省略）
Compiles and hot-reloads for development
```
yarn run serve
```
Compiles and minifies for production
```
yarn run build
```
Run your tests
```
yarn run test
```
Lints and fixes files
```
yarn run lint
```
## Vuecli 3.x 版本(上图)与 2.x 初始化目录对比

![](https://upload-images.jianshu.io/upload_images/7094266-35ec0c0fd8c70b11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/7094266-2e5b972e8f4586e0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# Vue Router

Vue Router 是 Vue.js 官方的路由管理器。
安装
```
npm install vue-router
```
引用
```
import VueRouter from 'vue-router'

Vue.use(VueRouter)
```
配置路由文件，并在vue实例中注入 
```
const router = new VueRouter({
  routes:[{
    path:'/user/:userId', // 指定要跳转的路径
    name: 'user',
    component: User// 指定要跳转的组件
    }]
})
const User = ({
  template: '<div>User</div>'
})
```

## 确定视图加载的位置

```
<router-view></router-view>
```

## 实现路由跳转

```
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
```

# Vuex

Vuex 是一个为 Vue.js 开发的状态管理模式：采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

## 在 store (存储)内有下列核心概念

**State()：核心原始数据** 展示
**Getter：计算属性，根据所依赖的数据的变化计算自身变化** 存储
**Mutation(转变)：提交 mutation 才能改变存储状态**
**Action：**Action 类似于 mutation，不同在于：
Action 提交的是 mutation，而不是直接变更状态。
Action 可以包含任意异步操作。
**Module：可以将将 store 分割**
一般放在 state 文件夹下

![](https://upload-images.jianshu.io/upload_images/7094266-c1e2d56805eff7e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## vuex状态管理的流程

view => actions => mutations => state => view

## 核心概念详解

### state：记录所有公共数据状态的对象
```
// 组件如何获取
this.$store.state.XXX
// 此处的 XXX 是 state 内定义的数据状态的键名
```
### mutations：包含所有 操作数据状态的方法 的对象
```
// 组件如何调用
this.$store.commit(XXX)
// 此处的 XXX是 mutations 中定义的方法名
```
### actions：用于操作 mutations 内方法 的对象
actions 提交的是 mutation，而不是直接变更状态 actions可以包含异步操作，但是 mutation 只能包含同步操作
```
// 如何调用
this.$store.dispatch(XXX)
// 此处的XXX是你在actions中定义的方法名
```
### getters：定义状态内容的方法 的对象
```
this.$store.getters.XXX
// 此处的XXX是你在getters里定义的方法名
```
### Module
当应用较大时，store将变得臃肿，Vuex 允许我们将 store 分割成模块（module）。
每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割
```
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```
# Axios 
axios 是一个基于Promise 用于浏览器和 nodejs 的 HTTP 客户端，它本身具有以下特征：
- 从浏览器中创建 XMLHttpRequest
- 从 node.js 发出 http 请求
- 支持 Promise API拦截
- 请求和响应转换
- 请求和响应数据取消
- 请求自动转换JSON数据
- 客户端支持防止 CSRF/XSRF
1. 安装
```
npm install axios
```
2. 引入加载
```
import axios from 'axios'
```
3. 将axios全局挂载到 Vue 原型上
```
Vue.prototype.$http = axios
```
## axios 的 url 有两种传递参数的形式
```
// 第一种 对象形式
this.$http.get('/user', {
    params: {
      ID: 12345
    }
  })
// 如果只有一个参数，可以省略 params
this.$http.get('/user', {
      ID: 12345
  }) 
--------------------------------- 
// 第二种 形式
this.$http.get('https://cnodejs.org/api/v1/topics?page=1&limit=15')
```
## POST 传递数据有两种格式：
1. form­-data ?page=1&limit=48
2. x-­www­-form-­urlencoded { page: 1,limit: 10 }

**在 axios 中，post 请求接收的参数必须是 form­-data 形式
如果要使用 x-­www­-form-­urlencoded 形式，需要用 qs 插件—qs.stringify 转换**
```
this.$http.post('/user', qs.stringify({
   ID: 12345
  })
);
```
---
待完善。。