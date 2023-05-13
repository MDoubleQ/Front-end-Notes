# 一、项目搭建

![image-20230315083418269](E:\coder\09_OneNote\image\image-20230315083434588.png)![image-20230315083451137](E:\coder\09_OneNote\image\image-20230315083451137.png)

> 上课最主要讲这个项目。
> 不用焦虑，只要能把上课的东西每个细节搞明白，并且全部运用起来，这样对Vue的使用就没有问题了
> 到公司做项目，也是不会把Git、modules放到文件里面，第一步，先`npm install`

## 1、创建Vue项目

### 方式1：Vue CLI

基于webpack工具，命令：`vue create`

### 方式2：create-vue

基于vite工具，命令：`npm init vue@latest`

## 2、项目配置

- 配置项目的icon
- 配置项目的标题
- 配置jsconfig.json

采用方式二`npm init vue@latest`，并且手动配置，目前阶段先都选择No，为了搞清楚每个文件的作用~

`Vue`

```git
PS E:\coder\00_Practice> npm init vue@latest
Need to install the following packages:
  create-vue@3.6.1
Ok to proceed? (y) y

Vue.js - The Progressive JavaScript Framework

√ Project name: ... vue-projecthy-trip
√ Add TypeScript? ... No / Yes
√ Add JSX Support? ... No / Yes
√ Add Vue Router for Single Page Application development? ... No / Yes
? Add Pinia for state management? » No / Yes    
√ Add Vitest for Unit Testing? ... No / Yes
√ Add an End-to-End Testing Solution? » No√ Add ESLint for code quality? ... No / Yes

Scaffolding project in E:\coder\00_Practice\hy-trip...

Done. Now run:

cd hy-trip
npm install
npm run dev
```

目前公司做项目还是按照下面这种结构，这种结构更常见：

`Vue`

```vue
<template>
  <div class="app">
    <h1>Hello Word</h1>
  </div>
</template>

<script setup>
</script>

<style scoped>
</style>
```

## 3、项目准备

### 3.1、配置icon

### 3.2、更改title

### 3.3、配置`jsconfig.json`

有这个东西的话，代码提示会更加友好，vite默认是没有的，因此从之前的项目中直接复制过来

`config.js`

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "esnext",
    "baseUrl": "./",
    "moduleResolution": "node",
    "jsx": "preserve",
    "paths": {
      "@/*": ["src/*"]
    },
    "lib": ["esnext", "dom", "dom.iterable", "scripthost"]
  }
}
```

- `"target": "es5"`：编译后的JavaScript代码的目标版本。在这个例子中，目标是ES5版本的JavaScript，这是一种广泛支持的JavaScript版本，可以在所有现代浏览器中运行。
- `"module": "esnext"`：使用的模块系统。这里是ES模块，这是一种现代的模块系统，它允许您在JavaScript代码中使用`import`和`export`语句。
- `"baseUrl": "./"`：用于解析相对模块的基本路径。在这个例子中，基本路径是项目的根目录。
- `"moduleResolution": "node"`：解析模块的方式。在这个例子中，使用Node.js的模块解析算法来解析模块。
- `"jsx": "preserve"`：处理JSX代码的方式。在这个例子中，将JSX代码保留为原始的JSX代码，不进行转换。
- `"paths": {"@/*": ["src/*"]}`：路径别名的配置，它允许您使用`@`作为`src/`目录的快捷方式。
- `"lib": ["esnext", "dom", "dom.iterable", "scripthost"]`：编译时所需的库文件。在这个例子中，需要ES6、DOM、可迭代的DOM和Script Host库文件。

### 3.4、对src目录结构划分

==assets==：`css`、`font`、`img`、`data`

==components==：`common`、`content`

==router==：`index.js`

==mock==

==service==

==stores==：`modules`

==utils==

==views==

> 到公司也是要先看目录结构的，之后才开始看相关的业务逻辑，创建完目录结构，项目的结构就非常清晰了~
> 
>**==项目目录结构==**
> 1、assets：项目的资源（img、css、font、audio、video）
> 
>- common：多个项目都会公用的文件
> - content：当前项目，多个页面公用的组件
> 
>3、hooks：多个组件公用代码逻辑，抽取到hooks里面
> 4、mock：模拟一些数据
> 5、router：路由相关的配置
> 6、service：网络请求
> 7、store：状态管理，Vuex配置
> 8、utils：工具，抽取一些工具函数
> 9、views：放页面，大的页面，大的视图

## 4、CSS样式重置

==normalize.css==

`npm install normalize.css`

- 是一个库，别人总结好的，对样式进行重置
- 一般情况先下，公司的项目都会包含
- 保证多个浏览器的样式统一

==reset.css==

样式重置文件

==common.css==

公共样式文件

==index.css==

目的：引入其他CSS文件，

比如引入`common.css`文件，防止`common.css`文件过于庞大和臃肿

[<a href="https://github.com/necolas/normalize.css/blob/master/normalize.css%5d(https:/github.com/necolas/normalize.css/blob/master/normalize.css)">https://github.com/necolas/normalize.css/blob/master/normalize.css](https://github.com/necolas/normalize.css/blob/master/normalize.css)</a>

### 4.1、CSS样式重置文件

`src/assets/css/main.js`

```javascript
import { createApp } from 'vue'
import App from './App.vue'

import 'normalize.css'
import './assets/css/index.css'

createApp(App).mount('#app')
```

`src/assets/css/reset.css`

```css
body, h1, h2, h3, h4,ul, li {
  margin: 0;
  padding: 0;
}
ul, li {
  list-style: none;
}
a {
  text-decoration: none;
  color: #333;
}
img {
  vertical-align: top;
}
```

还有其他的样式需要充值，先重置这么多

`src/assets/css/index.css`

```css
@import "./reset.css";
@import "./common.css"
```

> 在`vite`中，不要用URL引入，会出现问题，直接使用@import就好，
> 为什么要用`@import`，因为是CSS语法

`src/assets/css/common.css`

```css
body {
  font-size: 14px;
}
```

### 4.1、安装less

`npm install less`



# 二、路由配置

> 做项目，不仅会用到Vue核心代码，还会用到router和vuex，
>
> 刚刚我们选择的是no，因此我们手动自己搭一下，熟悉一下：

## 1、安装路由

`npm install vue-router`

## 2、基本路由配置

`src/router/index.js`

```javascript
import { createRouter, createWebHashHistory} from 'vue-router'
const router = createRouter({
  history: createWebHashHistory(),
  // 映射关系：path-> component
  routes: [
    {
    }
  ]
})
export default router
```

`src/main.js`

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from "./router"
import 'normalize.css'
import './assets/css/index.css'

createApp(App).use(router).mount('#app')
```

> tab-banner这个东西，不管在哪里开发都叫这个名字
> 目前来看，有四个页面，为了方便
>
> 管理，创建页面时，每个页面有一个自己的文件夹

`src/views/home/home.vue`

`src/views/favor/favor.vue`

`src/views/order/order.vue`

`message/message.vue`

> 文件名称：`index.vue/home.vue`，两种文件名称都可以，建议`home.vue`
> 文件名称：`HomeBanner.vue/home-banner.vue`，两种风格也都可以

### 2.2、生成VSCode片段

模板代生成VSCode片段

```html
<template>
  <div class="${1:home}">
    <h1>${2:home}</h1>
  </div>
</template>

<script setup>
</script>

<style lang="less" scoped>
</style>
```

生成VScode片段网站

[<a href="https://snippet-generator.app/%5d(https:/snippet-generator.app/)">https://snippet-generator.app/](https://snippet-generator.app/)</a>

## 3、配置路由映射

`src/router/index.js`

```javascript
import { createRouter, createWebHashHistory} from 'vue-router'
const router = createRouter({
  history: createWebHashHistory(),
  // 映射关系：path-> component
  routes: [
    {
      path: "/",
      redirect: '/home'
    },
    {
      path: "/home",
      component: () => import("../views/home/home.vue")
    },
    {
      path: "/favor",
      component: () => import("../views/favor/favor.vue")
    },
    {
      path: "/order",
      component: () => import("../views/order/order.vue")
    },
    {
      path: "/message",
      component: () => import("../views/message/message.vue")
    }
  ]
})
export default router
```

> ⚠⚠⚠（提示：以下依赖项已导入，但无法解析：）
> The following dependencies are imported but could not be resolved:
> Click outside or fix the code to dismiss.
> You can also disable this overlay by setting server.hmr.overlay to false in vite.config.js.

路由映射配置好之后最好做一个测试~出现问题，最终解决方案：将@换掉

> ❗❗❗
>
> "/home"不加.

添加占位、添加功能

`src/app.vue`

```html
<template>
  <div class="app">
    <h1>Hello Word</h1>
    <router-view></router-view>
    <router-link to="/home">首页</router-link>
    <router-link to="/favor">收藏</router-link>
    <router-link to="/order">订单</router-link>
    <router-link to="/message">消息</router-link>
  </div>
</template>
```

# 三、状态管理

## 1、状态管理的选择

vuex:目前依然使用较多的状态管理库；

pinia:强烈推荐，未来趋势的状态管理库；

## 2、状态管理使用步骤

1、先安装`npm install vuex`

2、新建文件`src/stores/index.js`

3、创建`src/stores/index.js`

4、`src/main.js`文件导入`src/stores/index.js`

5、使用`use(store)`

6、新建文件夹`src/stores/modules`分模块文件

## 3、状态管理仓库创建、分模块

`src/stores/index.js`

```javascript
import { createStore } from "vuex";
import useCityStore from "./modules/city"
import useSearchStore from "./modules/search"
const store = createStore({
  state: () => {
  },
  getters:{
  },
  mutations:{
  },
  actions:{
  },
  modules:{
    city: useCityStore,
    search: useSearchStore
  }
})
export default store
```

`src/stores/modules/city.js`

```javascript
const useCityStore = {
  store: () => {
    // cities: []
  },
  getters: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
}
export default useCityStore 
```

`src/stores/modules/search.js`

```javascript
const useSearchStore = {
  store: () => {
  },
  getters: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
}
export default useSearchStore 
```

`src/main.js`

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router/index'

import store from './stores/index'

import 'normalize.css'
import './assets/css/index.css'

createApp(App).use(router).use(store).mount('#app')
```

# 四、首页功能搭建

![image-20230322200047248](E:\coder\09_OneNote\image\image-20230322200047248.png)

## 1、TabBar组件

![image-20230314082848633](E:\coder\09_OneNote\image\image-20230314082848633.png)

### 1.1、TabBar静态搭建

> 之前说过json文件中不能写注释，
>
> VSCode对下面这两个有单独处理，因为这两个是对VSCode看的：
>
>  `jsconfig.js` 
>
>  `tsconfig.js` 
>
>  上课的时候可能用的新一些，但是公司时候，用稳定的版本，因为稳定的东西，遇见的问题好解决一些，网上也有解决方案，如果太新的话，不好解决。
>
> 上上上级目录： ==../../== 

`src/components/tabBar.vue`

```html
<template>
  <div class="tab-bar">
    <div class="tab-bar-item">
      <img src="../../assets/img/tabbar/tab_home.png" alt="">
      <span class="text">首页</span>
    </div>
    <div class="tab-bar-item">
      <img src="../../assets/img/tabbar/tab_favor.png" alt="">
      <span class="text">收藏</span>
    </div>
    <div class="tab-bar-item">
      <img src="../../assets/img/tabbar/tab_order.png" alt="">
      <span class="text">订单</span>
    </div>
    <div class="tab-bar-item">
      <img src="../../assets/img/tabbar/tab_message.png" alt="">
      <span class="text">消息</span>
    </div>
  </div>
</template>  

<script>
  export default {

  }
</script>

<style scoped>
  .tab-bar {
    position: fixed;
    bottom: 0px;
    left: 0;
    right: 0;
    height: 50px;
    
    border-top: 1px solid #f3f3f3;
    
    display:flex;
  }

  .tab-bar-item {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;    

    flex-direction: column;
  }

  img {
    width: 32px;
  }
</style>
```

### 1.2、TabBar动态搭建

#### 1.2.1、TabBar的动态数据

> 在公司的话数据可能来自于服务器，
>
> 我们可以模拟一下，把`tab-bar-item`数据抽离出去做一个for循环
>
> 在公司开发项目，⭐⭐⭐先完成业务，不要给自己加任务；
>
> 就像这种开发完了静态的之后，继续开发下一个业务，先开发出来再说；
>
> 有时间再考虑代码的==简洁、优雅、可复用性、可维护性、可扩展性==等等这种进阶的内容。

#### 1.2.2、将数据抽到单独的JS文件

抽取数据

`assets/data/tabbar.js`

```javascript
const tabbarDate = [
  {
    text: "首页",
    image: "/tabbar/tab_home.png",
    imageActive: "/tabbar/tab_home_active.png",
    path: "/home"
  },
  {
    text: "收藏",
    image: "/tabbar/tab_favor.png",
    imageActive: "/tabbar/tab_favor_active.png",
    path: "/favor"
  },
  {
    text: "订单",
    image: "/tabbar/tab_order.png",
    imageActive: "/tabbar/tab_order_active.png",
    path: "/order"
  },
  {
    text: "消息",
    image: "/tabbar/tab_message.png",
    imageActive: "/tabbar/tab_message.png",
    path: "/message"
  },
]
export default tabbarDate
```

#### 1.2.3、如何做动态图片

webpack一般使用`require`做一个包裹

```html
<img v-bind:src="require(item.image)" alt="">
```

vite环境中没有require，需要这样动态加载路径：拼接一个`url`地址

- 使用URL找东西，虽然麻烦但是是固定的方式

```javascript
methods: {
  getAssetURL(image){
    // 参数一：项目路径
    // 参数二：当前路径的rul
    return new URL("../../assets/img/" + image, import.meta.url).href
  }
}
```

**这是一个特殊情况，特殊的知识点，有两种情况是不需要这样做的：**

- 数据来自于服务器
- 数据一开始就是写好的，如果是放在某一个配置文件中就需要这样做

在公司使用封装好的就行，也可以直接去`stackoverflow`找一个拿过来就行

> 在 JavaScript 中，new URL() 用于创建一个新的 URL 对象，可以用于解析和操作 URL。

也可以自己封装成一个工具

#### 1.2.4、new URL如何使用

`new URL()` 的语法如下：

```js
const url = new URL(urlString[, baseString]);
```

其中，`urlString` 参数是要解析的 URL 字符串，`baseString` 是可选参数，是用来解析相对 URL 的基本 URL 字符串。如果省略 `baseString` 参数，则默认使用当前网页的 URL。

```js
const url = new URL('https://www.example.com/path?param=value#fragment');

console.log(url.href); // "*[https://www.example.com/path?param=value#fragment](https://www.example.com/path?param=value#fragment)"
console.log(url.protocol); // "https:"
console.log(url.host); // "[www.example.com](http://www.example.com)"
console.log(url.pathname); // "/path"
console.log(url.search); // "?param=value"
console.log(url.hash); // "#fragment"
```

在这个示例中，`new URL()` 用于解析一个 URL 字符串，并创建一个包含各种 URL 组件的 URL 对象。你可以使用 URL 对象的属性来访问每个组件，例如 `protocol`、`host`、`pathname`、`search` 和 `hash`。

#### 1.2.5、动态添加图片

#### 1.2.6、核心代码

```javascript
    getAssetURL(image){
      // 参数一：项目路径
      // 参数二：当前路径的rul
      return new URL("../../assets/img/" + image , 
                    import.meta.url
                    ).href
    }
```

> new URL()创建一个新的 URL 对象。
>
> "../../assets/img/" +image是图像文件的相对路径。该image变量包含图像文件的名称。
>
> import.meta.url是当前模块的URL。它用作图像文件相对路径的基本 URL。
>
> .href返回图像文件的完全限定 URL。

#### 1.2.7、项目代码

`src/components/tabBar.vue`

```javascript
<template>
  <div class="tab-bar">
    <template v-for="(item, index) in tabbarDate">
      <div class="tab-bar-item">
        <img v-bind:src="getAssetURL(item.image)" alt="">
        <span class="text">{{ item.text }}</span>
      </div>
    </template>
  </div>
</template>

<script>
import tabbarDate from '../../assets/data/tabbar.js'
export default {
  data() {
    return {
      tabbarDate,
    }
  },
  methods: {
    getAssetURL(image){
      // 参数一：项目路径
      // 参数二：当前路径的rul
      return new URL("../../assets/img/" + image , 
                    import.meta.url
                    ).href
    }
  }
}
</script>
```

#### 1.2.8、封装动态图片方法

`utils/load_assets.js`

```javascript
export const getAssetURL = (image) => {
  // 参数一: 相对路径
  // 参数二: 当前路径的URL
  return new URL(`../assets/img/${image}`, import.meta.url).href
}
```


-----

## 2、tabBar功能完善

![image-20230314091059290](E:\coder\09_OneNote\image\image-20230314091059290.png)

> 箭头函数和function，两种格式都可以，各有好处，每个人的习惯不一样
>

### 2.1、active制作

#### 2.1.1、核心代码

```javascript
<template>
  <div class="tab-bar">
    <template v-for="(item, index) in tabbarDate">
      <div class="tab-bar-item"
           @click="itemClick(item, index)"
           :class="{ active: currentIndex === index }"
      >
        <img v-if="currentIndex !== index" :src="getAssetURL(item.image)" alt="">
        <img v-else :src="getAssetURL(item.imageActive)" alt="">
        <span class="text">{{ item.text }}</span>
      </div>
    </template>
  </div>
</template>
```

⚠️⚠️⚠️ 这段代码好好练习

```javascript
export default {
  data() {
    return {
      tabbarDate,
      currentIndex: 0,
    }
  },
  methods: {
    getAssetURL(image){
      // 参数一：项目路径
      // 参数二：当前路径的rul
      return new URL("../../assets/img/" + image , 
                    import.meta.url
                    ).href
    },
    itemClick(index) {
      this.currentIndex = index
    }
  }
}
```

### 2.2、TabBar的路由切换

将item传递进点击事件中，push动态添加路由。

```js
@click="itemClick(item, index)"
```

```js
this.$router.push(item.path)
```

### 2.3项目代码

`src/components/tabBar.vue`

```html
<template>
  <div class="tab-bar">
    <template v-for="(item, index) in tabbarDate">
      <div class="tab-bar-item"
           @click="itemClick(item, index)"
           :class="{ active: currentIndex === index }"
      >
        <img v-if="currentIndex !== index" :src="getAssetURL(item.image)" alt="">
        <img v-else :src="getAssetURL(item.imageActive)" alt="">
        <span class="text">{{ item.text }}</span>
      </div>
    </template>
  </div>
</template>

<script>
import tabbarDate from '../../assets/data/tabbar.js'
export default {
  data() {
    return {
      tabbarDate,
      currentIndex: 0
    }
  },
  methods: {
    getAssetURL(image) {
      return new URL('../../assets/img/' + image, 
                    import.meta.url).href
    },
    itemClick(item, index) {
      console.log("holle click")
      this.currentIndex = index
      this.$router.push(item.path)
    }
  }
}
</script>

<style lang="less" scoped>
.tab-bar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 50px;

  border: 1px solod #f3f3f3;

  display: flex;
}

.tab-bar-item {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;

  flex-direction: column;
  
  img {
    width: 32px;
  }
  .text {
    font-size: 12px;
    margin-top: 3px;
  }
}

.active {
  color: var(--theme-color);
}

</style>
```

## 3、Vant库重构tabbar

![image-20230314092634903](E:\coder\09_OneNote\image\image-20230314092634903.png)

### 3.1、组件库

#### 3.1.1、类型一：后台管理系统

`Element-UI ( Vue2 ) / Element-Plus ( Vue3 )`

#### 3.1.2、类型二：小程序

`小程序原生UI库`/`Vant`

#### 3.1.3、类型三：移动Web页面

`Vant UI`

#### 3.1.4、类型四：网易云/知乎/Bilibili

`Element-Plus`

### 3.2、Vant的引入

轻量、可靠的移动端 Vue 组件库

#### 3.2.1、使用npm安装

Vue 3 项目，安装最新版 Vant

`npm i vant`

#### 3.2.2、安装插件

`npm i unplugin-vue-components -D`

#### 3.2.3、配置插件

`src/main.js`

```javascript
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import Components from 'unplugin-vue-components/vite';
import { VantResolver } from 'unplugin-vue-components/resolvers';


// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    Components({
      resolvers: [VantResolver()],
    })
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})
```

#### 3.2.4、使用：直接复制代码进来使用

> `Vant`
> https://vant-contrib.gitee.io/vant/v3/#/zh-CN/home
> `Element UI`
> https://element-plus.org/zh-CN/

> 在公司开发有些东西并不是完全手写的，可以直接去使用库，拿来用就好，
>
> 刚进去公司第一阶段，是要先能完成公司安排的任务，完成任务放在第一位，
>
> 之后再研究深入的东西，不要影响到日常工作开发效率，不管用什么方法，不要自己造轮子。
>
> 基本的东西还是要掌握好，这样使用别人的东西也能看懂，并且较好的使用

### 3.3、使用Vant重构homeTabbar

`src/components/tabBar.vue`

```html
<template>
  <van-tabbar v-model="currentIndex">
    <van-tabbar-item v-for="( item, index ) in tabbarDate">
      <span>{{ item.text }}</span>
      <template v-slot:icon>
        <img v-if="currentIndex !== index" v-bind:src="getAssetURL(item.image)" alt="">
        <img v-else v-bind:src="getAssetURL(item.imageActive)" alt="">
      </template>
    </van-tabbar-item>
  </van-tabbar>
</template>
<style scoped>
</style>
```

#### 3.3.1、重写样式、添加路由

去官网寻找对应的属性，官网一些属性是固定的，记得用`v-bind`绑定，

使用插槽插入进来的，我们可以将它默认的样式覆盖掉

#### 3.3.2、关于修改第三方UI组件库的样式

==就这四种:==

1、如果用的是插槽，并且插入的是自己的元素，那么直接在自己的作用域中直接修改中各个元素

2、全局定义的一个变量，覆盖它默认变量的值

缺点：全局修改

3、局部定义一个变量，覆盖它默认变量的值

优点：局部修改

4、直接找到对应的子组件选择器，进行修改

`：deep`(子组件中元素的选择器)进行修改

直接修改CS

> 如果以前学的一些忘记了，那就去回顾，一边做项目一边回顾，把以前学的回顾起来~

#### 3.3.3、使用Vant重写样式、添加路由

`:to`

`src/components/tabBar.vue`

```vue
<template>
<div class="tab-bar">
  <van-tabbar v-model="currentIndex" active-color="#ff9854">
    <template v-for="( item, index ) in tabbarDate">
      <van-tabbar-item v-bind:to="item.path">
        <template v-slot:default >
          <span>{{ item.text }}</span>
        </template>
      <template v-slot:icon>
        <img v-if="currentIndex !== index" v-bind:src="getAssetURL(item.image)" alt="">
        <img v-else v-bind:src="getAssetURL(item.imageActive)" alt="">
      </template>
    </van-tabbar-item>
    </template>
  </van-tabbar>
