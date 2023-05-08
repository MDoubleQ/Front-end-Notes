## 一、前言

vue3已成今年趋势，据我了解很多公司在今年都有计划将技术栈从vue2升级至vue3。所以在今年的金三银四过程中vue3也一定会是面试的大热门。在这里我汇总整理一些vue3必会知识点，持续更新，感谢关注！

## 二、跟vue2相比vue3有哪些变化？

1. 更小（vue2面向对象编程，vue3函数式编程）；
2. 更快；
3. 更好的类型推导，增强对TypeScript的支持；
4. `Options Api` 升级为 `composition Api`;
5. 响应式原理由`Object.defineProperty`变为ES2015中的`Proxy`;
6. 支持`template`中存在多个根节点；
7. 重写虚拟DOM；
8. 增加setup入口函数；
9. 支持`tree-shaking`，使vue3体积更小；
10. 组件渲染优化（vue2父组件渲染时，子组件也会渲染。vue3支持单独渲染父组件、子组件）;
11. vue3有`createApp()`,vue2是`new Vue()`。（`createApp(组件)`，`new Vue({template,render})`）;
12. `v-model`代替之前的`v-model`和`.sync`;
13. `diff`算法优化，使用静态树提升。

## 三、Proxy相比于defineProperty的优势

Object.defineProperty() 的问题主要有三个：

- 不能监听数组的变化
- 必须深层遍历嵌套的对象
- 必须遍历对象的每个属性

Proxy 在 ES2015 规范中被正式加入，它有以下几个特点：

- 针对对象：针对整个对象，而不是对象的某个属性，所以也就不需要对 keys 进行遍历。这解决了上述 Object.defineProperty() 第二个问题

支持数组：Proxy 不需要对数组的方法进行重载，省去了众多 hack，减少代码量等于减少了维护成本，而且标准的就是最好的。

除了上述两点之外，Proxy 还拥有以下优势：

- Proxy 的第二个参数可以有 13 种拦截方法，这比起 Object.defineProperty() 要更加丰富
- Proxy 作为新标准受到浏览器厂商的重点关注和性能优化，相比之下 Object.defineProperty() 是一个已有的老方法。

## 四、vue3性能比vue2好的原因

1. `diff`算法优化，在创建`虚拟Dom`时增加了静态标记；
2. 静态提升hoistStatic;
3. 事件侦听器缓存 cacheHandles。

## 五、Vue 3.0 所采用的 Composition Api 与 Vue 2.x使用的Options Api 有什么区别？

[# 什么是Vue3的组合式API？](https://juejin.cn/post/7028629804173770765)

## 六、vue3中删除了哪些内容

1. 移除`$on`、`$off`、`$once`；
2. 移除过滤器（|），可以使用`计算属性`或`方法`代替；
3. 移除`$children`。

## 七、vue3新增了哪些Api

1. setup；
2. ref；
3. reactive；
4. isRef;
5. toRefs;
6. watchEffect;
7. watchPostEffect；
8. shallowReactive;
9. watchSyncEffect；
10. shallowRef;
11. readonly;
12. shallowReadonly;
13. toRaw;
14. markRaw;
15. customRef;

### 详解链接

- [Vue.js](https://link.juejin.cn?target=https%3A%2F%2Fv3.cn.vuejs.org%2F)
- [关于Vue3中setup的实战应用](https://juejin.cn/post/7029339447078420493)
- [在实验 vue3.2中 的script setup时，关于...toRefs的应用尝试](https://juejin.cn/post/7030453540657037325)

## 八、vue3中新增了哪些新组件？

1. Fragment（虚拟容器，`template`支持多个根节点的原理）；
2. Teleport（传送门）；
3. Suspense（实验性，了解就行）。

## 九、vue3.2相较于vue3.0 更新了哪些内容？

[ [技术前沿\] 最新的 Vue3.2 都更新了些什么了解一下](https://juejin.cn/post/7000160263521435685)

## 十、vue3中的created和vue2中的created有什么区别？

根据生命周期对比，可以看到在vue3中`created`已完全被`setup`所替代，所以在vue3中是没有`created`的。这道题是在几天前被面试官问到的，所以在这里贴出来。

Tips：虽然vue3中没有`created`，但是在vue3中仍可以用`created`，只是用的是vue2中的`created`,因为vue3向下兼容vue2

![image.png](E:\coder\09_OneNote\image\8c9214d3f3794907aa4f6cdcca5c322etplv-k3u1fbpfcp-zoom-in-crop-mark4536000.webp)



作者：业务崽
链接：https://juejin.cn/post/7069413391114174500
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。