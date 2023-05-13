

## 1、法一

```javascript
import { createStore } from "vuex";
// A模块
const moduleA = {
  state: {
    username: "moduleA",
  },
  getters: {
    newName (state) {
      return state.username + "!!!!";
    },
  },
  mutations: {
    updateName (state) {
      state.username = "moduleAAAA";
    },
  },
};
// B模块
const moduleB = {
  namespaced: true,
  state: {
    username: "moduleB",
    age: 2
  },
  getters: {
    newName (state) {
      return state.username + "???";
    },
  },
  mutations: {
    // 更改数据函数
    updateName (state) {
      state.username = 'ls'
    },
    updateAge (state, playLoad) {
      console.log("playLoad", playLoad)
      state.age += playLoad
    }
  },
  actions: {
    // 请求数据函数
    updateName (ctx, count) {
      console.log('触发了')
      // 发请求
      setTimeout(() => {
        ctx.commit('updateAge', count)
      }, 1000)
    }
  },
};
export default createStore({
  // 分模块
  modules: {
    moduleA,
    moduleB,
  },
});
```

## 2、法二

基于原index.js代码进行改造拆分，假设有两个模块global和user，新建src/store/modules/global.js 、src/store/modules/user.js文件

拆分后代码如下（src/store/modules/global.js）

```javascript
// 全局store,存放全局使用共享的数据
export default { // 注意：全局模块中不需要开启命名空间
  state: {
  },
  mutations: {
  },
  actions: {
  },
  getters: {
  }
}
```

拆分后代码如下（src/store/modules/user.js）

```javascript
// 用户信息模块(局部模块)
export default {
  namespaced: true, // 开启命名空间
  state () {
    return {
      // 用户信息对象 
      profile: {
        id: '',
        avatar: '',
        nickname: 'yee',
        account: '',
        mobile: '',
        token: ''
      }
    }
  },
  mutations: {
    // 定义mutations，用于同步修改状态
    updateNickname (state, payload) {
      state.profile.nickname = payload
    }
  },
  actions: {
    // 定义actions，用于异步修改状态
    // 2秒后更新状态
    updateNickname (context, payload) {
      setTimeout(() => {
        context.commit('updateNickname', payload)
      }, 2000)
    }
  },
  getters: {
    // 定义一个getters
    formatNickname (state) {
      return 'Hi ' + state.profile.nickname
    }
  }
}
```

拆分后代码如下（src/store/index.js）

```javascript
import { createStore } from 'vuex'
// 全局模块
import global from './modules/global'
// 局部模块
import user from './modules/user'
export default createStore({
  // 全局模块，看着办吧
  ...global,
  // 局部模块
  modules: {
    user
  }
})
```

app.js

```javascript
// main.js
import { createApp } from "vue"
import App from "./App.vue"
import store from "./store"
createApp(App).use(store).mount("#app")
```

**使用**

```javascript
<template>
  <div>测试组件</div>
  <hr>
  <div>获取Store中user模块的getters: {{$store.getters['user/formatNickname']}}</div>
  <button @click='handleClick'>点击</button>
</template>

<script>
import { useStore } from 'vuex'

export default {
  name: 'Test',
  setup () {
    // this.$store.state.info
    // Vue3中store类似于Vue2中this.$store
    const store = useStore()
    console.log(store.state.user.profile.nickname)
    // 修改nickname的值
    const handleClick = () => {
      // 触发mutations，用于同步修改user模块state的信息
      // store.commit('updateNickname', 'Jackson')
      store.dispatch('user/updateNickname', 'Yee')
    }
    return { handleClick }
  }
}
</script>## 1、法一

import { createStore } from "vuex";
// A模块
const moduleA = {
  state: {
    username: "moduleA",
  },
  getters: {
    newName (state) {
      return state.username + "!!!!";
    },
  },
  mutations: {
    updateName (state) {
      state.username = "moduleAAAA";
    },
  },
};
// B模块
const moduleB = {
  namespaced: true,
  state: {
    username: "moduleB",
    age: 2
  },
  getters: {
    newName (state) {
      return state.username + "???";
    },
  },
  mutations: {
    // 更改数据函数
    updateName (state) {
      state.username = 'ls'
    },
    updateAge (state, playLoad) {
      console.log("playLoad", playLoad)
      state.age += playLoad
    }
  },
  actions: {
    // 请求数据函数
    updateName (ctx, count) {
      console.log('触发了')
      // 发请求
      setTimeout(() => {
        ctx.commit('updateAge', count)
      }, 1000)
    }
  },
};
export default createStore({
  // 分模块
  modules: {
    moduleA,
    moduleB,
  },
});
```

## 2、法二

基于原 index.js 代码进行改造拆分，假设有两个模块 global 和 user，新建 src/store/modules/global.js 、src/store/modules/user.js 文件

拆分后代码如下（src/store/modules/global.js）

```javascript
// 全局store,存放全局使用共享的数据
export default { // 注意：全局模块中不需要开启命名空间
  state: {
  },
  mutations: {
  },
  actions: {
  },
  getters: {
  }
}
```

拆分后代码如下（src/store/modules/user.js）

```javascript
// 用户信息模块(局部模块)
export default {
  namespaced: true, // 开启命名空间
  state () {
    return {
      // 用户信息对象
      profile: {
        id: '',
        avatar: '',
        nickname: 'yee',
        account: '',
        mobile: '',
        token: ''
      }
    }
  },
  mutations: {
    // 定义mutations，用于同步修改状态
    updateNickname (state, payload) {
      state.profile.nickname = payload
    }
  },
  actions: {
    // 定义actions，用于异步修改状态
    // 2秒后更新状态
    updateNickname (context, payload) {
      setTimeout(() => {
        context.commit('updateNickname', payload)
      }, 2000)
    }
  },
  getters: {
    // 定义一个getters
    formatNickname (state) {
      return 'Hi ' + state.profile.nickname
    }
  }
}
```

拆分后代码如下（src/store/index.js）

```javascript
import { createStore } from 'vuex'
// 全局模块
import global from './modules/global'
// 局部模块
import user from './modules/user'
export default createStore({
  // 全局模块，看着办吧
  ...global,
  // 局部模块
  modules: {
    user
  }
})
```

app.js

```javascript
// main.js
import { createApp } from "vue"
import App from "./App.vue"
import store from "./store"
createApp(App).use(store).mount("#app")
```

**使用**

```vue
<template>
  <div>测试组件</div>
  <hr>
  <div>获取Store中user模块的getters: {{$store.getters['user/formatNickname']}}</div>
  <button @click='handleClick'>点击</button>
</template>

<script>
import { useStore } from 'vuex'

export default {
  name: 'Test',
  setup () {
    // this.$store.state.info
    // Vue3中store类似于Vue2中this.$store
    const store = useStore()
    console.log(store.state.user.profile.nickname)
    // 修改nickname的值
    const handleClick = () => {
      // 触发mutations，用于同步修改user模块state的信息
      // store.commit('updateNickname', 'Jackson')
      store.dispatch('user/updateNickname', 'Yee')
    }
    return { handleClick }
  }
}
</script>
<div id="content_views" class="markdown_views prism-atom-one-dark">
<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
<path stroke-linecap="round" d="M5,0 0,2.5 5,5z" id="raphael-marker-block" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"> </path>
</svg>
<h2><a name="t0"></a><a id="1_0"></a>1、法一</h2>
```