</div>
</template>

<script>
import tabbarDate from '../../assets/data/tabbar.js'
export default {
  data() {
    return {
      tabbarDate,
      currentIndex: 0,
    }
  },
  methods: {
    getAssetURL(image) {
      // 参数一：项目路径
      // 参数二：当前路径的rul
      return new URL("../../assets/img/" + image,
        import.meta.url
      ).href
    },
    itemClick(index, item) {
      this.currentIndex = index,
        this.$router.push(item.path)
    }
  }
}
</script>
<style scoped>
img {
    height: 26px;
  }
</style>
```

#### 3.3.4、默认图标大小修改

![image-20230314093735095](E:\coder\09_OneNote\image\image-20230314093735095.png)

> 没听懂，之后把CSS高级学完后复习
>
> 引入进来的默认图标时候的是字体图标，修改大小的话，需要修改`font-size`的大小，

==修改变量的大小：==

##### 3.3.4.1、全局修改

任何地方使用到，都会被修改掉

  `--van-tabbar-item-icon-size: 30px !important;`

##### 3.3.4.2、局部修改

针对于`tabBar`中的类会生效，但是这里访问不到插槽插入进来的其他组件的作用域

  `--van-tabbar-item-icon-size: 30px !important;`


因此需要使用Vue提供的一个语法

##### 3.3.4.3、找到类，对类中的CSS属性重写

⭐⭐⭐（很重要）修改方式：`vue`专门提供的语法：

    `:deep(.van-tabbar-item_icon) {}`

##### 3.3.4.5、修改默认导入的库图标大小

`tab-bar.vue`

```
<style scoped>
.tab-bar:deep(.van-tabbar-item__icon) {
    font-size: 30px;
  }
</style>
```

## 4、HomeNavbar组件封装

![image-20230314094807991](E:\coder\09_OneNote\image\image-20230314094807991.png)



`src/views/home/home.vue`

### 4.1、NavBar基本搭建

> 简单的东西可以先自己做，==把能搞的东西先做好==，比较复杂的东西，之后再考虑去用库里面的东西。
>
> CSS的变量使用还没学会，先放着，回头再看，很多UI库都在用这个变量，很方便



`src/views/home/home.vue`

```js
<style lang="less" scoped>
.nav-bar {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 46px;

  border-bottom: 1px solid #f2f2f2;

  .title {
    color: var(--theme-color);
    font-size: 16px;
    font-weight: 600;
  }
}
</style>
```

`src/views/home/home.vue`

```html
<template>
  <div class="home">
    <div class="nav-bar">
      <div class="title">宏源旅途</div>
    </div>
  </div>
</template>

<script setup>
</script>

<style  scoped>
.nav-bar {
  display:flex;
  justify-content: center;
  align-items: center;
  height: 46px;
  border-bottom: 1px solid #f2f2f2;
}

.title {
  color:#ff9854 ;
  font-size: 16px;
  font-weight: 600;
}
</style>
```

### 4.2、NavBar组件封装

开发完之后，考虑将这一部分封装到单独的组件，刚开始没有想到复用性的时候先不要想着封装，不然会懵掉。

> 1、新建`src/views/home/cpns/HomeNavBar.vue`文件夹，
> 2、新建`HomeNavBar.vue`组件
> 3、导入组件

就算有些没有复用性的东西，也会将单独的逻辑、单独的样式、单独的HTML封装在一起。

`src/views/home/cpns/home-nav-bar.vue`

```vue
<template>
  <div class="nav-bar">
    <div class="title">DoubleQ</div>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="less" scoped>
.nav-bar {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 46px;

  border-bottom: 1px solid #f2f2f2;


  .title {
    color: var(--theme-color);
    font-size: 16px;
    font-weight: 600;
  }
}
</style>
```

`src/views/home/home.vue`

```vue
<template>
  <div class="home">
    <home-nav-bar></home-nav-bar>
  </div>
</template>
  
<script>
  import HomeNavBar from './cpns/home-nav-bar.vue'
  export default {
    components: {
      HomeNavBar,
    }
  }
</script>
<style  scoped>
</style>
```

## 5、HomeBanner搭建

![image-20230314095544307](E:\coder\09_OneNote\image\image-20230314095544307.png)

`src/views/home/cpns/HomeBanner.vue`

```html
<template>
  <div class="banner">
    <img src="../../../assets/img/home/banner.webp" alt="">
  </div>
  <div class="location">
    <div class="city">广州</div>
    <div class="position">
      <span>我的位置</span>
      <img src="../../../assets/img/home/icon_location.png" alt="">
    </div>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="less" scoped>
.banner {
  img {
    width: 100%;
  }
}
.location {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 44px;
    margin-left: 3px;

    .city {
      flex: 1;
      font-size: 16px;
    }

    .position {
      display: flex;
      // width: 74px;
      color: #333;
      align-items: center;
    }

    img {
      position: relative;
      top: -2px;
      margin-right: 3px;
      margin-left: 5px;
      width: 18px;
    }
  }

</style>
```

## 6、获取位置信息

位置栏功能完善

![image-20230314100320916](E:\coder\09_OneNote\image\image-20230314100320916.png)

![image-20230314100324401](E:\coder\09_OneNote\image\image-20230314100324401.png)

-----
### 6.1、获取位置

```javascript
  methods: {
    getPosition() {
      return new Promise((resolve, reject) => {
        navigator.geolocation.getCurrentPosition(
          res => {
            console.log("获取位置成功", res)
            resolve(res)
          },
          err => {
            console.log("获取位置失败", err)
            reject(err)
          }
        )
      })
    }
  }

```

> 💡💡💡 
>
> 定义了一个名为 `getPosition()` 的方法，用于获取设备的地理位置信息。
>
> `getPosition()` 方法返回了一个 Promise 对象，该对象在成功时会将获取的地理位置信息传递给 resolve() 方法，在失败时会将错误信息传递给 reject() 方法。
>
> 这种方式使用了 JavaScript 的 Promise API，可以使异步代码更易于编写和理解，并提供了更好的错误处理机制。
>
> 需要注意的是，在使用 `getCurrentPosition()` 方法获取地理位置信息时，浏览器会向用户显示一个请求位置的提示框，如果用户选择拒绝，将会触发错误回调函数并返回一个 `PermissionDeniedError` 错误。因此，如果您的应用程序需要获取位置信息，请确保向用户解释为什么需要该权限，并确保在代码中处理可能的错误情况。

### 6.2、抽取到HomePosition.vue

`src/views/home/cpns/HomePosition.vue`

```html
<template>
    <div class="location">
      <div class="city" @click="cityClick">广州</div>
      <div class="position" @click="getPosition()">
        <span>我的位置</span>
        <img src="../../../assets/img/home/icon_location.png" alt="">
      </div>
    </div>
</template>
<script>
export default {
  methods: {
    getPosition() {
      return new Promise((resolve, reject) => {
        navigator.geolocation.getCurrentPosition(
          res => {
            console.log("获取位置成功", res)
            resolve(res)
          },
          err => {
            console.log("获取位置失败", err)
            reject(err)
          }
        )
      })
    },
    cityClick() {
      console.log("city")
      this.$router.push("/city")
    }
  }
}
</script>

<style lang="less" scoped>
.location {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 44px;
  margin-left: 3px;
  .city {
    flex: 1;
    font-size: 16px;
  }
  .position {
    display: flex;
    // width: 74px;
    color: #333;
    align-items: center;
  }

  img {
    position: relative;
    top: -2px;
    margin-right: 3px;
    margin-left: 5px;
    width: 18px;
  }

}
</style>
```

`src/views/home/cpns/banner.vue`

```html
<template>
  <div class="banner">
    <img src="../../../assets/img/home/banner.webp" alt="">
  </div>
</template>

<script>
export default {
}
</script>

<style lang="less" scoped>
.banner {
  img {
    width: 100%;
  }
}
</style>
```

`src/views/home/home.vue`

```html
<template>
  <nav-bar></nav-bar>
  <banner></banner>
  <search-box></search-box>
</template>

<script>
import navBar from './cpns/nav-bar.vue'
import banner from './cpns/banner.vue'
import searchBox from './cpns/searchBox.vue'
export default {
  components: {
    navBar,
    banner,
    searchBox
  },
}
</script>

<style lang="less" scoped>
</style>
```

由于抽取组件步骤已有，后面不在放关于抽取组件的内容，想不到的话，就来前面参考~

## 7、城市搜索页面搭建

### 7.1、基本搭建

![image-20230314101117558](E:\coder\09_OneNote\image\image-20230314101117558.png)

`src/views/city/SearchPage.vue`

```html
<template>
  <div class="city">
    <van-search shape="round" class="searchIcon" v-model="searchValue" placeholder="城市/区域/位置" />
  </div>
</template>

<script>
export default {

}
</script>

<style lang="less" scoped>
  .searchIcon {
    --van-search-left-icon-color: var(--theme-color) !important;
  }
</style>

```

### 7.2、添加取消按钮和事件

![image-20230314101623399](E:\coder\09_OneNote\image\image-20230314101623399.png)

`src/views/city/SearchPage.vue`

```html
<template>
  <div class="city">
    <van-search shape="round" 
                class="searchIcon" 
                v-model="searchValue" 
                show-action
                @cancel="onCancel"
                placeholder="城市/区域/位置" />
  </div>
</template>
<script>
export default {
  methods:{
    onCancel() {
      this.$router.back()
    }
  }
}
</script>
```

### 7.3、添加标签选择

`src/views/city/SearchPage.vue`

```html
<template>
  <div class="city">
    <!-- 搜索区域 -->
    <van-search shape="round" class="searchIcon" v-model="searchValue" show-action @cancel="onCancel"
      placeholder="城市/区域/位置" />

    <!-- 标签选择 -->
    <van-tabs line-height="2px" color="var(--theme-color)" v-model:active="active">
      <van-tab title="国内·港澳台">国内·港澳台</van-tab>
      <van-tab title="海外">海外</van-tab>
    </van-tabs>
  </div>
</template>

<script>
export default {
  methods: {
    onCancel() {
      this.$router.back()
    }
  }  
}
</script>

<style lang="less" scoped>
.searchIcon {
  --van-search-left-icon-color: var(--theme-color) !important;
}
.city {
  --van-tabs-line-height:30px;
}
</style>
```

### 7.4、城市搜索界面隐藏TabBar

7.4.1、方案一：获取路由传递的参数

> 💡💡💡 注意==route==
>
>  `!this.$route.meta.hiddenTabBar` 

`src/App.vue`

```html
<template>
  <div class="app">
    <router-view></router-view>
    <tab-bar v-if="!this.$route.meta.hiddenTabBar"></tab-bar>
  </div>
</template>
```

`src/router/index.js`

```javascript
{
  path:"/city",
  component: () => import('../views/city/city.vue'),
  meta: {
    hiddenTabBar: true
  }
}
```

### 7.5、发送网络请求

安装==axios==

`npm install axios`

接口网址

[http://123.207.32.32:1888/api](http://123.207.32.32:1888/api)

#### 7.5.1、文件夹管理

**网络请求工具封装**

`src/services/request/index.js`

**网址管理文件**

`src/services/request/config.js`

**分模块文件**

`src/services/modules/city.js`

**导出管理文件**

`src/services/index.js`用来在这里统一给

它做一个导出

#### 7.5.2、操作流程

1、封装网络请求工具

`src/service/request/index.js`

```js
import axios from 'axios'

import { BASE_URL, TIMEOUT } from './config'

class DQRequest {
  constructor(baseURL, timeout=10000) {
    this.instance = axios.create({
      baseURL,
      timeout
    })
  }

  request(config) {
    return new Promise((resolve, reject) => {
      this.instance.request(config).then(res => {
        resolve(res.data)
      }).catch(err => {
        reject(err)
      })
    })
  }

  get(config) {
    return this.request({ ...config, method: "get" })
  }

  post(config) {
    return this.request({ ...config, method: "post" })
  }
}

export default new DQRequest(BASE_URL, TIMEOUT)
```

2、网址管理文件

`src/services/request/config.js`

```javascript
export const BASE_URL = " http://123.207.32.32:1888/api"
// export const BASE_URL = "http://codercba.com:1888/api"
export const TIMEOUT = 10000 
```

3、分模块文件

`src/services/modules/city.js`

```
import DQRequest from '../request/index'
export function getAllCity() {
  return DQRequest.get({
    url: "/city/all"
  })
}
```

##### ==这里被卡了两个多小时==

> ❗❗❗
> 1、在 city.js 文件中，我使用了 `dqRequest().get` 来调用 `getAllCity` 函数。根据 `dqRequest` 的定义，它是一个 `DQRequest` 的实例对象，不是一个函数。因此，我们需要将 `dqRequest()` 改成 `dqRequest`，即不需要在 `dqRequest` 后面加括号。
>
> 1、接口地址有误

4、统一导出管理文件

`src/services/index.js`

```js
export * from './modules/city'
```

这段代码 `export * from './modules/city'` 的意思是将一个模块 `city` 中的所有导出`（export）`重新导出`（re-export）`到当前模块中。

更具体地说，这个语句会将 `./modules/city` 模块中的所有导出都作为当前模块的导出。这包括该模块中所有被导出的变量、函数、类等。这样，其他模块可以通过导入当前模块来访问这些导出。

需要注意的是，这里使用的是 * 通配符来表示要重新导出的所有内容。这相当于把 city 模块的所有导出都导出到当前模块中，而不是仅导出其中的一部分。另外，export * 必须放在当前模块的顶层，不能嵌套在函数或代码块中。

#### 7.5.3、获取city数据

![image-20230314102354961](E:\coder\09_OneNote\image\image-20230314102354961.png)

`src/views/city/SearchPage.vue`

```html
<template>
  <div class="city">
    <!-- 搜索区域 -->
    <van-search shape="round" class="searchIcon" v-model="searchValue" show-action @cancel="onCancel"
      placeholder="城市/区域/位置" />

    <!-- 标签选择 -->
    <van-tabs line-height="2px" color="var(--theme-color)" v-model:active="active">
      <van-tab title="国内·港澳台">{{ cityList }}</van-tab>
      <van-tab title="海外">{{ cityList }}</van-tab>
    </van-tabs>
  </div>
</template>

<script>
import { getAllCity } from '../../service/index'
export default {
  data() {
    return {
      cityList:{},
      searchValue: "",
      active: 0
    }
  },
  methods: {
    onCancel() {
      this.$router.back()
    }
  },
    created() {
      getAllCity().then(res => {
        this.cityList = res
      })
    }
	}
</script>

<style lang="less" scoped>
.searchIcon {
  --van-search-left-icon-color: var(--theme-color) !important;
}

.city {
  --van-tabs-line-height: 30px;
}
</style>
```

1、在 Vue 组件中，`getAllCity().then(res => { console.log(res) })` 会在请求完成后打印响应数据，但它并没有对 `cityList` 进行赋值，因此城市列表数据并没有在页面上显示出来。建议将返回的城市列表数据存储在组件的 data 中，并在页面上使用 v-for 指令渲染城市列表。

2、有两个属性`searchValue`和`active`，它们在渲染过程中被访问但未在 Vue 实例上定义。当您尝试访问尚未在组件的数据或计算属性中声明或初始化的属性时，可能会发生这种情况。

要解决此问题，您应该确保在组件的数据或计算属性中正确声明和初始化“`searchValue`和`active`属性。（`Vant模板`中引入的，后面有用）

**生命周期中发送网络请求：**

```javascript
created() {
  getAllCity().then(res => {
    this.cityList = res
  })
}
```

还可以把网络请求相关的内容抽取到store中，之后在说~

#### 7.5.4、数据动态展示1

![image-20230314182508323](E:\coder\09_OneNote\image\image-20230314182508323.png)



遇见问题卡了一个小时，始终不能把数据展示出来，

原因在于：

> 想要在 van-tabs 中展示城市列表数据，但是由于 `cityList` 是在异步请求获取数据后才会更新的，所以在组件渲染时，数据可能还没有获取到。
>
> 为了解决这个问题，您可以在模板中添加一个判断，检查 `cityList` 是否有数据。只有在 `cityList` 数据有值时才渲染 `van-tabs` 组件。

最终代码

```
    <template v-if="Object.keys(cityList).length !== 0">
      <van-tabs line-height="2px" color="var(--theme-color)" v-model:active="active">
        <van-tab :title="cityList.data.cityGroup.title"></van-tab>
        <van-tab :title="cityList.data.cityGroupOverSea.title"></van-tab>
      </van-tabs>
    </template>
    <template v-else>
      <!-- 当没有数据时的提示信息 -->
      <div>暂无数据</div>
    </template>
```

```
  created() {
    getAllCity().then(res => {
      console.log(res)
      this.cityList = res
    })
  }
```

这里添加了一个 `Object.keys(cityList).length !== 0` 的判断，`Object.keys(cityList).length` 是通过 `Object.keys()` 方法将 `cityList` 对象的键转化为数组，然后取该数组的 `length` 属性得到键的数量。如果该数量不为 0，说明 `cityList` 中有数据，于是就显示标签选择的组件。

此外，我建议你将`getAllCity()`放在`mounted`钩子函数中，因为在`created`中赋值会在模板渲染之前完成，所以你的数据可能不会及时更新，而在`mounted`中赋值可以保证你的数据更新及时并正确地在模板中显示。

**问题二**

始终不能通过for循环展示出来想要的数据，因此就先不循环了，继续往下做~

#### 7.5.5、搜索栏滚动固定

![image-20230314183740731](E:\coder\09_OneNote\image\image-20230314183740731.png)

**设置固定高度**

```css
.content {
    height: calc(100vh - 98px);
    overflow: auto;
  }
```

这段代码定义了一个样式，用于设置 `.content` 元素的高度和溢出方式。

`height: calc(100vh 98px)` 表示设置元素的高度，`calc` 是一个计算函数，用于计算表达式中的值，这里计算的表达式是 `100vh - 98px`，即 `100vh` 减去 `98px`，因此这个样式设置了元素的高度为当前视窗高度减去 `98px`。

`overflow: auto` 表示当内容溢出元素的边界时，设置自动出现滚动条以显示溢出内容。如果元素的内容未溢出，则不显示滚动条。

#### 7.5.6、展示数据

获取选中标签时，拿到的数据

根据不同的key，拿到不同的值，

复盘的时候再说。

```html
<template v-if="Object.keys(cityList).length !== 0">
  <van-tabs line-height="2px" color="var(--theme-color)" v-model:active="active">
    <van-tab :title="cityList.data.cityGroup.title">{{cityList.data.cityGroup}}</van-tab>
    <van-tab :title="cityList.data.cityGroupOverSea.title">{{ cityList.data.cityGroupOverSea }}</van-tab>
  </van-tabs>
</template>
```

==小插曲==

打开了个许巍，把上面的v-for问题解决了。。。老师使用的是setup语法展示动态的，我想跟着他但是，自己使用用`Opations API`做，等之后再考虑使用他的方法。因此做的过程中，会有很多的问题~

解决方案：

```html
<template v-if="Object.keys(cityList).length !== 0">
  <van-tabs line-height="2px" color="var(--theme-color)" v-model:active="active">
      <template v-for="(group, index) in [cityList.data.cityGroup, cityList.data.cityGroupOverSea]" :key="index">
        <van-tab :title="group.title">{{group}}</van-tab>
      </template>
  </van-tabs>
</template>
```



还是解决不了。。。。

改用老师教的composition API吧还是，自己实在是搞不定。



## 8、搜索页面方案二（Composition API）

![image-20230316174149394](E:\coder\09_OneNote\image\image-20230316174149394.png)

方案一执行不下去了 ~

使用Composition API的`<script setup>`语法

### 8.1、基本搭建

之后再考虑抽取网络请求到单独的文件

`src/views/city/SearchPage.vue`

```html
<template>
  <div class="city">
    <!-- 搜索区域 -->
    <van-search shape="round" 
                class="searchIcon" 
                v-model="searchValue" 
                show-action 
                @cancel="onCancel"
      placeholder="城市/区域/位置" />

      <van-tabs line-height="2px" color="var(--theme-color)" v-model:active="tabActive">
        <template v-for="(value, key, index) in allCitys" >
          <van-tab :title="value.title"></van-tab>
        </template>
        <div class="content">
        <template v-for="(value, key, index) in allCitys" >
          {{ value }}
        </template>
        </div>
      </van-tabs>
  </div>
</template>

<script setup>

import { getAllCity } from '../../service/index'
import {ref} from 'vue'
import { useRouter } from 'vue-router';

const tabActive = ref()
const searchValue = ref()
const allCitys = ref()
const router = useRouter()

// 1、取消事件
const onCancel = () => {
  router.back()
}

// 2、网络请求
getAllCity().then(res => {
  allCitys.value = res.data
})

</script>

<style lang="less" scoped>
.searchIcon {
  --van-search-left-icon-color: var(--theme-color) !important;
}

.city {
  --van-tabs-line-height: 30px;

  .content {
    height: calc(100vh - 98px);
    overflow: auto;
  }

}
</style>
```

注意点：

```javascript
const allCitys = ref()
// 2、网络请求
getAllCity().then(res => {
  allCitys.value = res.data
})
```

首先，使用`ref()`函数创建一个响应式变量`allCitys`，这个变量的初始值为`undefined`。

接着，调用一个异步函数`getAllCity()`，这个函数返回一个Promise对象，用于获取所有城市列表的数

### 8.2、获取选中标签的值

![image-20230314212023078](E:\coder\09_OneNote\image\image-20230314212023078.png)

关键代码：

```html
    <van-tabs line-height="2px" color="var(--theme-color)" v-model:active="tabActive">
      <template v-for="(value, key, index) in allCities" :key="key" >
        <van-tab :title="value.title"
                  :name="key"  
                  ></van-tab>
      </template>
      <div class="content">
        <template v-for="item in currentGroup" >
          {{ item }}
        </template>
      </div>
    </van-tabs>
```

```javascript
const tabActive = ref()
const allCities = ref()
const currentGroup = computed(()=> allCities.value[tabActive.value])
```

代码说明：

> 使用 Vue.js 的模板语法来渲染一个带有标签页切换功能的页面。其中，使用了 `van-tabs` 组件来实现标签页切换，该组件的 `line-height` 和 `color` 属性分别用于设置标签页下划线的高度和颜色。`v-model:active` 属性用于实现标签页选中状态的双向绑定，即当用户点击标签页时，`tabActive` 的值将发生变化，从而触发 `currentGroup` 的重新计算。
>
> 使用 `const` 关键字创建了一个名为 `currentValue` 的常量，用于保存 `allCities` 中 `cityGroup` 对应的数据。由于 `allCities` 是响应式数据，因此在获取其中的数据时需要加上 `.value`，即 `allCities.value["cityGroup"]`。这样做是为了确保在数据发生变化时，能够及时触发相关的更新。
>
> 使用 `allCities.value` 来获取所有城市的数据，再通过 `tabActive.value` 来获取当前选中标签页的值，并将这个值作为下标来获取对应的城市数据。由于 `currentGroup` 是计算属性，所以它的值会自动更新，从而保证了页面的实时性。
>
> 在 `van-tabs` 中，使用 `v-for` 指令遍历 `allCities` 中的所有城市数据，并使用 `van-tab` 组件渲染每一个标签页。`title` 属性用于设置标签页的标题，`name` 属性用于指定标签页的名称，以便在点击标签页时更新 `tabActive` 的值。
>
> 在 `van-tabs` 下方，使用了一个 `div` 元素来展示当前选中标签页的内容。使用 `v-for` 指令遍历 `currentGroup` 中的所有数据，并将它们渲染到模板中。在这里，`computed` 函数被用来监听 `tabActive` 的变化，当 `tabActive` 的值发生变化时，重新计算 `currentGroup` 的值，从而更新当前展示的数据。同时，该代码中使用了 `ref()` 函数来创建响应式数据 `tabActive` 和 `allCities`，用于存储当前选中标签页和搜索关键字的值。
>
> 在这段代码中，`name` 属性用于指定标签页的名称，它与 `v-model:active` 指令中的 `tabActive` 变量建立了联系，用于标识当前选中的标签页。

#### 需要一个变量保存数据

`const currentValue = allCities.value["cityGroup"]`

只要是响应式数据，如果想使用，都需要加上`.value`

`computed` 函数被用来监听 `tabActive` 的变化，当 `tabActive` 的值发生变化时，重新计算 `currentGroup` 的值，从而更新当前展示的数据。

#### 根据不同的key拿到不同的值

`tabActive`绑定`key`

#### name标签作为匹配的标识符

数据处理是一个相对比较复杂的过程，特别是还需要切换时，

`src/views/city/SearchPage.vue`

```html
<template>
  <div class="city">
    <!-- 搜索区域 -->
    <van-search shape="round" 
                class="searchIcon" 
                v-model="searchValue" 
                show-action 
                @cancel="onCancel"
                placeholder="城市/区域/位置" 
      />

    <van-tabs line-height="2" color="var(--theme-color)" v-model:active="tabActive">
      <template v-for="(value, key, index) in allCities" :key="key" >
        <van-tab :title="value.title"
                  :name="key"  
                  ></van-tab>
      </template>
      <div class="content">
        <template v-for="item in currentGroup" >
          {{ item }}
        </template>
      </div>
    </van-tabs>
  </div>
</template>

<script setup>

import { getAllCity } from '../../service/index'
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router';

const tabActive = ref()
const searchValue = ref()
const allCities = ref()
const router = useRouter()

// 1、取消事件
const onCancel = () => {
  router.back()
}
// 2、网络请求
getAllCity().then(res => {
  allCities.value = res.data
})

// 3、获取选中标签的值
const currentGroup = computed(() => allCities.value[tabActive.value])
</script>

<style lang="less" scoped>
.searchIcon {
  --van-search-left-icon-color: var(--theme-color) !important;
}

.city {
  --van-tabs-line-height: 30px;

  .content {
    height: calc(100vh - 98px);
    overflow: auto;
  }

}
</style>
```

### 8.3、展示数据

![image-20230314215950315](E:\coder\09_OneNote\image\image-20230314215950315.png)



![image-20230314215608183](E:\coder\09_OneNote\image\image-20230314215608183.png)

数据有很多的嵌套关系，不好拿， 如果觉得比较难的话，先按简单的方法来做，不用考虑封装的问题。

核心代码

```html
<div class="content">
    <template v-for="(group, index) in currentGroup?.cities" :key="index">
      <div class="group-item">
        <div class="title">{{ group.group }}</div>
        <div class="list">
          <div v-for="(city, index) in group.cities" :key="index">
            <div class="city-list">{{ city.cityName }}</div>
          </div>
        </div>
      </div>
    </template>
  </div>
</div>
```

代码解释：

> 这是一个使用Vue.js的模板，用于渲染城市分组列表。下面是代码的详细解释：
>
> 1. 外层的`<div class="content">`包含了整个列表的内容。
> 2. `v-for`指令通过循环遍历`currentGroup?.cities`数组中的每个元素，并将当前元素的值存储在一个名为`group`的变量中。`index`是当前元素的索引。
> 3. `:key="index"`属性指定了循环中每个元素的唯一标识符。这是Vue.js在更新列表时使用的一种优化技巧，以确保每个元素都能正确地更新。
> 4. `<div class="group-item">`是每个城市分组的容器。它包含了一个标题和城市列表。
> 5. `<div class="title">{{ group.group }}</div>`是当前分组的标题。`group.group`使用了`group`变量的`group`属性来渲染。
> 6. `<div class="list">`是城市列表的容器。
> 7. 第二个`v-for`指令遍历`group.cities`数组中的每个城市，将其存储在一个名为`city`的变量中。
> 8. `<div class="city-list">{{ city.cityName }}</div>`是当前城市的显示名称。`city.cityName`使用了`city`变量的`cityName`属性来渲染。
>
> 注意，这里有一个问号，`currentGroup?.cities`，这是JavaScript中的可选链语法，以避免当`currentGroup`为`null`或`undefined`时发生错误。

### 8.4、展示数据方案二

![image-20230314234615554](E:\coder\09_OneNote\image\image-20230314234615554.png)

#### 获取数据难点

在于：需要梳理清除数据

直接去库里面找

增添颜色`highlight-color="var(--theme-color)"`

删除吸顶效果`:sticky="false"`

嵌套循环~

```html
<van-index-bar highlight-color="var(--theme-color)" :sticky="false">
  <template v-for="(letter, index) in currentGroup.cities" :key="index">
    <van-index-anchor :index="letter.group" />
    <template v-for="(city, indexb) in letter.cities" :key="indexb">
      <van-cell :title="city.cityName" />
    </template>
  </template>
</van-index-bar>
```

#### 问题❓：控制台一直报错

似乎你正在尝试访问未定义的对象。具体来说，你正在尝试访问`currentGroup.cities`的值，但是`currentGroup`是通过`computed`函数计算得到的，并且其依赖于`tabActive`和`allCities`的值。

在`getAllCity`请求完成之前，`allCities`的值将为`undefined`，这将导致`computed`函数返回未定义的对象，进而导致在`<van-index-bar>`标签内部的模板中访问`currentGroup.cities`时出现错误。

为了解决这个问题，你可以考虑在`computed`函数中添加一些检查，以确保`allCities`的值存在并且`tabActive`是一个有效的索引。例如，你可以尝试将`currentGroup`的定义更改为：

```javascript
const currentGroup = computed(() => {
  if (allCities.value && allCities.value.length !== 0) {
    return allCities.value[tabActive.value];
  } else {
    return { cities: [] };
  }
});
```

### 8.5、城市列表动态映射

![image-20230315115401307](E:\coder\09_OneNote\image\image-20230315115401307.png)

#### 8.5.1、模拟数据

![image-20230315123049230](E:\coder\09_OneNote\image\image-20230315123049230.png)

```html
<van-index-anchor index="热门"></van-index-anchor>
<div class="hot-cities">
  <template v-for="item in ['city', 'city', 'city', 'city', 'city']">
    <div class="city">{{ item }}</div>
  </template>
</div>
```

调整样式

```css
.hot-cities {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;

  .city {
    width: 70px;
    height: 28px;
    border-radius: 15px;
    margin-top: 6px;
    background-color: #fff4ec;

    line-height: 28px;
    text-align: center;
  }
}
```

> 注意justify-content的属性区别
>
> - space-around
> - space-between

#### 8.5.2、真实数据

![image-20230315123511196](E:\coder\09_OneNote\image\image-20230315123511196.png)

```html
      <van-index-bar highlight-color="var(--theme-color)" :sticky="false">
        <van-index-anchor index="热门"></van-index-anchor>
          <div class="hot-cities">
            <template v-for="(item, index) in currentGroup.hotCities" :key="index">
              <div class="city">{{ item.cityName }}</div>
            </template>
          </div>

        <template v-for="(letter, index) in currentGroup.cities" :key="index">
          <van-index-anchor :index="letter.group" />
          <template v-for="(city, indexb) in letter.cities" :key="indexb">
            <van-cell :title="city.cityName" />
          </template>
        </template>

      </van-index-bar>
```

> 样式不合适的话自己慢慢再调整
>
> 拿数据的时候要观察我们需要什么数据，在对其进行展示就可以了

#### 问题❓：索引动态映射

官方Vant库索引A~Z是默认排列，但是城市有些字母开头是没有的，导致后边的索引==对应关系==有问题，因此要重新排列索引~并且在第一个索引值加一个`#`

获取数据中的字母索引，绑定到`van-index-bar`，添加`#`

```html
<van-index-bar highlight-color="var(--theme-color)" :sticky="false" :index-list="indexList">
```

```javascript
const indexList = computed(() => {
  if (currentGroup.value && currentGroup.value.cities && currentGroup.value.cities.length !== 0) {
    const list = currentGroup.value.cities.map(item => item.group)
    list.unshift("#")
    return list
  }
})
```

`src/views/city/SearchPage.vue`

```html
<template>
  <div class="search-page">
    <!-- 搜索区域 -->
    <van-search shape="round" class="searchIcon" v-model="searchValue" show-action @cancel="onCancel"
      placeholder="城市/区域/位置" />

    <!-- 标签栏切换 -->
    <van-tabs line-height="2" color="var(--theme-color)" v-model:active="tabActive">
      <template v-for="(value, key, index) in allCities" :key="key">
        <van-tab :title="value.title" :name="key"></van-tab>
      </template>
    </van-tabs>


    <!-- 数据列表 -->
    <div class="content">
      <!-- 字母索引 -->
      <van-index-bar highlight-color="var(--theme-color)" :sticky="false" :index-list="indexList">
        <van-index-anchor index="热门"></van-index-anchor>
        <div class="hot-cities">
          <template v-for="(item, index) in currentGroup.hotCities" :key="index">
            <div class="city">{{ item.cityName }}</div>
          </template>
        </div>

        <template v-for="(letter, index) in currentGroup.cities" :key="index">
          <van-index-anchor :index="letter.group" />
          <template v-for="(city, indexb) in letter.cities" :key="indexb">
            <van-cell :title="city.cityName" />
          </template>
        </template>

      </van-index-bar>
      <!-- <template v-for="(group, index) in currentGroup?.cities" :key="index">
        <div class="group-item">
          <div class="title">{{ group.group }}</div>
          <div class="list">
            <div v-for="(city, index) in group.cities" :key="index">
              <div class="city-list">{{ city.cityName }}</div>
            </div>
          </div>
        </div>
      </template> -->
    </div>
  </div>
</template>

<script setup>

import { getAllCity } from '../../service/index'
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router';

const tabActive = ref()
const searchValue = ref()
const allCities = ref()
const router = useRouter()

// 1、取消事件
const onCancel = () => {
  router.back()
}
// 2、网络请求
getAllCity().then(res => {
  allCities.value = res.data
})

// 3、获取选中标签的值
const currentGroup = computed(() => {
  if (allCities.value && allCities.value.length !== 0) {
    return allCities.value[tabActive.value];
  } else {
    return { cities: [] };
  }
});

// 4、索引列表重映射
const indexList = computed(() => {
  if (currentGroup.value && currentGroup.value.cities && currentGroup.value.cities.length !== 0) {
    const list = currentGroup.value.cities.map(item => item.group)
    list.unshift("#")
    return list
  }
})
</script>

<style lang="less" scoped>
.searchIcon {
  --van-search-left-icon-color: var(--theme-color) !important;
}

.search-page {
  --van-tabs-line-height: 30px;

  .content {
    height: calc(100vh - 98px);
    overflow: auto;

    .hot-cities {
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;


      .city {
        width: 70px;
        height: 28px;
        border-radius: 15px;
        margin-top: 6px;
        background-color: #fff4ec;

        line-height: 28px;
        text-align: center;
      }
    }
  }

}
</style>
```

#### 8.5.3、优化代码

对于之前代码的优化，有以下几点

1、简化对于`allCities`的判断 `ref({})`

```javascript
const allCities = ref({})
getAllCity().then(res => {
  allCities.value = res.data
})
```

2、网络请求使用状态管理工具的`actions`

```javascript
const allCities = ref({});
async function getAllCityData() {
  const response = await getAllCity();
  allCities.value = response.data;
}
getAllCityData();
```

3、将组件抽取到一个单独的文件里

`src/views/city/cpns/SearchPageCitis.vue`

4、在`src/views/city/SearchPage.vue`页面添加`v-show`控制渲染页面

```html
<div class="content">
  <template v-for="(value, key, index) in allCities">
    <city-group v-show="tabActive === key" :group-data="value" />
  </template>
</div>
```

5、使用Vuex管理网络请求、数据等等

> ❗❗❗先往下继续做，完成功能与内容，之后再想办法抽取封装、简化代码等等

### 8.6、回退和回显效果

> 这个项目界面使用库来做的话，不是很复杂，复杂的难点在于数据的展示。
>
> 没有关系，理清顺序一步一步慢慢来

> **两步操作：**
>
> 1、选择某个城市，退出
>
> 2、首页展示
>
> **两部分：**
>
> 1、热门城市
>
> 2、列表城市

#### 8.6.1、监听点击获取数据、返回上一级

```html
<van-index-bar highlight-color="var(--theme-color)" :sticky="false" :index-list="indexList">
  <van-index-anchor index="热门"></van-index-anchor>
  <div class="hot-cities">
    <template v-for="(item, index) in currentGroup.hotCities" :key="index">
      <div class="city" @click="cityClick(item)">{{ item.cityName }}</div>
    </template>
  </div>

  <template v-for="(letter, index) in currentGroup.cities" :key="index">
    <van-index-anchor :index="letter.group" />
    <template v-for="(city, indexb) in letter.cities" :key="indexb">
      <van-cell :title="city.cityName" @click="cityListClick(city)"/>
    </template>
  </template>
</van-index-bar>
```

```javascript
const cityClick = (city) => {
  console.log(city)
  router.back()
}
```

#### 8.6.2、将数据传递到首页

当前点击的数据，可能在很多地方都会使用到，因此有两种方案：

1、事件总线

`eventBus.emit("cityChange", city)`

2、Vuex状态管理

##### 问题：关于状态管理命名

> 在Vuex中，您可以将实例命名为除了"store"以外的任何名称。 "store"只是一个常用的名称，用于表示Vuex的核心实例。

例如，您可以使用以下代码将实例命名为"myStore"：

```js
import { createStore } from "vuex";

const myStore = createStore({
  state: {
    // your state
  },
  mutations: {
    // your mutations
  },
  actions: {
    // your actions
  },
  getters: {
    // your getters
  }
});

export default myStore;
```

然后在其他组件中可以通过 `this.$store` 访问它。

```javascript
<script>
import myStore from '@/store/myStore'

export default {
  computed: {
    myState() {
      return this.$store.state.myState
    }
  }
}
</script>
```

在 `main.js` 文件中，您可以将Vuex实例命名为除 "store" 以外的任何名称。只需将其导入并使用所选名称即可。

例如，假设您将实例命名为 `myStore`，则您的 `main.js` 文件应如下所示：

```js
import { createApp } from 'vue'
import App from './App.vue'
import myStore from './store/myStore'

const app = createApp(App)
app.use(myStore)
app.mount('#app')
```

无论您在 `main.js` 中将Vuex实例命名为什么名称，在组件中都只能使用 `$store` 来访问它。

例如，假设您在 `main.js` 中将实例命名为 `myStore`，则您可以在组件中使用以下代码访问该实例的状态：

```js
<template>
  <div>
    <p>Current count: {{ $store.state.count }}</p>
    <button @click="$store.commit('increment')">Increment</button>
  </div>
</template>
```

需要注意的是，您也可以在组件中使用 `mapState`、`mapGetters`、`mapActions` 和 `mapMutations` 辅助函数来简化访问 Vuex 实例中的状态、getters、actions 和 mutations，而不必每次都写 `$store`。但是，这些辅助函数本质上也只是为了简化代码书写，它们实际上也是使用 `$store` 来访问 Vuex 实例的。

> 分模块需要加上命名空间

##### 为什么需要加命名空间

在 Vuex 中使用模块时，每个模块都有自己的局部状态、getters、mutations 和 actions。当您在组件中访问模块中的状态或触发模块中的 mutations 或 actions 时，如果没有命名空间，Vuex 就无法确定这些操作应该应用于哪个模块。

通过添加命名空间，您可以指定该操作是针对哪个模块的。使用命名空间的方式有两种：

1. 字符串方式命名空间：在 `mapState`、`mapGetters`、`mapMutations` 和 `mapActions` 辅助函数中使用字符串来指定命名空间，如下所示：

   ```
   ...mapState({
     someState: state => state.moduleName,someState
   })
   ```

   在这个例子中，`moduleName` 就是模块的命名空间。

2. 对象方式命名空间：在组件中直接使用 `$store` 时，可以在提交 mutations 或触发 actions 时使用对象来指定命名空间，如下所示：

   ```
   this.$store.commit("moduleName/someMutation", payload)
   this.$store.dispatch("moduleName/someAction", payload)
   ```

   在这个例子中，`moduleName` 就是模块的命名空间。

通过指定命名空间，您可以确保操作只针对特定的模块，从而避免状态或操作的名称冲突，使得代码更加清晰和易于维护。

#### 8.6.3、使用Vuex优化项目代码，

建立`store`分模块

`src/stores/modules/useCityStore`

```js
import { createStore } from "vuex";
import { getAllCity } from '../../service/modules/city'
const useCityStore = createStore({
  namespaced: true,
  state: () => ({
    currentClickCity: "西安",
    allCitiesStore: {}
  }),
  mutations: {
    setAllCities(state, data) {
      state.allCitiesStore = data
    }
  },
  actions: {
    async fetchAllCityData(context) {
      try {
        const res = await getAllCity();
        context.commit("setAllCities", res.data);
      } catch (error) {
        console.error(error);
      }
    },
  },
})

export default useCityStore
```

> 这段代码是一个异步的 Action，名为 `fetchAllcityData`。它包含了一个 `try...catch` 代码块，用于异步请求所有城市数据。
>
> 在 Action 的函数体中，我们调用了一个名为 `getAllCity` 的函数，这个函数会向服务器发起一个 HTTP 请求，获取所有城市的数据。
>
> 当请求成功时，Promise 将被解决，并返回一个响应对象。我们使用 `await` 关键字来等待这个响应对象的返回，并将其保存在一个名为 `res` 的变量中。
>
> 接下来，我们调用了 `commit` 函数来触发 `setAllCities` Mutation。这个 Mutation 会将所有城市数据保存到 Vuex 状态管理器中，以便在整个应用程序中使用。
>
> 如果请求失败，Promise 将会被拒绝，并抛出一个错误。我们使用 `catch` 关键字来捕获这个错误，并在控制台中输出错误信息。
>
> 总之，这段代码通过异步 Action，从服务器获取所有城市的数据，并将其保存到 Vuex 状态管理器中，以便在整个应用程序中使用。

如果模块不使用`createStore`，那么可以直接暴漏到顶部`store`使用

组件中发送网络请求：

#### 8.6.4、一个BUG卡两天：

`[vuex] unknown action type:`

整整卡了一天，算了，这样做下去，肯定是太难了，这个项目的老师主要使用了`CompositionAPI + pinia`，但是我不想用这个，于是老师教的是一套东西，而我做的又是想使用`opation API`+`Vuex`，导致一直出问题。不过功夫不负有心人。

#### 8.6.5、成功了

> **终于终于，解决了问题**
>
> 使用**debugger**
>
> 结果自己还是坚持了下来，整整**卡了两天**，但是，自己用`debugger`一直调试，最终把状态管理做出来了。
>
> 同时加深了`状态管理`、`命名空间`、`状态管理模块`、`watch`、`watEffect`、`toRefs`、`网络请求`、`computed`、`响应式`等等知识内容，并且学会了看控制台的错误，果然**调试bug**才是学的最快的，并且状态一直在线，从早干到晚，一直不困~

### 8.7、最终代码

#### 状态管理库：

目前的状态管理库还没有分模块，因为我尝试过，没有成功，应该是哪里还有问题，不过功能现在是有了，先把项目搭建出来，不然已经卡了三天了，在不继续就没时间了。

尽管老师说`Vuex`要写`commit`，`pinia`非常简单好用，但是我还是想先学会`vuex`，这样之后使用`pinia`也会更简单

`src/stores/index.js`

```js
import { createStore } from "vuex";
// import useCityStore from './modules/useCityStore'
import {getAllCity} from '../../src/service/index'
const store =createStore({
  state: () => ({
    currentClickCity: "西安",
    allCities: {}
  }),
  mutations: {
    setAllCities(state, data) {
      state.allCities = data
      console.log("我是mutations：",data)
    }
  },
  actions: {
    async fetchAllCitiesData( context ) {
      const res = await getAllCity()
      context.commit("setAllCities", res.data)
      console.log("网络请求之后的数据：", res.data)
    },
  }
})

export default store
```

#### 网络请求：

```js
// 2、网络请求
const store = useStore()
store.dispatch('fetchAllCitiesData')
const { allCities } = toRefs(store.state)
console.log(allCities)

const tabActive = ref()
// 3、获取选中标签的值
const currentGroup = computed(() => allCities.value[tabActive.value])
console.log("currentGroup:", currentGroup)

// 从网络请求到这里，卡了整整两天，最后解决了，学到了很多
```

#### Vant库使用：

##### 标签栏切换:

```js
<!-- 标签栏切换 -->
<van-tabs line-height="2" color="var(--theme-color)" v-model:active="tabActive">
  <template v-for="(value, key, index) in allCities" :key="key">
    <van-tab :title="value.title" :name="key"></van-tab>
  </template>
</van-tabs>
```

##### 热门城市:

```js
<!-- 热门标题 -->
<van-index-anchor index="热门"></van-index-anchor>
<!-- 热门城市 -->
<div class="hot-cities">
  <template v-for="(item, index) in currentGroup?.hotCities" :key="index">
    <div class="city">{{ item.cityName }}</div>
  </template>
</div>
```

##### 城市列表展示:

```js
<!-- 城市数据列表 -->
<div class="cities">
  <!-- 循环字母 -->
  <template v-for="(cityList, index) in currentGroup?.cities" :key="index">
    <van-index-anchor :index="cityList.group" />
    <!-- 循环城市 -->
    <template v-for="(city, indexL) in cityList.cities" :key="indexL">
      <van-cell :title="city.cityName" />
    </template>
  </template>
</div>
```

##### 索引重映射:

```
:index-list="indexList">
```

```html
<van-index-bar highlight-color="var(--theme-color)" 
               :sticky="false" 
               :index-list="indexList">
</van-index-bar>
```

```js
const indexList = computed(() => {
  if (currentGroup.value && currentGroup.value.cities && currentGroup.value.cities.length !== 0) {
    const list = currentGroup.value.cities.map(item => item.group)
    list.unshift("#")
    return list
  }
})
```

为什么需要判断呢？因为不加判断无法显示值。一直报错。和代码里的❓是一个意思。

#### 点击回退

两部分的城市，

1、热门城市；

```html
<div class="city" @click="cityClick(item)">{{ item.cityName }}</div>
```

2、城市列表

```html
<van-cell :title="city.cityName " @click="cityClick(city)" />
```

```js
// 5、监听城市的点击
const cityClick = (city) => {
  console.log(city)
  router.back()
}
```

#### 首页城市切换

##### 思路一、使用事件总线

##### 思路二、使用状态管理库

这个时候状态管理库的优势就出来了；

使用状态管理的mutations，在组件中传递值，从而改变库中的值，

```javascript
mutations: {
  setAllCities(state, data) {
    state.allCities = data
    console.log("我是mutations：",data)
  },
  setCurrentCity(state, city) {
    state.currentClickCity = city.cityName
  }
},
```

```js
const cityClick = (city) => {
  console.log(city)
  router.back()
  store.commit("setCurrentCity", city)
}
```

至此，搜索界面功能算是在找BUG的过程中搭建完成了，顺便复习了状态管理库的使用~

最终页面代码

#### 之前不使用模板做的数据展示

```js
<!-- 不使用模板做的数据展示 -->
<!-- <template v-for="(group, index) in currentGroup?.cities" :key="index">
  <div class="group-item">
    <div class="title">{{ group.group }}</div>
    <div class="list">
      <div v-for="(city, index) in group.cities" :key="index">
        <div class="city-list">{{ city.cityName }}</div>
      </div>
    </div>
  </div>
</template> -->
```

为什么非要用库来管理这些数据呢？其实我早在两天前就展示出来数据了，但是里面的数据牵扯到重新赋值与响应式，于是需要使用Vuex状态管理库来管理数据，不然使用事件总线会更加的麻烦。

这里还有点问题是：切换数据时候很卡，选要根据索引值来`v-show`没有显示的数据。并且使用`keep-alive`缓存下来~

#### 最终最终页面代码

> 虽然不是最终的，因为还有很多需要优化的地方，但是自己探索出来的东西还是很开心~
>
> 1、页面抽取
>
> 2、响应式加`？`的问题
>
> 3、需要使用`if`判断
>
> 4、响应式的数据访问都要加上`value`

`src/views/city/SearchPage.vue`

```html
<template>
  <div class="search-page">
    <!-- 搜索区域 -->
    <van-search shape="round" class="searchIcon" v-model="searchValue" show-action @cancel="onCancel"
      placeholder="城市/区域/位置" />

    <!-- 标签栏切换 -->
    <van-tabs line-height="2" color="var(--theme-color)" v-model:active="tabActive">
      <template v-for="(value, key, index) in allCities" :key="key">
        <van-tab :title="value.title" :name="key"></van-tab>
      </template>
    </van-tabs>


    <!-- 数据列表 -->
    <div class="content">
      <!-- 字母索引 -->
      <van-index-bar highlight-color="var(--theme-color)" :sticky="false" :index-list="indexList">
        <!-- 热门标题 -->
        <van-index-anchor index="热门"></van-index-anchor>
        <!-- 热门城市 -->
        <div class="hot-cities">
          <template v-for="(item, index) in currentGroup?.hotCities" :key="index">
            <div class="city" @click="cityClick(item)">{{ item.cityName }}</div>
          </template>
        </div>

        <!-- 城市数据列表 -->
        <div class="cities">
          <!-- 循环字母 -->
          <template v-show="" v-for="(cityList, index) in currentGroup?.cities" :key="index">
            <van-index-anchor :index="cityList.group" />
            <!-- 循环城市 -->
            <template v-for="(city, indexL) in cityList.cities" :key="indexL">
              <van-cell :title="city.cityName " @click="cityClick(city)" />
            </template>
          </template>
        </div>
      </van-index-bar>

      <!-- 不使用模板做的数据展示 -->
      <!-- <template v-for="(group, index) in currentGroup?.cities" :key="index">
        <div class="group-item">
          <div class="title">{{ group.group }}</div>
          <div class="list">
            <div v-for="(city, index) in group.cities" :key="index">
              <div class="city-list">{{ city.cityName }}</div>
            </div>
          </div>
        </div>
      </template> -->
      
    </div>
  </div>
</template>

<script setup>
import { ref, computed, toRefs } from 'vue'
import { useRouter } from 'vue-router';
import { useStore } from 'vuex';

const searchValue = ref()
const router = useRouter()

// 1、取消事件
const onCancel = () => {
  router.back()
}

// 2、网络请求
const store = useStore()
store.dispatch('fetchAllCitiesData')
const { allCities } = toRefs(store.state)
console.log(allCities)

const tabActive = ref()
// 3、获取选中标签的值
const currentGroup = computed(() => allCities.value[tabActive.value])
console.log("currentGroup:", currentGroup)

// 从2、网络请求到这里，卡了整整两天，最后解决了，学到了很多
// debugger、watch、watchEfect
// 4、索引列表重映射
const indexList = computed(() => {
  if (currentGroup.value && currentGroup.value.cities && currentGroup.value.cities.length !== 0) {
    const list = currentGroup.value.cities.map(item => item.group)
    list.unshift("#")
    return list
  }else {
    return []
  }
})
// 5、监听城市的点击
const cityClick = (city) => {
  console.log(city)
  router.back()
  store.commit("setCurrentCity", city)
}

</script>

<style lang="less" scoped>
.searchIcon {
  --van-search-left-icon-color: var(--theme-color) !important;
}

.search-page {
  --van-tabs-line-height: 30px;

  .content {
    height: calc(100vh - 98px);
    overflow: auto;

    .hot-cities {
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;


      .city {
        width: 70px;
        height: 28px;
        border-radius: 15px;
        margin-top: 6px;
        background-color: #fff4ec;

        line-height: 28px;
        text-align: center;
      }
    }
  }

}
</style>
```

打开老师的代码提示

`'vite' 不是内部或外部命令，也不是可运行的程序`

需要`npm i`

## 9、首页日期选择

### 9.1、静态搭建日期

![image-20230316174233598](E:\coder\09_OneNote\image\image-20230316174233598.png)

`src/views/home/cpns/HomeSearchBox.vue`

```html
<template>
  <div class="section date-range">
    <div class="start-date">
      <div class="date">
        <span class="behavior">入住</span>
        <span class="time">8月25日</span>
      </div>
    </div>
    <div class="stay-day">共一晚</div>
    <div class="end-date">
      <div class="date">
        <span class="behavior">离店</span>
        <span class="time">8月26日</span>
      </div>
    </div>
  </div>
</template>
```

```css
<style lang="less" scoped>
.section {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 0 20px;
  color: #999;

  .start-date {
    flex: 1;
    display: flex;
    height: 44px;
    align-items: center;
  }

  .end-date {
    min-width: 30%;
    padding-left: 20px;

  }

  .date {
    display: flex;
    flex-direction: column;

    .behavior {
      font-size: 12px;
      color: #999;
    }

    .time {
      margin-top: 3px;
      color: #333;
      font-size: 15px;
      font-weight: 500;
    }
  }
}

.date-range {
  height: 44px;

  .stay-day {
    flex: 1;
    text-align: center;
    font-size: 12px;
    color: #666;
  }
}
</style>
```

### 9.2、动态日期数据

![image-20230316194937811](E:\coder\09_OneNote\image\image-20230316194937811.png)

#### 9.2.1、日期格式化工具使用

官方文档：https://day.js.org/zh-CN/

这是一个 `JavaScript` 函数，它使用“dayjs”库将给定日期格式化为“月日”格式（汉字中的月和日）。

要使用此功能，您首先需要通过在终端中运行以下命令在您的项目中安装“dayjs”库：

```js
npm install dayjs
```

或者

```
yarn add dayjs
```

接下来，在`JavaScript`文件中引入`dayjs`库，例如：

```
import dayjs from 'dayjs';
```

现在，你可以使用dayjs来处理日期。下面是一些常见的用法：

##### 创建dayjs实例

```js
// 创建当前时间的dayjs实例
const now = dayjs();
console.log(now); // 输出当前时间的dayjs实例
javascriptCopy code// 通过传递日期字符串来创建dayjs实例
const dateStr = '2023-03-16';
const date = dayjs(dateStr);
console.log(date); // 输出指定日期的dayjs实例
```

##### 格式化日期

```js
// 将dayjs实例格式化为字符串
const now = dayjs();
const formattedDate = now.format('YYYY-MM-DD HH:mm:ss');
console.log(formattedDate); // 输出格式化后的日期字符串，例如：2023-03-16 13:24:10
```

##### 操作日期

```js
// 增加一天
const now = dayjs();
const tomorrow = now.add(1, 'day');
console.log(tomorrow); // 输出明天的dayjs实例
javascriptCopy code// 减去一小时
const now = dayjs();
const oneHourAgo = now.subtract(1, 'hour');
console.log(oneHourAgo); // 输出一小时前的dayjs实例
```

##### 获取日期信息

```js
// 获取年份
const now = dayjs();
const year = now.year();
console.log(year); // 输出当前年份，例如：2023
javascriptCopy code// 获取月份
const now = dayjs();
const month = now.month() + 1; // 注意：月份从0开始计数，需要加1才是实际月份
console.log(month); // 输出当前月份，例如：3
```

##### 计算日期间隔

在Day.js中，您可以使用`diff()`方法来计算两个日期之间的差异，该方法返回一个数字表示两个日期之间的时间差。该数字表示不同时间单位的数量，例如天数、小时数、分钟数等。`diff()`方法的语法如下：

```js
dayjs().diff(dayjs(anotherDay), 'unit')
```

其中，`dayjs()`返回当前日期时间，`dayjs(anotherDay)`返回另一个日期时间，`'unit'`参数指定所需的时间单位，例如`'days'`表示天数，`'hours'`表示小时数，`'minutes'`表示分钟数，等等。

例如，如果您要计算2023年3月16日和2023年3月1日之间的天数差异，可以使用以下代码：

```js
const day1 = dayjs('2023-03-16')
const day2 = dayjs('2023-03-01')
const diffDays = day1.diff(day2, 'day')
console.log(diffDays)
```

这个示例中，我们使用Day.js创建了两个日期对象`day1`和`day2`，然后使用`diff()`方法计算它们之间的天数差异，并将结果存储在`diffDays`变量中。最后，我们将差异天数打印到控制台中。

这些只是dayjs的一些基本用法，还有很多其他功能可以使用，例如解析日期字符串、比较日期、获取日期差等等。

#### 额外知识：

> vue3中控制台显示的RefImpl 是啥意思？
>
> 在Vue 3中，`RefImpl`是一个内部类，用于实现`ref`的具体实现细节。`ref`是一个响应式API，用于创建一个可变的、能够被响应式地监听的引用类型值。当我们使用`ref`创建一个引用类型值时，Vue会使用`RefImpl`来对该值进行封装，以便在该值被修改时能够触发相应的更新。
>
> 虽然`RefImpl`在Vue 3的内部实现中被使用，但在我们平时的开发过程中，我们通常不需要直接使用它。我们只需要使用`ref`来创建一个响应式的引用类型值即可。如果我们想要获取到`ref`的具体实现细节，可以通过在控制台中输出一个`ref`对象来查看它的原型链，从而找到它所使用的内部类`RefImpl`。

#### 9.2.2、响应式动态日期创建

日期格式化工具引入：

1、安装

`npm install dayjs`

2、封装成一个工具函数

`src/utils/formatDate .js`

```js
import dayjs from "dayjs";
export function formatMothDay(date) {
  return dayjs(date).format("MM月DD日")
}
```

3、导入工具

```js
import { formatMothDay } from '@/utils/formatDate'
```

4、定义开始日期

```js
const nowDate = new Date()
const startDate = ref(formatMothDay(nowDate))
```

5、定义结束日期

```js
const afterDate = nowDate.setDate(nowDate.getDate() + 1)
const endDate = ref(formatMothDay(afterDate))
console.log(nowDate, endDate)
```

> 代码说明：
>
> 这段代码的作用是创建一个响应式的`endDate`变量，用于存储当前日期的下一天的日期，并将其格式化为指定的日期字符串格式。
>
> 具体来说，代码分为两行：
>
> 第一行代码通过`nowDate.setDate(nowDate.getDate() + 1)`获取当前日期对象`nowDate`的下一天日期，并将该日期的==毫秒数==存储在一个名为`afterDate`的常量中。
>
> 第二行代码使用`ref()`函数将`afterDate`格式化为指定的日期字符串格式，并将结果存储在一个名为`endDate`的响应式变量中。
>
> 在Vue 3中，使用`ref()`函数可以将一个普通的JavaScript对象或值转换为响应式的对象或值，使得当对象或值发生变化时，可以自动通知相关的组件进行重新渲染。
>
> 在这里，我们使用`ref()`函数将一个格式化后的日期字符串转换为响应式变量，以便在该日期发生变化时，相关的组件可以根据新的日期进行重新渲染。

#### 9.3.3、点击日期栏，弹出日历

去Vant库中寻找一个

```js
<van-calendar v-model:show="showCalendar" 
              type="range" 
              @confirm="onConfirm"
              color="var(--theme-color)" />
```

```js
const showCalendar = ref(false)
const onConfirm = (value) => {
  console.log(value)
  
  const selectStartDay = value[0]
  console.log(selectStartDay)
  
  const selectEndDay = value[1]
  console.log(selectEndDay)
  
  startDate.value = formatMothDay(selectStartDay)
  endDate.value = formatMothDay(selectEndDay)
  showCalendar.value = false
}
```

> 代码说明：
>
> 这段代码是Vue 3中的代码片段，它包括一个ref变量showCalendar和一个函数onConfirm。解释如下：
>
> 1. `const showCalendar = ref(false)` - 这行代码声明了一个名为`showCalendar`的响应式变量，并将其初始化为`false`。该变量用于控制日历组件的显示或隐藏。
> 2. `const onConfirm = (value) => { ... }` - 这行代码声明了一个名为`onConfirm`的函数，并定义了一个参数`value`。当用户确认选择日历中的日期时，此函数将被触发。该函数包括以下逻辑：
>
> - `console.log(value)` - 将用户选择的日期值打印到控制台中。
> - `const selectStartDay = value[0]` - 将用户选择的起始日期存储在一个名为`selectStartDay`的变量中。
> - `console.log(selectStartDay)` - 将`selectStartDay`的值打印到控制台中。
> - `const selectEndDay = value[1]` - 将用户选择的结束日期存储在一个名为`selectEndDay`的变量中。
> - `console.log(selectEndDay)` - 将`selectEndDay`的值打印到控制台中。
> - `startDate.value = formatMothDay(selectStartDay)` - 将格式化后的起始日期值存储在名为`startDate`的响应式变量中。`formatMothDay`是一个格式化日期的自定义函数。
> - `endDate.value = formatMothDay(selectEndDay)` - 将格式化后的结束日期值存储在名为`endDate`的响应式变量中。
> - `showCalendar.value = false` - 将`showCalendar`的值设置为`false`，隐藏日历组件。
>
> 总的来说，这段代码实现了一个选择日期范围的功能，并将选择的日期范围以及格式化后的起始日期和结束日期存储在相应的变量中。

#### 9.3.4、首页动态显示天数

如何计算间隔天数？

时间格式化工具添加时间差方法：

```js
export function getDiffDay(startDay, endDay) {
  return dayjs(endDay).diff(startDay, "day")
}
```

> 两个时间：
>
> - 首页默认天数
> - 首页选择天数

```html
<div class="stay-day">共 {{stayDays}} 晚</div>
```

首页默认天数计算：

```js
const nowDate = new Date()
const newDate = new Date()
newDate.setDate(nowDate.getDate() +1 )
const stayDays = ref(getDiffDay(nowDate,newDate))
```

首页天数选择计算：

```js
// 首页天数选择计算
stayDays.value = getDiffDay(selectStartDay,selectEndDay)
console.log(stayDays.value)
```

### 9.3、首页人数和关键字区域

![image-20230316210247402](E:\coder\09_OneNote\image\image-20230316210247402.png)



新建组件`src/views/home/cpns/HomeCountKey.vue`

公共CSS样式，添加底部横线~哪里需要添哪里~方便后期维护与管理

```css
:root {
  --theme-color: #ff9854;
}
body {
  font-size: 14px;
}

.bottom-gray-line {
  border-bottom: 1px solid #f8f8f8;
}
```

```html
<template>
  <div class="home-count-key ">
    <div class="message-select">
      <div class="price-count  bottom-gray-line">
        <div class="price">价格不限</div>
        <div class="count">人数不限</div>
      </div>
      <div class="keyword bottom-gray-line">关键字/位置/民宿名</div>
    </div>
  </div>
</template>

<script setup>

</script>

<style lang="less" scoped>
.message-select {
  padding: 0 20px;
  font-size: 12px;
  color: #999;

  .price-count {
    display: flex;
    justify-content: space-between;
    height: 44px;
    line-height: 44px;
  }

  .keyword {
    min-width: 30%;
    height: 44px;
    line-height: 44px;
  }
}
</style>
```

### 9.4、热门建议部分

![image-20230316214159648](E:\coder\09_OneNote\image\image-20230316214159648.png)

同样也是动态搭建，需要网络请求

**步骤如下：**

- 新建组件

- 发送网络请求
  - 尽量不要在小组件里面发送网络请求，之后找起来就不是很方便了，应该统一进行管理，这个地方就是页面的父组件`src/views/home/home.vue`
- 传数据
- 抽离
- 分层架构
- 展示

#### 9.4.1、基本步骤

`src/views/home/home.vue`

```js
import  dqRequest  from '@/service/request/index';
dqRequest.get({
  url: "/home/hotSuggests"
}).then(res => {
  console.log(res.data)
})
```

拿到数据后，赋值

注意`ref([])`和`ref({})`的区分，根据数据类型

```js
import { ref } from "vue"
import dqRequest from '@/service/request/index';
const hotSuggests = ref([])
dqRequest.get({
  url: "/home/hotSuggests"
}).then(res => {
  hotSuggests.value = res.data
  console.log(hotSuggests.value)
})
```

传递给子组件

```html
<home-suggests-cities :hot-suggests="hotSuggests"></home-suggests-cities>
```

子组件接收

```js
import { defineProps } from 'vue';
defineProps({
  hotSuggests: {
    type: Array,
    default:() => []
  }
})
```

子组件展示

 ```html
 <template v-for="(hotCities, index) in hotSuggests">
   <div class="city">{{ hotCities.tagText.text }}</div>
 </template>
 ```

调整样式

```css
.suggest {
  margin-left: 20px;

    .city {
      padding: 4px 8px;
      margin: 4px;
      border-radius: 10px;
      font-size: 12px;
      line-height: 1.2;
  }
}
```

> 这里的line-height设置为1.2，
>
> 原因在于我们导入的`normalize.css`有一个默认的1.15，意思是1.15*12 -12 = 1.8 ，上0.8，下1.0，
>
> 默认情况下，中文字体，会自动向上走一些，但是英文会下沉，是一种设计特点

![image-20230320153631213](E:\coder\09_OneNote\image\image-20230320153631213.png)

浏览数据，发现服务器有关于样式的数据，因此，可以把`style`变成动态的

 ```html
 <template v-for="(itemCity, index) in hotSuggests">
   <div class="city" 
        :style="{color:itemCity.tagText.color, background:itemCity.tagText.background.color}"
        >{{ itemCity.tagText.text }}</div>
 </template>
 ```

再次调整样式

```css
.suggest {
  margin: 10px 20px ;
  display: flex; 
  flex-wrap: wrap;
    .city {
      padding: 4px 8px;
      margin: 4px;
      border-radius: 14px;
      font-size: 12px;
  }
}
```

#### 9.4.2、分层架构

目前的做法是将网络请求放在了组件中，这个数据是页面里面去发送对应的一个网络请求，在页面里面通过一个变量hotsuggest拿到我们对应的一个数据，之后的话将对应的数据单独的传递给这里的这个组件，再对数据做一个展示

目前只有一个网络请求，所以你感觉没有什么东西。但是实际开发里面，这里的网络请求可能是很多的，如果放在store会更方便~

对于子组件，就可以直接去对应的`store`中直接去拿数据，不需要在自己的页面中做传递操作~

##### 9.4.2.1、抽取网络请求

`src/stores/modules/home.js`

```js
import { getHotSuggests } from "@/service"
export default {
  namespaced: true,
  state() {
    return {
      hotSuggests: []
    }
  },
  mutations:{
    setHotSuggests(state,data) {
      state.hotSuggests = data
    }
  },
  actions: {
    async fetHotSuggestData(context) {
      const res = await getHotSuggests()
      context.commit("setHotSuggests", res.data)
      console.log("热门建议网络请求", res.data)
    }
  }
}
```

`src/store/index.js`

```js
modules: {
  home
}
```

`src/views/home/home.vue`

```js
import { computed } from "vue"
// import dqRequest from '@/service/request/index';
// const hotSuggests = ref([])
// dqRequest.get({
//   url: "/home/hotSuggests"
// }).then(res => {
//   hotSuggests.value = res.data
//   console.log(hotSuggests.value)
// })
import { useStore } from 'vuex'
const homeStore = useStore()
const hotSuggests = computed(() =>homeStore.state.home.hotSuggests)
// console.log(hotSuggests)
homeStore.dispatch('home/fetHotSuggestData')
// console.log(hotSuggests)
```

> 项目的流程就是之前所做的那些，工作中大多情况也是这些，从服务器拿数据，之后进行展示，这些也是核心的东西~
>
> 对于数据管理方式的两种方案：
>
> 1、页面组件中
>
> 2、store中（会让逻辑更加清晰一些）

#### 9.4.2、搜索按钮

![image-20230320155055773](E:\coder\09_OneNote\image\image-20230320155055773.png)

```html
<div class="suggest-btn">
  <div class="btn">开始搜索</div>
</div>
```

```css
.suggest-btn {
  display: flex;
  padding: 0 20px;
  .btn {
    flex: 1;
    width: 342px;
    height: 38px;
    max-height: 50px;
    font-weight: 500px;
    font-size: 18px;
    border-radius: 25px;
    text-align: center;
    line-height: 38px;
    color: #fff;
    background-image:  linear-gradient(90deg,#fa8c1d,#fcaf3f);
  }
}
```

> 颜色的渐变是**图片**，也可以定义在全局css的变量中，

## 10、搜索页面搭建

### 10.1、路由配置

`src/route/index.js`

```js
{
  path:"/search-page",
  component: () => import('../views/search/search.vue'),
},
```

### 10.2、监听点击

`src/views/home/cpns/HomeSearchBox.vue`

```html
<div class="btn" @click="searchClick">开始搜索</div>
```

点击事件传递参数

```js
import { useRouter } from 'vue-router'
const route = useRouter()
const searchClick = function () {
  return route.push({
    path: "/search-page",
    query: {
      startDate: startDate.value,
      endDate:endDate.value
    }
  })
}
```

> 这里由于需要传递参数，因此，将之前抽离出去的组件又合并了在一起，
>
> 另一种方案就是将数据放在库里~
>
> 就是下面这些合并在了一个文件`src/views/home/cpns/HomeSearchBox.vue`

![image-20230320165056152](E:\coder\09_OneNote\image\image-20230320165056152.png)

### 10.3、搜索页面接收参数

```vue
<template>
  <h1>Search</h1>
  <h2>{{ $route.query.startDate }}</h2>
  <h2>{{ $route.query.endDate }}</h2>
  <h2>{{ $store.state.currentClickCity }}</h2>
</template>

<script setup>
import {useStore} from 'vuex'
const store = useStore()
console.log(store.state.currentClickCity)
</script>
```

## 11、首页图标分类

### 11.1、状态管理

`src/stores/modules/home.js`

```js
import { getHotSuggests, getCategories } from "@/service"
export default {
  namespaced: true,
  state() {
    return {
      hotSuggests: [],
      categories: []
    }
  },
  mutations:{
    setHotSuggests(state,data) {
      state.hotSuggests = data
    },
    setCategories(state, data) {
      state.categories = data
    }
  },
  actions: {
    async fetchHotSuggestData(context) {
      const res = await getHotSuggests()
      context.commit("setHotSuggests", res.data)
      // console.log("热门建议网络请求", res.data)
    },
    async fetchCategories(context) {
      const res = await getCategories() 
      context.commit("setCategories", res.data)

    }
  }
}
```

### 11.2、网络请求

`src/views/home/home.js`

```js
homeStore.dispatch('home/fetchCategories')
```

解构库：

```js
const categories = computed(() => homeStore.state.home.categories)
```

向子组件传递数据

```html
<home-categories :home-categories="categories"></home-categories>
```

### 11.3、新建组件

`src/views/home/cpns/HomeCategories.vue`



```vue
<template>
  <div class="categories">
    <template v-for="(item, index) in homeCategories" :key="item.id">
      <div class="item">
        <img :src="item.pictureUrl" alt="">
        <div>{{item.title}}</div>
      </div>
    </template>
  </div>
</template>

<script setup>
import {defineProps} from "vue"
const props = defineProps({
  homeCategories:{
    type: Array,
    default:() => []
  }
}) 
</script>

<style lang="less" scoped>
.categories {
  display: flex;
  overflow-x: auto;
  height: 80px;
  padding: 0 10px;
  .item {
    flex-shrink: 0;
    display:flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width:70px;
    img {
      width: 32px;
      height: 32px;
    }
  }
}
</style>
```

==关于如何隐藏滚动条==

对于Chrome和Safari浏览器，我们必须使用CSS滚动条选择器，然后使用display：none隐藏它：

```css
::-webkit-scrollbar {
  display: none; /* Chrome Safari */
}
```

https://zxuqian.cn/css-how-to-hide-scrollbars/

## 12、首页的内容模块封装

![image-20230320180012856](E:\coder\09_OneNote\image\image-20230320180012856.png)

### 12.1、首页的房间列表分页数据请求

### 12.3、初步功能

先做第一件事情：点击按钮后，就展示不同页面数据

`src/views/home/home.vue`

```javascript
const currentPage = computed(() => homeStore.state.home.currentPage)
const moreBtnClick = () =>{
  console.log(currentPage.value)
  console.log("jiazaigengduo")
  homeStore.dispatch('home/fetchHouselist',currentPage.value)
}
```

`src/service/modules/home.js`

```javascript
export function getHouselist(currentPage) {
  return DQRequest.get({
    url: "/home/houselist",
    params: {
      page:currentPage,
    }
  })
```

`src/stores/modules/home.js`

```javascript
import { getHotSuggests, getCategories, getHouselist } from "@/service"
export default {
  namespaced: true,
  state() {
    return {
      houselist: [],
      currentPage: 1
    }
  },
  mutations:{
    setHouselist(state, data) {
      state.houselist.push(...data)
    },
    setCurrentPage(state, data) {
      state.currentPage++
    }
  },
  actions: {
    async fetchHouselist(context, currentPage) {
      const res = await getHouselist(currentPage)
      context.commit("setHouselist",res.data)
      context.commit("setCurrentPage",currentPage)
      // console.log(res)
    }
  }
}
```

> 要解决三个问题：
>
> 1、将新的20条数据进行添加进来，而不是替换，因此要用**push**
>
> 2、使用展开运算符，将数据展开
>
> 3、抽取到状态管理库
>
> 关于分页数据传递参数问题，不能像以前一样写死，而要动态传递参数，根据参数进行请求

在这段代码中，`push` 方法和展开运算符 `...` 用于将从服务器获取的新数据追加到现有的数据数组中。

具体来说，`setHouselist` 函数中的 `state.houselist` 属性是一个数组，用于存储房屋列表数据。

当调用 `fetchHouselist` 函数从服务器获取新数据时，这些数据需要追加到 `state.houselist` 数组中。这可以通过调用 `push` 方法实现。

但是，如果仅仅调用 `push` 方法并传入从服务器获取的新数据数组，会将整个数组作为`一个元素`追加到现有数组中，而不是将新数组的所有元素`逐个追加`到现有数组中。为了解决这个问题，可以使用展开运算符 `...` 将新数据数组中的所有元素展开，以便能够将其逐个追加到现有数组中，如下所示：

```js
state.houselist.push(...data)
```

这样做的效果等同于以下代码：

```js
for (let i = 0; i < data.length; i++) {
  state.houselist.push(data[i])
}
```

但是使用展开运算符可以让代码更简洁和易读。

`currentPage` 参数用于指定获取的房屋列表数据的页码，它的类型应该是数字类型。

在 `fetchHouselist` 函数中，`currentPage` 参数是通过函数调用时传递进来的。在这个例子中，`currentPage` 参数被传递给了 `getHouselist` 函数，用于从服务器获取对应页码的房屋列表数据。然后，`getHouselist` 函数返回一个包含房屋列表数据的 Promise 对象，`res.data` 表示获取到的数据。

在 `fetchHouselist` 函数中，`currentPage` 参数还被用于更新当前页码的状态，这个操作是通过调用 `setCurrentPage` mutation 来实现的。在这个例子中，`setCurrentPage` mutation 只是将 `state.currentPage` 属性的值加 1，用于记录下一次需要获取的页码。

综上所述，`currentPage` 参数没有问题，它在这个例子中被用于从服务器获取对应页码的数据，并更新当前页码的状态。

### 12.3、数据展示

![image-20230320221856879](E:\coder\09_OneNote\image\image-20230320221856879.png)

`src/views/home/cnps/HomeContent.vue`

```vue
<template>
  <div class="content">
    <div class="title">热门精选</div>
    <div class="list">
      <template v-for="(item, index ) in houselist" :key="item.data.houseId">
        <h3 v-if="item.discoveryContentType === 3" class="type-3">
          type-3:{{ item.data.houseName }}
        </h3>
        <h3 v-else-if="item.discoveryContentType === 9" class="type-9">
          type-9:{{ item.data.houseName }}
        </h3>
      </template>
    </div>

  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useStore } from 'vuex'
const houseStore = useStore()
const houselist = computed(() => houseStore.state.home.houselist)
console.log(houselist)
</script>
```

### 12.4、封装不同组件

#### 12.4.1、hous-item-v9

![image-20230321145506733](E:\coder\09_OneNote\image\image-20230321145506733.png)

`src/components/houseItemV9/hous-item-v9.vue`

```vue
<template>
  <div class="house-item-v9">
    <div class="item-inner">
      <div class="cover">
        <img :src="itemData.image.url" alt="">
      </div>
      <div class="infos">
        <div class="summary">{{ itemData.summaryText }}</div>
        <div class="name">{{ itemData.houseName }}</div>
        <div class="score-price">
          <van-rate :model-value="commentScore" readonly allow-half color="#fff" size="15px"/>
          <div class="price">￥{{ itemData.finalPrice }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, computed } from "vue"
const props = defineProps({
  itemData: {
    type: Object,
    default: () => {}
  }
})

const commentScore = computed(() => {
  return Number(props.itemData.commentScore)
})
</script>
<style lang="less" scoped>
.house-item-v9 {
  width: 50%;
  .item-inner {
    position:relative;
    margin: 5px;
    background-color: #fff;
    border-radius: 6px;
    overflow: hidden;
    .cover {
      img {
        width:100%;
      }
    }
    .infos {
      position: absolute;
      bottom: 0px;
      padding: 8px 10px;
      color: #fff;
      .summary {
        font-size: 12px;
      }
      .name {
        margin: 5px 0;
        text-overflow: ellipsis;
        overflow: hidden;
        display: -webkit-box;
        -webkit-line-clamp:2;
        -webkit-box-orient: vertical;
      }
      .score-price {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top: 10px;
      }
    }
  }
}
```

==关键点1==

包裹一个`inner`

```html
  <div class="house-item-v9">
    <div class="item-inner">···
    </div>
  </div>
```

==关键点2==

**`-webkit-line-clamp`** CSS 属性可以把[块容器](https://developer.mozilla.org/zh-CN/docs/Glossary/Block)中的内容限制为指定的行数。

它只有在 [`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 属性设置成 `-webkit-box` 或者 `-webkit-inline-box` 并且 [`box-orient`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-orient) 属性设置成 `vertical`时才有效果。

在大部分情况下，也需要设置 [`overflow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow) 属性为 `hidden`，否则，里面的内容不会被裁减，并且在内容显示为指定行数后还会显示省略号。

当应用于锚（anchor）元素时，截断可以发生在文本中间，而不必在末尾。

```css
.name {
  margin: 5px 0;
  text-overflow: ellipsis;
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp:2;
  -webkit-box-orient: vertical;
}
```

==关键点3==

圆角设置，同时使用

```css
border-radius: 12px;
overflow: hidden;
```

==关键点4==

服务器的==评分数据==是字符串类型，需要转换数据类型

两种方式：

1、直接转换

```vue
<van-rate :model-value="Number(props.itemData.commentScore)" readonly allow-half color="#fff" size="15px"/>
```

2、变量

```javascript
const commentScore = computed(() => {
  return Number(props.itemData.commentScore)
})
```

==关键点5==

`:model-value`

```vue
<van-rate :model-value="commentScore" readonly allow-half color="#fff" size="15px"/>
```

==关键6==

模板中使用数据，可以直接使用`{{ itemData.houseName }}`

`javascript`中需要定义变量`props`

```js
import { defineProps, computed } from "vue"
const props = defineProps({
  itemData: {
    type: Object,
    default: () => {}
  }
})

const commentScore = computed(() => {
  return Number(props.itemData.commentScore)
})
```

#### 12.4.2、hous-item-v3

![image-20230321172319414](E:\coder\09_OneNote\image\image-20230321172319414.png)

`src/components/houseItemV3/hous-item-v3.vue`

```vue
<template>
  <div class="house-item-v3">
    <div class="item-inner">
      <div class="cover">
        <img :src="itemData.image.url" alt="">
      </div>
      <div class="infos">
        <div class="position">
          <img src="@/assets/img/home/location.png" alt="">
          <div class="location">{{ itemData.location }}</div>
        </div>
        <div class="name">{{ itemData?.houseName }}</div>
        <div class="summary">{{ itemData?.summaryText }}</div>
        <div class="price">
          <div class="new">￥{{ itemData?.finalPrice }}</div>
          <div class="old">{{ itemData?.productPrice }}</div>
          <!-- 减少subtract -->
          <div :style="{ 
               backgroundImage: `linear-gradient(${270}deg, ${startColor}, #${endColor})` 
               }"
               class="sub">
               {{ itemData?.priceTipBadge?.text }}
          </div>
        </div>
      </div>

    </div>
  </div>
</template>
  
<script setup>
import { defineProps, ref } from "vue"
const props = defineProps({
  itemData: {
    type: Object,
    default: () => { }
  }
})

const startColor = props.itemData?.priceTipBadge?.gradient?.startColor
const endColor = props.itemData?.priceTipBadge?.gradient?.endColor
</script>
<style lang="less" scoped>
.house-item-v3 {
  width: 50%;
  margin-bottom: 10px;

  .item-inner {
    position: relative;
    margin: 5px;
    background-color: #fff;
    overflow: hidden;
    border-radius: 6px;

    .cover {
      img {
        width: 100%;
      }
    }

    .infos {
      padding: 8px 10px;
    }
    .position {
      display: flex;
      justify-self: center;
      align-items: center;
      img {
        width: 12px;
        height: 12px;
      }
    }

    .name {
      margin: 5px 0;
      text-overflow: ellipsis;
      overflow: hidden;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
    }
    .summary {
      font-size:12px;
    }
    .price {
      display: flex;
      // justify-content: space-between;
      align-items: flex-start;
      margin:5px 0;
      .new {
        font-size: 16px;
        color: var(--theme-color);

      }

      .old {
        font-size: 14px;
        color: #999;
        text-decoration:line-through;
        margin: 0 6px;

      }
      .sub {
        padding: 0px 6px;
        border-radius: 12px;
        color: #fff;
      }
    }
  }

}
</style>
```

==关键点一==

动态绑定`style`

```js
const startColor = props.itemData.priceTipBadge.gradient.startColor
const endColor = props.itemData.priceTipBadge.gradient.endColor
```

```html
<div :style="{ 
     backgroundImage: `linear-gradient(${270}deg, ${startColor}, #${endColor})` 
     }"
     class="sub">
     {{ itemData.priceTipBadge.text }}
</div>
```

==关键点二==

```css
align-items: flex-start;
```
==关键点三==

ES6语法中，从`undefined`中取值时会报错，最新的vue支持添加`?`

对于存在很多数据嵌套的结构，获取数据时，会经常遇见这种问题

#### 12.4.3、调整视图布局

![image-20230321172302189](E:\coder\09_OneNote\image\image-20230321172302189.png)

`src/views/home/cnps/HomeContent.vue`

```vue
<template>
  <div class="content">
    <div class="title">热门精选</div>
    <div class="list">
      <template v-for="(item, index ) in houselist" :key="index">
        <house-item-v9 :item-data="item.data" v-if="item.discoveryContentType === 9">
        </house-item-v9>
        <house-item-v3 :item-data="item.data" v-else-if="item.discoveryContentType === 3">
        </house-item-v3>
      </template>
    </div>

  </div>
</template>

<script setup>
import { computed } from 'vue'
import HouseItemV9 from '@/components/houseItemV9/houseItemV9.vue'
import HouseItemV3 from '@/components/houseItemV3/houseItemV3.vue'
import { useStore } from 'vuex'
const houseStore = useStore()
const houselist = computed(() => houseStore.state.home.houselist)
</script>
<style lang="less" scoped>
.content {
  padding: 10px 8px;
  .title {
    font-size: 18px;
    padding: 5px;
    font-weight: 500;
  }
  .list {
      display: flex;
      flex-wrap: wrap;
    }
}
</style>
```

### 12.5、监听页面滚动到底部

![metric-all](E:\coder\09_OneNote\image\metric-all.png)

> **页面为什么会滚动？区分清楚两种情况：**
>
> 1、window窗口
>
> 2、元素：overflow-y：auto

**思路：**

1、监听window窗口的滚动，当页面到达了底部时

==scrollTop + clientHeight >= scrollHeight==

`src/views/home/home.vue`

```js
// 监听页面到达了底部
window.addEventListener("scroll", () =>{
  const scrollTop = document.documentElement.scrollTop
  const scrollHeight = document.documentElement.scrollHeight
  const clientHeight = document.documentElement.clientHeight
  console.log(scrollTop, scrollHeight, clientHeight)
  if(scrollTop + clientHeight >= scrollHeight) {
    console.log("到达了底部")
  }
}
```

### 12.6、监听滚动的Hooks函数的抽取

两点：

1、当我们离开页面时，移除监听

2、如果其他页面也想进行类似的监听，需要封装到工具函数中

`src/hooks/useScroll.js`

```js
import { onMounted, onUnmounted} from "vue"
export default function useScroll(callback) {
  const scrollListenerHandler = () => {
    const scrollTop = document.documentElement.scrollTop
    const scrollHeight = document.documentElement.scrollHeight
    const clientHeight = document.documentElement.clientHeight
    console.log(scrollTop, scrollHeight, clientHeight)
    if (scrollTop + clientHeight >= scrollHeight) {
      // homeStore.dispatch('home/fetchHouselist', currentPage.value)
      callback()
      console.log("滚动到了底部")
    }
  }
  // 挂载
  onMounted(() => {
    window.addEventListener("scroll", scrollListenerHandler)
  })
  // 移除
  onUnmounted(() => {
    window.removeEventListener("scroll", scrollListenerHandler)
  })
}
```

> 定义了一个名为`useScroll`的函数，用来监听页面滚动事件。该函数接受一个回调函数`callback`作为参数，用来指定滚动到底部时需要执行的操作。
>
> 在函数内部，我们首先定义了一个名为`scrollListenerHandler`的函数，用来处理滚动事件。在该函数中，我们获取了页面的滚动高度`scrollTop`、文档的总高度`scrollHeight`以及浏览器窗口的可视高度`clientHeight`。
>
> 如果`scrollTop + clientHeight >= scrollHeight`，则表示页面已经滚动到了底部。此时，我们执行回调函数`callback`，即调用传递进来的操作。同时，我们也打印出“滚动到了底部”的信息。
>
> 在`onMounted`和`onUnmounted`生命周期钩子中，我们分别调用`window.addEventListener`和`window.removeEventListener`函数来注册和取消滚动事件的监听器。这样可以确保在组件挂载和卸载时都能正确监听和取消滚动事件，避免内存泄漏和性能问题。
>
> 总之，这段代码是用来封装一个通用的页面滚动事件监听器，并且可以根据需要执行自定义操作的。
>
> 建议在封装代码中增加对滚动事件的节流处理，避免频繁触发滚动事件导致性能问题。

**调用：**

`src/views/home/home.vue`

```js
import useScroll from '@/hooks/useScroll.js'

useScroll(() => {
  homeStore.dispatch('home/fetchHouselist', currentPage.value)
})
```

等同于

```js
const loadMoreData = () => {
  homeStore.dispatch('home/fetchHouselist', currentPage.value)
}

useScroll(loadMoreData)
```

> 定义一个`loadMoreData`函数作为回调函数传入`useScroll`函数中，当滚动到页面底部时，`loadMoreData`函数会被调用，执行异步加载数据的操作

### 12.7、节流、防抖

为了避免滚动事件过于频繁地触发回调函数而影响页面性能，可以考虑对滚动事件进行节流处理。可以使用`lodash`等工具库提供的`throttle`函数来实现节流。`throttle`函数的作用是在指定时间内只执行一次函数。

首先，需要安装`lodash`工具库。可以使用以下命令安装：

```
npm install lodash
```

然后，在`useScroll`函数中使用`throttle`函数对`scrollListenerHandler`函数进行节流处理。代码如下：

`src/hooks/useScroll.js`

```js
import { onMounted, onUnmounted} from "vue"
import { throttle } from 'lodash'

export default function useScroll(callback) {
  const scrollListenerHandler = throttle(() => {
    const scrollTop = document.documentElement.scrollTop
    const scrollHeight = document.documentElement.scrollHeight
    const clientHeight = document.documentElement.clientHeight
    console.log(scrollTop, scrollHeight, clientHeight)
    if (scrollTop + clientHeight >= scrollHeight) {
      // homeStore.dispatch('home/fetchHouselist', currentPage.value)
      callback()
      console.log("滚动到了底部")
    }
  }, 1000) // 1秒钟内最多执行一次回调函数

  onMounted(() => {
    window.addEventListener("scroll", scrollListenerHandler)
  })
  onUnmounted(() => {
    window.removeEventListener("scroll", scrollListenerHandler)
  })
}
```

> 在上述代码中，我们通过`throttle`函数对`scrollListenerHandler`函数进行节流处理，使得滚动事件每`1秒钟`最多触发`一次`回调函数。这样可以有效降低滚动事件的触发频率，提高页面性能。

**节流和防抖的区别**

节流和防抖都是用来限制事件处理频率的技术，但是它们的实现方式有所不同。

节流（throttling）是指限制事件的处理频率，使得每隔一定时间间隔只执行一次事件处理函数。例如，当用户不断滚动页面时，使用节流可以确保页面滚动事件处理函数每隔一定时间执行一次，而不是每次滚动都执行一次。

防抖（debouncing）是指在事件被触发后，等待一定时间间隔，如果在这个时间间隔内没有再次触发事件，则执行事件处理函数。例如，当用户不断输入搜索关键字时，使用防抖可以确保只在用户停止输入一段时间后才执行搜索函数，而不是每次输入都执行一次搜索。

### 12.8、 方案优化

> **通过变量**
>
> 抽取hook的好处，在任何地方都可以调用，思想慢慢体会，Vue2没有这种方法，必须使用混入mixins，放入data中，虽然更难了，但是好处是大大的
>
> 不要纠结于你为什么想不到，做得少，但是你学会之后，在react中也是这种思想
>
> 那为什么不直接使用react？如果想更加灵活的话，在react中会更加更加的灵活，所以，这个问题也是社区一直讨论的。可能也会有一大部分人转手使用react。
>
> vue有优势也优劣势
>
> 不要只知道api的使用，做一个opations API工程师，关键的点要掌握函数式编程的灵魂，这样才能学到精髓

如何优化，做到不传入回调，假如说以后还有别的事件，就需要传另外的回调，相对来说是不好管理的

`src/hooks/useScroll.js`

```js
import { onMounted, onUnmounted, ref } from "vue"
import { throttle } from 'lodash'
export default function useScroll() {
  // 创建一个名为 isReachBottom 的响应式数据，初始值为 false
  const isReachBottom = ref(false)
  // 创建一个防抖/节流的事件监听器，用于检测是否滚动到页面底部
  const scrollListenerHandler = throttle(() => {
    // 获取页面滚动条距离顶部的距离、整个页面的高度、以及浏览器窗口的高度
    const scrollTop = document.documentElement.scrollTop
    const scrollHeight = document.documentElement.scrollHeight
    const clientHeight = document.documentElement.clientHeight
    console.log(scrollTop, scrollHeight, clientHeight)

    // 如果滚动到了页面底部，就把 isReachBottom 的值设置为 true
    if (scrollTop + clientHeight >= scrollHeight) {
      console.log("滚动到了底部")
      isReachBottom.value = true
    }
  }, 100)
  // 在组件挂载时注册事件监听器
  onMounted(() => {
    window.addEventListener("scroll", scrollListenerHandler)
  })
  // 在组件卸载时取消事件监听器
  onUnmounted(() => {
    window.removeEventListener("scroll", scrollListenerHandler)
  })
  // 返回 isReachBottom 的值，以便在组件中使用
  return { isReachBottom }
}
```

> 这段代码定义了一个名为`useScroll`的自定义Vue Composition API函数，它返回一个对象，包含一个名为`isReachBottom`的响应式变量。`isReachBottom`变量用于检测是否滚动到页面底部。
>
> `useScroll`函数使用`ref`创建了一个名为`isReachBottom`的响应式变量，并将其初始化为`false`。然后使用`throttle`函数创建了一个名为`scrollListenerHandler`的函数，这个函数将在滚动事件被触发时被调用。当滚动到页面底部时，将`isReachBottom`变量的值设置为`true`。
>
> `onMounted`和`onUnmounted`钩子分别在组件`挂载`和`卸载`时添加和移除了一个滚动监听器。监听器函数是`scrollListenerHandler`。
>
> `return { isReachBottom }`将一个对象返回，包含了`isReachBottom`属性，这个属性在组件中可以被使用。
>
> 在Vue 3中，一个组合函数可以返回一个包含多个响应式数据和方法的对象。因此，使用对象字面量语法（用花括号包含）来包含一个或多个响应式数据是一个常见的做法。在这个例子中，`useScroll`函数返回一个包含单个响应式数据`isReachBottom`的对象，因此需要使用对象字面量来返回它。如果在函数中返回多个响应式数据，则需要使用逗号分隔它们，并在最后一个响应式数据后面添加一个对象字面量，例如`return { data1, data2, ..., dataN, methods: {...} }`。

**调用：**

`src/views/home/home.vue`

```javascript
import useScroll from '@/hooks/useScroll'

const { isReachBottom } = useScroll()
watch (isReachBottom, (newValue, oldValue) => {
  console.log(newValue,oldValue)
  if(newValue) {
    homeStore.dispatch('home/fetchHouselist', currentPage.value).then(() => {
      isReachBottom.value = false
    })
  }
})
```

> 由于 `useScroll` 函数返回的是一个对象，因此需要使用花括号来解构。
>
> `const { isReachBottom } = useScroll()`是从`useScroll`函数返回的对象中提取`isReachBottom`属性的一种语法糖。它等价于`const isReachBottom = useScroll().isReachBottom`。
>
> `watch`函数用于监听`isReachBottom`变量的变化，并在`isReachBottom`变为`true`时，调用`homeStore.dispatch('home/fetchHouselist', currentPage.value)`方法。
>
> `homeStore`是一个Vuex Store对象，`fetchHouselist`是一个异步action。该异步action用于获取当前页面的房屋列表，并将`isReachBottom`变量重置为`false`，以便下次检测。
>
> 使用`then`方法是因为`homeStore.dispatch`方法返回的是一个Promise对象，而`then`方法用于在异步操作执行成功后执行回调函数，将`isReachBottom`的值重置为`false`，以便下次滚动到页面底部进行判断~

 `const { isReachBottom } = useScroll()` 和 `return { isReachBottom }` 的作用？

在 `useScroll` 函数中，我们通过使用 `ref` 函数来创建一个响应式属性 `isReachBottom`。然后，我们将 `isReachBottom` 属性作为对象的一个属性返回。因此，在使用 `useScroll` 函数后，我们需要解构返回的对象，以获取 `isReachBottom` 属性的值。

例如，如果我们写下以下代码：

```js
const result = useScroll()
console.log(result) // 输出 { isReachBottom: ref(false) }
```

然后，我们可以通过以下方式获取 `isReachBottom` 的值：

```js
const isReachBottom = result.isReachBottom
console.log(isReachBottom.value) // 输出 false
```

为了避免这种繁琐的过程，我们可以使用解构赋值来直接获取 `isReachBottom` 属性的值：

```js
const { isReachBottom } = useScroll()
console.log(isReachBottom.value) // 输出 false
```

## 13、监听页面滚动显示搜索工具栏

### 13.1、抽取滚动数据

**那我们怎么知道滚动到哪个位置？**

封装的`useScroll`中有这个数据

`src/hooks/useScroll.js`

```js
import { onMounted, onUnmounted, ref } from "vue"
import { throttle } from 'lodash'
export default function useScroll() {
  const isReachBottom = ref(false)
  
  const scrollTop = ref(0)
  const scrollHeight = ref(0)
  const clientHeight = ref(0)
  
  const scrollListenerHandler = throttle(() => {
    scrollTop.value = document.documentElement.scrollTop
    scrollHeight.value = document.documentElement.scrollHeight
    clientHeight.value = document.documentElement.clientHeight
    // console.log(scrollTop, scrollHeight, clientHeight)
    if (scrollTop.value + clientHeight.value >= scrollHeight.value) {
      console.log("滚动到了底部")
      isReachBottom.value = true
    }
  }, 100)
  onMounted(() => {
    window.addEventListener("scroll", scrollListenerHandler)
  })
  onUnmounted(() => {
    window.removeEventListener("scroll", scrollListenerHandler)
  })

  return { isReachBottom, scrollTop, scrollHeight, clientHeight  }
}
```

==注意：==

```js
const scrollTop = ref(0)
const scrollHeight = ref(0)
const clientHeight = ref(0)
  
scrollTop.value
scrollHeight.value
clientHeight.value
```

> 1、定义完响应式数据后，要加上`value`
>
> 2、返回的对象，没有顺序要求，但是`react`中返回的是数组，有顺序要求
>
> 3、抽取的好处，可以获取返回值，别的地方也可以使用

### 13.2、监听滚动

`src/views/home/home.vue`

```html
<div v-show="isShowSearch" class="search-box">我是搜索内容</div>
```

**方案一：**`watch`

==错题==

```js
// 滚动到一定位置，显示搜索
const isShowSearch = ref(false)
watch(scrollTop, (newValue, oldValue) => {
  // console.log(newValue, oldValue)
  if(newValue >= 350) {
    // console.log("daowei")
    isShowSearch.value = true
  }
})
```

> 使用了 `watch` 函数来监听 `scrollTop` 变量的变化。每次 `scrollTop` 的值发生改变时，都会调用回调函数并传入新值和旧值。在回调函数中，判断新值是否大于等于 300。如果等于大于等于，将 `isShowSearch` 的值设置为 `true`。
>
> ==但是==每次滚动时都设置 `isShowSearch.value` 的值为 `true`，即使它的值已经为 `true`。
>
> 这意味着在用户滚动时，`isShowSearch.value` 可能会不断地被设置为 `true`，导致不必要的性能开销和可能的错误行为。

```js
const isShowSearch = ref(false)
watch(scrollTop, (newValue, oldValue) => {
    isShowSearch.value = newValue >= 350
})
```

> 通过检查 `newValue` 是否大于等于 300 来控制何时设置 `isShowSearch.value` 的值为 `true`。如果 `newValue` 小于 300，则 `isShowSearch.value` 会保持为 `false`。这种方法可以避免不必要的性能开销和可能的错误行为，因为它只在 `newValue` 发生实际变化时才会更改 `isShowSearch.value` 的值。
>
> `isShowSearch.value = newValue >= 300`
>
> 这句代码的含义是，将 `isShowSearch.value` 的值设置为一个布尔值，该布尔值取决于 `newValue` 是否大于等于 300。如果 `newValue` 大于等于 300，则将 `isShowSearch.value` 的值设置为 `true`；否则，将 `isShowSearch.value` 的值设置为 `false`。
>
> 因为 `isShowSearch` 是一个 `ref` 对象，因此使用 `.value` 属性来访问和设置其值。这个代码行利用了 JavaScript 中布尔值可以转换为数字的特性，如果 `newValue` 大于等于 300，将返回 `true`，该值会被隐式转换为数字 `1`；如果 `newValue` 小于 300，则返回 `false`，该值会被隐式转换为数字 `0`。因此，这一行代码将 `isShowSearch.value` 的值设置为 `0` 或 `1`，表示搜索框是否应该显示。

**方案二：**`computed`

```js
const isShowSearch = computed(() => {
  return scrollTop.value >= 350
})
```

> 使用了 `computed` 函数来创建一个响应式的 `isShowSearch` 变量。这个变量会根据 `scrollTop` 的值是否大于等于 300 来自动更新。如果 `scrollTop` 大于等于 300，那么 `isShowSearch` 会变成 `true`，否则为 `false`。

**两者如何选择？**

两种代码块的区别在于它们实现同样的功能的方式不同。而第一个代码块则使用了 `watch` 函数来手动监听变量的变化，并在变量满足特定条件时更新另一个变量的值。第二个代码块使用了 `computed` 函数来创建一个自动更新的响应式变量，

如果需要手动监听一个变量的变化，并在满足特定条件时执行一些操作，那么可以使用 `watch` 函数。

如果需要实现一个响应式变量，其值是根据其他变量的值自动更新的，那么可以使用 `computed` 函数。

> 当一个可响应数据（例如响应式变量）的值是根据其他可响应数据的值计算而来时，我们可以使用 `computed` 函数来创建一个响应式的计算属性。这个计算属性会自动==依赖其他响应式数据的变化==，并在需要时自动重新计算自己的值。
>
> 而当我们只需要监听某个可响应数据的变化，并在其变化时==执行一些逻辑==时，我们可以使用 `watch` 函数来手动监听这个可响应数据的变化。在监听到变化时，`watch` 函数会执行我们指定的回调函数，并传入变化前后的值。
>
> 需要注意的是，这只是一般情况下的使用建议。在某些情况下，可能会存在一些例外，例如某个==计算属性的计算逻辑比较复杂==，导致计算时间较长，此时可能需要使用 `watch` 函数手动监听依赖数据的变化，并在变化后手动调用计算属性的计算方法。

### 13.3、搜索工具栏的封装和静态展示

关于命名规范：

https://v2.cn.vuejs.org/v2/style-guide/index.html#%E8%A7%84%E5%88%99%E5%BD%92%E7%B1%BB

![image-20230322174102943](E:\coder\09_OneNote\image\image-20230322174102943.png)

`src/views/home/home.vue`

```vue
<div v-show="isShowSearch" class="search-box">
  <search-bar></search-bar>
</div>

<script setup>
import SearchBar from '@/components/searchBar/SearchBar.vue'
</script>

<style lang="less" scoped>
.search-box {
  position: fixed;
  height: 45px;
  top: 0;
  left: 0;
  right: 0;
  z-index: 9;
  background-color: #fff;
  padding: 16px 16px 10px;
}
</style>
```

`src/components/searchBar/SearchBar.vue`

```vue
<template>
  <div class="search-bar">
    <div class="select-time">
      <div class="time start">
        <div class="name">住</div>
        <div class="date">07.25</div>
      </div>
      <div class="time end">
        <div class="name">离</div>
        <div class="date">07.26</div>
      </div>
    </div>
    <div class="content">
      <div class="keyword">关键字/位置/民宿</div>
    </div>
    <div class="right">
      <i class="icon-search"></i>
    </div>
  </div>
</template>

<script>

</script>

<style lang="less" scoped>
.search-bar {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 0 14px;

  font-size: 14px;
  color: #999;
  border-radius: 6px;
  background-color: #f2f4f6;
.select-time {
  display:flex;
  flex-direction: column;
  
  .time {
    display: flex;
    flex-direction: row;
    align-items: center;
    line-height: normal;
    font-size: 10px;
    .date {
      color: #333;
      margin: 0px 10px 0 3px
    }
  }
}
.content {
  flex: 1;
  padding: 0 6px;
  text-align: left;
  border-left: 1px solod #fff;
}
.right {
  display: flex;
  align-items: center;
}
.icon-search {
  width: 24px;
  height: 24px;
  display: inline-block;
  background-image: url(@/assets/img/home/home-sprite.png);
  background-position: -29px -151px;
  background-size: 207px 192px;
}
}
</style>
```

### 13.4、时间数据抽取store

将之前的`startDate`、`endDate`抽取到单独的`main.js`中，这俩数据在很多地方都会使用到~

`src/stores/modules/main.js`

```js
const startDate = new Date()
const endDate = new Date()
endDate.setDate(startDate.getDate() + 1 )
export default {
  namespaced:true,
  state(){
    return {
      startDate: startDate,
      endDate: endDate
    }
  }
}
```

`src/views/home/cpns/HomeSearchBox.vue`

```js
import { formatMothDay, getDiffDays } from '@/utils/formatDate'
const mainStore = useStore()
const { startDate, endDate } = toRefs(mainStore.state.main)

const startDateStr = computed(() => formatMothDay(startDate.value))
const endDateStr = computed(() => formatMothDay(endDate.value))

const stayDays = ref(getDiffDays(startDate.value, endDate.value))
const showCalendar = ref(false)
const onConfirm = (value) => {
  
  const selectStartDay = value[0]
  const selectEndDay = value[1]
  
  
  mainStore.state.main.startDate = formatMothDay(selectStartDay)
  mainStore.state.main.endtDate = formatMothDay(selectEndDay)
  
  showCalendar.value = false

  // 首页天数计算
  stayDays.value = getDiffDays(selectStartDay, selectEndDay)
}
```

==额外补充：==

关于`toRefs`、`computed`

```js
const { hotSuggests, categories, currentPage } = toRefs(homeStore.state.home)
```

```js
const hotSuggests = computed(() => homeStore.state.home.hotSuggests)
const categories = computed(() => homeStore.state.home.categories)
const currentage = computed(() => homeStore.state.home.currentPage)
```

> 这两种写法都是用于解构 `homeStore.state.home` 对象中的属性，并将其赋值给变量。区别在于：
>
> 1. 第一种写法使用了 `toRefs` 函数，将解构出来的属性转换为 `ref` 对象。这意味着变量的值会自动响应式地更新，当 `homeStore.state.home` 对象中对应的属性发生变化时，变量的值也会相应地更新。因此，如果你希望变量的值在组件中自动更新，可以使用这种写法。
>
> 2. 第二种写法使用了 `computed` 函数，将解构出来的属性封装成了一个计算属性。这样，当依赖该计算属性的其他属性发生变化时，计算属性也会重新计算。如果你希望在获取属性值时进行一些计算操作，可以使用这种写法。
>
>    这两种写法在获取属性值方面都是等价的，只是在响应式更新和计算方面有所不同。
>
> ❗❗❗一定不要忘记`.value`

### 13.4、搜索工具栏动态数据

![image-20230322195139568](E:\coder\09_OneNote\image\image-20230322195139568.png)

`src/components/searchBar/SearchBar.vue`

```js
import {useStore} from "vuex"
import { formatMothDay} from '@/utils/formatDate'
import {toRefs, computed} from 'vue' 

const mainStore = useStore()
const { startDate, endDate } = toRefs(mainStore.state.main)

const startDateStr = computed(() => formatMothDay(startDate.value))
const endDateStr = computed(() => formatMothDay(endDate.value))
```

### 13.5、动态时间格式

将时间格式化工具进行优化，可以传入格式进行不同的展示

`src/utils/formatDate.js`

```js
import dayjs from "dayjs";
export function formatMothDay(date, format = "MM月DD日") {
  return dayjs(date).format(format)
}

export function getDiffDays(startDay, endDay) {
  return dayjs(endDay).diff(startDay, "day")
}
```

> 将函数传入两个参数：“date”和“format”，前者是要格式化的日期，后者是指定所需格式的字符串。
>
> 默认格式为“MM月DD日”，即函数返回格式为“月月日”的字符串。例如，如果输入日期为“2023-03-22”，则此函数的默认格式输出为“03 月 22 日”。

`src/components/searchBar/SearchBar.vue`

![image-20230322195730943](E:\coder\09_OneNote\image\image-20230322195730943.png)

```js
import {useStore} from "vuex"
import { formatMothDay} from '@/utils/formatDate'
import {toRefs, computed} from 'vue' 

const mainStore = useStore()
const { startDate, endDate } = toRefs(mainStore.state.main)

const startDateStr = computed(() => formatMothDay(startDate.value， "MM.DD"))
const endDateStr = computed(() => formatMothDay(endDate.value, "MM.DD"))
```

# 五、加载动画组件

## 1、组件展示

![image-20230322225956457](E:\coder\09_OneNote\image\image-20230322225956457.png)

==思路：==

- 加载动画，这个东西是不属于任何页面

- 控制显示的变量需要放在库`main.js`中管理

- 将这个东西做出来显示在页面中，之后再对这个页面进行控制，

- 发送网络请求显示，请求完消失

  

  `src/store/modules/main.js`

```js
isShowAnimate: false
```
**使用这种方式，同样要掌握：**

```html
<div class="loading-animate" v-show="$store.state.main.isShowAnimate">
```

`src/components/LoadingAnimate/LoadingAnimate.vue`

```vue
<template>
  <div class="loading-animate">
  <div class="loading-animate" v-show="$store.state.main.isShowAnimate">
      <img src="@/assets/img/home/full-screen-loading.gif" alt="">
    </div>
  </div>
</template>

<script>
</script>

<style lang="less" scoped>
.loading-animate {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;

  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, .2);

  .loading-bgc {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 104px;
    height: 104px;
    background: url(@/assets/img/home/loading-bg.png) 0 0 / 100% 100%;

    img {
      width: 70px;
      height: 70px;
      margin-bottom: 8px;
      // background-image: url(@/assets/img/home/loading-bg.png);

    }
  }
}
</style>
```

> `z-index`只对定位元素有效

## 2、网络请求中控制`isShowAnimate`

`src/servics/request/index.js`

```js
import axios from 'axios'
import { BASE_URL, TIMEOUT } from './config'
// 导入store
import useMainStore from '@/stores/index'

class DQRequest {
  constructor(baseURL, timeout = 10000) {
    this.instance = axios.create({
      baseURL,
      timeout
    })
  }

  request(config) {
    // 显示加载动画
    useMainStore.state.main.isShowAnimate= true
    return new Promise((resolve, reject) => {
      this.instance.request(config).then(res => {
        resolve(res.data)
        // 隐藏加载动画
        useMainStore.state.main.isShowAnimate= false
      }).catch(err => {
        reject(err)
      })
    })
  }

  get(config) {
    return this.request({ ...config, method: "get" })
  }

  post(config) {
    return this.request({ ...config, method: "post" })
  }
}

export default new DQRequest(BASE_URL, TIMEOUT)
```

放在网络请求內部不是特别清晰，因此可以放在拦截器里面

```js
import axios from 'axios'
import { BASE_URL, TIMEOUT } from './config'
import useMainStore from '@/stores/index'
class DQRequest {
  constructor(baseURL, timeout = 10000) {
    this.instance = axios.create({
      baseURL,
      timeout
    })

    this.instance.interceptors.request.use((config) => {
      useMainStore.state.main.isShowAnimate= true
      return config
    }, err => {
      return err
    })

    this.instance.interceptors.response.use((res) => {
      useMainStore.state.main.isShowAnimate= false
      return res
    }, err => {
      useMainStore.state.main.isShowAnimate= false
      return err
    } )
  }

  request(config) {
    return new Promise((resolve, reject) => {
      this.instance.request(config).then(res => {
        resolve(res.data)
      }).catch(err => {
        reject(err)
      })
    })
  }

  get(config) {
    return this.request({ ...config, method: "get" })
  }

  post(config) {
    return this.request({ ...config, method: "post" })
  }
}

export default new DQRequest(BASE_URL, TIMEOUT)
```

# 六、详情页

## 1、点击跳转详情页

- 跳转到详情页

- 携带对应的参数id

### 1.1、监听item的点击

**是否能直接绑定到组件上**❓❓❓

> **取决于场景**
>
> 为什么说取决于场景？
>
> 其实是绑定到了组件内部的根元素上，如果有多个根，就不知道加在了那里，会有警报，
>
> 如果**没有多个根**，就直接绑定就可以了
>
> 这个知识点还是比较有用的，记一下，有时候会方便一些

`src/views/home/cpns/HomeContent.vue`

```vue
<div class="list">
  <template v-for="(item, index ) in houselist" :key="index">
    <house-item-v9 @click="itemClick(item)" :item-data="item.data" v-if="item.discoveryContentType === 9">
    </house-item-v9>
    <house-item-v3 @click="itemClick(item)" :item-data="item.data" v-else-if="item.discoveryContentType === 3">
    </house-item-v3>
  </template>
</div>
```

### 1.2、跳转到详情页

通过`params`传送数据

#### 1.2.1、路由设置：

```js
{
  path:"/detail/:id",
  component: () => import('@/views/detail/detail.vue')
},
```

#### 1.2.2、传输数据

`src/views/home/cpns/HomeContent.vue`

```js
const itemClick = (item) => {
  route.push("/detail/" + item.data.houseId)
}
```

#### 1.2.3、接受数据

`src/views/detail/detail.vue`

```vue
<template>
  <div class="detail-page top-page">
    <h1>houseId:{{ $route.params.id }}</h1>
  </div>
</template>

<script setup>
import { useRoute } from "vue-router"
const route = useRoute()
console.log(route.params.id)
</script>

<style scoped></style>
```

> `top-page`公共页面样式置顶

## 2、导航栏的搭建和主题色修改

```vue
<template>
  <div class="detail-page top-page">
    <van-nav-bar title="房屋详情" left-text="返回" left-arrow @click-left="onClickLeft" />
    <h1>houseId:{{ $route.params.id }}</h1>
  </div>
</template>

<script setup>
import { useRoute, useRouter } from "vue-router"
const route = useRoute()
const router = useRouter()
const onClickLeft = () => {
  router.back()
}
</script>
```

> ==route==和==router==有什么区别？
>
> `useRoute`和`useRouter`都是Vue Router提供的hook函数。
>
> `useRoute`返回当前路由信息的对象，包括路由的路径、参数、查询参数等。
>
> `useRouter`返回路由实例，可以用它来导航到其他路由或获取路由信息。
>
> 在你的代码中，`route`是通过`useRoute`获取到的当前路由信息对象，而`router`是通过`useRouter`获取到的Vue Router实例。
>
> 当你想要在代码中访问当前路由信息时，可以使用`useRoute`来获取；当你想要在代码中进行路由导航或获取路由信息时，可以使用`useRouter`来获取Vue Router实例。

`common.css`全局修改颜色，直接修改变量

`src/assets/css/common.css`

```css
--van-primary-color:var(--theme-color) !important;
```

## 3、获取数据

### 3.1、网络请求组件

`src/service/modules/detail.js`

```js
import DQRequest from '../request/index'
export function getDetailInfos(houseId) {
  return DQRequest.get({
    url: "/detail/infos",
    params: {
      houseId,
    }
  })
}
```

> 代码导入了一个名为 DQRequest 的模块，这个模块是对 axios 进行了一些封装，使得发送 HTTP 请求更加方便。该模块被导入后，通过 `getDetailInfos` 函数暴露出来。`getDetailInfos` 函数接受一个 `houseId` 参数，用于指定要获取详细信息的房屋的 ID。
>
> 在函数中，它使用 `DQRequest` 模块的 `get` 方法来发送 HTTP GET 请求。请求的 URL 是 "/detail/infos"，即获取房屋详细信息的接口。请求的参数是一个对象，包含一个 `houseId` 属性，它的值是传入的 `houseId` 参数。

### 3.2、统一导出

`src/service/index.js`

```js
export * from "./modules/detail"
```

### 3.3、页面请求数据

`src/views/detail/detail.js`

```js
const houseId = route.params.id

const detailInfos = ref({})

getDetailInfos(houseId).then((res) => {
  detailInfos.value = res.data
})
```

在页面发送网络请求，需要一个变量用来保存数据

> 定义了一个名为 `houseId` 的变量，它的值是从路由参数中获取的房屋 ID。接着，代码使用 Vue.js 提供的 `ref` 函数定义了一个名为 `detailInfos` 的响应式变量，它用于保存获取到的房屋详细信息。
>
> 最后，代码调用了 `getDetailInfos` 函数来获取房屋详细信息，并在返回结果后将获取到的信息保存在 `detailInfos` 变量中。值得注意的是，`detailInfos` 是一个响应式变量，当它的值发生改变时，相关的组件会自动更新。

### 3.4、拆解数据

![image-20230323190224419](E:\coder\09_OneNote\image\image-20230323190224419.png)

页面拆解数据，这样就不用再模板中，写一大堆的`mainPart`了，用起来会方便很多 

```js
// 网络请求
const houseId = route.params.id
const detailInfos = ref({})
// 拆解mainPart
const mainPart = computed(() => detailInfos.value.mainPart)
getDetailInfos(houseId).then((res) => {
  detailInfos.value = res.data
})
```

`ref({})`中在网络请求成功之前是没有值的，`undefined`会报错

两种解决方案：

```vue
<detail-banner :swipe-data="mainPart?.topModules?.housePicture?.housePics"></detail-banner>
```

方案二

```html
<div v-if="mainPart" class="main">
  <detail-banner :swipe-data="mainPart.topModules.housePicture.housePics"></detail-banner>
</div>
```


## 4、详解页轮播图

公司一般不会手写轮播图，只接拿就好

发送数据

```vue
<detail-banner :swipe-data="mainPart?.housePicture?.housePics"></detail-banner>
```

接收数据时，需要看数据类型

```js
defineProps({
  swipeData: {
    type: Array,
    default: () => []
  }
})
```

### 4.1、初步效果

![image-20230325163759989](E:\coder\09_OneNote\image\image-20230325163759989.png)

```html
<template>
  <div class="swipe">
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <template v-for="(item, index) in swipeData">
        <van-swipe-item>
          <img :src="item.url" alt="">
        </van-swipe-item>
      </template>
      <template #indicator="{ active, total }">
        <div class="indicator">{{ active + 1 }}/{{ total }}</div>
      </template>
    </van-swipe>
  </div>
</template>
```

文档的写法相当于做了一个解构

`#indicator="{ active, total }"`--->`{{ active + 1 }}/{{ total }}`

### 4.2、数据处理

需要做到如下效果，因此需要对数据进行处理~

#### 方案一：将数据处理成对象

```js
const swipeGroup = {}
for (const item of props.swipeData) {
  swipeGroup[item.enumPictureCategory] = []
}
for (const item of props.swipeData) {
  const valueArray = swipeGroup[item.enumPictureCategory]
  valueArray.push(item)
}
```

> 这段代码的作用是将 `props.swipeData` 数组中的每个元素按照 `enumPictureCategory` 属性的值进行分组，并将分组后的结果存储在 `swipeGroup` 对象中。
>
> 首先，代码创建一个空对象 `swipeGroup` 作为分组后的结果容器。
>
> 接下来，代码使用 for-of 循环遍历 `props.swipeData` 数组中的每个元素，每个元素被存储在 `item` 变量中。在这个循环中，代码使用 `item.enumPictureCategory` 属性的值作为键，向 `swipeGroup` 对象中添加一个空数组，用于存储同一类别的元素。
>
> 第二个 for-of 循环也是遍历 `props.swipeData` 数组中的每个元素。然而，此时代码将 `swipeGroup` 对象中的值数组取出，并将当前元素 `item` 添加到该数组中，以此将所有属于同一类别的元素都添加到该类别对应的数组中。
>
> 最终，`swipeGroup` 对象中的每个键都对应一个值数组，该数组中包含了所有属于该类别的元素。

#### 方案二：数组操作

```js
for (const item of props.swipeData) {
  let valueArray = swipeGroup[item.enumPictureCategory]
  if (!valueArray) {
    valueArray = []
    swipeGroup[item.enumPictureCategory] = valueArray
  }
  valueArray.push(item)
}
```

> 使用了一个 for-of 循环遍历 `props.swipeData` 数组中的每个元素，每个元素被存储在 `item` 变量中。
>
> 接下来，代码使用 `item.enumPictureCategory` 属性的值作为键，从 `swipeGroup` 对象中获取相应的值数组 `valueArray`。如果 `valueArray` 不存在，则创建一个空数组并将其赋值给 `valueArray`，然后将其存储在 `swipeGroup` 对象中，以便后续访问。
>
> 最后，代码将 `item` 对象添加到 `valueArray` 数组中。
>
> 该代码段的作用是将 `props.swipeData` 数组中的每个元素按照 `enumPictureCategory` 属性的值进行分组，并将分组后的结果存储在 `swipeGroup` 对象中。

### 4.3、展示数据

![image-20230325173345023](E:\coder\09_OneNote\image\image-20230325173345023.png)

#### 4.3.1、去除冒号、去除中括号

```js
const getName = (name) => {
  return name.replace("：", "").replace("【", "").replace("】", "")
}
```

#### 4.3.2、正则表达式

```js
const nameReg = /【（.*?）】/i
const getName = (name) => {
  const results = nameReg.exec(name)
  return results[1]
}
```

展示`:class="{active:true}"`

```html
<template #indicator="{ active, total }">
  <div class="indicator">
    <template v-for="(value, key, index) in swipeGroup" :key="key">
      <div class="item" :class="{active:true}">{{ getName(value[0].title) }}</div>
    </template>
  </div>
</template>
```

### 4.4、如何知道图片显示的是那一组？

![image-20230325174210191](E:\coder\09_OneNote\image\image-20230325174210191.png)

展示`:class="{active:swipeData[active].enumPictureCategory == key}"`

```html
<template #indicator="{ active, total }">
  <div class="indicator">
    <template v-for="(value, key, index) in swipeGroup" :key="key">
      <div class="item" :class="{active:swipeData[active].enumPictureCategory == key}">{{ getName(value[0].title) }}</div>
    </template>
  </div>
</template>
```

> 这里不能写`===`，因为数据是一个数字类型，而对象里的key是字符串类型，需要写成`==`，会进行默认转换

### 4.5、显示索引

![image-20230325180102575](E:\coder\09_OneNote\image\image-20230325180102575.png)

```js
const getCategoryIndex = (item) => {
  const valueArray = swipeGroup[item.enumPictureCategory]
  return valueArray.findIndex(data => data === item) + 1
}
```

> 这段代码定义了一个名为 `getCategoryIndex` 的函数，该函数接受一个参数 `item`。该函数执行以下步骤：
>
> 1. 从 `swipeGroup` 中获取名为 `item.enumPictureCategory` 的属性的值，并将其赋值给 `valueArray`。`swipeGroup` 可能是一个对象，其中包含了多个属性和值，`item.enumPictureCategory` 可能是其中一个属性的名称。
> 2. 在 `valueArray` 数组中查找第一个与 `item` 相等的元素，并返回它的下标（从 0 开始计数），并将其加 1。
> 3. 将步骤 2 中查找到的下标返回作为函数的结果。
>
> 可以看出，该函数的作用是根据 `item` 对象中的 `enumPictureCategory` 属性值在 `swipeGroup` 中找到对应的数组，并返回 `item` 在该数组中的下标（从 1 开始计数）。
>
> 需要注意的是，如果在 `valueArray` 中找不到与 `item` 相等的元素，则返回 -1。

```vue
<template #indicator="{ active, total }">
  <div class="indicator">
    <template v-for="(value, key, index) in swipeGroup" :key="key">
      <div class="item" :class="{ active: swipeData[active]?.enumPictureCategory == key }">
        <span>
          {{ getName(value[0].title) }}
        </span>
        <span class="count" v-if="swipeData[active]?.enumPictureCategory == key">
          {{ getCategoryIndex(swipeData[active]) }} / {{ value.length }}
        </span>
      </div>
    </template>
  </div>
</template>
```

> 这一部分相对来说较为复杂，最难的部分就是刚刚的数据处理部分，但是只需要记住就好~接下来就是对数据进行展示！
>
> 这段代码是一个 Vue.js 模板语法，用于渲染一个轮播图指示器。具体来说，这里使用了 Vue.js 中的“具名插槽”（named slot）功能，用于传递指示器相关的参数。
>
> 下面是代码的详细解释：
>
> 1. `<template #indicator="{ active, total }">`：这是一个 Vue.js 具名插槽，名称为 `indicator`。它使用了 Vue.js 3.0 的语法，可以通过 `#` 符号指定插槽名称，并使用花括号 `{}` 来指定插槽的参数。在这里，插槽接受两个参数 `active` 和 `total`，分别表示当前轮播图的激活项和总项数。
> 2. `<div class="indicator">`：这是一个 HTML `div` 元素，用于包裹轮播图指示器的所有内容。
> 3. `<template v-for="(value, key, index) in swipeGroup" :key="key">`：这是一个 Vue.js 列表渲染指令，用于遍历 `swipeGroup` 对象的所有属性。在每次循环中，变量 `key` 表示当前属性的名称，`value` 表示当前属性的值，`index` 表示当前属性的索引。
> 4. `<div class="item" :class="{ active: swipeData[active]?.enumPictureCategory == key }">`：这是一个 HTML `div` 元素，表示指示器的一个项。它使用了 Vue.js 的计算属性语法 `:class="{ active: ... }"` 来动态设置 CSS 类名，根据当前轮播图的激活项和当前项的 `enumPictureCategory` 属性值是否相等来确定是否激活。
> 5. `<span>{{ getName(value[0].title) }}</span>`：这是一个 HTML `span` 元素，用于显示当前项的标题。它使用了一个名为 `getName` 的函数来获取标题的显示文本。
> 6. `<span class="count" v-if="swipeData[active]?.enumPictureCategory == key">{{ getCategoryIndex(swipeData[active]) }} / {{ value.length }}</span>`：这是一个 HTML `span` 元素，用于显示当前项在当前轮播图中的序号。它使用了一个名为 `getCategoryIndex` 的函数来获取当前项在当前分类中的序号，并将其与该分类的总项数一起显示。
>
> 综上所述，该代码是一个用于渲染轮播图指示器的 Vue.js 模板语法，它根据传入的参数和轮播图数据来动态渲染指示器的各个项，以便用户了解当前轮播图的内容和状态。

## 5、详情页房屋信息展示

由于结构相似，因此做一个组件，根据不同内容展示不同数据

组件文件起名时可以加数字，这样可以保证，文件的排序和页面展示顺序一样，但是导入组件时可以自定名字~

```js
import DetailsSwipe from detail_01-swipe
```

### 5.1、搭建结构

![image-20230325213032682](E:\coder\09_OneNote\image\image-20230325213032682.png)

```vue
<template>
  <div class="infos">
    <div class="name">
      {{ infosData.houseName }}
    </div>
    <div class="tags">
      <template v-for="(item, index) in infosData.houseTags" :key="index">
        <span 
         class="text" 
         v-if="item.tagText"
         :style="{color:item.tagText.color,background:item.tagText.background.color}"
        >
         {{ item.tagText.text }}
        </span>
      </template>
    </div>
    <div class="comment extra">
      <div class="left">
        <span class="overall"> {{ infosData.commentBrief.overall }}</span>
        <span class="score-title"> {{ infosData.commentBrief.scoreTitle }}</span>
        <span class="comment-brief"> {{ infosData.commentBrief.commentBrief }}</span>
      </div>
      <div class="right">
        <span class="total-count"> {{ infosData.commentBrief.totalCount }}条评论
        <van-icon name="arrow" />
        </span>
      </div>
    </div>
    <div class="position extra">
      <div class="location">
        <span>{{ infosData.nearByPosition.address }}</span>
      </div>
      <div class="right">
        地图 周边
        <van-icon name="arrow" />
      </div>
    </div>
  </div>
</template>
```

> 这里`infoData`没有使用`?`的原因在于父组件已经通过`v-if`判断过了，也就相当于传递过来的值不用添加判断了

### 5.2、调整样式

```css
<style lang="less" scoped>
.infos {
  padding: 16px;

  .name {
    font-size: 20px;
    font-weight: 700;
    color: #333;
    text-align: justify;
    line-height: 24px;
    overflow: hidden;
    margin-bottom: 6px;
  }

  .tags {
    margin: 10px 0;

    .text {
      font-size: 12px;
      padding: 1px 3px;
      margin: 0 2px;
    }
  }

  .extra {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 12px;
    margin: 12px 0;
    border-radius: 5px;
    background-color: #f5f7fa;

    .right {
      color: var(--theme-color);
    }
  }

  .comment {
    .overall {
      font-size: 18px;
      color: #333;
      font-weight: 700;
    }

    .score-title {
      font-weight: 700;
      margin: 0 3px;
      color: #333;
    }

    .comment-brief {
      color: #666;
    }
  }

  .position {
    .location {
      font-weight: 700;
      font-size: 14px;
      color: #333;
    }
  }
}</style>
```

> 最终回归到的，还是html和css，前面的数据，逻辑之类的，也是回归到最后的样式调整
>

## 6、组件-插槽制作

![image-20230325214225809](E:\coder\09_OneNote\image\image-20230325214225809.png)

由于结构相似，因此做一个组件，根据不同内容展示不同数据

组件文件起名时可以加数字，这样可以保证，文件的排序和页面展示顺序一样，但是导入组件时可以自定名字~

```js
import DetailsSwipe from detail_01-swipe
```

![image-20230325222240275](E:\coder\09_OneNote\image\image-20230325222240275.png)

`src/components/detail-section/detail-section.vue`

```vue
<template>
  <div class="section">
    <div class="header">
      <div class="title">{{ title }}</div>
    </div>
    <div class="content">
      <slot>插槽默认值</slot>
    </div>
    <div class="footer">
      <div class="more">{{ moreInfos }}</div>
      <van-icon name="arrow" />
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: {
    type: String,
    default: "default-title"
  },
  moreInfos: {
    type: String,
    default: "look~"
  },
})
</script>

<style lang="less" scoped>
.section {
  padding: 0 15px;
  margin-top: 12px;

  .header {
    height: 50px;
    line-height: 50px;
    border-bottom: 1px solid #eee;

    .title {
      font-size: 20px;
      color: #333;
      font-weight: 700;
    }
  }

  .content {
    padding: 8px 0;
  }

  .footer {
    display: flex;
    justify-content: flex-end;
    align-items: center;

    height: 44px;
    color: var(--theme-color);
    font-size: 14px;
    font-weight: 600;
  }
}</style>
```

## 7、房屋设施

![image-20230325234425778](E:\coder\09_OneNote\image\image-20230325234425778.png)

`src/views/detail/detail_03-facility.vue`

```vue
<template>
  <div class="facility">
    <detail-section title="房屋设施" more-infos="查看全部">
      <div class="facility-inner">
        <template v-for="(item, index) in facilityData.houseFacilitys" :key="index">
          <div class="item" v-if="facilityData.facilitySort?.includes(index)">
            <div class="head">
              <img :src="item.icon" alt="">
              <div class="text">{{ item.groupName }}</div>
            </div>
            <div class="list">
              <template v-for="(itemA, indexA) in item.facilitys.slice(0, 4)" :key="indexA">
                <div class="item-a">
                  <i class="item-a-icon"></i>
                  <span>{{ itemA.name }}</span>
                </div>
              </template>
            </div>
          </div>
        </template>
      </div>
    </detail-section>
  </div>
</template>

<script setup>
import DetailSection from "@/components/detail-section/detail-section.vue"
defineProps({
  facilityData: {
    type: Object,
    default: () => { }
  }
})
</script>

<style lang="less" scoped>
.facility-inner {
  padding: 5px 0;
  border-radius: 6px;
  font-size: 12px;
  background-color: #f7f9fb;

  .item {
    display: flex;
    margin: 25px 0;

    .head {
      text-align: center;
      width: 90px;
      .text {
        margin-top: 5px;
      }

      img {
        width: 20px;
        height: 20px;
      }
    }

    .list {
      flex: 1;
      display: flex;
      flex-wrap: wrap;
      align-items: center;

      .item-a {
        display: flex;
        
        align-items: center;
        box-sizing: border-box;
        width: 50%;
        margin: 4px 0;

        .item-a-icon {
          display: inline-block;
          margin: 0 3px;
          width: 12px;
          height: 12px;
          background: url(@/assets/img/detail/icon_check.png) 0 0 / 100% 100%;
        }
      }
    }
  }
}
</style>
```

## 8、房东介绍

> 封装完组件做这些东西就会比较的简单了，
>
> 后面的有些东西不想做也没有关系，都是html、css的样式的东西，确保**自己掌握了**就可以不用做了
>
> 做核心的逻辑东西就好，如果想练习那么也可以做一下

![image-20230326180241287](E:\coder\09_OneNote\image\image-20230326180241287.png)

`src/views/detail/cpns/detail_04-landlore.vue`

```vue
<template>
  <div class="landlord">
    <detail-section title="房东介绍" more-infos="查看房东主页">
      <div class="landlord-inner">
        <div class="top">
          <img :src="landloreData.topScroll" alt="">
        </div>
        <div class="header">
          <div class="left">
            <div class="logo">
              <img :src="landloreData.hotelLogo" alt="">
            </div>
            <div class="infos">
              <div class="name">{{ landloreData.hotelName }}</div>
              <div class="tags">
                <template v-for="(item, index) in landloreData.hotelTags" :key="index">
                  <div class="item">
                    <div class="text">{{ item.tagText.text }}</div>
                    <div v-if="index !== landloreData.hotelTags.length - 1" class="divider">|</div>
                  </div>
                </template>
              </div>
            </div>
          </div>
          <div class="right">
            <div class="content">联系房东</div>
          </div>
        </div>
        <div class="bottom">
          <template v-for="(item, index) in landloreData.hotelSummary ">
            <div class="title">{{ item.title }}</div>
            <div class="intro">{{ item.introduction }}</div>
            <div class="tip">{{ item.tip }}</div>
          </template>
        </div>
      </div>
    </detail-section>
  </div>
</template>
```

==注意==插入`|`

`<div v-if="index !== landloreData.hotelTags.length - 1" class="divider">|</div>`

调整样式

```css
```

## 9、热门评论

![image-20230331163810363](E:\coder\09_OneNote\image\image-20230331163810363.png)

## 10、预定须知

![image-20230331163824341](E:\coder\09_OneNote\image\image-20230331163824341.png)

## 11、百度地图的集成和使用过程

![image-20230327000221683](E:\coder\09_OneNote\image\image-20230327000221683.png)

> 地图模块遇到会比较少，但是有可能~
>
> map在编程语言中叫做映射，

不能直接再`setup`中使用，这个东西是介于`create`和`created`之间的，对应的元素还没有被挂载

需要在`onMounted`中使用

其他的也可以自行设置，很简单，相当于直接调用~想研究更多东西可以去看官方API文档就好了

`index.html`

```html
<script type="text/javascript" src="https://api.map.baidu.com/getscript?v=3.0&type=webgl&ak=你的AK"></script>

```

`src/views/cpns/detail/detail_07-map.vue`

```vue
<template>
  <div class="map">
    <detail-section title="位置周边" moreInfos="查看更多周边信息">
      <div class="baidu-map" ref="mapRef"></div>
    </detail-section>
  </div>
</template>

<script setup>
import detailSection from '@/components/detail-section/detail-section.vue';
import { onMounted, ref } from 'vue';
const mapRef = ref()
onMounted(() => {
  var map = new BMapGL.Map(mapRef.value);          // 创建地图实例 
  var point = new BMapGL.Point(props.positionModule.longitude, props.positionModule.latitude);  // 创建点坐标 
  map.centerAndZoom(point, 15);                 // 初始化地图，设置中心点坐标和地图级别
  map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
  var marker = new BMapGL.Marker(point);        // 创建标注   
  map.addOverlay(marker);                     // 将标注添加到地图中
})

const props = defineProps({
  positionModule: {
    type: Object,
    default: () => { }
  }
})
</script>

<style scoped>
.baidu-map {
  height: 300px;
}
</style>
```

## 12、价格说明

![image-20230326233228261](E:\coder\09_OneNote\image\image-20230326233228261.png)

`src/views/detail/cpns/detail_08-intro.vue`

```vue
<template>
  <div class="introduction">
    <detail-section :title="introductionData.title">
      <div class="content">
        {{ introductionData.introduction }}
      </div>
    </detail-section>
  </div>
</template>

<script setup>
import DetailSection from '@/components/detail-section/detail-section.vue'
defineProps({
  introductionData: {
    type: Object,
    default: () => { }
  }
})
</script>

<style lang="less" scoped>
.introduction {
  .content {
    color: #333;
    font-size: 14px;
    font-weight: 300;
    line-height: 22px;
  }
}
</style>
```

## 13、底部

![image-20230327000157342](E:\coder\09_OneNote\image\image-20230327000157342.png)

## 14、TabControl的展示和监听滚动过程

![image-20230327000318352](E:\coder\09_OneNote\image\image-20230327000318352.png)

> 拖到某一个位置展示这个东西，并且点击后定位到具体位置
>
> **思路：**
>
> 1、开发出来一个tabcontrol
>
> 2、监听滚动，滚动到一定位罟，显示出来
>
> 3、监听tabcontrol点击，点击之后滚动到正确的位置
>
> **两种方式**
>
> 1、vant
>
> 2、自己封装过~（用自己的），用自己的会更好控制

目前使用封装的`useScroll`函数不能正确监听到滚动的原因，是因为我们封装的`useScroll`是监听的`window`，而这个页面是块级元素`<div>`内部的滚动，因此需要优化之前封装的`useScroll`。

想监听元素的滚动，是需要传递参数的~

这样既可以监听元素，同时也可以监听`window`

`src/components/detail-section/detail-section.js`

```js
import { onMounted, onUnmounted, ref } from "vue" // 导入 Vue3 的相关 API
import { throttle } from 'lodash' // 导入 Lodash 库中的节流函数 throttle

export default function useScroll(elRef) { // 定义一个名为 useScroll 的组合式函数，接收一个名为 elRef 的参数
  let el = window // 初始化一个变量 el，表示被监听滚动事件的元素，默认为 window
  const isReachBottom = ref(false) // 初始化一个 ref 类型的变量 isReachBottom，表示当前页面是否已滚动到底部，默认为 false

  const scrollTop = ref(0) // 初始化一个 ref 类型的变量 scrollTop，表示当前滚动条的垂直位置，默认为 0
  const scrollHeight = ref(0) // 初始化一个 ref 类型的变量 scrollHeight，表示当前元素的滚动高度，默认为 0
  const clientHeight = ref(0) // 初始化一个 ref 类型的变量 clientHeight，表示当前元素的可视高度，默认为 0

  const scrollListenerHandler = throttle(() => { // 初始化一个函数 scrollListenerHandler，用 Lodash 的 throttle 方法将其节流，即每 100ms 执行一次
    if (el === window) { // 判断被监听的元素是否为 window
      scrollTop.value = document.documentElement.scrollTop // 如果是，则将 scrollTop 的值设置为当前文档垂直滚动位置
      scrollHeight.value = document.documentElement.scrollHeight // 将 scrollHeight 的值设置为文档总高度
      clientHeight.value = document.documentElement.clientHeight // 将 clientHeight 的值设置为窗口可视高度
    } else {
      scrollTop.value = el.scrollTop // 如果不是，则将 scrollTop 的值设置为当前元素的垂直滚动位置
      scrollHeight.value = el.scrollHeight // 将 scrollHeight 的值设置为当前元素的总高度
      clientHeight.value = el.clientHeight // 将 clientHeight 的值设置为当前元素的可视高度
    }
    if (scrollTop.value + clientHeight.value >= scrollHeight.value) { // 判断是否滚动到底部
      console.log("滚动到了底部")
      isReachBottom.value = true // 如果滚动到底部，则将 isReachBottom 的值设置为 true
    }
  }, 100)
  onMounted(() => { // 当组件挂载时执行
    if (elRef) { // 如果传入了 elRef 参数，则将 el 的值设置为 elRef 所引用的元素
      el = elRef.value
    }
    el.addEventListener("scroll", scrollListenerHandler) // 为 el 添加滚动事件监听器，当滚动时执行 scrollListenerHandler 函数
  })
  onUnmounted(() => { // 当组件卸载时执行
    el.removeEventListener("scroll", scrollListenerHandler) // 移除滚动事件监听器
  })

  return { isReachBottom, scrollTop, scrollHeight, clientHeight } // 返回一个对象，包含当前页面是否已滚动到底部、滚动条的垂

```

`src/views/detail/cpns/detail.vue`

```js
// html
<div class="detail-page top-page" ref="tabRef">

// script
import useScroll from '@/hooks/useScroll'

const tabRef = ref()

const { scrollTop } = useScroll(tabRef)
const isShowTabControl = computed(() => {
  console.log(scrollTop.value)
  return scrollTop.value > 300
})
```

> 在Vue 3中，为了访问DOM元素，可以使用`ref`函数创建一个响应式对象。`ref`函数可以将任何JavaScript值转换为响应式对象，并且在模板中使用`$refs`属性访问它们。
>
> 在给定的代码中，将`tabRef`定义为`ref`是为了让Vue跟踪这个DOM元素的状态。通过将元素包装在`ref`中，Vue可以检测到何时该元素被创建、更新或销毁，从而允许我们执行相应的操作。
>
> 例如，在这个示例中，我们可以使用`$refs`属性访问`tabRef`，并且当在代码中更新`tabRef`时，Vue会自动重新渲染相关的DOM。
>
> 为什么不直接使用`useScroll(document.querySelector("detail-page"))`
>
> 因为setup中，这个div还没有被挂载，是传不进去的~

## 15、TabControl的交互和滚动过程

### 15.1、发出一个事件给父元素details

`src/components/tab-control/tab-control.vue`

```vue
<template>
  <div class="tab-control" >
    <template v-for="(item, index ) in title " :key="index">
      <div class="tab-control-item" @click="tabControlClick(index)" :class="{ active: currentIndex === index }">{{ item }}
      </div>
    </template>
  </div>
</template>
```

```js
const emits = defineEmits(["tabControlClick"])

const currentIndex = ref(0)
const tabControlClick = (index) => {
  // console.log(index)
  currentIndex.value = index
  emits("tabControlClick", index)
}
```

### 15.2、父元素监听跳转到元素位置

`src/views/detial/detial.vue`

```vue
<tab-control @tabControlClick="tabItemClick"...></tab-control>
```

#### 15.2.1、跳转到固定位置

```js
const tabItemClick = (index) =>{
  console.log(index)
  tabRef.value.scrollTo({
    top:200,
    behavior:'smooth'
  })
}
```

想跳转到对应的位置，需要拿到每个元素的Top值，并且不是这个组件的元素，而是根元素中的top值

`src/views/detial/detial.vue`

```vue
<div v-if="mainPart" class="main">
  <detail-swipe :swipe-data="mainPart.topModule.housePicture.housePics"></detail-swipe>
  <detail-infos :infos-data="mainPart.topModule"></detail-infos>
  <detail-facility :facility-data="mainPart.dynamicModule.facilityModule.houseFacility"></detail-facility>
  <detail-landlord :landlore-data="mainPart.dynamicModule.landlordModule"></detail-landlord>
  <detail-comment ref="toRef"></detail-comment>
  <detail-notice></detail-notice>
  <detail-map :position-data="mainPart.dynamicModule.positionModule"></detail-map>
  <detail-introduction :introduction-data="mainPart.introductionModule"></detail-introduction>
</div>
```

#### 15.2.2、第二步：跳转到固定根元素

```vue
<detail-comment ref="toRef"></detail-comment>
```

```js
const toRef = ref()
const tabItemClick = (index) =>{
  console.log(index)
  tabRef.value.scrollTo({
    top:toRef.value.$el.offsetTop - 44,
    behavior:'smooth'
  })
}
```

> 需要减去tab栏的脱标高度，可以动态获取，但我们知道高度也可以写死

#### 15.2.3、第三步、获取每一个元素的offectTop

`src/views/detial/detial.vue`

```vue
<detail-swipe :ref="getSectionEl".../>
<detail-infos :ref="getSectionEl" .../>
<detail-facility :ref="getSectionEl" .../>
<detail-landlord :ref="getSectionEl" .../>
<detail-comment :ref="getSectionEl" .../>
<detail-notice :ref="getSectionEl" .../>
<detail-map :ref="getSectionEl" .../>
<detail-introduction :ref="getSectionEl" .../>
```

```js
const sectionEl = ([])
const getSectionEl = (value) => {
  sectionEl.push(value.$el)
}
```

> 通过 `:ref` 指令和一个函数 `getSectionEl` 进行绑定，该函数将被调用并传递一个参数，当组件被挂载到DOM树上时，`getSectionEl` 函数将被调用，并将组件的 `$el` 属性（即该组件的根元素）作为参数传递进来。
>
> `getSectionEl` 函数将该元素放在 `sectionEl` 数组中。

问题一：滚动造成刷新，不停的获取元素

==v-memo="[mainPart]"==

```html
<div v-if="mainPart" class="main" v-memo="[mainPart]">
```

> 当组件重新渲染，如果`mainPart`保持不变，这个 `<div>` 及其子项的所有更新都将被跳过。实际上，甚至虚拟 DOM 的 vnode 创建也将被跳过，因为缓存的子树副本可以被重新使用。
>
> `v-memo` 传入空依赖数组 (`v-memo="[]"`) 将与 `v-once` 效果相同。

#### 15.2.4、第四步，跳转到元素的offectTop

`src/views/detial/detial.vue`

```js
const sectionEl = []

const getSectionEl = (value) => {
  sectionEl.push(value.$el)
  console.log(value.$el)
}

const tabItemClick = (index) =>{
  console.log(index)
  tabRef.value.scrollTo({
    top:sectionEl[index].offsetTop-44,
    behavior:'smooth'
  })
}
```

#### 15.2.4、第五步，动态绑定`name`重构代码

```html
<tab-control ...:title="['abc', 'bac', 'cba', 'acb', 'nba']"/>
```

定义一个对象，里面的`key`是我们需要的`title`

1、定义一个属性，name、title都可以，这里面的名字来自于这里

`src/views/detial/detial.vue`

```html
// src/views/detial/detial.vue
<detail-infos ...name="描述".../>
<detail-facility ...name="设施".../>
...
```

2、封装成一个ref 变成响应式的

```js
// src/views/detial/detial.vue
const sectionEl = ref({})

const getSectionEl = (value) => {
  console.log(value.$el) 
}
```

3、从元素中获取属性

```js
//src/views/detial/detial.vue
const getSectionEl = (value) => {
  const name = value.$el.getAttribute("name")
  console.log(name) // 描述 设施 房东 评论 须知 地图
}
```

4、把key作为值放进去，最终代码

```html
<tab-control ...:title="names"></tab-control>
```

```js
// 创建一个名为sectionEl的响应式引用对象
const sectionEl = ref({})

// 创建一个名为getSectionEl的函数，用于获取元素节点
const getSectionEl = (value) => {
  if (!value) return
  // 从传入的value参数中获取节点的name属性值
  const name = value.$el.getAttribute("name")
  // 在控制台打印节点的name属性值
  console.log(name)
  // 将节点的name属性值作为键名，将节点对象作为键值，存储到sectionEl对象中
  sectionEl.value[name] = value.$el
}

// 创建一个计算属性名为names，用于获取所有sectionEl对象中的键名
const names = computed(() => {
  // 使用Object.keys()方法获取sectionEl对象的所有键名，并返回
  return Object.keys(sectionEl.value)
})
```

![image-20230330182156994](E:\coder\09_OneNote\image\image-20230330182156994.png)

#### 问题

绑定到ref中的函数，挂载时候会执行，并且在卸载时候也会执行，比如说返回的时候，这个时候的值是一个**null**，因此浏览器会报错~因此需要添加` if (!value) return` 作为判断

> 这种问题是会**经常**遇见的，遇见的时候也不要慌，并且这种错误在开发中遇见的次数最多也不为过~
>
> 一般情况下，报错是null、undefined的时候，某个位置加一个逻辑判断就好了~
>
> 要学会读错误，才能解决问题，
>
> 1、定位到错误位置，
>
> 2、使用debugger、或者clg

#### 15.2.6、转为数组

现在虽然是动态的，但是不是一个数组，无法跳转

```js
// 创建一个名为tabItemClick的函数，用于处理标签页的点击事件
const tabItemClick = (index) => {
  // 获取点击的标签页所对应的内容区域的键名
  const key = Object.keys(sectionEl.value)[index]
  // 根据键名获取对应的内容区域节点对象
  const el = sectionEl.value[key]
  // 获取内容区域节点对象距离页面顶部的距离
  let instance = el.offsetTop
  // 如果不是第一个标签页，则将距离减去标签栏的高度
  if (index !== 0) {
    instance -= 44
  }
  // 通过tabRef引用对象的scrollTo方法，使页面滚动到对应的内容区域
  tabRef.value.scrollTo({
    top: instance,
    behavior: 'smooth'
  })
}
```

> 现在做很多东西的思路想不到，主要是因为做的太少~
>
>  **需要达到这种程度：**
>
> 1、能在不看老师的代码情况下，把项目做出来；
>
> 2、课下还是要好好的一步一步来写，关于样式也要自己去调；
>
> 3、边做边总结。不用着急一点一点来~
>
> 4、关于重构，先完成需求，之后再想着从一些小的模块开始一点一点来重构，一次性就能达到最优解是不现实的， 

## 16、页面滚动位置显示正确的索引

```js
watch(scrollTop, (newValue) => { // 使用Vue的watch函数监听scrollTop的变化，newValue为新的值
  const els = Object.values(sectionEl.value) // 获取所有需要匹配的元素
  const values = els.map(el => el.offsetTop) // 获取所有需要匹配的元素的offsetTop值
  let index = values.length - 1 // 初始化索引值为最后一个元素的索引
  for (let i = 0; i < values.length; i++) { // 遍历所有元素的offsetTop值
    if(values[i] < newValue + 44) { // 如果当前元素的offsetTop值大于newValue和tabber的和
      index= i-1 // 则将索引值设置为当前元素的前一个元素的索引
      break // 找到了符合条件的元素，退出循环
    }
  }
  console.log(index) // 打印最终匹配到的索引值
})
```

> 函数中的主要逻辑如下：
>
> 1. 获取所有需要匹配的元素的offsetTop值。这里使用了Vue 3的ref和reactive功能，通过sectionEl.value获取所有需要匹配的元素，然后通过Object.values方法将其转换为一个数组，最后通过map方法遍历获取每个元素的offsetTop值。
> 2. 遍历所有的offsetTop值，与当前的scrollTop值进行比较，找到第一个比scrollTop大的offsetTop值，对应的索引即为TabControl的索引。这里使用了一个for循环来遍历比较，如果找到第一个比scrollTop大的offsetTop值，则将其对应的索引减去1，这样就可以得到TabControl的索引了。
> 3. 注意处理一些边界情况。例如，如果scrollTop小于第一个offsetTop值，则默认为第一个TabControl的索引；如果scrollTop大于最后一个offsetTop值，则默认为最后一个TabControl的索引。
> 4. 最后，将找到的TabControl的索引打印出来，可以根据需要进行其他处理。
>
> 这个算法与网易云音乐中歌词的算法类似，都是根据值匹配到区间的问题。通过遍历比较的方式，找到第一个大于目标值的元素，即可确定匹配到的区间。
>
> 总的来说，这段代码实现了监听页面滚动事件，并根据当前的滚动位置匹配到对应的TabControl的索引。它使用了Vue 3的ref和reactive功能来获取需要匹配的元素的offsetTop值，并使用一个for循环来遍历比较。需要注意一些边界情况的处理，例如第一个和最后一个元素。

### 16.2、索引值匹配tabbar

1、子元素`tab-control.vue`暴露`currentIndex`

```js
// src/components/tab-control/tab-control.vue
// 子组件通过 defineExpose 将 currentIndex 暴露给父组件
defineExpose ({
  currentIndex
})
```

2、父组件接收，并且改变

使用`defineExpose`将子组件的属性和方法暴露给父组件，然后通过`ref`引用获取子组件实例并访问其属性和方法。

```vue
<!-- 在父组件中创建一个ref引用，用于将子组件的实例存储到该引用中，然后可以使用该引用来访问子组件的属性和方法。-->
<tab-control ...ref="tabControlRef"></tab-control>
```

```js
// 在父组件中创建一个空的ref引用。用于引用子组件实例
const tabControlRef = ref(null)
watch(scrollTop, (newValue) => {
  const els = Object.values(sectionEl.value)
  const values = els.map(el => el.offsetTop)
  let index = values.length - 1
  for (let i = 0; i < values.length; i++) {
		// 计算出当前所在位置
    if (values[i] > newValue + 44 ) {
      index = i - 1
      break
    }
  }
  console.log(index)
	// 将父组件中的currentIndex属性的值赋值为子组件中计算出的index值
  tabControlRef.value.currentIndex = index
})
```

**整体是不难的，难的是这个算法，做过之后就会简单多了**

> 这些功能如果觉得太难，实在做不出来，其实**组件库**也是可以找到的，
>
> 或者大部分功能其实**别人也都是做过的**，都可以找到，
>
> 并且组件库的东西都是**可以自己实现的**，也可以去看源码是如何实现的！
>
> 自己实现，更加清晰自己的代码，组件库的有些BUG不好找原因~

### 16.3、小bug修复

滚动中`tab-control`栏会进行挨个匹配，

如何做？点击事件是不需要操作的，并且

滚动到位置后，需要将isClick设置回去，才能运行下面代码

```js
定义一个标记变量，用于判断是否是点击tab导致的scrollTop变化
let isClick = false
初始化当前距离为-1
let currentDistance = -1


// 定义一个点击tab的函数，用于滚动到对应的section
const tabItemClick = (index) => {
  // 获取对应section的key
  const key = Object.keys(sectionEl.value)[index]
// 获取对应section的距离
  const el = sectionEl.value[key]
  let instance = el.offsetTop
  if (index !== 0) {
    instance = instance - 44
  }
	将isClick标记为true，表示此次scrollTop变化是由点击tab导致的
  isClick = true
  
  记录当前距离
  currentDistance = instance
  // 使用ref获取tab-control组件的引用，调用scrollTo方法进行滚动
  tabRef.value.scrollTo({
    top: instance,
    behavior: 'smooth'
  })
}

// 使用ref获取tab-control组件的引用
const tabControlRef = ref(null)

// 监听scrollTop的变化
watch(scrollTop, (newValue) => {
  
  如果scrollTop已经滚动到了目标距离，将isClick标记为false
  if (newValue === currentDistance){
    isClick = false
  }
  
  如果此次scrollTop变化是由点击tab导致的，直接返回
  if(isClick) return
  
  // 获取所有section元素的距离值
  const els = Object.values(sectionEl.value)
  const values = els.map(el => el.offsetTop)
  
  // 计算当前处于哪个section，并将其索引值设置为currentIndex
  let index = values.length - 1
  for (let i = 0; i < values.length; i++) {
    if (values[i] > newValue + 44 ) {
      index = i - 1
      break
    }
  }
  console.log(index)
  // 将计算得到的索引值赋给tab-control组件的currentIndex属性
  tabControlRef.value.currentIndex = index
})
```



# 七、代码优化

> 之前主要做了首页、详情页、其他页面想自己搭建也可以自己来实现，
>
> 但是课上这些要在**不看老师的代码下实现**，
>
> 有些API或者属性实在记不住，去看笔记或者搜索寻找都可以~
>
> 但是业务逻辑要清晰

## 1、代码优化——缓存home.vue网络请求

在切换页面时会重新发送网络请求：

![image-20230331135440613](E:\coder\09_OneNote\image\image-20230331135440613.png)

> 本质上是因为路由切换后，会将home删掉后，重新创建home页面，但是store是一个全局对象，有保留

官方文档：https://cn.vuejs.org/api/built-in-components.html#keepalive

1、使用`<keep-alive>`

这里是Vue不建议使用`keep-alive`了，建议使用插槽的方式，`router-view`本质是一个组件，当匹配到对应的路由，会将组件替代`router-view`

```vue
<!-- src/App.vue -->
<router-view v-slot="props">
  <keep-alive includ="home">
    <component :is="props.Component"></component>
  </keep-alive>
</router-view>
```

> 路由器视图（router-view）组件，用于在应用程序中动态呈现不同的组件。
>
> 具体地，它使用了一个具名插槽（v-slot），该插槽名称为"props"。在路由器视图中，该插槽可以用于访问路由器视图的属性，例如当前路由匹配的组件（Component）。
>
> 在这个例子中，该路由器视图组件被包裹在了一个保持活动状态（keep-alive）的组件中。keep-alive可以缓存组件的实例以避免重复渲染，这可以提高应用程序的性能。在这个例子中，keep-alive指定了一个名为"home"的组件作为缓存的标识符，这意味着只有具有该标识符的组件才会被缓存。
>
> 最后，该路由器视图组件将通过动态组件（component）的方式渲染出来，其中动态组件会根据组件名称（Component）来动态地加载和渲染不同的组件。由于keep-alive的缓存机制，如果该组件已经被缓存，则不需要重新创建组件实例，可以直接从缓存中读取，从而提高了性能。

2、但是`setup`语法糖写法是没法定义name属性的，因此要如何定义呢？

目前没有相关的属性，只能多写一个`setup`，定义一个`name`

![image-20230331141928005](E:\coder\09_OneNote\image\image-20230331141928005.png)

```html
// src/views/home/cpns/home.vue
<script>
  export default { name: "home" }
</script>

<script>
</script>
```

## 2、返回home后，保留位置

```html
// src/views/home/cpns/home.vue
<div ...ref="homeRef">
```

```js
// ...
const homeRef = ref()
// ...
const { isReachBottom, scrollTop } = useScroll(homeRef)
// ...
//  缓存位置
onActivated(() => {
  homeRef.value.scrollTo({
    top: scrollTop.value
  })
})
```

> 使用了ref指令将一个属性名为"homeRef"的引用属性绑定到了一个DOM元素上。这个DOM元素可能是一个容器元素，用于显示一些动态数据，例如图片、文本等。
>
> 在脚本中，使用了ref函数来创建一个名为"homeRef"的响应式引用对象，该引用对象引用了模板中绑定的DOM元素。
>
> 在onActivated生命周期钩子函数中，可以在组件被激活时执行代码。在这个例子中，通过homeRef.value.scrollTo()函数，将DOM元素的滚动条位置滚动到指定的位置，该位置由scrollTop.value变量指定。
>
> 总的来说，这段代码实现了一个将页面滚动到指定位置的功能，当组件被激活时，将滚动条位置滚动到scrollTop.value所指定的位置。其中，通过使用ref指令将DOM元素和响应式引用对象建立关联，实现了对DOM元素的引用和操作。

### 2.1、方案二移除滚动

![image-20230331150945391](E:\coder\09_OneNote\image\image-20230331150945391.png)

# 八、其他

## 8.1、其他页面

目前已经做了这三个页面了，其他页面想做的话，自己可以参考代码来做：

**搜索页面，**搭建可能麻烦一些，之前学习的jquery可能做过，想做的话自己来做一下~

**收藏页面**，将在某个页面收藏一下，将对应的收藏数据id传给服务器，最终是服务器那边来收藏的，然后你来到收藏页面，就是发送一个网络请求，服务器来告诉你的收藏数据，再进行展示就好了~

**订单页面**，类似~

**信息页面**，就是一个全屏的页面~

## 8.2、移动端适配

### 8.2.1、禁止缩放

对于移动端项目，有可能用户会进行页面的缩放，但是不希望用户进行缩放怎么做？

**需要设置视口**

之前移动端适配有讲过

`index.html`

```
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0,user-scalable=no">
```

文档：

https://developer.mozilla.org/zh-CN/docs/Web/HTML/Viewport_meta_tag

### 8.2.2、Viewport 布局

在 Vite 中，你可以在 `postcss.config.js` 文件中配置 PostCSS 插件。

要使用 `postcss-px-to-viewport` 插件，你需要首先安装它：

```
npm install postcss-px-to-viewport --save-dev
```

然后，在 `postcss.config.js` 文件中配置插件选项，如下所示：

```js
module.exports = {
  plugins: {
    'postcss-px-to-viewport': {
      viewportWidth: 375,
    },
  },
};
```

这个配置告诉 `postcss-px-to-viewport` 插件将所有像素值转换为视口单位。在这个例子中，我们将视口宽度设置为 375 像素。

你可以根据你的需要调整这个配置，比如设置更多的选项来自定义插件的行为。要了解更多信息，请查阅 `postcss-px-to-viewport` 插件的文档。

https://github.com/evrone/postcss-px-to-viewport



