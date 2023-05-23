# 📁Vue3.0基础

## Vue2.0 的基本原理

当一个Vue实例创建时，Vue会遍历`data`中的属性，用`Object.defineProperty`（vue3.0使用proxy ）将它们转为 getter/setter，并且在内部追踪相关依赖，在属性被访问和修改时通知变化。

每个组件实例都有相应的 watcher 程序实例，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的setter被调用时，会通知watcher重新计算，从而致使它关联的组件得以更新。

![0_tB3MJCzh_cB6i3mS-1.png](E:\coder\09_OneNote\image\b1b16025a35b4cd2b343a92e740621b7tplv-k3u1fbpfcp-zoom-in-crop-mark1512000.webp)

## Vue3.0有什么更新

**（1）监测机制的改变**

- 3.0 将带来基于代理 Proxy的 observer 实现，提供全语言覆盖的反应性跟踪。
- 消除了 Vue 2 当中基于 Object.defineProperty 的实现所存在的很多限制：

**（2）只能监测属性，不能监测对象**

- 检测属性的添加和删除；
- 检测数组索引和长度的变更；
- 支持 Map、Set、WeakMap 和 WeakSet。

**（3）模板**

- 作用域插槽，2.x 的机制导致作用域插槽变了，父组件会重新渲染，而 3.0 把作用域插槽改成了函数的方式，这样只会影响子组件的重新渲染，提升了渲染的性能。
- 同时，对于 render 函数的方面，vue3.0 也会进行一系列更改来方便习惯直接使用 api 来生成 vdom 。

**（4）对象式的组件声明方式**

- vue2.x 中的组件是通过声明的方式传入一系列 option，和 TypeScript 的结合需要通过一些装饰器的方式来做，虽然能实现功能，但是比较麻烦。
- 3.0 修改了组件的声明方式，改成了类式的写法，这样使得和 TypeScript 的结合变得很容易

**（5）其它方面的更改**

- 支持自定义渲染器，从而使得 weex 可以通过自定义渲染器的方式来扩展，而不是直接 fork 源码来改的方式。
- 支持 Fragment（多个根节点）和 Protal（在 dom 其他部分渲染组建内容）组件，针对一些特殊的场景做了处理。
- 基于 tree shaking 优化，提供了更多的内置功能。

## delete和Vue.delete删除数组的区别

- `delete` 只是被删除的元素变成了 `empty/undefined` 其他的元素的键值还是不变。
- `Vue.delete` 直接删除了数组 改变了数组的键值。

## Vue的优点？

Vue 是一个流行的 JavaScript 框架，具有以下优点：

1. 简单易学：Vue 的 API 简单明了，语法易懂，上手成本低，有很好的文档和社区支持。
2. 组件化开发：Vue 具有强大的组件化开发能力，使得代码具有更好的复用性和可维护性，同时也更容易实现模块化开发。
3. 双向数据绑定：Vue 的双向数据绑定使得数据与视图之间的同步更加简单，开发者不需要手动处理 DOM 元素与数据之间的关系。
4. 轻量级框架：Vue 的体积非常小，性能出色，能够很好地满足轻量级项目的需求。
5. 生态系统完备：Vue 有非常完整的生态系统，包括 Vue Router、Vuex 等工具，可以帮助开发者更好地实现路由管理、状态管理等功能。
6. 社区活跃度高：Vue 拥有一个庞大的社区，开发者可以很方便地找到解决问题的方法或者开源项目，从而提高开发效率。
7. 渐进式框架：Vue.js是一个渐进式框架，可以根据具体需求选择不同的构建方式，比如只使用其核心库来构建轻量级的应用，或者使用其全家桶来构建复杂的应用。

综上所述，Vue 具有简单易学、组件化开发、双向数据绑定、轻量级框架、完备的生态系统和活跃的社区等优点，是一个非常优秀的 JavaScript 框架。

> - 轻量级框架：只关注视图层，是一个构建数据的视图集合，大小只有几十 `kb` ；
> - 简单易学：国人开发，中文文档，不存在语言障碍 ，易于理解和学习；
> - 双向数据绑定：保留了 `angular` 的特点，在数据操作方面更为简单；
> - 组件化：保留了 `react` 的优点，实现了 `html` 的封装和重用，在构建单页面应用方面有着独特的优势；
> - 视图，数据，结构分离：使数据的更改更为简单，不需要进行逻辑代码的修改，只需要操作数据就能完成相关操作；
> - 虚拟DOM：`dom` 操作是非常耗费性能的，不再使用原生的 `dom` 操作节点，极大解放 `dom` 操作，但具体操作的还是 `dom` 不过是换了另一种方式；
> - 运行速度更快：相比较于 `react` 而言，同样是操作虚拟 `dom`，就性能而言， `vue` 存在很大的优势。

## 对 React 和 Vue 的理解，它们的异同

**相似之处：**

- 都将注意力集中保持在核心库，而将其他功能如路由和全局状态管理交给相关的库；
- 都有自己的构建工具，能让你得到一个根据最佳实践设置的项目模板；
- 都使用了Virtual DOM（虚拟DOM）提高重绘性能；
- 都有props的概念，允许组件间的数据传递；
- 都鼓励组件化应用，将应用分拆成一个个功能明确的模块，提高复用性。

**不同之处 ：**

**1）数据流**

Vue默认支持数据双向绑定，而React一直提倡单向数据流

**2）虚拟DOM**

Vue2.x开始引入"Virtual DOM"，消除了和React在这方面的差异，但是在具体的细节还是有各自的特点。

- Vue宣称可以更快地计算出Virtual DOM的差异，这是由于它在渲染过程中，会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树。
- 对于React而言，每当应用的状态被改变时，全部子组件都会重新渲染。当然，这可以通过 PureComponent/shouldComponentUpdate这个生命周期方法来进行控制，但Vue将此视为默认的优化。

**3）组件化**

React与Vue最大的不同是模板的编写。

- Vue鼓励写近似常规HTML的模板。写起来很接近标准 HTML元素，只是多了一些属性。
- React推荐你所有的模板通用JavaScript的语法扩展——JSX书写。

具体来讲：React中render函数是支持闭包特性的，所以import的组件在render中可以直接调用。但是在Vue中，由于模板中使用的数据都必须挂在 this 上进行一次中转，所以 import 一个组件完了之后，还需要在 components 中再声明下。 **4）监听数据变化的实现原理不同**

- Vue 通过 getter/setter 以及一些函数的劫持，能精确知道数据变化，不需要特别的优化就能达到很好的性能
- React 默认是通过比较引用的方式进行的，如果不优化（PureComponent/shouldComponentUpdate）可能导致大量不必要的vDOM的重新渲染。这是因为 Vue 使用的是可变数据，而React更强调数据的不可变。

**5）高阶组件**

react可以通过高阶组件（HOC）来扩展，而Vue需要通过mixins来扩展。

高阶组件就是高阶函数，而React的组件本身就是纯粹的函数，所以高阶函数对React来说易如反掌。相反Vue.js使用HTML模板创建视图组件，这时模板无法有效的编译，因此Vue不能采用HOC来实现。

**6）构建工具**

两者都有自己的构建工具：

- React ==> Create React APP
- Vue ==> vue-cli

**7）跨平台**

- React ==> React Native
- Vue ==> Weex

## 双向绑定原理

Vue.js 2 和 Vue.js 3 的双向绑定原理都是基于 JavaScript 对象的 getter 和 setter 方法来实现的。

在 Vue.js 2 中，每个 Vue 实例都有一个被称为“响应式系统”的模块，它的核心是一个名为“依赖追踪”的机制。当 Vue 实例创建时，响应式系统会遍历数据对象中的每个属性，并使用 Object.defineProperty() 方法将它们转换为“getter”和“setter”形式。当属性被读取时，Vue.js 会记录一个依赖，并在属性被修改时重新计算这个依赖，从而自动更新视图中相应的数据。

在 Vue.js 3 中，使用了一种新的响应式系统，它基于 ES6 的 Proxy 对象实现。当 Vue 实例创建时，响应式系统会使用 Proxy 对象代理原始数据对象，从而可以在数据对象的访问和修改时拦截对应的操作，进行依赖追踪和更新视图等操作。相对于 Vue.js 2 的响应式系统，Vue.js 3 的响应式系统具有更好的性能和更少的限制，同时也支持更灵活的 API。

无论是 Vue.js 2 还是 Vue.js 3，双向绑定的实现方式都是通过在数据对象的 getter 和 setter 方法中执行相关的操作，从而实现自动更新视图的效果。在 Vue.js 2 中，数据对象的 getter 和 setter 方法是通过 Object.defineProperty() 方法实现的；在 Vue.js 3 中，数据对象的 getter 和 setter 方法是通过 Proxy 对象实现的。

## 双向数据绑定的原理

Vue.js 是采用**数据劫持**结合**发布者-订阅者模式**的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。主要分为以下几个步骤：

1. 需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化
2. compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图
3. Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是: ①在自身实例化时往属性订阅器(dep)里面添加自己 ②自身必须有一个update()方法 ③待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。
4. MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。

![image-20230430233809936](E:\coder\09_OneNote\image\image-20230430233809936.png)

## 单项数据流

Vue是一个基于MVVM模式的前端框架，它采用了单向数据流的数据流模型，也称为单向数据绑定。

单向数据流指的是数据只能从父组件传递到子组件，不能反向传递。父组件通过属性的方式将数据传递给子组件，在子组件中使用这些数据进行渲染和操作，但是子组件无法直接修改父组件传递过来的数据。如果需要修改这些数据，子组件需要通过$emit()方法向父组件发送事件，由父组件来修改数据。

这种单向数据流的数据流模型具有以下优点：

1. 数据流清晰：通过单向数据流的方式，可以清晰地追踪数据的来源和修改方式，避免了数据流混乱和难以维护的情况。
2. 提高了组件的可复用性：子组件只依赖于父组件传递过来的数据，可以根据不同的数据进行渲染和操作，提高了组件的可复用性。
3. 降低了耦合度：通过单向数据流的方式，父组件和子组件之间的耦合度降低，可以使得组件之间更加独立和可维护。

总之，Vue的单向数据流模型为前端开发带来了更加清晰、可复用和可维护的开发方式，是Vue框架的核心特性之一。

##  data为什么是一个函数而不是对象

JavaScript中的对象是引用类型的数据，当多个实例引用同一个对象时，只要一个实例对这个对象进行操作，其他实例中的数据也会发生变化。

在Vue 3.0中，为了支持更加灵活和高效的组件开发，data选项被设计成一个函数而不是一个对象。这个函数返回一个普通的对象，它的属性被包装成响应式对象，从而实现数据的响应式更新。

这种设计使用了ES6的Proxy来代理对象，使得任何属性的访问和修改都能被捕获并触发响应式更新。这样的设计避免了与响应式实现方式的冲突。

此外，在Vue中，为了避免多个组件之间相互干扰，需要每个组件都有自己的数据。因此，组件的数据不能写成对象的形式，而是要写成函数的形式。每次复用组件时，都会返回一个新的data，每个组件都有自己的私有数据空间，它们各自维护自己的数据，不会干扰其他组件的正常运行。这种设计也有助于提高代码的可维护性和可扩展性。

总之，Vue 3.0中的data选项采用函数式的设计，既能支持动态数据和响应式更新，又能实现组件的独立性和可维护性。

## Vue data 中某一个属性的值发生改变后，视图会立即同步执行重新渲染吗？

不会立即同步执行重新渲染。Vue 实现响应式并不是数据发生变化之后 DOM 立即变化，而是按一定的策略进行 DOM 的更新。Vue 在更新 DOM 时是异步执行的。只要侦听到数据变化， Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。

如果同一个watcher被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作是非常重要的。然后，在下一个的事件循环tick中，Vue 刷新队列并执行实际（已去重的）工作。

## 什么是 mixin ？

- Mixin 使我们能够为 Vue 组件编写可插拔和可重用的功能。
- 如果希望在多个组件之间重用一组组件选项，例如生命周期 hook、 方法等，则可以将其编写为 mixin，并在组件中简单的引用它。
- 然后将 mixin 的内容合并到组件中。如果你要在 mixin 中定义生命周期 hook，那么它在执行时将优化于组件自已的 hook。

## 简述 mixin、extends 的覆盖逻辑

**（1）mixin 和 extends** mixin 和 extends均是用于合并、拓展组件的，两者均通过 mergeOptions 方法实现合并。

- mixins 接收一个混入对象的数组，其中混入对象可以像正常的实例对象一样包含实例选项，这些选项会被合并到最终的选项中。Mixin 钩子按照传入顺序依次调用，并在调用组件自身的钩子之前被调用。
- extends 主要是为了便于扩展单文件组件，接收一个对象或构造函数。

| 属性名称              | 合并策略                                                     | 对应合并函数             |
| --------------------- | ------------------------------------------------------------ | ------------------------ |
| data                  | mixins/extends 只会将自己有的但是组件上没有内容混合到组件上,重复定义默认使用组件上 的 如果data里的值是对象,将递归内部对象继续按照该策略合并 | mergeDataOrFn, mergeData |
| provide               | 同上                                                         | mergeDataOrFn, mergeData |
| props                 | mixins/extends 只会将自己有的但是组件上没有内容混合到组件上  | extend                   |
| methods               | 同上                                                         | extend                   |
| inject                | 同上                                                         | extend                   |
| computed              | 同上                                                         | extend                   |
| 组件,过滤器,指令属 性 | 同上                                                         | extend                   |
| el                    | 同上                                                         | defaultStrat             |
| propsData             | 同上                                                         | defaultStrat             |
| watch                 | 合并watch监控的回调方法 执行顺序是先mixins/extends里watch定义的回调,然后是组件的回掉 | strats.watch             |
| HOOKS生命周期钩子     | 同一种钩子的回调函数会被合并成数组 执行顺序是先mixins/extends里定义的钩子函数,然后才是组件里定义的 | mergeHook                |

**（2）mergeOptions 的执行过程**

- 规范化选项（normalizeProps、normalizelnject、normalizeDirectives)
- 对未合并的选项，进行判断

```javascript
if (!child._base) {
  if (child.extends) {
    parent = mergeOptions(parent, child.extends, vm);
  }
  if (child.mixins) {
    for (let i = 0, l = child.mixins.length; i < l; i++) {
      parent = mergeOptions(parent, child.mixins[i], vm);
    }
  }
}
```

- 合并处理。根据一个通用 Vue 实例所包含的选项进行分类逐一判断合并，如 props、data、 methods、watch、computed、生命周期等，将合并结果存储在新定义的 options 对象里。
- 返回合并结果 options。

## 使用 Object.defineProperty() 来进行数据劫持有什么缺点？

在对一些属性进行操作时，使用这种方法无法拦截，比如通过下标方式修改数组数据或者给对象新增属性，这都不能触发组件的重新渲染，因为 Object.defineProperty 不能拦截到这些操作。更精确的来说，对于数组而言，大部分操作都是拦截不到的，只是 Vue 内部通过重写函数的方式解决了这个问题。

在 Vue3.0 中已经不使用这种方式了，而是通过使用 Proxy 对对象进行代理，从而实现数据劫持。使用Proxy 的好处是它可以完美的监听到任何方式的数据改变，唯一的缺点是兼容性的问题，因为 Proxy 是 ES6 的语法。

## defineProperty和proxy的区别

Vue 在实例初始化时遍历 data 中的所有属性，并使用 Object.defineProperty 把这些属性全部转为 getter/setter。这样当追踪数据发生变化时，setter 会被自动调用。

Object.defineProperty 是 ES5 中一个无法 shim 的特性，这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。

但是这样做有以下问题：

1. 添加或删除对象的属性时，Vue 检测不到。因为添加或删除的对象没有在初始化进行响应式处理，只能通过`$set` 来调用`Object.defineProperty()`处理。
2. 无法监控到数组下标和长度的变化。

Vue3 使用 Proxy 来监控数据的变化。Proxy 是 ES6 中提供的功能，其作用为：用于定义基本操作的自定义行为（如属性查找，赋值，枚举，函数调用等）。相对于`Object.defineProperty()`，其有以下特点：

1. Proxy 直接代理整个对象而非对象属性，这样只需做一层代理就可以监听同级结构下的所有属性变化，包括新增属性和删除属性。
2. Proxy 可以监听数组的变化。

## Vue3.0 为什么要用 proxy？

在 Vue2 中， 0bject.defineProperty 会改变原始数据，而 Proxy 是创建对象的虚拟表示，并提供 set 、get 和 deleteProperty 等处理器，这些处理器可在访问或修改原始对象上的属性时进行拦截，有以下特点∶

- 不需用使用 `Vue.$set` 或 `Vue.$delete` 触发响应式。
- 全方位的数组变化检测，消除了Vue2 无效的边界情况。
- 支持 Map，Set，WeakMap 和 WeakSet。

Proxy 实现的响应式原理与 Vue2的实现原理相同，实现方式大同小异∶

- get 收集依赖
- Set、delete 等触发依赖
- 对于集合类型，就是对集合对象的方法做一层包装：原方法执行后执行依赖相关的收集或触发逻辑。

## Vue 3.0 中的 Vue Composition API？

在 Vue2 中，代码是 Options API 风格的，也就是通过填充 (option) data、methods、computed 等属性来完成一个 Vue 组件。这种风格使得 Vue 相对于 React极为容易上手，同时也造成了几个问题：

1. 由于 Options API 不够灵活的开发方式，使得Vue开发缺乏优雅的方法来在组件间共用代码。
2. Vue 组件过于依赖`this`上下文，Vue 背后的一些小技巧使得 Vue 组件的开发看起来与 JavaScript 的开发原则相悖，比如在`methods` 中的`this`竟然指向组件实例来不指向`methods`所在的对象。这也使得 TypeScript 在Vue2 中很不好用。

于是在 Vue3 中，舍弃了 Options API，转而投向 Composition API。Composition API本质上是将 Options API 背后的机制暴露给用户直接使用，这样用户就拥有了更多的灵活性，也使得 Vue3 更适合于 TypeScript 结合。

如下，是一个使用了 Vue Composition API 的 Vue3 组件：

```javascript
<template>
  <button @click="increment">
    Count: {{ count }}
  </button>
</template>
 
<script>
// Composition API 将组件属性暴露为函数，因此第一步是导入所需的函数
import { ref, computed, onMounted } from 'vue'
 
export default {
  setup() {
// 使用 ref 函数声明了称为 count 的响应属性，对应于Vue2中的data函数
    const count = ref(0)
 
// Vue2中需要在methods option中声明的函数，现在直接声明
    function increment() {
      count.value++
    }
 // 对应于Vue2中的mounted声明周期
    onMounted(() => console.log('component mounted!'))
 
    return {
      count,
      increment
    }
  }
}
</script>

```

显而易见，Vue Composition API 使得 Vue3 的开发风格更接近于原生 JavaScript，带给开发者更多地灵活性

## Composition API与React Hook很像，区别是什么

从React Hook的实现角度看，React Hook是根据useState调用的顺序来确定下一次重渲染时的state是来源于哪个useState，所以出现了以下限制

- 不能在循环、条件、嵌套函数中调用Hook
- 必须确保总是在你的React函数的顶层调用Hook
- useEffect、useMemo等函数必须手动确定依赖关系

而Composition API是基于Vue的响应式系统实现的，与React Hook的相比

- 声明在setup函数内，一次组件实例化只调用一次setup，而React Hook每次重渲染都需要调用Hook，使得React的GC比Vue更有压力，性能也相对于Vue来说也较慢
- Compositon API的调用不需要顾虑调用顺序，也可以在循环、条件、嵌套函数中使用
- 响应式系统自动实现了依赖收集，进而组件的部分的性能优化由Vue内部自己完成，而React Hook需要手动传入依赖，而且必须必须保证依赖的顺序，让useEffect、useMemo等函数正确的捕获依赖变量，否则会由于依赖不正确使得组件性能下降。

虽然Compositon API看起来比React Hook好用，但是其设计思想也是借鉴React Hook的。

## vue数据加载一次后不在变更

如果您想要在Vue中仅加载一次数据，然后不再更新它，可以使用Vue的计算属性（computed property）。

计算属性是Vue组件中的一种属性，它会基于现有的响应式数据进行计算，并返回一个新的计算结果。计算属性的值会被缓存，只要依赖的响应式数据没有变化，就不会重新计算。

在您的组件中定义一个计算属性来获取您要加载的数据，并在模板中使用这个计算属性。这样，当您第一次访问该计算属性时，它会计算并返回您想要的数据。然后，由于这个计算属性的值已经被缓存了，即使后续更新了组件的响应式数据，也不会再次计算该计算属性。

以下是一个示例，演示如何在Vue中使用计算属性来实现只加载一次数据：

```vue
<template>
  <div>
    <p v-for="item in data">{{ item }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loadedData: false,
      data: []
    };
  },
  computed: {
    fetchData() {
      if (!this.loadedData) {
        // 在第一次计算时，加载数据并将loadedData设置为true
        this.data = // 加载数据的代码
        this.loadedData = true;
      }
      return this.data;
    }
  }
};
</script>
```

在这个示例中，我们定义了一个计算属性`fetchData`，它在第一次计算时加载数据，然后将`loadedData`设置为`true`，以便在后续计算中不会再次加载数据。在模板中，我们使用`v-for`指令循环遍历计算属性中的数据，以便将其呈现为一组`<p>`标签。

请注意，这只是一个示例。实际上，您需要根据您的具体应用场景和数据加载方式来调整代码。

## 声明式编程和命令式编程的区别

一、声明式编程

- 声明式编程关注的是 “what to do”，由框架(机器)完成 “how”的过程
- 我们会在createApp传入的对象中声明需要的内容，模板template、数据data、方法methods;这样的编写代码的过程，我们称之为是**声明式编程**
- 目前Vue、React、Angular、小程序的编程模式，我们称之为**声明式编程**

二、命令式编程

- 命令式编程关注的是 “how to do”自己完成整个how的过程
- 我们每完成一个操作，都需要通过JavaScript编写一条代码，来给浏览器一个指令; 这样的编写代码的过程，我们称之为**命令式编程**
- 在早期的原生JavaScript和jQuery开发的过程中，我们都是通过这种命令式的方式在编写代码的

三、ChatGPT

声明式编程和命令式编程是两种不同的编程范式。

在命令式编程中，程序员需要编写一系列指令，以告诉计算机如何执行任务。程序员需要控制程序的每一个步骤，包括控制流程和修改变量的值。在命令式编程中，程序员需要关注“怎么做”，而不是“做什么”。

在声明式编程中，程序员需要描述目标，而不是指定一系列指令。程序员只需要告诉计算机“做什么”，而不需要关心“怎么做”。在声明式编程中，程序员需要描述目标的状态，而不是控制状态的变化。

Vue是一个流行的声明式编程框架，它使用模板语法来声明视图的结构和行为。Vue框架提供了一系列组件和指令，以帮助程序员描述视图的行为。例如，下面的Vue代码使用v-for指令来循环渲染一个列表：

```vue
<template>
  <ul>
    <li v-for="item in items">{{ item }}</li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      items: ['item 1', 'item 2', 'item 3']
    }
  }
}
</script>
```

在这个例子中，程序员只需要声明一个列表，并使用v-for指令来告诉Vue如何循环渲染这个列表。Vue会自动处理循环和渲染过程，而程序员不需要控制这个过程的每一个步骤。

相比之下，JavaScript是一种命令式编程语言，程序员需要编写一系列指令来控制程序的行为。例如，下面的JavaScript代码使用循环来渲染一个列表：

```js
const items = ['item 1', 'item 2', 'item 3'];
const ul = document.createElement('ul');
for (let i = 0; i < items.length; i++) {
  const li = document.createElement('li');
  li.textContent = items[i];
  ul.appendChild(li);
}
document.body.appendChild(ul);
```

在这个例子中，程序员需要编写一系列指令来创建列表元素、渲染文本内容，并将元素添加到DOM树中。程序员需要控制每一个步骤，以确保列表被正确渲染。

## 说说什么是Options API？

Options API是Vue.js框架的一种API，用于在Vue组件中定义和访问选项（options）。

Vue组件是Vue.js应用程序的基本构建块。每个组件都可以具有自己的选项，例如数据（data）、计算属性（computed）、生命周期钩子（lifecycle hooks）等。Options API允许开发人员在组件定义中声明这些选项，并在组件实例中访问它们。

**options api的data详解**

- data必须是一个函数, 函数会返回一个对象( 在Vue3.x的时候)
- data返回的对象, 会被Vue进行劫持(放到响应式系统中),     所以data的数据发生改变时, 界面会重新渲染

**options api的methods详解**

- methods属性是一个对象 -> 定义很多方法 -> 这些方法可以绑定到模板上

- 在该方法中，我们可以使用**this关键字**来直接访问到**data中返回的对象的属性**

- 里面函数不能是箭头函数:

- - 如果是箭头函数,因为箭头函数不绑定this,所以它会在上层作用域中查找this,      查找到this-->window

## Vue事件绑定如何传递参数？如何传递event参数？

情况一：如果该方法不需要额外参数，那么方法后的()可以不添加。

- 如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去

情况二：如果需要同时传入某个参数，同时需要event时，可以通过**$event**传入事件。

```html
<!-- 1.默认传递event对象 -->
<button @click="btnClick">按钮1</button>
<!-- 2.只传递自己的参数 -->
<button @click="btnClick2('hello',1111)">按钮2</button>
<!-- data里的变量 -->
<button @click="btnClick3(info,name)">按钮2</button>
<!-- 3.传递自己的参数和event对象 -->
<!-- 在模板中想要明确的获取event对象: $event -->
<button @click="btnClick4('哈哈哈哈',$event)">按钮3</button>
```

## v-if和v-show有什么区别？

**⾸先，在⽤法上的区别：**

- v-show是不⽀持template；
- v-show不可以和v-else⼀起使⽤；

**其次，本质的区别：**

- v-show元素⽆论是否需要显示到浏览器上，它的DOM实际都是有存在的，只是通过CSS的display
- 属性来进⾏切换；
- v-if当条件为false时，其对应的原⽣压根不会被渲染到DOM中；

**开发中如何进⾏选择呢？**

- 如果我们的原⽣需要在显示和隐藏之间频繁的切换，那么使⽤v-show；
- 如果不会频繁的发⽣切换，那么使⽤v-if；

**手段**：v-if是动态的向DOM树内添加或者删除DOM元素；v-show是通过设置DOM元素的display样式属性控制显隐；

**编译过程**：v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件；v-show只是简单的基于css切换；

**编译条件**：v-if是惰性的，如果初始条件为假，则什么也不做；只有在条件第一次变为真时才开始局部编译; v-show是在任何条件下，无论首次条件是否为真，都被编译，然后被缓存，而且DOM元素保留；

**性能消耗**：v-if有更高的切换消耗；v-show有更高的初始渲染消耗；

**使用场景**：v-if适合运营条件不大可能改变；v-show适合频繁切换。

## v-if、v-show、v-html 的原理

v-if会调用addIfCondition方法，生成vnode的时候会忽略对应节点，render的时候就不会渲染；

v-show会生成vnode，render的时候也会渲染成真实节点，只是在render过程中会在节点的属性中修改show属性值，也就是常说的display；

v-html会先移除节点下的所有节点，调用html方法，通过addProp添加innerHTML属性，归根结底还是设置innerHTML为v-html的值。

## v-if和v-for优先级

在Vue中，v-if和v-for的优先级是不同的。

v-for具有更高的优先级，因此在一个元素上同时使用v-if和v-for时，v-for会优先执行，即先根据数据生成循环列表，然后再根据v-if的条件决定是否显示每个循环中的元素。

这意味着，如果在同一个元素上同时使用v-if和v-for，并且v-if的条件为false，则该元素将不会渲染，即使它在v-for的循环列表中。而如果v-if的条件为true，则该元素将会被渲染，并且根据v-for生成的循环列表来重复显示。

例如，考虑以下代码片段：

```html
<div v-for="item in items" v-if="item.active">{{ item.name }}</div>
```

在这个例子中，v-for指令将生成一个循环列表，然后v-if指令将决定是否显示循环中的每个元素。只有当item.active为true时，该元素才会被渲染并显示。

需要注意的是，在某些情况下，v-if和v-for可能会互相影响，例如当v-if指令中使用了一个耗时的计算属性时，会影响v-for循环的性能。在这种情况下，应该尽可能地将计算属性移动到父组件中，以避免不必要的计算和重复渲染。

## v-for中的key有什么作用？

在Vue的v-for指令中，为每个v-for循环生成的元素指定一个唯一的key值，可以帮助Vue在更新DOM时更有效地识别出哪些元素是新增、哪些元素是更新、哪些元素是删除。

这样可以避免不必要的DOM操作，提高应用程序的性能。如果没有指定key值，则Vue将使用默认的算法进行处理，这可能会导致不必要的DOM操作和性能下降。

**有key的操作:**

- 根据key找到之前的VNode进行复用;
- 没有VNode可以复用, 再创建新的VNode

**没有key的操作:**

- diff算法, 后续VNode复用性就不强

VNode是Vue内部用于表示虚拟DOM元素的数据结构，它是一个JavaScript对象。在Vue中，当我们定义一个template元素时，Vue会将其解析为一棵VNode树，然后通过该树构建虚拟DOM。

虚拟DOM是一个轻量级的JavaScript对象，它与真实DOM具有相同的层次结构，并存储了元素的所有信息。通过使用虚拟DOM，Vue可以在不直接操作真实DOM的情况下，快速地更新视图并提高性能。

**虚拟DOM的作用有两个方面：**

第一，它方便进行diff算法，因为它可以轻松比较两个VNode树之间的差异，并仅更新必要的部分。

第二，它方便进行跨平台，因为虚拟DOM是一个JavaScript对象，可以在不同平台上使用相同的代码进行渲染。

**VNode**

- VNode的全称是Virtual Node，也就是虚拟节点
- VNode的本质是一个JavaScript的对象
- template元素 ---> 解析成 VNode --->     转换为真实DOM元素

**虚拟DOM**

- template元素--->一个个VNode虚拟节点--->VNode Tree -->虚拟DOM--->真实DOM
- 作用
- 方便进行diff算法
- 方便进行跨平台

## 什么是虚拟DOM？

虚拟 DOM（Virtual DOM）是一种虚拟的、轻量级的、以 JavaScript 对象为基础的 DOM 表示形式。Vue 3.0 使用虚拟 DOM 来管理组件的更新和渲染。

Vue 3.0 的虚拟 DOM 基于 Snabbdom 库，它的核心思想是通过比较新旧两个虚拟 DOM 树之间的差异来进行高效的 DOM 更新。当组件的数据发生变化时，Vue 3.0 会先创建一个新的虚拟 DOM 树，然后通过 diff 算法比较新旧两个虚拟 DOM 树的差异，最后只更新真正需要更新的部分，从而避免不必要的 DOM 操作，提高性能和渲染效率。

Vue 3.0 的虚拟 DOM 不仅可以减少 DOM 操作的次数，还可以将 DOM 操作的批处理，优化渲染性能，同时也提高了开发效率，因为 Vue 3.0 不需要直接操作 DOM，而是通过操作虚拟 DOM 来进行组件的更新和渲染。

总之，虚拟 DOM 是 Vue 3.0 中一个非常重要的概念，它是实现高效的组件更新和渲染的核心机制之一。

## 为什么要添加一个虚拟DOM？

方便去做dif算法

方便我们的代码⭐跨平台⭐（因为他只是一个原生的JS对象，因此可以将它解析到各种平台）

- 可以将虚拟DOM转换成为真实DOM，显示在浏览器上
- 将虚拟DOM解析为移动端的button/view/image等等，直接渲染为移动端的原生控件，在移动端显示出来。
- 渲染成为桌面端的一些控件

- VR设备

## 虚拟DOM

### 1. 对虚拟DOM的理解？

从本质上来说，Virtual Dom是一个JavaScript对象，通过对象的方式来表示DOM结构。将页面的状态抽象为JS对象的形式，配合不同的渲染工具，使跨平台渲染成为可能。通过事务处理机制，将多次DOM修改的结果一次性的更新到页面上，从而有效的减少页面渲染的次数，减少修改DOM的重绘重排次数，提高渲染性能。

虚拟DOM是对DOM的抽象，这个对象是更加轻量级的对 DOM的描述。它设计的最初目的，就是更好的跨平台，比如Node.js就没有DOM，如果想实现SSR，那么一个方式就是借助虚拟DOM，因为虚拟DOM本身是js对象。 在代码渲染到页面之前，vue会把代码转换成一个对象（虚拟 DOM）。以对象的形式来描述真实DOM结构，最终渲染到页面。在每次数据发生变化前，虚拟DOM都会缓存一份，变化之时，现在的虚拟DOM会与缓存的虚拟DOM进行比较。在vue内部封装了diff算法，通过这个算法来进行比较，渲染时修改改变的变化，原先没有发生改变的通过原先的数据进行渲染。

另外现代前端框架的一个基本要求就是无须手动操作DOM，一方面是因为手动操作DOM无法保证程序性能，多人协作的项目中如果review不严格，可能会有开发者写出性能较低的代码，另一方面更重要的是省略手动DOM操作可以大大提高开发效率。

### 2. 虚拟DOM的解析过程

虚拟DOM的解析过程：

- 首先对将要插入到文档中的 DOM 树结构进行分析，使用 js 对象将其表示出来，比如一个元素对象，包含 TagName、props 和 Children 这些属性。然后将这个 js 对象树给保存下来，最后再将 DOM 片段插入到文档中。
- 当页面的状态发生改变，需要对页面的 DOM 的结构进行调整的时候，首先根据变更的状态，重新构建起一棵对象树，然后将这棵新的对象树和旧的对象树进行比较，记录下两棵树的的差异。
- 最后将记录的有差异的地方应用到真正的 DOM 树中去，这样视图就更新了。

### 3. 为什么要用虚拟DOM

**（1）保证性能下限，在不进行手动优化的情况下，提供过得去的性能** 看一下页面渲染的流程：**解析HTML -> 生成DOM -> 生成 CSSOM -> Layout -> Paint -> Compiler** 下面对比一下修改DOM时真实DOM操作和Virtual DOM的过程，来看一下它们重排重绘的性能消耗∶

- 真实DOM∶ 生成HTML字符串＋重建所有的DOM元素
- 虚拟DOM∶ 生成vNode+ DOMDiff＋必要的dom更新

Virtual DOM的更新DOM的准备工作耗费更多的时间，也就是JS层面，相比于更多的DOM操作它的消费是极其便宜的。尤雨溪在社区论坛中说道∶ 框架给你的保证是，你不需要手动优化的情况下，依然可以给你提供过得去的性能。 **（2）跨平台** Virtual DOM本质上是JavaScript的对象，它可以很方便的跨平台操作，比如服务端渲染、uniapp等。

### 4. 虚拟DOM真的比真实DOM性能好吗

- 首次渲染大量DOM时，由于多了一层虚拟DOM的计算，会比innerHTML插入慢。
- 正如它能保证性能下限，在真实DOM操作的时候进行针对性的优化时，还是更快的。

### 5. DIFF算法的原理

在新老虚拟DOM对比时：

- 首先，对比节点本身，判断是否为同一节点，如果不为相同节点，则删除该节点重新创建节点进行替换
- 如果为相同节点，进行patchVnode，判断如何对该节点的子节点进行处理，先判断一方有子节点一方没有子节点的情况(如果新的children没有子节点，将旧的子节点移除)
- 比较如果都有子节点，则进行updateChildren，判断如何对这些新老节点的子节点进行操作（diff核心）。
- 匹配时，找到相同的子节点，递归比较子节点

在diff中，只对同层的子节点进行比较，放弃跨级的节点比较，使得时间复杂从O(n3)降低值O(n)，也就是说，只有当新旧children都为多个子节点时才需要用核心的Diff算法进行同层级比较。

### 6. Vue中key的作用

vue 中 key 值的作用可以分为两种情况来考虑：

- 第一种情况是 v-if 中使用 key。由于 Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。因此当使用 v-if 来实现元素切换的时候，如果切换前后含有相同类型的元素，那么这个元素就会被复用。如果是相同的 input 元素，那么切换前后用户的输入不会被清除掉，这样是不符合需求的。因此可以通过使用 key 来唯一的标识一个元素，这个情况下，使用 key 的元素不会被复用。这个时候 key 的作用是用来标识一个独立的元素。
- 第二种情况是 v-for 中使用 key。用 v-for 更新已渲染过的元素列表时，它默认使用“就地复用”的策略。如果数据项的顺序发生了改变，Vue 不会移动 DOM 元素来匹配数据项的顺序，而是简单复用此处的每个元素。因此通过为每个列表项提供一个 key 值，来以便 Vue 跟踪元素的身份，从而高效的实现复用。这个时候 key 的作用是为了高效的更新渲染虚拟 DOM。

key 是为 Vue 中 vnode 的唯一标记，通过这个 key，diff 操作可以更准确、更快速

- 更准确：因为带 key 就不是就地复用了，在 sameNode 函数a.key === b.key对比中可以避免就地复用的情况。所以会更加准确。
- 更快速：利用 key 的唯一性生成 map 对象来获取对应节点，比遍历方式更快

### 7. 为什么不建议用index作为key?

使用index 作为 key和没写基本上没区别，因为不管数组的顺序怎么颠倒，index 都是 0, 1, 2...这样排列，导致 Vue 会复用错误的旧子节点，做很多额外的工作。

## 讲一下MVVM

一、MVVM是什么：

MVVM是一种设计模式，它将用户界面(UI)与应用程序数据和逻辑分离开来，通过中间的ViewModel来协调UI和数据之间的交互。

二、MVVM的三个组成部分：

- Model：数据层，用于管理应用程序的数据和业务逻辑。
- View：视图层，用于显示数据和接收用户交互。
- ViewModel：连接View和Model的中间层，它通过数据绑定机制将数据从Model传递到View，同时监听View的用户交互事件，将用户交互事件转化为对Model的数据操作。

三、作用：

在MVVM中，数据绑定是一个非常重要的概念。它使得ViewModel和View之间的数据同步变得非常容易和自然。当ViewModel中的数据发生变化时，View会自动更新，而当用户在View中进行操作时，ViewModel中的数据也会自动更新。这种自动化的数据绑定使得开发者能够更专注于业务逻辑的实现，而不需要过多地关注UI和数据之间的关系。

MVVM常常与现代前端框架如Vue.js、Angular和React等联系在一起。这些框架提供了非常强大的数据绑定和组件化的功能，使得开发者能够更轻松地实现MVVM模式。同时，这些框架还提供了很多工具和技术来优化应用程序的性能、可维护性和可扩展性，使得开发者能够更加高效地开发出高质量的应用程序。

## MVVM的优缺点

MVVM（Model-View-ViewModel）是一种软件架构模式，它将应用程序分为三个主要部分：模型、视图和视图模型。下面是MVVM的优缺点：

一、优点：

- 分离关注点：MVVM能够有效地将视图与应用程序的其余部分分离，从而实现更好的关注点分离，使应用程序更易于维护和扩展。
- 可测试性：MVVM通过使代码更容易测试，提高了代码质量和可靠性。
- 可重用性：MVVM提倡代码的重用，减少了代码冗余，使得开发更加高效。
- 双向数据绑定：MVVM具有双向数据绑定的特性，能够自动更新视图和模型之间的数据，减少了开发人员的代码量。

二、缺点：

- Bug很难被调试：因为使⽤双向绑定的模式，当你看到界⾯异常了，有可能是你View的代码有Bug，也可能是Model的代码有问题。数据绑定使得⼀个位置的Bug被快速传递到别的位置，要定位原始出问题的地⽅就变得不那么容易了。另外，数据绑定的声明是指令式地写在View的模版当中的，这些内容是没办法去打断点debug的
- 维护的成本较⾼：对于⼤型的图形应⽤程序，视图状态较多，ViewModel的构建和维护的成本都会⽐较⾼。
- 数据绑定的复杂性：双向数据绑定是MVVM的一个优点，但也可能增加开发人员的复杂性，因为他们需要确保数据绑定正确且可靠。
- 常规需求开发复杂性增加：当MVVM被应用于需要频繁进行数据绑定的大型应用程序时，由于视图模型的引入，开发复杂性可能会增加。

## Vue 全家桶以及 MVVM 思想

⭐实际项目中，如何运用 Vue 全家桶以及 MVVM 思想来提升开发效率？请结合具体项目案例谈谈您的实践经验。

Vue全家桶包含了Vue.js、Vue Router、Vuex和Vue CLI，是一个完整的前端开发框架。MVVM是一种前端架构模式，指的是Model-View-ViewModel模式。在Vue中，使用MVVM模式能够使前端开发更加规范和高效。

下面是我在实践中使用Vue全家桶和MVVM模式的一些经验总结：

1. 使用Vue.js提升开发效率 Vue.js是一个高效、灵活的前端框架，可以快速开发单页面应用程序（SPA）。使用Vue.js能够有效地提升开发效率，因为它提供了许多方便的功能和组件。例如，Vue.js可以通过指令实现数据绑定，让开发者更容易地实现响应式界面。同时，Vue.js还提供了很多可复用的组件，如路由组件和表单组件等，能够加速开发进程。在实际项目中，我们通常使用Vue.js来构建前端界面和交互，通过调用API和后端通信。
2. 使用Vue Router实现路由控制 Vue Router是一个官方的路由管理工具，能够帮助我们实现SPA的路由控制。在项目中，使用Vue Router能够使页面之间的跳转更加便捷和可控。例如，在管理后台系统中，使用Vue Router能够实现左侧菜单栏和主内容区的联动，让用户更加方便地访问不同的页面。在实践中，我们通常将Vue Router集成到项目中，通过配置路由表和使用路由守卫来实现路由控制。
3. 使用Vuex管理全局状态 Vuex是一个官方的状态管理工具，能够帮助我们实现全局状态管理。在项目中，使用Vuex能够使状态管理更加规范和高效。例如，在电商网站中，使用Vuex能够方便地管理购物车状态和订单状态。在实践中，我们通常将Vuex集成到项目中，通过定义state、mutation、action和getter等来管理全局状态。
4. 采用MVVM模式提升代码质量 MVVM模式是一种前端架构模式，能够有效地提升代码质量和可维护性。在Vue中，采用MVVM模式能够更好地组织代码和逻辑。在实践中，我们通常将数据和逻辑抽象成ViewModel，然后通过Vue.js来实现View与ViewModel的绑定。例如，在一个日历应用中，ViewModel负责处理日历数据和逻辑，View负责展示日历。通过MVVM模式，能够更好地解耦业务逻辑和界面展示，提高代码的可维护性，同时也使得代码更易于测试和重构。

举个实际项目案例，我曾经参与开发一个在线教育平台的前端项目，我们采用了Vue全家桶和MVVM模式。在项目中，我们使用了Vue.js来构建界面和交互，通过调用后端API实现数据交互。同时，我们也使用了Vue Router来实现路由控制，让用户能够方便地访问不同的页面。我们还使用了Vuex来管理全局状态，例如用户信息和购物车状态。最重要的是，我们采用了MVVM模式来实现业务逻辑和界面展示的分离，提高了代码的可维护性和可测试性。

在项目中，我们将数据和逻辑抽象成ViewModel，然后通过Vue.js来实现View与ViewModel的绑定。例如，在课程详情页中，ViewModel负责处理课程信息和逻辑，View负责展示课程信息。通过MVVM模式，能够更好地解耦业务逻辑和界面展示，让我们能够更加专注于业务逻辑的实现。同时，也使得代码更易于维护和测试，让项目开发更加高效和可靠。

## 写一个简单的 MVVM 框架

写一个简单的 MVVM 框架，可以简要介绍下您的实现思路和遇到的挑战吗？

一、MVVM框架的实现思路：

MVVM框架的核心是数据绑定。我们可以通过监听数据的变化来自动更新视图，并且也可以通过视图的操作来自动更新数据。实现MVVM框架的关键在于如何实现数据绑定。

二、在实现MVVM框架时，可以通过以下步骤来实现数据绑定：

1. 定义一个Observer对象，用来监听数据变化。
2. 定义一个Compile对象，用来解析视图模板并进行数据绑定。
3. 定义一个Watcher对象，用来更新视图。
4. 定义一个MVVM对象，将Observer、Compile和Watcher对象组合在一起。
5. 在MVVM对象中，通过Observer对象监听数据变化，并且通过Compile对象将模板中的表达式进行解析和绑定。Watcher对象负责更新视图。

三、遇到的挑战：

实现MVVM框架的过程中，最大的挑战在于数据绑定的实现。数据绑定需要监听数据变化，并且在数据变化时自动更新视图。实现数据绑定的方式有很多种，比如通过Object.defineProperty方法实现数据劫持，也可以通过ES6中的Proxy实现数据劫持。在实现数据绑定的过程中，需要注意内存泄漏的问题，避免引起性能问题。此外，在解析模板和绑定数据时，也需要注意性能问题，避免造成页面卡顿或渲染延迟的问题。

四、总结：

MVVM框架的实现思路主要是通过数据绑定来实现视图自动更新。在实现MVVM框架时，需要注意数据绑定的实现方式和性能问题，避免引起内存泄漏和性能问题。

## MVVM、MVC、MVP的区别

MVC、MVP 和 MVVM 是三种常见的软件架构设计模式，主要通过分离关注点的方式来组织代码结构，优化开发效率。

在开发单页面应用时，往往一个路由页面对应了一个脚本文件，所有的页面逻辑都在一个脚本文件里。页面的渲染、数据的获取，对用户事件的响应所有的应用逻辑都混合在一起，这样在开发简单项目时，可能看不出什么问题，如果项目变得复杂，那么整个文件就会变得冗长、混乱，这样对项目开发和后期的项目维护是非常不利的。

（1）MVC

MVC 通过分离 Model、View 和 Controller 的方式来组织代码结构。其中 View 负责页面的显示逻辑，Model 负责存储页面的业务数据，以及对相应数据的操作。并且 View 和 Model 应用了观察者模式，当 Model 层发生改变的时候它会通知有关 View 层更新页面。Controller 层是 View 层和 Model 层的纽带，它主要负责用户与应用的响应操作，当用户与页面产生交互的时候，Controller 中的事件触发器就开始工作了，通过调用 Model 层，来完成对 Model 的修改，然后 Model 层再去通知 View 层更新。

![image-20230430234641312](E:\coder\09_OneNote\image\image-20230430234641312.png)

（2）MVVM

MVVM 分为 Model、View、ViewModel：

- Model代表数据模型，数据和业务逻辑都在Model层中定义；
- View代表UI视图，负责数据的展示；
- ViewModel负责监听Model中数据的改变并且控制视图的更新，处理用户交互操作；

Model和View并无直接关联，而是通过ViewModel来进行联系的，Model和ViewModel之间有着双向数据绑定的联系。因此当Model中的数据改变时会触发View层的刷新，View中由于用户交互操作而改变的数据也会在Model中同步。

这种模式实现了 Model和View的数据自动同步，因此开发者只需要专注于数据的维护操作即可，而不需要自己操作DOM。

![image-20230430234646719](E:\coder\09_OneNote\image\image-20230430234646719.png)

（3）MVP

MVP 模式与 MVC 唯一不同的在于 Presenter 和 Controller。在 MVC 模式中使用观察者模式，来实现当 Model 层数据发生变化的时候，通知 View 层的更新。这样 View 层和 Model 层耦合在一起，当项目逻辑变得复杂的时候，可能会造成代码的混乱，并且可能会对代码的复用性造成一些问题。MVP 的模式通过使用 Presenter 来实现对 View 层和 Model 层的解耦。MVC 中的Controller 只知道 Model 的接口，因此它没有办法控制 View 层的更新，MVP 模式中，View 层的接口暴露给了 Presenter 因此可以在 Presenter 中将 Model 的变化和 View 的变化绑定在一起，以此来实现 View 和 Model 的同步更新。这样就实现了对 View 和 Model 的解耦，Presenter 还包含了其他的响应逻辑。

## nextTick是什么？

在 Vue.js 中，nextTick 是一个函数，它用于在下一个 DOM 更新周期之后执行回调函数。这个函数接收一个回调函数作为参数，并将这个回调函数放入队列中，等待下一次 DOM 更新周期之后执行。

Vue.js 中使用 nextTick 函数的主要场景是在数据变化后立即操作 DOM。由于 Vue.js 的数据响应式系统是异步的，即数据变化后需要等待一段时间才会更新 DOM，如果需要在数据更新后立即操作 DOM，就需要使用 nextTick 函数来等待 DOM 更新完成后再执行操作。

> 简而言之：在 Vue.js 中，nextTick 函数用于在下一个 DOM 更新周期之后执行回调函数，主要用于在数据变化后立即操作 DOM，等待 DOM 更新完成后再执行操作。

例如，在下面的代码中，当点击按钮时，使用 nextTick 函数更新 DOM 中的文本内容：

```vue
<template>
  <div>
    <p>{{ message }}</p>
    <button @click="updateMessage">Update Message</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: 'Hello, world!'
    }
  },
  methods: {
    updateMessage() {
      this.message = 'Updated message'
      this.$nextTick(() => {
        // DOM 更新完成后执行操作
        console.log('DOM updated')
      })
    }
  }
}
</script>
```

在上述代码中，当点击按钮时，会将 message 数据更新为 'Updated message'，然后调用 nextTick 函数，在 DOM 更新完成后执行回调函数，输出 'DOM updated'。这样就可以确保操作 DOM 的代码在数据更新后执行，而不是在更新之前执行，从而避免因为 DOM 更新延迟导致的错误。

## $nextTick 原理及作用

Vue 的 nextTick 其本质是对 JavaScript 执行原理 EventLoop 的一种应用。

nextTick 的核心是利用了如 Promise 、MutationObserver、setImmediate、setTimeout的原生 JavaScript 方法来模拟对应的微/宏任务的实现，本质是为了利用 JavaScript 的这些异步回调任务队列来实现 Vue 框架中自己的异步回调队列。

nextTick 不仅是 Vue 内部的异步队列的调用方法，同时也允许开发者在实际项目中使用这个方法来满足实际应用中对 DOM 更新数据时机的后续逻辑处理

nextTick 是典型的将底层 JavaScript 执行原理应用到具体案例中的示例，引入异步更新队列机制的原因∶

- 如果是同步更新，则多次对一个或多个属性赋值，会频繁触发 UI/DOM 的渲染，可以减少一些无用渲染
- 同时由于 VirtualDOM 的引入，每一次状态发生变化后，状态变化的信号会发送给组件，组件内部使用 VirtualDOM 进行计算得出需要更新的具体的 DOM 节点，然后对 DOM 进行更新操作，每次更新状态后的渲染过程需要更多的计算，而这种无用功也将浪费更多的性能，所以异步渲染变得更加至关重要

Vue采用了数据驱动视图的思想，但是在一些情况下，仍然需要操作DOM。有时候，可能遇到这样的情况，DOM1的数据发生了变化，而DOM2需要从DOM1中获取数据，那这时就会发现DOM2的视图并没有更新，这时就需要用到了`nextTick`了。

由于Vue的DOM操作是异步的，所以，在上面的情况中，就要将DOM2获取数据的操作写在`$nextTick`中。

```javascript
this.$nextTick(() => {    // 获取数据的操作...})
```

所以，在以下情况下，会用到nextTick：

- 在数据变化后执行的某个操作，而这个操作需要使用随数据变化而变化的DOM结构的时候，这个操作就需要方法在`nextTick()`的回调函数中。
- 在vue生命周期中，如果在created()钩子进行DOM操作，也一定要放在`nextTick()`的回调函数中。

因为在created()钩子函数中，页面的DOM还未渲染，这时候也没办法操作DOM，所以，此时如果想要操作DOM，必须将操作的代码放在`nextTick()`的回调函数中。

## Vue中如何做样式穿透

在 Vue 3.0 中，样式穿透使用 `::v-deep` 代替了 Vue 2.x 中的 `/deep/` 或 `>>>`。

`::v-deep` 用于将样式规则应用于子组件中的所有元素，包括嵌套子组件中的元素。在使用 `::v-deep` 时，需要在样式规则前添加该伪类选择器，如下所示：

```css
/* 在组件中使用 ::v-deep */
.my-component ::v-deep h1 {
  color: red;
}
```

上述代码将将应用于   .my-component   组件中所有嵌套子组件的   h1   元素。

在 Vue 3.0 中，`::v-deep` 可以被简写为 `:deep`，虽然在 Vue 3.0 中可以使用 `:deep` 来进行样式穿透，但是由于该语法已经被弃用并不推荐使用，建议尽可能地使用 `::v-deep` 来进行样式穿透，以保证代码的可读性和可维护性。

除了 `::v-deep`，Vue 3.0 还提供了 `::slotted()` 伪类选择器，用于在父组件中应用样式到插槽内容中的元素，例如：

```css
/* 在父组件中使用 ::slotted() */
.parent ::slotted(span) {
  color: red;
}
```

上述代码将应用于 `.parent` 组件中插槽内容中的所有 `span` 元素。

需要注意的是，样式穿透虽然可以解决一些特定的问题，但是应该尽可能地避免使用。使用样式穿透可能会导致样式的不可预测性和难以维护，因此应该优先考虑其他解决方案，如使用 props 和事件等机制进行组件间通信。

## Vue 中给 data 中的对象属性添加一个新的属性时会发生什么？如何解决？

```javascript
<template> 
   <div>
      <ul>
         <li v-for="value in obj" :key="value"> {{value}} </li> 
      </ul> 
      <button @click="addObjB">添加 obj.b</button> 
   </div>
</template>

<script>
    export default { 
       data () { 
          return { 
              obj: { 
                  a: 'obj.a' 
              } 
          } 
       },
       methods: { 
          addObjB () { 
              this.obj.b = 'obj.b' 
              console.log(this.obj) 
          } 
      }
   }
</script>
```

点击 button 会发现，obj.b 已经成功添加，但是视图并未刷新。这是因为在Vue实例创建时，obj.b并未声明，因此就没有被Vue转换为响应式的属性，自然就不会触发视图的更新，这时就需要使用Vue的全局 api **$set()：**

$set() 方法接受三个参数，第一个参数是目标对象，第二个参数是要添加的属性名，第三个参数是要添加的属性值。

```javascript
addObjB () (
   this.$set(this.obj, 'b', 'obj.b')
   console.log(this.obj)
}
```

$set()方法相当于手动的去把obj.b处理成一个响应式的属性，此时视图也会跟着改变了。

## Vue中封装的数组方法有哪些，其如何实现页面更新

在 Vue 中，可以使用以下数组方法来修改响应式数组，并保证页面可以自动更新：

1. `push()` - 在数组末尾添加一个或多个元素。
2. `pop()` - 删除并返回数组的最后一个元素。
3. `shift()` - 删除并返回数组的第一个元素。
4. `unshift()` - 在数组的开头添加一个或多个元素。
5. `splice()` - 从数组中删除元素并用新元素替换它们。
6. `sort()` - 对数组元素进行排序。
7. `reverse()` - 颠倒数组中元素的顺序。

这些方法都可以自动触发 Vue 的响应式机制来更新视图。

例如，如果您使用 `push()` 方法向响应式数组中添加新元素，Vue 会自动检测到更改，并在视图中添加新的元素。

```
this.items.push('new item')
```

这将在响应式数组中添加一个新元素，并自动更新页面中的视图。

类似地，如果您使用 `splice()` 方法来从数组中删除一个元素，Vue 也会自动检测到更改并更新视图。

```
this.items.splice(1, 1)
```

这将从数组中删除索引为 1 的元素，并自动更新页面中的视图。

> 总的来说，Vue 会在响应式数组上劫持这些数组方法，从而能够检测到这些数组的更改并触发相应的视图更新。

那Vue是如何实现让这些数组方法实现元素的实时更新的呢，下面是Vue中对这些方法的封装：

```javascript
// 缓存数组原型
const arrayProto = Array.prototype;
// 实现 arrayMethods.__proto__ === Array.prototype
export const arrayMethods = Object.create(arrayProto);
// 需要进行功能拓展的方法
const methodsToPatch = [
  "push",
  "pop",
  "shift",
  "unshift",
  "splice",
  "sort",
  "reverse"
];

/**
 * Intercept mutating methods and emit events
 */
methodsToPatch.forEach(function(method) {
  // 缓存原生数组方法
  const original = arrayProto[method];
  def(arrayMethods, method, function mutator(...args) {
    // 执行并缓存原生数组功能
    const result = original.apply(this, args);
    // 响应式处理
    const ob = this.__ob__;
    let inserted;
    switch (method) {
    // push、unshift会新增索引，所以要手动observer
      case "push":
      case "unshift":
        inserted = args;
        break;
      // splice方法，如果传入了第三个参数，也会有索引加入，也要手动observer。
      case "splice":
        inserted = args.slice(2);
        break;
    }
    // 
    if (inserted) ob.observeArray(inserted);// 获取插入的值，并设置响应式监听
    // notify change
    ob.dep.notify();// 通知依赖更新
    // 返回原生数组方法的执行结果
    return result;
  });
});
```

简单来说就是，重写了数组中的那些原生方法，首先获取到这个数组的__ob__，也就是它的Observer对象，如果有新的值，就调用observeArray继续对新的值观察变化（也就是通过`target__proto__ == arrayMethods`来改变了数组实例的型），然后手动调用notify，通知渲染watcher，执行update。

## diff算法

diff 算法是一种通过比较新旧两个虚拟 DOM 树之间的差异，最终只更新真正需要更新的部分来进行高效的 DOM 更新的算法。

Vue 3.0 中使用的 diff 算法是基于 Snabbdom 库的。它的核心思想是将树形结构转化为列表结构，通过遍历列表来比较新旧两个虚拟 DOM 树之间的差异。

具体来说，Snabbdom 将 VNode 树中的每个节点转化为一个唯一的 key，然后将它们放到一个列表中进行遍历。遍历过程中，Snabbdom 会比较新旧两个列表之间的差异，然后只更新需要更新的部分。

在比较新旧两个列表之间的差异时，Snabbdom 采用了四个步骤：

1. 首先比较列表的头部，如果相同，则继续比较下一个节点。
2. 如果头部不同，那么就比较尾部，如果相同，则继续比较下一个节点。
3. 如果头部和尾部都不同，则进行 diff 操作，寻找新列表中与旧列表中相同节点的位置，并判断是否需要更新。
4. 如果以上步骤都无法匹配，则使用 key 进行匹配。

在进行 diff 操作时，Snabbdom 会尽可能地复用节点，而不是直接替换节点，从而减少不必要的 DOM 操作，提高性能和渲染效率。

总之，diff 算法是一种通过比较新旧两个虚拟 DOM 树之间的差异来进行高效的 DOM 更新的算法，它可以优化组件更新和渲染的性能，并且是实现虚拟 DOM 的核心机制之一。

## Vue组件传值

在 Vue 中，组件之间的通信方式有以下几种：

1、父子组件通信：

父组件通过 props 向子组件传递数据，子组件通过 $emit 触发事件向父组件传递数据。

2、兄弟组件通信：

使用一个共同的父组件作为中转，将数据通过 props 和 $emit 分别传递给两个子组件。

3、跨级组件通信：

使用 provide 和 inject 选项实现跨级组件的数据传递。

4、非父子组件通信：

使用事件总线（Event Bus）、Vuex 状态管理等方式实现非父子组件之间的数据共享。

## 介绍一下SPA以及SPA有什么缺点？

**SPA是什么：**

SPA（Single Page Application），即单页应用，是一种Web应用程序的架构模式。相比于传统的多页应用，SPA 只有一个HTML页面，通过 AJAX、WebSocket 等技术，实现在一个页面中动态加载页面内容实现页面切换，从而提供更加流畅的用户体验。

**SPA的优点：**

1、用户体验好：

SPA采用了前后端分离的设计思路，通过异步加载数据、局部刷新页面等技术提高了页面加载速度，从而提供了更加流畅的用户体验。

2、开发效率高**：**

SPA采用了模块化、组件化的开发模式，可以实现代码复用，从而提高了开发效率。

3、可维护性好**：**

由于采用了前后端分离的设计思路，不同的开发人员可以专注于各自的领域，从而提高了代码的可维护性。

4、可扩展性好：

由于采用了前后端分离的设计思路，后端只需要提供API接口，前端只需要调用API接口进行开发，从而实现了前后端的松耦合，提高了可扩展性。

**SPA的缺点：**

1、初次加载时间长：

由于SPA只有一个HTML页面，需要一次性加载所有JavaScript和CSS资源，因此初次加载时间可能较长。

2、SEO不友好：

由于大部分页面内容是通过JavaScript动态生成的，而搜索引擎爬虫不支持JavaScript，因此SEO不友好。

3、内存占用高：

由于SPA在浏览器中运行，需要消耗一定的内存资源，如果页面过于复杂，会导致内存占用较高，从而影响用户体验。

4、安全性较低：

由于SPA是通过异步加载数据、局部刷新页面等技术实现的，如果没有采取相应的安全措施，可能会存在XSS等安全漏洞。

## Vue 单页应用与多页应用的区别

**概念：**

- SPA单页面应用（SinglePage Web Application），指只有一个主页面的应用，一开始只需要加载一次js、css等相关资源。所有内容都包含在主页面，对每一个功能模块组件化。单页应用跳转，就是切换相关组件，仅仅刷新局部资源。
- MPA多页面应用 （MultiPage Application），指有多个独立页面的应用，每个页面必须重复加载js、css等相关资源。多页应用跳转，需要整页资源刷新。

**区别：**

| 对比项\模式 | SPA                                                          | MPA                                                          |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 结构        | 一个主页面 许多模块的组件                                    | 许多完整的页面                                               |
| 体验        | 页面切换快,体验佳;当初次加载文 件过多时,需要做相关的调优。   | 页面切换慢,网速慢的时候,体验 尤其不好                        |
| 资源文件    | 组件公用的资源只需要加载一次                                 | 每个页面都要自己加载公用的资源                               |
| 适用场景    | 对体验度和流畅度有较高要求的应 用,不利于SEO(可借助SSR优化 SEO) | 适用于对SEO要求较高的应用                                    |
| 过渡动画    | Vue提供了transition 的封装组件, 容易实现                     | 很难实现                                                     |
| 内容更新    | 相关组件的切换,即局部更新                                    | 整体HTML的切换,费钱(重复 HTTP请求)                           |
| 路由模式    | 可以使用hash,也可以使用 history                              | 普通链接跳转                                                 |
| 数据传递    | 因为单页面,使用全局变量就好 (Vuex)                           | cookie 、 localStorage 等缓存方 案,URL参数,调用接口保存等    |
| 相关成本    | 前期开发成本较高,后期维护较为容 易                           | 前期开发成本低,后期维护就比较 麻烦,因为可能一个功能需要改很 多地方 |

Vue单页应用（Single-Page Application，SPA）与多页应用（Multiple-Page Application，MPA）有以下区别：

1. 页面切换方式不同：在SPA中，页面切换是通过JavaScript在同一页面中动态加载不同的组件和视图来实现的，而在MPA中，每个页面都是独立的HTML页面，每次切换都会重新加载整个页面。
2. 数据交互方式不同：在SPA中，数据通常是通过异步请求从API中获取，然后更新视图，而在MPA中，每个页面都是独立的，它们之间通常通过传统的同步表单提交和服务器渲染来进行数据交互。
3. 代码结构和复杂度不同：在SPA中，所有的代码都是在同一页面中运行的，因此整个应用程序的代码结构相对简单，但是单个文件的代码可能非常复杂。而在MPA中，每个页面都是独立的，因此每个页面都有自己的代码结构和复杂度。
4. 性能不同：SPA通常具有更快的初始加载速度，因为只需要加载一次应用程序和资源。但是，由于SPA将所有内容都加载到同一个页面中，可能会导致较大的初始负载和较长的加载时间。MPA则具有更快的页面加载速度，因为每个页面都是独立的，但是在初始加载时需要加载多个页面和资源。

总体而言，SPA适用于需要高交互性、较复杂视图和快速响应时间的应用程序，而MPA适用于需要页面间相对独立、交互性较低和数据交互较少的应用程序。

## XSS安全漏洞

XSS（Cross-Site Scripting）是一种安全漏洞，攻击者通过在网站输入框、URL 参数等地方注入恶意脚本代码，使用户在浏览网站时执行这些脚本代码，从而达到窃取用户信息、利用用户身份执行操作等目的。

一、XSS 攻击可以分为以下几种类型：

1. 反射型 XSS：攻击者通过构造 URL 或者发送带有恶意脚本的邮件等方式，诱导用户点击链接，在浏览器中执行恶意代码，达到攻击的目的。
2. 存储型 XSS：攻击者将恶意脚本代码存储在网站数据库中，当用户访问包含该脚本的页面时，恶意脚本将被执行，造成安全问题。
3. DOM 型 XSS：攻击者通过恶意 URL 参数或者表单提交等方式，让网站 JavaScript 代码在用户浏览器中执行恶意操作。

二、防范 XSS 攻击的方法：

1. 对用户输入进行过滤和转义，特别是在表单提交、URL 参数等输入框中。
2. 对网站的 JavaScript 代码进行安全编码，比如使用 innerText 而不是 innerHTML。
3. 对 Cookie 进行 HttpOnly 标记，防止被窃取。
4. 定期进行安全测试和漏洞扫描，及时发现和修复安全问题。

除了 XSS，常见的安全漏洞还包括 CSRF（Cross-Site Request Forgery，跨站请求伪造）、SQL 注入等，防范这些安全漏洞同样需要进行输入过滤、编码、验证等操作，同时加强系统的安全认证和权限控制。

## Computed 和 Watch 的区别

**对于Computed：**

- 它支持缓存，只有依赖的数据发生了变化，才会重新计算
- 不支持异步，当Computed中有异步操作时，无法监听数据的变化
- computed的值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data声明过，或者父组件传递过来的props中的数据进行计算的。
- 如果一个属性是由其他属性计算而来的，这个属性依赖其他的属性，一般会使用computed
- 如果computed属性的属性值是函数，那么默认使用get方法，函数的返回值就是属性的属性值；在computed中，属性有一个get方法和一个set方法，当数据发生变化时，会调用set方法。

**对于Watch：**

- 它不支持缓存，数据变化时，它就会触发相应的操作
- 支持异步监听
- 监听的函数接收两个参数，第一个参数是最新的值，第二个是变化之前的值
- 当一个属性发生变化时，就需要执行相应的操作
- 监听数据必须是data中声明的或者父组件传递过来的props中的数据，当发生变化时，会触发其他操作，函数有两个的参数：
  - immediate：组件加载立即触发回调函数
  - deep：深度监听，发现数据内部的变化，在复杂数据类型中使用，例如数组中的对象发生变化。需要注意的是，deep无法监听到数组和对象内部的变化。

当想要执行异步或者昂贵的操作以响应不断的变化时，就需要使用watch。

**总结：**

- computed 计算属性 : 依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed 的值。
- watch 侦听器 : 更多的是**观察**的作用，**无缓存性**，类似于某些数据的监听回调，每当监听的数据变化时都会执行回调进行后续操作。

**运用场景：**

- 当需要进行数值计算,并且依赖于其它数据时，应该使用 computed，因为可以利用 computed 的缓存特性，避免每次获取值时都要重新计算。
- 当需要在数据变化时执行异步或开销较大的操作时，应该使用 watch，使用 watch 选项允许执行异步操作 ( 访问一个 API )，限制执行该操作的频率，并在得到最终结果前，设置中间状态。这些都是计算属性无法做到的。

## Computed 和 Methods 的区别

可以将同一函数定义为一个 method 或者一个计算属性。对于最终的结果，两种方式是相同的

**不同点：**

- computed: 计算属性是基于它们的依赖进行缓存的，只有在它的相关依赖发生改变时才会重新求值；
- method 调用总会执行该函数。

## 什么是计算属性？和method有什么区别？

计算属性和 method 都是在 Vue.js 中用于处理数据的方式

二者区别：

1. 计算属性是基于它所依赖的数据进行计算，只有在它所依赖的数据发生改变时才会重新计算，而 method 每次调用都会重新计算。
2. 计算属性是可以缓存的，只有当计算属性所依赖的数据发生改变时才会重新计算，而 method 每次调用都会重新计算，无法缓存。
3. 计算属性一般用于模板中的表达式，而 method 一般用于事件处理或复杂的逻辑计算。
4. 计算属性可以像普通属性一样使用，直接在模板中绑定，而 method 只能通过事件或指令等方式调用。

综上所述，如果需要进行简单的数据计算或者在模板中使用的数据，可以使用计算属性，如果需要进行事件处理或者复杂的逻辑计算，可以使用 method。

## 如何在Vue中侦听一个数据的改变？

Vue 提供了两种侦听器的方式：

- 通过 `watch` 函数来侦听数据的改变
- 通过计算属性（computed）来侦听数据的改变

通过 `watch` 函数来侦听数据的改变，可以监听到数据的旧值和新值。而通过计算属性来侦听数据的改变，只能监听到数据的新值。

```js
// 侦听器
watch: {
  // 1,监听message
  // 默认有两个参数:newValue,oldValue
  message(newValue, oldValue) {
    console.log("watch message ,messag发生改变");
    console.log("newValue--", newValue);
    console.log("oldValue---", oldValue);
  },
  // 2.监听info
  info(newValue, oldValue) {
    // 2.如果是对象类型, 那么拿到的是代理对象
    console.log("info--newValue", newValue);
    console.log("info--oldValue", oldValue);
    //3.获取原始对象
    // 方式一:因为代理对象可迭代
    console.log({ ...newValue });
    console.log(Vue.toRaw(newValue));
  },
},
```

侦听的选项

- deep  深度监听
- immediate   第一次渲染直接执行一次监听器

```js
// 侦听器
watch: {
  // 2.监听info
  // 默认watch监听不会进行深度监听
  // info(newValue, oldValue) {
  //   // 2.如果是对象类型, 那么拿到的是代理对象
  //   console.log("info--newValue", newValue);
  //   console.log("info--oldValue", oldValue);
  // },
  info: {
    handler(newValue, oldValue) {
      // 2.如果是对象类型, 那么拿到的是代理对象
      console.log("info--newValue", newValue);
      console.log("info--oldValue", oldValue);
      console.log(newValue === oldValue); //ture
    },
    // 深度监听
    deep: true,
    // 一开始就会立即执行一次
    immediate: true,
  },
  "info.age": function (newValue, oldValue) {
    console.log("info-age-newVAL", newValue);
    console.log("info-age-oldVAL", oldValue);
  },
},
```

## 什么是双向绑定？v-model的本质是什么？

一、双向绑定:

双向绑定是指视图（View）和模型（Model）之间的双向数据绑定。当视图（View）的数据发生改变时，模型（Model）的数据也会随之改变，反之亦然。在 Vue 中，可以使用 `v-model` 指令来实现双向绑定。

二、本质

`v-model` 的本质是一个语法糖，实际上它是一个绑定属性和事件的组合。

```
<input v-model="message" />
```

等价

```
<input :value="message" @input="message = $event.target.value" />
```

三、v-model的原理

- v-bind绑定value属性的值
- v-on绑定input事件监听到函数,函数会获取最新的值赋值到绑定的属性中

需要注意的是，在 Vue 中，双向绑定并不是万能的，它可能会导致性能问题和代码复杂性的增加。在使用 `v-model` 指令时，应该谨慎考虑是否需要使用双向绑定。如果只需要单向绑定，可以使用 `v-bind` 和事件来实现。

## v-model 可以被用在自定义组件上吗？如果可以，如何使用？

可以。v-model 实际上是一个语法糖，如：

```vue
<input v-model="searchText">
```

实际上相当于：

```vue
<input
  v-bind:value="searchText"
  v-on:input="searchText = $event.target.value"
>
```

用在自定义组件上也是同理：

```vue
<custom-input v-model="searchText">
```

相当于：

```vue
<custom-input
  v-bind:value="searchText"
  v-on:input="searchText = $event"
></custom-input>
```

显然，custom-input 与父组件的交互如下：

1. 父组件将`searchText`变量传入custom-input 组件，使用的 prop 名为`value`；
2. custom-input 组件向父组件传出名为`input`的事件，父组件将接收到的值赋值给`searchText`；

所以，custom-input 组件的实现应该类似于这样：

```vue
Vue.component('custom-input', {
  props: ['value'],
  template: `
    <input
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
    >
  `
})
```

## v-model 是如何实现的，语法糖实际是什么？

**（1）作用在表单元素上** 动态绑定了 input 的 value 指向了 messgae 变量，并且在触发 input 事件的时候去动态把 message设置为目标值：

```vue
<input v-model="sth" />
//  等同于
<input 
    v-bind:value="message" 
    v-on:input="message=$event.target.value"
>
//$event 指代当前触发的事件对象;
//$event.target 指代当前触发的事件对象的dom;
//$event.target.value 就是当前dom的value值;
//在@input方法中，value => sth;
//在:value中,sth => value;
```

**（2）作用在组件上** 在自定义组件中，v-model 默认会利用名为 value 的 prop和名为 input 的事件

**本质是一个父子组件通信的语法糖，通过prop和$.emit实现。** 因此父组件 v-model 语法糖本质上可以修改为：

```vue
<child :value="message"  @input="function(e){message = e}"></child>
```

在组件的实现中，可以通过 v-model属性来配置子组件接收的prop名称，以及派发的事件名称。 例子：

```js
// 父组件
<aa-input v-model="aa"></aa-input>
// 等价于
<aa-input v-bind:value="aa" v-on:input="aa=$event.target.value"></aa-input>

// 子组件：
<input v-bind:value="aa" v-on:input="onmessage"></aa-input>

props:{value:aa,}
methods:{
    onmessage(e){
        $emit('input',e.target.value)
    }
}
```

默认情况下，一个组件上的v-model 会把 value 用作 prop且把 input 用作 event。但是一些输入类型比如单选框和复选框按钮可能想使用 value prop 来达到不同的目的。使用 model 选项可以回避这些情况产生的冲突。js 监听input 输入框输入数据改变，用oninput，数据改变以后就会立刻出发这个事件。通过input事件把数据$emit 出去，在父组件接受。父组件设置v-model的值为input `$emit`过来的值。

## 什么是组件化开发？有什么作用？

一、组件化开发

Vue3 中的组件化开发指的是将页面拆分为多个独立的组件，每个组件都有自己的 HTML 模板、CSS 样式和 JavaScript 逻辑。

- 我们将一个完整的页面分成很多个组件；
- 每个组件都用于实现页面的一个功能块；
- 而每一个组件又可以进行细分；
- 而组件本身又可以在多个地方进行复用

二、作用

- 模块化开发：组件化开发能够让开发者更好地组织代码，将代码按照功能或模块进行划分，方便开发者进行维护和复用。
- 提高可维护性：组件化开发能够让页面更加清晰，结构更加简洁，易于维护。
- 提高可重用性：组件化开发能够让相同或类似的功能模块在不同的页面中得到重用，避免了代码的重复编写。
- 提高开发效率：组件化开发能够让多人协同开发变得更加容易，各自负责不同的组件，提高开发效率。

## Vue中注册全局组件和局部组件有什么区别？

在Vue中，注册全局组件和局部组件的主要区别是其作用域的范围和可用性。

一、作用域范围：

全局组件在整个应用程序中可用，而局部组件只在它们被注册的组件中可用。

二、可用性：

全局组件可以在任何地方使用，而局部组件只能在其父组件中使用。

三、命名冲突：

全局组件的命名必须唯一，而局部组件只需要在其父组件中唯一即可。

四、性能：

局部组件的加载速度更快，因为它们只在需要时被加载，而全局组件需要在整个应用程序中被加载。

通常来说，应该尽可能地使用局部组件，因为它们可以提高性能并且更具有封装性。只有在需要在整个应用程序中使用某个组件时才需要使用全局组件。

## 什么是Vue CLI，如何使用它创建Vue项目？

Vue CLI是一个命令行工具，用于创建和管理Vue.js项目。它提供了一系列的插件和工具，帮助开发者快速搭建一个现代化的Vue.js项目。

- Vue的脚手架,可以通过它选择项目的配置,并且创建出我们的项目
- Vue CLI已经内置了webpack相关的配置，我们不需要从零来配置

Vue CLI 的安装和使用

```bash
# 安装
npm install @vue/cli -g

# 升级
npm update @vue/cli -g

# 使用
vue create 项目的名称
```

## Vue项目目录结构中各个文件的作用

```js
my-project/
├── node_modules/      // 存放项目所需的依赖包
├── public/            // 存放静态资源文件，如图片、字体等
│   ├── favicon.ico    // 网站图标
│   └── index.html     // 网站入口文件
├── src/               // 存放源代码文件
│   ├── assets/        // 存放资源文件，如图片、字体等
│   ├── components/    // 存放组件文件
│   ├── router/        // 存放路由配置文件
│   ├── store/         // 存放Vuex状态管理相关文件
│   ├── views/         // 存放视图文件
│   ├── App.vue        // 根组件文件
│   └── main.js        // 项目入口文件
├── .browserslistrc    // 浏览器兼容性配置文件
├── .eslintrc.js       // ESLint配置文件
├── .gitignore         // Git忽略文件配置
├── babel.config.js    // Babel配置文件
├── jsconfig.json      // 给VSCode进行读取，可以给我们代码更加友好的提示
├── package-lock.json  // 项目包的锁定文件，npm install可以通过package-lock文件来检测lock中包的版本是否和package.json中一致
├── package.json       // npm配置文件，记录这你项目的名称、版本号、项目描述，也记录项目所依赖的其他库的信息和依赖库的版本号
├── README.md          // 项目说明（描述）
└── vue.config.js      // Vue的配置文件，包含了对项目的配置选项，比如配置webpack的一些参数等
```

## Vue3.0的runtime和runtime+comiple的版本区别？

在Vue 2中，我们可以选择使用不同的构建版本（runtime-only或standalone），而在Vue 3中，这种选择被进一步简化为了两个版本：runtime only和runtime + compiler。

- Runtime-only版本：只包含运行时的Vue库，代码体积更小，渲染性能更高。但它无法编译模板，需要在开发时使用手写render函数(返回h函数)或者使用单文件组件（.vue）进行开发。
- Runtime + Compiler版本：包含运行时的Vue库和模板编译器，可以在运行时动态编译模板。将template模板通过compile转换成对应的vnode节点。这种版本相对于Runtime-only版本，需要额外的编译器代码，因此体积更大，性能也稍微低一些。但是使用这个版本可以在开发时直接使用模板进行开发。

总之，如果我们使用了单文件组件，则可以使用Runtime-only版本，因为单文件组件可以在构建时进行预编译。而如果我们使用了template选项，则需要使用Runtime + Compiler版本。

在实际项目中，如果使用了类似于Vue CLI这样的工具进行构建，那么我们通常可以不用考虑这个问题，因为工具会自动选择最优的构建版本。

## slot是什么？有什么作用？原理是什么？

slot又名插槽，是Vue的内容分发机制，组件内部的模板引擎使用slot元素作为承载分发内容的出口。插槽slot是子组件的一个模板标签元素，而这一个标签元素是否显示，以及怎么显示是由父组件决定的。slot又分三类，默认插槽，具名插槽和作用域插槽。

- 默认插槽：又名匿名查抄，当slot没有指定name属性值的时候一个默认显示插槽，一个组件内只有有一个匿名插槽。
- 具名插槽：带有具体名字的插槽，也就是带有name属性的slot，一个组件可以出现多个具名插槽。
- 作用域插槽：默认插槽、具名插槽的一个变体，可以是匿名插槽，也可以是具名插槽，该插槽的不同点是在子组件渲染作用域插槽时，可以将子组件内部的数据传递给父组件，让父组件根据子组件的传递过来的数据决定如何渲染该插槽。

实现原理：当子组件vm实例化时，获取到父组件传入的slot标签的内容，存放在`vm.$slot`中，默认插槽为`vm.$slot.default`，具名插槽为`vm.$slot.xxx`，xxx 为插槽名，当组件执行渲染函数时候，遇到slot标签，使用`$slot`中的内容进行替换，此时可以为插槽传递数据，若存在数据，则可称该插槽为作用域插槽。

## scoped原理

Vue中的scoped样式是通过给样式加上`scoped`属性来实现的。其原理是通过在编译器编译Vue组件时，给每个组件的样式选择器都添加一个类似于`data-v-xxxxxxx`的唯一标识符。这个标识符是根据组件的UID生成的。

在样式被应用时，只有匹配到带有相同标识符的元素才会应用这个样式。这样就避免了样式的污染和冲突，使得组件之间的样式不会互相影响。

例如，如果我们在一个组件的样式中这样写：

```css
/* 父组件的样式 */
button {
  font-size: 16px;
}

/* 子组件的样式 */
button {
  color: red;
}
```

如果不使用`scoped`，那么父组件和子组件中的`button`样式都会被应用到页面上的所有`button`元素上。但是如果在子组件的样式中加上`scoped`，就会变成这样：

```css
/* 父组件的样式 */
button {
  font-size: 16px;
}

/* 子组件的样式 */
button[data-v-f3f3eg9] {
  color: red;
}
```

这时只有带有`data-v-f3f3eg9`属性的`button`元素才会应用子组件的样式。这个`data-v-f3f3eg9`是根据组件的UID生成的，确保了每个组件的样式是独立的，不会互相干扰。

## Vue双向绑定和单向绑定

Vue中的数据绑定可以分为单向绑定和双向绑定两种。

一、单向绑定

单向绑定（One-way Binding）是指只将数据从模型层传递到视图层的过程，当模型层的数据发生改变时，视图层会自动更新。常见的单向绑定方式有插值绑定、属性绑定和事件绑定等。

例如，在Vue中，我们可以使用插值绑定将模型层的数据显示到视图层中：

```
<div>{{ message }}</div>
```

这里的`message`就是模型层中的数据，Vue会自动将其更新到视图层中。

二、双向绑定

双向绑定（Two-way Binding）是指不仅可以将数据从模型层传递到视图层，还可以将用户在视图层中的操作同步到模型层中。当用户在视图层中修改数据时，模型层的数据也会跟着自动更新。常见的双向绑定方式有`v-model`指令。

例如，我们可以使用`v-model`指令实现表单元素和模型层数据的双向绑定：

```
<input v-model="message" />
```

这里的`message`是模型层中的数据，用户在输入框中输入时，模型层中的`message`也会随之更新。

> 总的来说：单向绑定适用于将数据从模型层传递到视图层，而双向绑定适用于将数据从模型层传递到视图层以及从视图层传递回模型层。
>
> 在实际开发中，我们需要根据具体情况选择不同的数据绑定方式。

## props和data优先级谁高？

在 Vue.js 中，props 和 data 都是用来管理组件数据的属性。其中，props 是用于接收父组件传递过来的数据，而 data 则是用于定义组件自身的数据。

在组件中，props 的优先级高于 data。这是因为 props 是用于接收父组件传递过来的数据，而父组件传递的 props 可能会覆盖组件自身的 data 中的属性。

如果组件中的 data 属性与父组件传递的 props 属性同名，那么 props 中的值会覆盖 data 中的值。这种情况下，组件中的属性优先级就是 props > data。

```
props ===> methods ===> data ===> computed ===> watch
```

举个例子，假设有一个组件定义如下：

```vue
<template>
  <div>{{ message }}</div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      default: 'Hello, World!'
    }
  },
  data() {
    return {
      message: 'Welcome to my website!'
    }
  }
}
</script>
```

在这个例子中，组件中定义了一个名为 `message` 的 props 属性和一个名为 `message` 的 data 属性。如果父组件传递了一个 `message` 值，那么它会覆盖 data 中的 `message` 值，从而在组件中显示父组件传递过来的值。如果父组件没有传递 `message` 值，那么组件中会显示 data 中的默认值。

需要注意的是，在组件内部，不应该直接修改 props 的值，因为 props 是只读的。如果需要修改组件内部的数据，应该通过修改 data 中的值来实现。

## computed、methods、watch有什么区别？

在 Vue.js 中，computed、methods 和 watch 都是用来处理组件内部的逻辑的方法，但它们的实现方式和使用场景略有不同。

一、computed

computed 是一个计算属性，用于根据其他数据属性的值计算出一个新的值。computed 属性是基于它的依赖缓存的，只有当它的相关依赖发生改变时才会重新计算，因此在模板中多次使用同一个 computed 属性，实际上只会计算一次。computed 属性返回的值可以直接在模板中使用。

computed 适合用于需要根据已有数据属性计算得出的属性，例如将字符串转换为大写字母或者将价格格式化为货币形式等。

- 它支持缓存，只有依赖的数据发生了变化，才会重新计算
- 不支持异步，当Computed中有异步操作时，无法监听数据的变化
- computed的值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data声明过，或者父组件传递过来的props中的数据进行计算的。
- 如果一个属性是由其他属性计算而来的，这个属性依赖其他的属性，一般会使用computed
- 如果computed属性的属性值是函数，那么默认使用get方法，函数的返回值就是属性的属性值；在computed中，属性有一个get方法和一个set方法，当数据发生变化时，会调用set方法。

二、methods

methods 是一个普通方法，用于定义组件中的一些逻辑或操作。每次在模板中调用方法时都会重新计算。methods 可以接收参数，并可以在方法中使用其他属性或方法。

methods 适合用于组件中的一些操作或事件处理，例如点击按钮时执行某个操作、表单提交时验证数据等。

三、watch

watch 是一个观察者，更多的是观察的作用，无缓存性，用于监听数据的变化并执行一些操作。watch 需要监听的数据发生变化时会立即执行回调函数。watch 的回调函数接收两个参数，新值和旧值。

watch 适合用于需要在数据变化时执行异步或开销较大的操作，例如请求后端接口获取数据等。

- 它不支持缓存，数据变化时，它就会触发相应的操作
- 支持异步监听
- 监听的函数接收两个参数，第一个参数是最新的值，第二个是变化之前的值
- 当一个属性发生变化时，就需要执行相应的操作
- 监听数据必须是data中声明的或者父组件传递过来的props中的数据，当发生变化时，会触发其他操作，函数有两个的参数：
  - immediate：组件加载立即触发回调函数
  - deep：深度监听，发现数据内部的变化，在复杂数据类型中使用，例如数组中的对象发生变化。需要注意的是，deep无法监听到数组和对象内部的变化。


需要注意的是，在使用这些方法时，应该根据实际情况选择适合的方式。computed 适合用于计算属性，methods 适合用于操作和事件处理，watch 适合用于监听数据的变化并执行操作。如果不确定应该使用哪种方式，可以根据具体场景进行选择。

## 过滤器的作用，如何实现一个过滤器

根据过滤器的名称，过滤器是用来过滤数据的，在Vue2.0 中使用`filters`来过滤数据，`filters`不会修改数据，而是过滤数据，改变用户看到的输出（计算属性 `computed` ，方法 `methods` 都是通过修改数据来处理数据格式的输出显示）。

**使用场景：**

- 需要格式化数据的情况，比如需要处理时间、价格等数据格式的输出 / 显示。
- 比如后端返回一个 **年月日的日期字符串**，前端需要展示为 **多少天前** 的数据格式，此时就可以用`fliters`过滤器来处理数据。

过滤器是一个函数，它会把表达式中的值始终当作函数的第一个参数。过滤器用在 插值表达式 `{{ }}` 和 `v-bind` 表达式中，然后放在操作符“ `|` ”后面进行指示。

例如，在显示金额，给商品价格添加单位：

```javascript
<li>商品价格：{{item.price | filterPrice}}</li>

 filters: {
    filterPrice (price) {
      return price ? ('￥' + price) : '--'
    }
  }
```

## 如何保存页面的当前的状态

既然是要保持页面的状态（其实也就是组件的状态），那么会出现以下两种情况：

- 前组件会被卸载
- 前组件不会被卸载

那么可以按照这两种情况分别得到以下方法：

**组件会被卸载：**

**（1）将状态存储在LocalStorage / SessionStorage**

只需要在组件即将被销毁的生命周期 `componentWillUnmount` （react）中在 LocalStorage / SessionStorage 中把当前组件的 state 通过 JSON.stringify() 储存下来就可以了。在这里面需要注意的是组件更新状态的时机。

比如从 B 组件跳转到 A 组件的时候，A 组件需要更新自身的状态。但是如果从别的组件跳转到 B 组件的时候，实际上是希望 B 组件重新渲染的，也就是不要从 Storage 中读取信息。所以需要在 Storage 中的状态加入一个 flag 属性，用来控制 A 组件是否读取 Storage 中的状态。

**优点：**

- 兼容性好，不需要额外库或工具。
- 简单快捷，基本可以满足大部分需求。

**缺点：**

- 状态通过 JSON 方法储存（相当于深拷贝），如果状态中有特殊情况（比如 Date 对象、Regexp 对象等）的时候会得到字符串而不是原来的值。（具体参考用 JSON 深拷贝的缺点）
- 如果 B 组件后退或者下一页跳转并不是前组件，那么 flag 判断会失效，导致从其他页面进入 A 组件页面时 A 组件会重新读取 Storage，会造成很奇怪的现象

**（2）路由传值**

通过 react-router 的 Link 组件的 prop —— to 可以实现路由间传递参数的效果。

在这里需要用到 state 参数，在 B 组件中通过 history.location.state 就可以拿到 state 值，保存它。返回 A 组件时再次携带 state 达到路由状态保持的效果。

**优点：**

- 简单快捷，不会污染 LocalStorage / SessionStorage。
- 可以传递 Date、RegExp 等特殊对象（不用担心 JSON.stringify / parse 的不足）

**缺点：**

- 如果 A 组件可以跳转至多个组件，那么在每一个跳转组件内都要写相同的逻辑。

**组件不会被卸载：**

**（1）单页面渲染**

要切换的组件作为子组件全屏渲染，父组件中正常储存页面状态。

**优点：**

- 代码量少
- 不需要考虑状态传递过程中的错误

**缺点：**

- 增加 A 组件维护成本
- 需要传入额外的 prop 到 B 组件
- 无法利用路由定位页面

除此之外，在Vue中，还可以是用keep-alive来缓存页面，当组件在keep-alive内被切换时组件的**activated、deactivated**这两个生命周期钩子函数会被执行 被包裹在keep-alive中的组件的状态将会被保留：

```vue
<keep-alive>
    <router-view v-if="$route.meta.keepAlive"></router-view>
</kepp-alive>
```

**router.js**

```js
{
  path: '/',
  name: 'xxx',
  component: ()=>import('../src/views/xxx.vue'),
  meta:{
    keepAlive: true // 需要被缓存
  }
},
```

## 常见的事件修饰符及其作用

- `.stop`：等同于 JavaScript 中的 `event.stopPropagation()` ，防止事件冒泡；
- `.prevent` ：等同于 JavaScript 中的 `event.preventDefault()` ，防止执行预设的行为（如果事件可取消，则取消该事件，而不停止事件的进一步传播）；
- `.capture` ：与事件冒泡的方向相反，事件捕获由外到内；
- `.self` ：只会触发自己范围内的事件，不包含子元素；
- `.once` ：只会触发一次。

## 对keep-alive的理解，它是如何实现的，具体缓存的是什么？

如果需要在组件切换的时候，保存一些组件的状态防止多次渲染，就可以使用 keep-alive 组件包裹需要保存的组件。

**（1）keep-alive**

keep-alive有以下三个属性：

- include 字符串或正则表达式，只有名称匹配的组件会被匹配；
- exclude 字符串或正则表达式，任何名称匹配的组件都不会被缓存；
- max 数字，最多可以缓存多少组件实例。

注意：keep-alive 包裹动态组件时，会缓存不活动的组件实例。

**主要流程**

1. 判断组件 name ，不在 include 或者在 exclude 中，直接返回 vnode，说明该组件不被缓存。
2. 获取组件实例 key ，如果有获取实例的 key，否则重新生成。
3. key生成规则，cid +"∶∶"+ tag ，仅靠cid是不够的，因为相同的构造函数可以注册为不同的本地组件。
4. 如果缓存对象内存在，则直接从缓存对象中获取组件实例给 vnode ，不存在则添加到缓存对象中。 5.最大缓存数量，当缓存组件数量超过 max 值时，清除 keys 数组内第一个组件。

**（2）keep-alive 的实现**

```javascript
const patternTypes: Array<Function> = [String, RegExp, Array] // 接收：字符串，正则，数组

export default {
  name: 'keep-alive',
  abstract: true, // 抽象组件，是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在父组件链中。

  props: {
    include: patternTypes, // 匹配的组件，缓存
    exclude: patternTypes, // 不去匹配的组件，不缓存
    max: [String, Number], // 缓存组件的最大实例数量, 由于缓存的是组件实例（vnode），数量过多的时候，会占用过多的内存，可以用max指定上限
  },

  created() {
    // 用于初始化缓存虚拟DOM数组和vnode的key
    this.cache = Object.create(null)
    this.keys = []
  },

  destroyed() {
    // 销毁缓存cache的组件实例
    for (const key in this.cache) {
      pruneCacheEntry(this.cache, key, this.keys)
    }
  },

  mounted() {
    // prune 削减精简[v.]
    // 去监控include和exclude的改变，根据最新的include和exclude的内容，来实时削减缓存的组件的内容
    this.$watch('include', (val) => {
      pruneCache(this, (name) => matches(val, name))
    })
    this.$watch('exclude', (val) => {
      pruneCache(this, (name) => !matches(val, name))
    })
  },
}
复制代码
```

**render函数：**

1. 会在 keep-alive 组件内部去写自己的内容，所以可以去获取默认 slot 的内容，然后根据这个去获取组件
2. keep-alive 只对第一个组件有效，所以获取第一个子组件。
3. 和 keep-alive 搭配使用的一般有：动态组件 和router-view

```javascript
render () {
  //
  function getFirstComponentChild (children: ?Array<VNode>): ?VNode {
    if (Array.isArray(children)) {
  for (let i = 0; i < children.length; i++) {
    const c = children[i]
    if (isDef(c) && (isDef(c.componentOptions) || isAsyncPlaceholder(c))) {
      return c
    }
  }
  }
  }
  const slot = this.$slots.default // 获取默认插槽
  const vnode: VNode = getFirstComponentChild(slot)// 获取第一个子组件
  const componentOptions: ?VNodeComponentOptions = vnode && vnode.componentOptions // 组件参数
  if (componentOptions) { // 是否有组件参数
    // check pattern
    const name: ?string = getComponentName(componentOptions) // 获取组件名
    const { include, exclude } = this
    if (
      // not included
      (include && (!name || !matches(include, name))) ||
      // excluded
      (exclude && name && matches(exclude, name))
    ) {
      // 如果不匹配当前组件的名字和include以及exclude
      // 那么直接返回组件的实例
      return vnode
    }

    const { cache, keys } = this

    // 获取这个组件的key
    const key: ?string = vnode.key == null
      // same constructor may get registered as different local components
      // so cid alone is not enough (#3269)
      ? componentOptions.Ctor.cid + (componentOptions.tag ? `::${componentOptions.tag}` : '')
      : vnode.key

    if (cache[key]) {
      // LRU缓存策略执行
      vnode.componentInstance = cache[key].componentInstance // 组件初次渲染的时候componentInstance为undefined

      // make current key freshest
      remove(keys, key)
      keys.push(key)
      // 根据LRU缓存策略执行，将key从原来的位置移除，然后将这个key值放到最后面
    } else {
      // 在缓存列表里面没有的话，则加入，同时判断当前加入之后，是否超过了max所设定的范围，如果是，则去除
      // 使用时间间隔最长的一个
      cache[key] = vnode
      keys.push(key)
      // prune oldest entry
      if (this.max && keys.length > parseInt(this.max)) {
        pruneCacheEntry(cache, keys[0], keys, this._vnode)
      }
    }
    // 将组件的keepAlive属性设置为true
    vnode.data.keepAlive = true // 作用：判断是否要执行组件的created、mounted生命周期函数
  }
  return vnode || (slot && slot[0])
}
复制代码
```

keep-alive 具体是通过 cache 数组缓存所有组件的 vnode 实例。当 cache 内原有组件被使用时会将该组件 key 从 keys 数组中删除，然后 push 到 keys数组最后，以便清除最不常用组件。

**实现步骤：**

1. 获取 keep-alive 下第一个子组件的实例对象，通过他去获取这个组件的组件名
2. 通过当前组件名去匹配原来 include 和 exclude，判断当前组件是否需要缓存，不需要缓存，直接返回当前组件的实例vNode
3. 需要缓存，判断他当前是否在缓存数组里面：
- 存在，则将他原来位置上的 key 给移除，同时将这个组件的 key 放到数组最后面（LRU）
- 不存在，将组件 key 放入数组，然后判断当前 key数组是否超过 max 所设置的范围，超过，那么削减未使用时间最长的一个组件的 key
1. 最后将这个组件的 keepAlive 设置为 true

**（3）keep-alive 本身的创建过程和 patch 过程**

缓存渲染的时候，会根据 vnode.componentInstance（首次渲染 vnode.componentInstance 为 undefined） 和 keepAlive 属性判断不会执行组件的 created、mounted 等钩子函数，而是对缓存的组件执行 patch 过程∶ 直接把缓存的 DOM 对象直接插入到目标元素中，完成了数据更新的情况下的渲染过程。

**首次渲染**

- 组件的首次渲染∶判断组件的 abstract 属性，才往父组件里面挂载 DOM

```javascript
// core/instance/lifecycle
function initLifecycle (vm: Component) {
  const options = vm.$options

  // locate first non-abstract parent
  let parent = options.parent
  if (parent && !options.abstract) { // 判断组件的abstract属性，才往父组件里面挂载DOM
    while (parent.$options.abstract && parent.$parent) {
      parent = parent.$parent
    }
    parent.$children.push(vm)
  }

  vm.$parent = parent
  vm.$root = parent ? parent.$root : vm

  vm.$children = []
  vm.$refs = {}

  vm._watcher = null
  vm._inactive = null
  vm._directInactive = false
  vm._isMounted = false
  vm._isDestroyed = false
  vm._isBeingDestroyed = false
}
复制代码
```

- 判断当前 keepAlive 和 componentInstance 是否存在来判断是否要执行组件 prepatch 还是执行创建 componentlnstance

```javascript
// core/vdom/create-component
init (vnode: VNodeWithData, hydrating: boolean): ?boolean {
    if (
      vnode.componentInstance &&
      !vnode.componentInstance._isDestroyed &&
      vnode.data.keepAlive
    ) { // componentInstance在初次是undefined!!!
      // kept-alive components, treat as a patch
      const mountedNode: any = vnode // work around flow
      componentVNodeHooks.prepatch(mountedNode, mountedNode) // prepatch函数执行的是组件更新的过程
    } else {
      const child = vnode.componentInstance = createComponentInstanceForVnode(
        vnode,
        activeInstance
      )
      child.$mount(hydrating ? vnode.elm : undefined, hydrating)
    }
  },
复制代码
```

prepatch 操作就不会在执行组件的 mounted 和 created 生命周期函数，而是直接将 DOM 插入

**（4）LRU （least recently used）缓存策略**

LRU 缓存策略∶ 从内存中找出最久未使用的数据并置换新的数据。 LRU（Least rencently used）算法根据数据的历史访问记录来进行淘汰数据，其核心思想是 **"如果数据最近被访问过，那么将来被访问的几率也更高"**。 最常见的实现是使用一个链表保存缓存数据，详细算法实现如下∶

- 新数据插入到链表头部
- 每当缓存命中（即缓存数据被访问），则将数据移到链表头部
- 链表满的时候，将链表尾部的数据丢弃。

# 📁 组件通信

## 组件通信的方式

### （1） props  /  $emit

父组件通过`props`向子组件传递数据，子组件通过`$emit`和父组件通信

##### 1. 父组件向子组件传值

- `props`只能是父组件向子组件进行传值，`props`使得父子组件之间形成了一个单向下行绑定。子组件的数据会随着父组件不断更新。
- `props` 可以显示定义一个或一个以上的数据，对于接收的数据，可以是各种数据类型，同样也可以传递一个函数。
- `props`属性名规则：若在`props`中使用驼峰形式，模板中需要使用短横线的形式

```javascript
// 父组件
<template>
    <div id="father">
        <son :msg="msgData" :fn="myFunction"></son>
    </div>
</template>

<script>
import son from "./son.vue";
export default {
    name: father,
    data() {
        msgData: "父组件数据";
    },
    methods: {
        myFunction() {
            console.log("vue");
        }
    },
    components: {
        son
    }
};
</script>

// 子组件
<template>
    <div id="son">
        <p>{{msg}}</p>
        <button @click="fn">按钮</button>
    </div>
</template>
<script>
export default {
    name: "son",
    props: ["msg", "fn"]
};
</script>

```

##### 2. 子组件向父组件传值

- `$emit`绑定一个自定义事件，当这个事件被执行的时就会将参数传递给父组件，而父组件通过`v-on`监听并接收参数。

```javascript
// 父组件
<template>
  <div class="section">
    <com-article :articles="articleList" @onEmitIndex="onEmitIndex"></com-article>
    <p>{{currentIndex}}</p>
  </div>
</template>

<script>
import comArticle from './test/article.vue'
export default {
  name: 'comArticle',
  components: { comArticle },
  data() {
    return {
      currentIndex: -1,
      articleList: ['红楼梦', '西游记', '三国演义']
    }
  },
  methods: {
    onEmitIndex(idx) {
      this.currentIndex = idx
    }
  }
}
</script>

//子组件
<template>
  <div>
    <div v-for="(item, index) in articles" :key="index" @click="emitIndex(index)">{{item}}</div>
  </div>
</template>

<script>
export default {
  props: ['articles'],
  methods: {
    emitIndex(index) {
      this.$emit('onEmitIndex', index) // 触发父组件的方法，并传递参数index
    }
  }
}
</script>

```

### （2）eventBus事件总线（`$emit / $on`）

`eventBus`事件总线适用于**父子组件**、**非父子组件**等之间的通信，使用步骤如下： **（1）创建事件中心管理组件之间的通信**

```javascript
// event-bus.js

import Vue from 'vue'
export const EventBus = new Vue()

```

**（2）发送事件** 假设有两个兄弟组件`firstCom`和`secondCom`：

```javascript
<template>
  <div>
    <first-com></first-com>
    <second-com></second-com>
  </div>
</template>

<script>
import firstCom from './firstCom.vue'
import secondCom from './secondCom.vue'
export default {
  components: { firstCom, secondCom }
}
</script>

```

在`firstCom`组件中发送事件：

```javascript
<template>
  <div>
    <button @click="add">加法</button>    
  </div>
</template>

<script>
import {EventBus} from './event-bus.js' // 引入事件中心

export default {
  data(){
    return{
      num:0
    }
  },
  methods:{
    add(){
      EventBus.$emit('addition', {
        num:this.num++
      })
    }
  }
}
</script>

```

**（3）接收事件** 在`secondCom`组件中发送事件：

```javascript
<template>
  <div>求和: {{count}}</div>
</template>

<script>
import { EventBus } from './event-bus.js'
export default {
  data() {
    return {
      count: 0
    }
  },
  mounted() {
    EventBus.$on('addition', param => {
      this.count = this.count + param.num;
    })
  }
}
</script>

```

在上述代码中，这就相当于将`num`值存贮在了事件总线中，在其他组件中可以直接访问。事件总线就相当于一个桥梁，不用组件通过它来通信。

虽然看起来比较简单，但是这种方法也有不变之处，如果项目过大，使用这种方式进行通信，后期维护起来会很困难。

### （3）依赖注入（provide / inject）

这种方式就是Vue中的**依赖注入**，该方法用于**父子组件之间的通信**。当然这里所说的父子不一定是真正的父子，也可以是祖孙组件，在层数很深的情况下，可以使用这种方法来进行传值。就不用一层一层的传递了。

`provide / inject`是Vue提供的两个钩子，和`data`、`methods`是同级的。并且`provide`的书写形式和`data`一样。

- `provide` 钩子用来发送数据或方法
- `inject`钩子用来接收数据或方法

在父组件中：

```javascript
provide() { 
    return {     
        num: this.num  
    };
}

```

在子组件中：

```javascript
inject: ['num']

```

还可以这样写，这样写就可以访问父组件中的所有属性：

```javascript
provide() {
 return {
    app: this
  };
}
data() {
 return {
    num: 1
  };
}

inject: ['app']
console.log(this.app.num)

```

**注意：** 依赖注入所提供的属性是**非响应式**的。

### （3）ref / $refs

这种方式也是实现**父子组件**之间的通信。

`ref`： 这个属性用在子组件上，它的引用就指向了子组件的实例。可以通过实例来访问组件的数据和方法。

在子组件中：

```javascript
export default {
  data () {
    return {
      name: 'JavaScript'
    }
  },
  methods: {
    sayHello () {
      console.log('hello')
    }
  }
}

```

在父组件中：

```javascript
<template>
  <child ref="child"></component-a>
</template>
<script>
  import child from './child.vue'
  export default {
    components: { child },
    mounted () {
      console.log(this.$refs.child.name);  // JavaScript
      this.$refs.child.sayHello();  // hello
    }
  }
</script>

```

### （4）`$parent / $children`

- 使用`$parent`可以让组件访问父组件的实例（访问的是上一级父组件的属性和方法）
- 使用`$children`可以让组件访问子组件的实例，但是，`$children`并不能保证顺序，并且访问的数据也不是响应式的。

在子组件中：

```javascript
<template>
  <div>
    <span>{{message}}</span>
    <p>获取父组件的值为:  {{parentVal}}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: 'Vue'
    }
  },
  computed:{
    parentVal(){
      return this.$parent.msg;
    }
  }
}
</script>

```

在父组件中：

```javascript
// 父组件中
<template>
  <div class="hello_world">
    <div>{{msg}}</div>
    <child></child>
    <button @click="change">点击改变子组件值</button>
  </div>
</template>

<script>
import child from './child.vue'
export default {
  components: { child },
  data() {
    return {
      msg: 'Welcome'
    }
  },
  methods: {
    change() {
      // 获取到子组件
      this.$children[0].message = 'JavaScript'
    }
  }
}
</script>

```

在上面的代码中，子组件获取到了父组件的`parentVal`值，父组件改变了子组件中`message`的值。 **需要注意：**

- 通过`$parent`访问到的是上一级父组件的实例，可以使用`$root`来访问根组件的实例
- 在组件中使用`$children`拿到的是所有的子组件的实例，它是一个数组，并且是无序的
- 在根组件`#app`上拿`$parent`得到的是`new Vue()`的实例，在这实例上再拿`$parent`得到的是`undefined`，而在最底层的子组件拿`$children`是个空数组
- `$children` 的值是**数组**，而`$parent`是个**对象**

### （5）`$attrs / $listeners`

考虑一种场景，如果A是B组件的父组件，B是C组件的父组件。如果想要组件A给组件C传递数据，这种隔代的数据，该使用哪种方式呢？

如果是用`props/$emit`来一级一级的传递，确实可以完成，但是比较复杂；如果使用事件总线，在多人开发或者项目较大的时候，维护起来很麻烦；如果使用Vuex，的确也可以，但是如果仅仅是传递数据，那可能就有点浪费了。

针对上述情况，Vue引入了`$attrs / $listeners`，实现组件之间的跨代通信。

先来看一下`inheritAttrs`，它的默认值true，继承所有的父组件属性除`props`之外的所有属性；`inheritAttrs：false` 只继承class属性 。

- `$attrs`：继承所有的父组件属性（除了prop传递的属性、class 和 style ），一般用在子组件的子元素上
- `$listeners`：该属性是一个对象，里面包含了作用在这个组件上的所有监听器，可以配合 `v-on="$listeners"` 将所有的事件监听器指向这个组件的某个特定的子元素。（相当于子组件继承父组件的事件）

A组件（`APP.vue`）：

```javascript
<template>
    <div id="app">
        //此处监听了两个事件，可以在B组件或者C组件中直接触发 
        <child1 :p-child1="child1" :p-child2="child2" @test1="onTest1" @test2="onTest2"></child1>
    </div>
</template>
<script>
import Child1 from './Child1.vue';
export default {
    components: { Child1 },
    methods: {
        onTest1() {
            console.log('test1 running');
        },
        onTest2() {
            console.log('test2 running');
        }
    }
};
</script>

```

B组件（`Child1.vue`）：

```javascript
<template>
    <div class="child-1">
        <p>props: {{pChild1}}</p>
        <p>$attrs: {{$attrs}}</p>
        <child2 v-bind="$attrs" v-on="$listeners"></child2>
    </div>
</template>
<script>
import Child2 from './Child2.vue';
export default {
    props: ['pChild1'],
    components: { Child2 },
    inheritAttrs: false,
    mounted() {
        this.$emit('test1'); // 触发APP.vue中的test1方法
    }
};
</script>

```

C 组件 (`Child2.vue`)：

```javascript
<template>
    <div class="child-2">
        <p>props: {{pChild2}}</p>
        <p>$attrs: {{$attrs}}</p>
    </div>
</template>
<script>
export default {
    props: ['pChild2'],
    inheritAttrs: false,
    mounted() {
        this.$emit('test2');// 触发APP.vue中的test2方法
    }
};
</script>

```

在上述代码中：

- C组件中能直接触发test的原因在于 B组件调用C组件时 使用 v-on 绑定了`$listeners` 属性
- 在B组件中通过v-bind 绑定`$attrs`属性，C组件可以直接获取到A组件中传递下来的props（除了B组件中props声明的）

### （6）总结

**（1）父子组件间通信**

- 子组件通过 props 属性来接受父组件的数据，然后父组件在子组件上注册监听事件，子组件通过 emit 触发事件来向父组件发送数据。
- 通过 ref 属性给子组件设置一个名字。父组件通过 `$refs` 组件名来获得子组件，子组件通过 `$parent` 获得父组件，这样也可以实现通信。
- 使用 provide/inject，在父组件中通过 provide提供变量，在子组件中通过 inject 来将变量注入到组件中。不论子组件有多深，只要调用了 inject 那么就可以注入 provide中的数据。

**（2）兄弟组件间通信**

- 使用 eventBus 的方法，它的本质是通过创建一个空的 Vue 实例来作为消息传递的对象，通信的组件引入这个实例，通信的组件通过在这个实例上监听和触发事件，来实现消息的传递。
- 通过 `$parent/$refs` 来获取到兄弟组件，也可以进行通信。

**（3）任意组件之间**

- 使用 eventBus ，其实就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。

如果业务逻辑复杂，很多组件之间需要同时处理一些公共的数据，这个时候采用上面这一些方法可能不利于项目的维护。这个时候可以使用 vuex ，vuex 的思想就是将这一些公共的数据抽离出来，将它作为一个全局的变量来管理，然后其他组件就可以对这个公共数据进行读写操作，这样达到了解耦的目的。

## 父子组件在开发中如何进行通信，并且写出案例

在 Vue.js 3 中，父子组件之间的通信可以通过 props 和 $emit 实现。

一、使用 props 进行父组件向子组件的通信

在父组件中，可以通过 props 将数据传递给子组件。在子组件中，可以使用 props 接收父组件传递过来的数据。当父组件中的数据发生变化时，子组件中的数据也会同步更新。

以下是一个父组件向子组件传递数据的例子：

```vue
// 父组件
<template>
  <div>
    <ChildComponent :message="message" />
  </div>
</template>

<script>
import ChildComponent from './ChildComponent.vue'

export default {
  data() {
    return {
      message: 'Hello, World!'
    }
  },
  components: {
    ChildComponent
  }
}
</script>

// 子组件
<template>
  <div>{{ message }}</div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true
    }
  }
}
</script>
```

在这个例子中，父组件通过 props 将 `message` 数据传递给了子组件，并在子组件中通过 props 接收了该数据。

二、使用 $emit 进行子组件向父组件的通信

在子组件中，可以通过 emit 方法向父组件发送事件。父组件可以通过监听子组件发出的事件来获取子组件传递的数据。

以下是一个子组件向父组件传递数据的例子：

```vue
// 子组件
<template>
  <button @click="onClick">Click me</button>
</template>

<script>
export default {
  data() {
    return {
      message: 'Hello, World!'
    }
  },
  methods: {
    onClick() {
      this.$emit('child-click', this.message)
    }
  }
}
</script>

// 父组件
<template>
  <div>
    <ChildComponent @child-click="onChildClick" />
  </div>
</template>

<script>
import ChildComponent from './ChildComponent.vue'

export default {
  data() {
    return {
      messageFromChild: ''
    }
  },
  components: {
    ChildComponent
  },
  methods: {
    onChildClick(message) {
      this.messageFromChild = message
    }
  }
}
</script>
```

在这个例子中，子组件通过 `$emit` 方法向父组件发送了一个 `child-click` 事件，并将 `message` 数据作为参数传递给了父组件。父组件监听了该事件，并在回调函数中获取了子组件传递的数据。

需要注意的是，使用 emit 传递数据时，可以在第二个参数中传递任意数据，不仅限于字符串类型。

## Vue插槽的作用和平时开发中的应用

Vue 中的插槽（slot）是一种将父组件中的内容传递到子组件的技术。通过插槽，父组件可以将自己的内容嵌入到子组件中的指定位置。这样可以使得子组件具有更高的可复用性和灵活性，而且可以更好地分离组件之间的耦合度。

插槽可以分为默认插槽、具名插槽和作用于插槽三种。

默认插槽是没有名字的插槽，可以在子组件中使用 `slot` 标签来定义。

具名插槽是带有名字的插槽，可以在子组件中使用 `slot` 标签，并指定 `name` 属性来定义。一个组件可以出现多个具名插槽。

作用域插槽：默认插槽、具名插槽的一个变体，可以是匿名插槽，也可以是具名插槽，该插槽的不同点是在子组件渲染作用域插槽时，可以将子组件内部的数据传递给父组件，让父组件根据子组件的传递过来的数据决定如何渲染该插槽。

**实现原理：**

当子组件vm实例化时，获取到父组件传入的slot标签的内容，存放在vm.$slot中，默认插槽为vm.$slot.default，具名插槽为vm.$slot.xxx，xxx 为插槽名，当组件执行渲染函数时候，遇到slot标签，使用$slot中的内容进行替换，此时可以为插槽传递数据，若存在数据，则可称该插槽为作用域插槽。

**下面是一些平时开发中常见的插槽应用：**

1、组件内容的分发

使用插槽可以将父组件中的内容分发到子组件中的特定位置。这个应用场景非常常见，比如我们可以在父组件中使用插槽来分发按钮组件中的文本、图标等内容。

2、布局控制

使用插槽可以灵活地控制布局。比如我们可以在一个布局组件中使用插槽来控制内容的位置，实现各种不同的布局效果。

3、数据传递

使用插槽还可以实现数据的传递。比如我们可以在父组件中通过插槽将一些数据传递给子组件，子组件可以在相应的插槽中读取这些数据。

4、多列布局

使用插槽还可以实现多列布局。比如我们可以在父组件中使用多个具名插槽来定义多个列，并将数据分发到不同的列中，从而实现多列布局效果。

总的来说，插槽在 Vue.js 中非常重要，可以使我们的组件更加灵活和可复用。在实际开发中，我们可以根据具体的需求来合理地使用插槽，从而实现更好的开发效果。

## 理解作用域插槽以及在什么场景下使用

作用域插槽（Scoped Slots）是一种特殊的插槽，可以将子组件中的数据传递到父组件中，并在父组件中进行处理。相比于普通插槽，作用域插槽能够更加灵活地传递数据和控制组件的行为，尤其适用于需要自定义渲染逻辑的场景。

作用域插槽的实现方式是在子组件中使用 `v-slot` 指令，并在其后面添加一个参数，该参数是一个函数，用来传递数据到父组件中。父组件可以通过这个函数的参数来接收子组件传递过来的数据，并进行处理。

以下是一个使用作用域插槽的例子：

```vue
// 子组件
<template>
  <div>
    <slot name="message" :text="message"></slot>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: 'Hello, World!'
    }
  }
}
</script>

// 父组件
<template>
  <div>
    <ChildComponent>
      <template v-slot:message="{ text }">
        <div>{{ text }}</div>
      </template>
    </ChildComponent>
  </div>
</template>

<script>
import ChildComponent from './ChildComponent.vue'

export default {
  components: {
    ChildComponent
  }
}
</script>
```

在这个例子中，子组件使用了作用域插槽来将 `message` 数据传递到父组件中。父组件中定义了一个具名插槽，并使用 `v-slot` 指令来指定该插槽的名称为 `message`，并传递了一个参数 `text`，用来接收子组件传递过来的数据。在具名插槽中，可以使用这个参数来渲染自定义的内容。

作用域插槽的应用场景非常广泛，例如：

- 根据条件自定义组件的渲染逻辑；
- 在一个组件中包含另一个组件，并在子组件中渲染父组件中的数据；
- 根据数据自定义列表项的样式和渲染方式等。

总之，作用域插槽能够提供更高级的组件通信方式，使得组件能够更加灵活和可复用。

## 如何进行非父子组件的通信？

除了Vuex/Pinia其他方式:

1、全局事件总线

- 先安装库   `npm install hy-event-store`
- 封装一个工具eventbus.js
- 在组件A中 通过eventBus.on监听事件
- 在组件B中通过eventBus.emit发射事件

2、Provide/Inject用于非父子组件之间共享数据

- 父组件有一个 provide 选项来提供数据
- 子组件有一个 inject 选项来开始使用这些数据(注入)

注意点:

> provide选项一般写成一个返回数据的函数，以避免不必要的副作用。
>
> 处理响应式数据：通过computed函数,computed返回的是一个ref对象，需要取出其中的value来使用

##  子组件可以直接改变父组件的数据吗？

子组件不可以直接改变父组件的数据。这样做主要是为了维护父子组件的单向数据流。每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。如果这样做了，Vue 会在浏览器的控制台中发出警告。

Vue提倡单向数据流，即父级 props 的更新会流向子组件，但是反过来则不行。这是为了防止意外的改变父组件状态，使得应用的数据流变得难以理解，导致数据流混乱。如果破坏了单向数据流，当应用复杂时，debug 的成本会非常高。

**只能通过 `$emit` 派发一个自定义事件，父组件接收到后，由父组件修改。**

## Vue2.x生命周期有哪些？

Vue 2.x 的生命周期钩子函数共有 8 个，按照调用顺序可以分为四个阶段：

一、创建阶段（creation）

- beforeCreate: 在实例初始化之后、数据观测 (data observer) 和 event/watcher 事件配置之前被调用。
- created: 实例创建完成后被立即调用，这个阶段完成了数据的观测，属性和方法的运算，watcher 和 event 事件的配置等。

二、挂载阶段（mounting）

- beforeMount: 在挂载开始之前被调用，即在 render 函数执行之前。
- mounted: 在挂载完成之后被调用，即 DOM 元素被插入页面后。

三、更新阶段（updating）

- beforeUpdate: 在组件更新之前被调用，发生在虚拟 DOM 重新渲染和打补丁之前。
- updated: 在组件更新之后被调用，发生在重新渲染之后。当组件的子组件更新时，该钩子函数也会被调用。

四、销毁阶段（destruction）

- beforeDestroy: 在实例销毁之前调用。这个时候，实例仍然完全可用。
- destroyed: 在实例销毁之后调用。这个时候，所有的绑定都已解绑，所有的子实例也已经被销毁。

这些钩子函数的调用顺序是固定的，开发者可以通过它们来在不同的阶段进行操作和处理，例如在 created 钩子函数中发送异步请求获取数据，在 mounted 钩子函数中对 DOM 元素进行操作等。

需要注意的是，在 beforeCreate 钩子函数中不能访问到实例的数据和方法，在 created 钩子函数中可以访问到实例的数据和方法但不能操作 DOM 元素，而在 mounted 钩子函数中可以访问到实例的数据和方法并可以操作 DOM 元素。

⭐⭐⭐每个周期执行完能干嘛？

## 在 Vue 3 中，组件实例被创建时，会依次执行哪些生命周期函数？

在 Vue 3 中，组件实例被创建时，会依次执行以下生命周期函数：

1. `beforeCreate`: 组件实例刚被创建，但是数据观测和事件机制都还未初始化，因此无法访问 `this`。
2. `created`: 组件实例已经完成数据观测和事件机制的初始化，可以访问 `this`，但是尚未挂载到 DOM 上。
3. `beforeMount`: 组件即将被挂载到 DOM 上。
4. `mounted`: 组件已经被挂载到 DOM 上，此时可以访问到挂载后的 DOM 元素。
5. `beforeUpdate`: 组件数据更新前被调用，此时数据尚未更新。
6. `updated`: 组件数据更新后被调用，此时数据已经更新完毕。
7. `beforeUnmount`: 组件即将被销毁前调用。
8. `unmounted`: 组件已经被销毁，此时无法再访问到组件实例。

除了组件生命周期函数外，Vue 3 还引入了全局生命周期函数 `beforeMount` 和 `mounted`，分别在 Vue 实例挂载到 DOM 上前和后执行，这两个生命周期函数和 `beforeCreate` 和 `created` 的作用类似，只是它们是钩子函数，而不是组件生命周期函数。这两个生命周期函数的主要作用是用于 Vue 3 应用的初始化和插件的安装。

## 说一下Vue的生命周期

Vue 实例有⼀个完整的⽣命周期，也就是从开始创建、初始化数据、编译模版、挂载Dom -> 渲染、更新 -> 渲染、卸载 等⼀系列过程，称这是Vue的⽣命周期。

1. **beforeCreate（创建前）**：数据观测和初始化事件还未开始，此时 data 的响应式追踪、event/watcher 都还没有被设置，也就是说不能访问到data、computed、watch、methods上的方法和数据。
2. **created（创建后）** ：实例创建完成，实例上配置的 options 包括 data、computed、watch、methods 等都配置完成，但是此时渲染得节点还未挂载到 DOM，所以不能访问到 `$el` 属性。
3. **beforeMount（挂载前）**：在挂载开始之前被调用，相关的render函数首次被调用。实例已完成以下的配置：编译模板，把data里面的数据和模板生成html。此时还没有挂载html到页面上。
4. **mounted（挂载后）**：在el被新创建的 vm.$el 替换，并挂载到实例上去之后调用。实例已完成以下的配置：用上面编译好的html内容替换el属性指向的DOM对象。完成模板中的html渲染到html 页面中。此过程中进行ajax交互。
5. **beforeUpdate（更新前）**：响应式数据更新时调用，此时虽然响应式数据更新了，但是对应的真实 DOM 还没有被渲染。
6. **updated（更新后）** ：在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。此时 DOM 已经根据响应式数据的变化更新了。调用时，组件 DOM已经更新，所以可以执行依赖于DOM的操作。然而在大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。该钩子在服务器端渲染期间不被调用。
7. **beforeDestroy（销毁前）**：实例销毁之前调用。这一步，实例仍然完全可用，`this` 仍能获取到实例。
8. **destroyed（销毁后）**：实例销毁后调用，调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务端渲染期间不被调用。

另外还有 `keep-alive` 独有的生命周期，分别为 `activated` 和 `deactivated` 。用 `keep-alive` 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 `deactivated` 钩子函数，命中缓存渲染后会执行 `activated` 钩子函数。

##  Vue 子组件和父组件执行顺序


在 Vue 中，父组件和子组件的执行顺序遵循一定的生命周期，具体如下：

1. 父组件创建和挂载阶段：
   1. `beforeCreate` 钩子函数被触发；
   2. `created` 钩子函数被触发；
   3. `beforeMount` 钩子函数被触发；
   4. 子组件的 `beforeCreate` 和 `created` 钩子函数被触发；
   5. 子组件的 `beforeMount` 钩子函数被触发；
   6. 子组件的 `mounted` 钩子函数被触发；
   7. 父组件的 `mounted` 钩子函数被触发。
2. 父组件更新阶段：
   1. 父组件的数据发生改变，触发重新渲染；
   2. `beforeUpdate` 钩子函数被触发；
   3. 子组件的 `beforeUpdate` 钩子函数被触发；
   4. 子组件的 `updated` 钩子函数被触发；
   5. 父组件的 `updated` 钩子函数被触发。
3. 父组件卸载阶段：
   1. 父组件执行 `beforeDestroy` 钩子函数；
   2. 子组件执行 `beforeDestroy` 钩子函数；
   3. 子组件执行 `destroyed` 钩子函数；
   4. 父组件执行 `destroyed` 钩子函数。

在父组件和子组件的生命周期函数中，可以执行一些初始化、异步请求、DOM 操作等任务，以及监听数据变化、清除定时器、取消订阅等任务。对于数据流的变化，子组件会在父组件之前先进行更新，这是因为子组件内部的数据变化会引起父组件重新渲染。

## created和mounted的区别

- created:在模板渲染成html前调用，即通常初始化某些属性值，然后再渲染成视图。
- mounted:在模板渲染成html后调用，通常是初始化页面完成后，再对html的dom节点进行一些需要的操作。

## 一般在哪个生命周期请求异步数据

我们可以在钩子函数 created、beforeMount、mounted 中进行调用，因为在这三个钩子函数中，data 已经创建，可以将服务端端返回的数据进行赋值。 

推荐在 created 钩子函数中调用异步请求，因为在 created 钩子函数中调用异步请求有以下优点：

- 能更快获取到服务端数据，减少页面加载时间，用户体验更好；
- SSR不支持 beforeMount 、mounted 钩子函数，放在 created 中有助于一致性。

## keep-alive 中的生命周期哪些

keep-alive是 Vue 提供的一个内置组件，用来对组件进行缓存——在组件切换过程中将状态保留在内存中，防止重复渲染DOM。

如果为一个组件包裹了 keep-alive，那么它会多出两个生命周期：deactivated、activated。同时，beforeDestroy 和 destroyed 就不会再被触发了，因为组件不会被真正销毁。

当组件被换掉时，会被缓存到内存中、触发 deactivated 生命周期；当组件被切回来时，再去缓存里找这个组件、触发 activated钩子函数。

## 第一次进入组件或者页面，会执行哪些生命周期？

当组件或页面首次进入时，会触发 Vue 的创建阶段生命周期钩子函数，即 `beforeCreate` 和 `created`。

- `beforeCreate` 在实例初始化之后、数据观测（data observer）和 event/watcher 事件配置之前被调用。
- `created` 实例创建完成后被立即调用，这个阶段完成了数据的观测，属性和方法的运算，watcher 和 event 事件的配置等。

在 `beforeCreate` 钩子函数中，实例的数据和方法都还没有被初始化，所以不能访问实例的数据和方法。在 `created` 钩子函数中，实例已经创建完成，数据和方法已经被初始化，但是 DOM 元素还没有被挂载到页面上，所以不能对页面进行操作。

如果该组件或页面是通过路由跳转进入的，则还会触发 `beforeMount` 和 `mounted` 钩子函数，即挂载阶段生命周期钩子函数，具体可以参考 Vue 的生命周期。

## 什么是生命周期函数？说说你对它回调的理解

生命周期函数是一些钩子函数（回调函数），用于在组件的不同阶段执行特定的代码。

Vue 组件的生命周期可以分为创建、挂载、更新和销毁四个阶段，每个阶段都有对应的生命周期函数。

通过对生命周期函数的回调，我们可以知道目前组件正在经历什么阶段。

**Vue的生命周期函数**

- beforeCreate :组件实例在创建之前
- created: 组件被创建完成
  - 可以发送网络请求
  - 可以事件监听
  - this.$watch()

- beforeMount : 组件template准备被挂载
- mounted :组件template已经被挂载
  - 可以获取DOM,可以使用DOM,虚拟DOM -> 真实DOM

- beforeUpdate:  准备更新DOM
- updated: 更新DOM,根据最新数据生成新的VNode,生成新的虚拟DOM,转换为真实的DOM
- beforeUnmount: 卸载之前（）
- unmounted: DOM 元素被卸载完成
  - 回收操作(取消事件监听)


```js
export default {
    // 1.组件被创建之前
    beforeCreate() {
      console.log("beforeCreate")
    },
    // 2.组件被创建完成
    created() {
      console.log("created")
      console.log("1.发送网络请求, 请求数据")
      console.log("2.监听eventbus事件")
      console.log("3.监听watch数据")
    },
    // 3.组件template准备被挂载
    beforeMount() {
      console.log("beforeMount")
    },
    // 4.组件template被挂载: 虚拟DOM -> 真实DOM
    mounted() {
      console.log("mounted")
      console.log("1.获取DOM")
      console.log("2.使用DOM")
    },
    // 5.数据发生改变
    // 5.1. 准备更新DOM
    beforeUpdate() {
      console.log("beforeUpdate")
    },
    // 5.2. 更新DOM
    updated() {
      console.log("updated")
    },

    // 6.卸载VNode -> DOM元素
    // 6.1.卸载之前
    beforeUnmount() {
      console.log("beforeUnmount")
    },
    // 6.2.DOM元素被卸载完成
    unmounted() {
      console.log("unmounted")
    }
  }
```

## 请谈谈你对Vue的生命周期钩子函数的理解以及常见的应用场景

Vue3 的生命周期钩子函数指的是在组件的生命周期中，Vue3 框架提供的一系列回调函数，用于控制和管理组件的各个阶段。

在 Vue3 中，组件的生命周期分为三个阶段：创建阶段、更新阶段和销毁阶段。

创建阶段：

1、创建阶段：

- beforeCreate：实例创建之前调用，此时 data、methods、computed、watch 等选项都不可用。
- created：实例创建完成后调用，此时实例已完成数据观测（data observer），可以访问 data、methods、computed 和 watch 等选项。

2、挂载阶段：

- beforeMount：实例挂载之前调用，此时模板编译完成，但尚未挂载到页面上。
- mounted：实例挂载完成后调用，此时实例已经挂载到页面上，可以访问到实例对应的 DOM 元素。

3、更新阶段

- beforeUpdate: 在组件数据更新之前执行，此时组件数据已经发生变化，但尚未重新渲染DOM。此钩子函数可以用来进行一些数据的处理工作。
- updated: 在组件数据更新之后执行，此时组件已经重新渲染了DOM。此钩子函数可以用来进行一些与DOM元素相关的操作，如更新后的DOM元素的位置、样式等。

4、销毁阶段：

- beforeUnmount：实例销毁之前调用，此时实例仍然完全可用，可以访问 data、methods、computed 和 watch 等选项。
- unmounted：实例销毁后调用，此时实例已经完全销毁，无法访问实例对应的 DOM 元素。

常见的应用场景包括：

1. beforeCreate 和 created：常用于初始化数据，网络请求，设置事件监听器等。
2. beforeMount 和 mounted：常用于获取组件的 DOM 元素，并进行一些必要的 DOM 操作，如添加事件监听器、初始化插件等。
3. beforeUpdate 和 updated：常用于在组件更新前后进行一些操作，如手动更新 DOM 元素、重新计算计算属性等。
4. beforeUnmount 和 unmounted：常用于清除定时器、取消事件监听器等，以避免内存泄漏。

总之，在使用 Vue3 开发应用时，生命周期钩子函数是非常重要的一个部分，通过合理使用生命周期钩子函数，可以更好地控制和管理组件的生命周期，实现更高效的开发。

## 对动态组件和keep-alive的作用理解

**动态组件`＜component>`：**

动态组件是指在同一个挂载点上动态切换不同的组件，可以根据不同的条件渲染不同的组件，从而实现页面的动态切换和加载。动态组件可以通过 `<component>` 标签实现，需要设置 `:is` 属性指定当前组件的名称。

用来动态地挂载不同的组件, 使用 `is` 属性来选择要挂载的组件

- 根据 v-bind:is="组件名" 中的组件名去自动匹配组件，如果匹配不到则不显示

**keep-alive：**

`keep-alive` 组件是 Vue 提供的一个内置组件，用于缓存已经渲染过的组件实例。当一个组件被包裹在 `keep-alive` 组件内部时，这个组件在被销毁之前会被缓存起来，下次需要渲染这个组件时，会从缓存中直接读取，避免重复创建和销毁组件，从而提高应用的性能。

让组件缓存起来, 存活下来

- 属性:include, exclude,max
- 注意:include 和exclude 使用时，要求匹配的组件需要有 **name 选项**

通常情况下，动态组件和 `keep-alive` 一起使用，可以实现更加灵活和高效的组件切换和缓存。例如，在一个 tab 切换页面的场景中，可以使用动态组件来切换不同的页面组件，并结合 `keep-alive` 来缓存已经加载过的组件，提高页面的响应速度和用户体验。

## 组件使用v-model的本质是什么？

v-model 是 Vue.js 中一个常用的指令，用于实现双向数据绑定，它可以在表单控件（如 input、textarea、select）以及自定义组件中创建双向数据绑定。

本质上，v-model 是语法糖，它实际上是一个简化的写法，用于同时实现数据的读取和更新。当我们使用 v-model 绑定一个表单控件时，它会自动监听表单控件的输入事件，当用户在表单控件中输入数据时，v-model 会自动将输入的数据更新到绑定的数据对象中。

同时，当我们在数据对象中更新数据时，v-model 也会自动将更新后的数据同步到表单控件中。

在自定义组件中使用 v-model 时，我们需要定义一个名为 value 的 prop 以及一个名为 input 的事件。其中，value prop 用于接收父组件传递的数据，input 事件用于向父组件传递更新后的数据。这样，当父组件使用 v-model 绑定自定义组件时，就可以实现双向数据绑定了。

总之，v-model 的本质就是双向数据绑定，它能够使数据在视图和数据模型之间保持同步，从而简化开发流程，提高开发效率。

# 📁 Composition API

## 什么是Composition API？

和之前的options API有什么区别？（面试比较喜欢问这个问题）

Composition API 是 Vue.js 3.0 引入的一种新的 API，它是一种基于函数的 API，用于组织和重用有关联逻辑的代码。

与 Vue.js 2.x 中的 options API 不同，Composition API 是一种更加灵活和组合性更强的 API，它允许开发者更加自由地组合和重用逻辑代码，并且可以更好地处理复杂的业务逻辑和组件复用。

**与 options API 相比，Composition API 具有以下几个优势：**

1、更好的代码组织结构

使用 options API 时，组件的逻辑会被拆分到不同的选项中，例如 `data`、`computed`、`methods` 等，这样容易导致代码组织结构混乱、难以维护。而使用 Composition API，可以将相关逻辑放在同一个函数中，从而更好地组织代码。

2、更好的代码复用

在 options API 中，组件之间的代码复用往往需要使用 mixin 或者高阶组件等方式，这样会增加代码的复杂性。而在 Composition API 中，可以将组件内的逻辑封装成一个独立的函数，并在需要使用的地方进行引用和复用。

3、更好的类型推导支持

在 options API 中，由于组件选项的定义分散在不同的地方，因此在使用 TypeScript 等类型系统时，类型推导支持较差。而在 Composition API 中，组件逻辑都集中在一个函数中，可以更方便地进行类型推导。

4、更好的测试支持

在 options API 中，由于组件选项分散在不同的地方，因此在进行单元测试时，需要分别测试组件的不同选项。而在 Composition API 中，可以将组件逻辑封装成一个函数，更方便地进行单元测试。

5、更好的响应式支持

在 options API 中，响应式数据的处理需要通过 Vue 的实例来进行，而在 Composition API 中，可以通过 `reactive`、`ref` 等 API 直接处理响应式数据，更方便地进行响应式编程。

总之，Composition API 是一种更加灵活、组合性更强的 API，它允许开发者更加自由地组合和重用逻辑代码，从而提高代码的可读性、可维护性和可复用性。同时，它也可以更好地处理复杂的业务逻辑和组件复用。

## 如何使用setup函数，并且让数据是响应式的？

在 Vue.js 3.0 中，setup 函数是一个特殊的函数，用于定义组件的数据、方法和生命周期函数等。setup 函数只会在组件实例化时执行一次，它需要返回一个对象，包含了组件的所有响应式数据和方法。

为了让数据是响应式的，我们可以使用 Vue.js 3.0 中新增的 reactive 和 ref 函数。其中，reactive 函数用于创建一个响应式对象，而 ref 函数用于创建一个响应式引用。

在 Vue.js 3.0 中，setup 函数有两个参数：props 和 context。

props 对象包含了父组件传递过来的属性，这些属性是只读的，也就是说我们不能直接修改 props 对象中的属性值。props 对象中的属性值是响应式的，这意味着当父组件的属性值发生变化时，子组件会自动响应更新。

context 对象包含了一些与组件上下文相关的属性，包括 attrs、slots 和 emit。

- attrs 对象包含了组件接收的所有非 prop 属性，这些属性是响应式的。
- slots 对象包含了父组件传递过来的插槽内容，它是一个函数或对象，可以用于渲染父组件中的具名插槽或默认插槽。
- emit 函数用于在组件内部触发自定义事件，并向父组件派发事件。emit 函数的参数是一个事件名称和可选的参数，父组件可以监听这些事件并执行相应的操作。

在 setup 函数中返回一个对象，这个对象中的属性和方法都是响应式的。我们可以使用这个对象来替代 data 选项，这样可以让组件的数据是响应式的，并且可以使用更加简洁的语法来定义组件的状态和方法。

## 整理学习过的Options API ，并且说出每一个作用

一、data（定义数据）

- data必须是一个函数, 函数会返回一个对象( 在Vue3.x的时候)
- data返回的对象, 会被Vue进行劫持(放到响应式系统中), 所以data的数据发生改变时, 界面会重新渲染

二、methods（定义方法）

- methods属性是一个对象 -> 定义很多方法--->这些方法可以绑定到模板上
- 在该方法中，我们可以使用**this关键字**来直接访问到**data中返回的对象的属性**
- 里面函数不能是箭头函数:
  - 如果是箭头函数,因为箭头函数不绑定this,所以它会在上层作用域中查找this, 查找到this-->window

三、computed（计算属性）

- 对于任何包含响应式数据的**复杂逻辑**，你都应该使用**计算属性**
- 可以通过this访问数据
- 计算属性会基于它们的依赖关系进行**缓存**
  - 在数据不发生变化时，计算属性是不需要重新计算的
  - 如果依赖的数据发生变化，在使用时，计算属性依然会重新进行计算

四、watch（侦听器）

- 用来监听某个数据的变化
- deep  深度监听
- immediate   第一次渲染直接执行一次监听器

五、components

- 注册局部组件
- 该components选项对应的是一个对象，对象中的键值对是 组件的名称: 组件对象

六、props（完成父子组件之间通信）

- Props是你可以在组件上注册一些自定义的attribute
- 父组件给这些attribute赋值，子组件通过attribute的名称获取到对应的值

七、emits

- 记录发射了哪些自定义事件
- emits 可以是数组或对象，从组件触发自定义事件，emits 可以是简单的数组，也可以是对象，后者允许配置事件验证

八、provide（用于非父子组件之间共享数据）

- 父组件有一个 provide 选项来提供数据

inject（用于非父子组件之间共享数据）

- 子组件有一个 inject 选项来开始使用提供provide的数据

九、生命周期函数

- beforeCreate :组件实例在创建之前
- created: 组件被创建完成
  - 可以发送网络请求
  - 可以事件监听
  - this.$watch()

- beforeMount : 组件template准备被挂载
- mounted :组件template已经被挂载
  - 可以获取DOM,可以使用DOM

- beforeUpdate:  准备更新DOM
- updated: 更新DOM,根据最新数据生成新的VNode,生成新的虚拟DOM,转换为真实的DOM
- beforeUnmount:  卸载之前
- unmounted: DOM 元素被卸载完成
  - 回收操作(取消事件监听)

## ref是什么？

在 Vue 3.0 中，`ref` 是一个用于创建响应式数据的函数。

`ref` 函数接受一个参数作为初始值，并返回一个包含 `value` 属性的对象，该属性包含传入的初始值。在组件中使用 `ref` 函数创建的响应式数据，可以像普通 JavaScript 对象一样使用，但是当该数据发生变化时，Vue 会自动更新与该数据相关的视图。

请注意，使用`ref`创建的响应式数据的值始终是存储在`value`属性中的。因此，在访问或修改`ref`对象的值时，我们需要使用`refObject.value`的语法。

除了在 setup 函数中使用 ref 函数创建响应式数据外，我们还可以在模板中使用 ref 函数来创建一个 ref 对象，并将它绑定到一个 DOM 元素上，以便在组件中操作这个元素。

## ref和reactive有什么区别？开发中如何选择？

1、数据类型：

`ref`和`reactive`都可以包裹任意数据类型，但`ref`会将其包裹的值封装为一个具有`value`属性的对象，而`reactive`会将其包裹的值转换为一个代理对象，可以通过代理对象访问和修改对象属性。

2、用法：

在JavaScript代码中使用`ref`时，需要使用`refObject.value`语法来访问和修改其值；在模板中使用`ref`时，可以直接使用`refObject`，Vue会自动解包`ref`对象，渲染其`value`属性。而在使用`reactive`时，可以直接访问和修改其属性，不需要额外的语法。

3、适用场景：

`ref`适用于处理单个值的场景，而`reactive`适用于处理包含多个属性的复杂数据类型的场景。在实际开发中，我们可以根据具体需求选择合适的响应式数据类型。

4、选择建议

1. 如果你只需要响应式地处理一个简单的值，可以使用`ref`。
2. 如果你需要响应式地处理一个对象或数组，可以使用`reactive`。
3. 如果你需要将响应式数据传递给子组件或其他函数，可以使用`ref`或`toRef`来创建一个`ref`对象或将属性转换为`ref`对象。这可以避免将响应式数据作为普通的非响应式数据传递，并确保在传递过程中保持响应式。
4. 如果你需要监听响应式数据的变化，可以使用`watch`或`watchEffect`函数。`watch`适用于监听特定的数据变化，而`watchEffect`适用于监听整个响应式对象的变化。

## Composition API常见的几个函数用法？

1、ref

- 包裹任意类型的值，将包裹的值加入响应式

2、reactive

- 包裹复杂类型的值，将包裹的值加入响应式

3、readonly

- 我们通过父组件向子组件传递数据后，子组件拿到数据，在组件中是不能修改这个拿到的数据
- 因为这不符合单项数据流的原则
- 如果你想这样做，需要在子组件发射事件并携带参数，父组件进行事件监听，然后再修改传递的值
- 但是为了避免子组件误操作，我们需要为其包裹一个readonly
- 这样传递过去的值，被更改时，会报警告，且执行失败

4、computed

- 把一些复杂逻辑用computed进行包裹，如同Options API中的计算属性一样
- computed会自动收集相关依赖，当依赖发生变化时，会自动进行更新

5、生命周期

- 想要在beforeCreate和created中做的事，直接在setup中做即可
- 其他的生命周期函数都要在前面加一个on，然后需要在vue中主动引入

6、watch

- watch可以监听单个数据源，也可以监听多个数据源
- watch是懒执行，第一次是不会执行的，除非你为其提供第三个参数中的immediate属性为true
- watch只有等到监听的数据源发生了变化后，才会执行第二个参数（回调）
- watch可以获取监听数据源的前后变化的值
- 侦听多个数据源的时候，第一个参数是数组类型

7、watchEffect

- watchEffect会自动收集依赖，收集的依赖是第一个参数，也就是回调函数中有哪些东西是加入响应式的
- 如果这个值加入了响应式就会被收集起来，当被收集的值发生了变化，就会重新执行这个回调函数
- watchEffect第一次执行是在DOM挂载前执行的，所以如果你想在第一次执行时拿到DOM元素
- 需要传入第二个参数，第二个参数是一个对象，让其flush属性的值为post即可

8、toRefs

- 对reactive进行解构后就失去了响应式的效果，因为reactive返回的是一个Proxy对象
- 对Proxy对象进行解构，拿到的是纯净的值，所以没有了响应式的效果
- 如果想要对reactive进行解构，需要对其包裹一个toRefs
- 这么做相当于为reactive中的每一个值包裹了一个ref

## watch和watchEffect有什么区别？

区别1：懒执行副作用

watch和watchEffect都是用于监听响应式数据变化，但它们在执行副作用时的机制略有不同。

watch是懒执行的，也就是说只有在监听的数据源发生变化时才会执行回调函数，而第一次不会直接执行。

而watchEffect则会立即执行回调函数，并自动收集依赖，如果收集到的依赖发生变化，会再次执行回调函数。

区别2：监听单个数据源和多个数据源

watch可以监听单个数据源，也可以监听多个数据源，而watchEffect只能监听一个数据源。

当需要监听多个数据源时，watch的第一个参数是一个数组类型。

区别3：访问侦听状态变化前后的值

watch和watchEffect都可以访问侦听状态变化前后的值，但实现方式略有不同。

watch可以通过回调函数的第二个参数来获取状态变化前后的值，而watchEffect需要使用Vue提供的ref或reactive等API来创建响应式数据，并在回调函数中访问这些数据的旧值和新值。

区别4：初始执行和停止监听

watch和watchEffect在初始执行和停止监听时的机制也略有不同。

watch可以通过第四个参数来配置侦听器是否在初始渲染时执行，而watchEffect不支持这个选项。而watch需要手动停止监听，而watchEffect会在组件卸载时自动停止监听。

区别5：适用场景

watch和watchEffect适用于不同的场景。watch适用于需要在数据发生变化时执行副作用的情况，比如发起网络请求或更新其他的状态。

而watchEffect适用于需要在数据发生变化时自动执行某个函数的情况，比如计算属性或响应式数据的变化。

同时，watch支持通过第三个参数中的deep选项来监听对象或数组的深度变化，而watchEffect则不需要配置这个选项。

需要注意的是，watch和watchEffect是Vue 3中新增的API，与Vue 2.x版本中的watch并不完全一样。

## script setup语法糖的常见用法

script setup是Vue 3中新增的语法糖，用于简化组件的书写和增强类型推导能力。

常见的用法如下：

1. 声明顶层绑定：在script setup中声明的顶层绑定（包括变量、函数声明和import引入的内容）可以在模板中直接使用，无需使用this访问。
2. 响应式数据：使用ref和reactive来创建响应式数据。
3. 导入组件：可以直接在script setup中导入组件，并在模板中使用。
4. defineProps和defineEmits：用于定义组件的props和emits，可以通过类型推导自动进行类型校验。
5. defineExpose：用于将组件中的方法或变量暴露给父组件或其他外部使用，可以在组件的setup函数中使用。需要注意的是，使用defineExpose暴露的方法或变量需要通过组件的ref获取组件实例后才能访问。

需要注意的是，defineProps、defineEmits、defineExpose不需要导入，直接使用即可。

# 📁 路由

## 什么是前端路由？前端路由的发展历程是怎么样的？

前端路由是指在前端应用中，前端路由是指在前端页面中，通过改变URL路径而不刷新整个页面的方式，实现不同页面之间的切换和展示不同内容的技术。它是一种单页应用（SPA）的实现方式。

前端路由的发展历程主要经历了以下几个阶段：

1. Hash URL 时代：在早期的前端路由实现中，由于浏览器不支持 HTML5 History API，开发者们通常使用 Hash URL（例如：/#/home）来模拟路由。这种方式不利于 SEO，而且 URL 不够美观。
2. HTML5 History API 时代：随着 HTML5 History API 的出现，前端路由的实现得以更加优雅。通过 History API 可以直接修改 URL，而不需要使用 Hash URL。但这种方式需要后端服务器的支持，来确保在用户手动输入 URL 时返回正确的页面。
3. 前端路由框架的出现：由于手动实现前端路由比较繁琐，因此出现了许多前端路由框架，例如 Backbone.js、AngularJS、React Router、Vue Router 等。这些框架提供了强大的路由功能，可以方便地管理路由，并提供了路由守卫、动态路由等高级功能。
4. 路由组件化：为了更好地组织代码，一些前端框架开始采用路由组件化的思想，将路由信息和对应的组件封装在一起。这种方式可以更好地维护代码，使得路由和组件之间的关系更加清晰。

总的来说，随着前端应用的日益复杂和SPA应用的流行，前端路由成为了现代前端开发中不可或缺的一部分。前端路由的发展历程也是从简单到复杂、从依赖于浏览器Hash值到依赖于HTML5的History API、从单纯的路由跳转到支持路由嵌套和守卫等功能的演化过程。

## 对前端路由的理解

在前端技术早期，一个 url 对应一个页面，如果要从 A 页面切换到 B 页面，那么必然伴随着页面的刷新。这个体验并不好，不过在最初也是无奈之举——用户只有在刷新页面的情况下，才可以重新去请求数据。

后来，改变发生了——Ajax 出现了，它允许人们在不刷新页面的情况下发起请求；与之共生的，还有“不刷新页面即可更新页面内容”这种需求。在这样的背景下，出现了 **SPA（单页面应用**）。

SPA极大地提升了用户体验，它允许页面在不刷新的情况下更新页面内容，使内容的切换更加流畅。但是在 SPA 诞生之初，人们并没有考虑到“定位”这个问题——在内容切换前后，页面的 URL 都是一样的，这就带来了两个问题：

- SPA 其实并不知道当前的页面“进展到了哪一步”。可能在一个站点下经过了反复的“前进”才终于唤出了某一块内容，但是此时只要刷新一下页面，一切就会被清零，必须重复之前的操作、才可以重新对内容进行定位——SPA 并不会“记住”你的操作。
- 由于有且仅有一个 URL 给页面做映射，这对 SEO 也不够友好，搜索引擎无法收集全面的信息

为了解决这个问题，前端路由出现了。

前端路由可以帮助我们在仅有一个页面的情况下，“记住”用户当前走到了哪一步——为 SPA 中的各个视图匹配一个唯一标识。这意味着用户前进、后退触发的新内容，都会映射到不同的 URL 上去。此时即便他刷新页面，因为当前的 URL 可以标识出他所处的位置，因此内容也不会丢失。

那么如何实现这个目的呢？首先要解决两个问题：

- 当用户刷新页面时，浏览器会默认根据当前 URL 对资源进行重新定位（发送请求）。这个动作对 SPA 是不必要的，因为我们的 SPA 作为单页面，无论如何也只会有一个资源与之对应。此时若走正常的请求-刷新流程，反而会使用户的前进后退操作无法被记录。
- 单页面应用对服务端来说，就是一个URL、一套资源，那么如何做到用“不同的URL”来映射不同的视图内容呢？

从这两个问题来看，服务端已经完全救不了这个场景了。所以要靠咱们前端自力更生，不然怎么叫“前端路由”呢？作为前端，可以提供这样的解决思路：

- 拦截用户的刷新操作，避免服务端盲目响应、返回不符合预期的资源内容。把刷新这个动作完全放到前端逻辑里消化掉。
- 感知 URL 的变化。这里不是说要改造 URL、凭空制造出 N 个 URL 来。而是说 URL 还是那个 URL，只不过我们可以给它做一些微小的处理——这些处理并不会影响 URL 本身的性质，不会影响服务器对它的识别，只有我们前端感知的到。一旦我们感知到了，我们就根据这些变化、用 JS 去给它生成不同的内容。

## Vue-router跳转和location.href有什么区别

- 使用 `location.href= /url `来跳转，简单方便，但是刷新了页面；
- 使用 `history.pushState( /url )` ，无刷新页面，静态跳转；
- 引进 router ，然后使用 `router.push( /url )` 来跳转，使用了 `diff` 算法，实现了按需加载，减少了 dom 的消耗。其实使用 router 跳转和使用 `history.pushState()` 没什么差别的，因为vue-router就是用了 `history.pushState()` ，尤其是在history模式下。

## 单页面富应用 

一、SPA（single page web application）

单页面富应用（SPA）是一种Web应用程序，它在加载时将所有必要的代码一次性加载到浏览器中，而不是像传统的多页面应用程序（MPA）那样在每个页面切换时重新加载整个页面。

二、SPA最主要的特点

在前后端分离的基础上加了一层**前端路由**，使得用户在使用应用程序时感觉像是在一个单独的页面中导航，实际上却是在同一个页面中进行不同的操作和交互。

三、实现方式

SPA可以通过使用JavaScript框架（如AngularJS、React和Vue.js等）来实现。这些框架通常提供了一个单页应用程序所需的所有功能，如组件化开发、数据绑定、路由、状态管理和服务器通信等。SPA还可以使用RESTful API与后端服务器进行通信，以获取数据和执行其他操作。

四、SPA的优点包括：

- 更快的页面加载速度和更好的用户体验，因为整个应用程序只需要加载一次，而不是每次页面切换时都需要重新加载。
- 更好的可维护性，因为前端代码和后端代码相互独立，可以更容易地进行修改和更新。
- 更好的扩展性，因为可以使用现代的前端技术和框架来构建应用程序，并且可以通过RESTful API与各种后端技术进行集成。

五、SPA的缺点包括：

- 对搜索引擎不友好，因为搜索引擎爬虫通常只能识别HTML文档，而无法解析动态生成的内容。
- 初始加载时间可能会更长，因为需要加载整个应用程序。
- 对于老旧的浏览器，可能会出现兼容性问题。

## 对 SPA 单页面的理解，它的优缺点分别是什么？

SPA（ single-page application ）仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。一旦页面加载完成，SPA 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 HTML 内容的变换，UI 与用户的交互，避免页面的重新加载。

**优点：**

- 用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染；
- 基于上面一点，SPA 相对对服务器压力小；
- 前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理；

**缺点：**

- 初次加载耗时多：为实现单页 Web 应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一加载，部分页面按需加载；
- 前进后退路由管理：由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理；
- SEO 难度较大：由于所有的内容都在一个页面中动态替换显示，所以在 SEO 上其有着天然的弱势。

## 前端路由切换的本质是什么？

前端路由切换的本质是通过 JavaScript 监听 URL 的变化，并根据 URL 的变化来更新页面中的内容和组件。当用户点击页面上的链接或者通过程序改变 URL 的时候，前端路由会拦截这个事件，然后根据 URL 的变化，更新页面上的相应组件和内容，从而实现页面的切换和渲染。

具体来说，前端路由切换的过程可以分为以下几个步骤：

1. 监听 URL 的变化：前端路由会监听浏览器地址栏中 URL 的变化，并通过 JavaScript 对 URL 进行解析。
2. 匹配路由规则：前端路由会根据路由规则来匹配 URL，找到对应的页面组件。
3. 渲染页面组件：一旦找到了对应的页面组件，前端路由就会通过 JavaScript 渲染页面组件，并将其插入到页面中。
4. 更新页面状态：在页面组件被渲染后，前端路由会更新页面的状态，包括页面标题、浏览器历史记录等。

总之，前端路由切换的本质是在前端通过 JavaScript 监听 URL 的变化，并根据 URL 的变化来更新页面的内容和状态，从而实现页面的切换和渲染。

## hash和history有什么区别？⭐⭐⭐

Vue-Router有两种模式：**hash模式**和**history模式**。默认的路由模式是hash模式。

- history 模式使用 HTML5 中的 History API 来实现，通过修改 URL 地址的 path 和 query 参数来实现路由跳转，URL 地址看起来更加干净，没有 # 号。但是需要后端支持，否则会出现刷新后 404 的情况。
- hash 模式通过 URL 地址中的 # 号来实现路由跳转，URL 地址中 hash 值的变化不会导致浏览器向服务器发出请求，因此对后端支持较小，但是需要注意的是，如果在浏览器中直接访问带有 hash 值的 URL，会先访问服务器，然后再进行路由跳转。

在打包后前端自测时，如果使用 history 模式，则需要服务器配置，否则会出现空白页；而 hash 模式可以直接在浏览器中访问，不需要服务器配置。

hash模式和history模式都有各自的优势和缺陷，还是要根据实际情况选择性的使用。

| 特性     | hash                                                         | history                                                      |
| :------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| URL 格式 | 使用 # 号来分隔 URL 的片段，如 [http://example.com/#/home](http://example.com/#/home) | 使用真实的 URL 格式，如 [http://example.com/home](http://example.com/home) |
| 兼容性   | 兼容性较好，能够兼容到IE8，所有现代浏览器都支持              | 只能兼容到IE10，需要使用 polyfill 库来实现在低版本浏览器中的兼容 |
| 实现原理 | 将路由信息保存在 URL 的片段中，不会将路由信息发送到服务器，因此不需要在服务器层面上进行任何处理 | 通过修改浏览器历史记录来实现路由切换，需要在服务器端进行路由匹配并返回相应的 HTML 文件 |
| 刷新页面 | 不会导致 404 错误，因为路由信息保存在 URL 的片段中           | 可能会导致 404 错误，需要在服务器端配置回调路由来避免这种情况 |
| 安全性   | 由于路由信息保存在 URL 的片段中，不会被发送到服务器，因此更加安全 | 需要在服务器端进行路由匹配和返回 HTML 文件，存在一定的安全风险 |

### 1. hash模式

**简介：** hash模式是开发中默认的模式，它的URL带着一个#，例如：[www.abc.com/#/vue](https://link.juejin.cn?target=http%3A%2F%2Fwww.abc.com%2F%23%2Fvue)，它的hash值就是`#/vue`。

**特点**：hash值会出现在URL里面，但是不会出现在HTTP请求中，对后端完全没有影响。所以改变hash值，不会重新加载页面。这种模式的浏览器支持度很好，低版本的IE浏览器也支持这种模式。hash路由被称为是前端路由，已经成为SPA（单页面应用）的标配。

**原理：** hash模式的主要原理就是**onhashchange()事件**：

```javascript
window.onhashchange = function(event){
	console.log(event.oldURL, event.newURL);
	let hash = location.hash.slice(1);
}

```

使用onhashchange()事件的好处就是，在页面的hash值发生变化时，无需向后端发起请求，window就可以监听事件的改变，并按规则加载相应的代码。除此之外，hash值变化对应的URL都会被浏览器记录下来，这样浏览器就能实现页面的前进和后退。虽然是没有请求后端服务器，但是页面的hash值和对应的URL关联起来了。

### 2. history模式

**简介：** history模式的URL中没有#，它使用的是传统的路由分发模式，即用户在输入一个URL时，服务器会接收这个请求，并解析这个URL，然后做出相应的逻辑处理。 

**特点：** 当使用history模式时，URL就像这样：[abc.com/user/id](https://link.juejin.cn?target=http%3A%2F%2Fabc.com%2Fuser%2Fid)。相比hash模式更加好看。但是，history模式需要后台配置支持。如果后台没有正确配置，访问时会返回404。 

**API：** history api可以分为两大部分，切换历史状态和修改历史状态：

- **修改历史状态**：包括了 HTML5 History Interface 中新增的 `pushState()` 和 `replaceState()` 方法，这两个方法应用于浏览器的历史记录栈，提供了对历史记录进行修改的功能。只是当他们进行修改时，虽然修改了url，但浏览器不会立即向后端发送请求。如果要做到改变url但又不刷新页面的效果，就需要前端用上这两个API。
- **切换历史状态：** 包括`forward()`、`back()`、`go()`三个方法，对应浏览器的前进，后退，跳转操作。

虽然history模式丢弃了丑陋的#。但是，它也有自己的缺点，就是在刷新页面的时候，如果没有相应的路由或资源，就会刷出404来。

如果想要切换到history模式，就要进行以下配置（后端也要进行配置）：

```javascript
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})

```

### 3. 两种模式对比

调用 history.pushState() 相比于直接修改 hash，存在以下优势:

- pushState() 设置的新 URL 可以是与当前 URL 同源的任意 URL；而 hash 只可修改 # 后面的部分，因此只能设置与当前 URL 同文档的 URL；
- pushState() 设置的新 URL 可以与当前 URL 一模一样，这样也会把记录添加到栈中；而 hash 设置的新值必须与原来不一样才会触发动作将记录添加到栈中；
- pushState() 通过 stateObject 参数可以添加任意类型的数据到记录中；而 hash 只可添加短字符串；
- pushState() 可额外设置 title 属性供后续使用。
- hash模式下，仅hash符号之前的url会被包含在请求中，后端如果没有做到对路由的全覆盖，也不会返回404错误；history模式下，前端的url必须和实际向后端发起请求的url一致，如果没有对用的路由处理，将返回404错误。

## 如何获取页面的hash变化

**（1）监听$route的变化**

```js
// 监听,当路由发生变化的时候执行
watch: {
  $route: {
    handler: function(val, oldVal){
      console.log(val);
    },
    // 深度观察监听
    deep: true
  }
}
```

**（2）window.location.hash读取#值** window.location.hash 的值可读可写，读取来判断状态是否改变，写入时可以在不重载网页的前提下，添加一条历史访问记录。

## `$route`和`$router` 的区别

$route 是“路由信息对象”，包括 path，params，hash，query，fullPath，matched，name 等路由信息参数

$router 是“路由实例”对象包括了路由的跳转方法，钩子函数等。

## 路由的使用步骤是什么？

一、安装:

```
npm install vue-router 
```

二、使用:

1、通过 createRouter 创建 router 对象，并传入 routes 和 history 模式

routes：

- 配置映射关系，定义每个路由的 path 和对应的组件 component

history：

- 指定采用的模式，可以是 hash 模式或 history 模式

hash 模式

- history：createWebHashHistory()

history 模式

- history：createWebHistory()

2、使用 app.use(router) 注册路由对象

3、使用路径:

- router-view：用于渲染当前路由对应的组件。如果当前路由没有匹配到任何组件，则不渲染任何内容。
- router-link：用于进行路由的切换，可以使用 :to 绑定跳转的路径，也可以使用 tag 指定渲染成什么 HTML 标签。

4、支持编程式导航，通过 router.push 或 router.replace 方法实现跳转

5、使用 name，属性指定路由名称，可以在编程式导航和模板中使用

## Vue-Router 的懒加载如何实现

Vue 路由懒加载是一种优化技术，它允许在需要时按需加载路由组件，而不是在应用程序初始加载时将所有路由组件一次性加载。

要实现路由懒加载，你可以使用 Vue Router 的 `import()` 语法或 Webpack 的动态导入功能。

非懒加载：

```javascript
import List from '@/components/list.vue'
const router = new VueRouter({
  routes: [
    { path: '/list', component: List }
  ]
})

```

（1）方案一(常用)：使用箭头函数+import动态加载

```javascript
const List = () => import('@/components/list.vue')
const router = new VueRouter({
  routes: [
    { path: '/list', component: List }
  ]
})

```

（2）方案二：使用箭头函数+require动态加载

```javascript
const router = new Router({
  routes: [
   {
     path: '/list',
     component: resolve => require(['@/components/list'], resolve)
   }
  ]
})

```

（3）方案三：使用webpack的require.ensure技术，也可以实现按需加载。 这种情况下，多个路由指定相同的chunkName，会合并打包成一个js文件。

```javascript
// r就是resolve
const List = r => require.ensure([], () => r(require('@/components/list')), 'list');
// 路由也是正常的写法  这种是官方推荐的写的 按模块划分懒加载 
const router = new Router({
  routes: [
  {
    path: '/list',
    component: List,
    name: 'list'
  }
 ]
}))
```

## params和query的区别

**用法**：query要用path来引入，params要用name来引入，接收参数都是类似的，分别是 `this.$route.query.name` 和 `this.$route.params.name` 。

**url地址显示**：query更加类似于ajax中get传参，params则类似于post，说的再简单一点，前者在浏览器地址栏中显示参数，后者则不显示

**注意**：query刷新不会丢失query里面的数据 params刷新会丢失 params里面的数据。

## 如何给路由跳转的组件传递数据

路由跳转的组件传递数据有两种方式：动态路由和query参数。

一、动态路由：

使用动态路由时，可以在路由定义时使用冒号(`:`)指定动态参数，如`/user/:id`，其中`:id`是一个动态参数，可以在路由跳转时传递具体的值。获取动态路由参数的方式有：

- 在模板中，直接使用 `$route.params.id` 获取参数值。
- 在 `created` 钩子函数中，使用 `this.$route.params.id` 获取参数值。
- 在 `setup` 函数中使用 `useRoute` Hook 获取参数值，如

```js
const route = useRoute();
const id = route.params.id
```


另外，在使用动态路由时，还可以使用 `onBeforeRouteUpdate` 钩子函数来处理当前路由发生变化时的情况，如在同一个组件中复用了不同的动态路由。

二、query参数：

在路由跳转时，可以通过 `query` 属性传递参数，如：

```js
this.$router.push({
  path: '/about',
  query: {
    name: 'John',
    age: 20
  }
})
```

在目标组件中，可以使用 `$route.query` 来获取传递过来的参数，如：

```vue
<template>
  <div>
    <p>Name: {{ $route.query.name }}</p>
    <p>Age: {{ $route.query.age }}</p>
  </div>
</template>
```

注意，query参数会被编码，因此如果要传递中文等特殊字符，需要使用 `encodeURIComponent` 进行编码。

## 如何实现路由的嵌套？

在 Vue Router 中，可以通过嵌套路由来实现路由的嵌套。嵌套路由的原理是将子路由的 path 与父路由的 path 拼接起来形成完整的路径。

**以下是实现路由嵌套的步骤：**

1、创建路由对象并配置路由映射关系。

```js
const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/',
      component: Home,
      children: [
        {
          path: 'profile',
          component: Profile
        },
        {
          path: 'settings',
          component: Settings
        }
      ]
    }
  ]
})
```

在这个例子中，我们定义了一个父路由 `/`，它的组件是 `Home`。它还有两个子路由 `/profile` 和 `/settings`，分别对应的组件是 `Profile` 和 `Settings`。

2、在父路由的组件中使用 `<router-view> `占位符。

```
<template>
  <div>
    <h1>Home</h1>
    <ul>
      <li><router-link to="/profile">Profile</router-link></li>
      <li><router-link to="/settings">Settings</router-link></li>
    </ul>
    <router-view></router-view>
  </div>
</template>
```

在父路由的组件中，我们使用 `<router-view>` 标签来占位子路由的位置。

3、在子路由的组件中同样使用 `<router-view>` 标签。

```
<template>
  <div>
    <h2>Profile</h2>
    <router-view></router-view>
  </div>
</template>
```

在子路由的组件中，我们同样使用 `<router-view>` 标签来占位子路由的位置。

通过以上三个步骤，我们就实现了路由的嵌套。当访问 `/profile` 路径时，Vue Router 会先加载父路由的组件 `Home`，然后根据子路由的路径拼接后再加载对应的子路由组件 `Profile`。同时，子路由的组件中同样可以嵌套其他子路由。

## 如何动态的添加路由对象？这样做的意义是什么？

动态添加路由对象可以在运行时根据具体的业务需求来动态生成路由，以实现更灵活的路由配置。

这样做的意义在于，当我们的应用程序需要根据用户的权限或其他因素动态生成一些路由时，我们就可以使用动态路由的方式来实现这个功能。

例如，当我们做关于后台管理系统相关的项目时，不同的人就会有不同的权限，那么不同的人对应能访问的页面能做的操作也就不同。

这个时候，前端路由就不能写死，一般情况下，路由会通过后端返回对应不同的人对应不同的数据，这个时候，就需要前端进行一个动态路由的添加，对应不同的权限，不同的页面显示。

Vue Router 提供了一些方法来动态添加路由对象：

1、通过 router.addRoute() 方法添加路由对象

```js
// 通过 addRoute 方法添加路由对象
router.addRoute({
  path: '/dynamic',
  component: () => import('@/views/Dynamic.vue')
})
```

2、通过 router.addRoutes() 方法添加一组路由对象

```js
// 通过 addRoutes 方法添加一组路由对象
router.addRoutes([
  {
    path: '/dynamic',
    component: () => import('@/views/Dynamic.vue')
  },
  {
    path: '/another',
    component: () => import('@/views/Another.vue')
  }
])
```

3、在使用动态路由的时候，我们需要注意以下几点：

1. 动态路由必须在路由实例化之后再添加，否则会出现路由无法匹配的问题；
2. 当我们动态添加路由之后，需要通过 `$router.push()` 或 `$router.replace()` 方法来触发路由的切换；
3. 当我们动态添加的路由是嵌套路由时，需要在父级路由中添加 `children` 属性来定义子路由。

总的来说，动态添加路由对象可以使我们的路由配置更加灵活和动态，使应用程序更好地适应各种业务场景。

## 如何定义动态路由？如何获取传过来的动态参数？

**（1）param方式**

- 配置路由格式：`/router/:id`
- 传递的方式：在path后面跟上对应的值
- 传递后形成的路径：`/router/123`

1）路由定义

```javascript
//在APP.vue中
<router-link :to="'/user/'+userId" replace>用户</router-link>    

//在index.js
{
   path: '/user/:userid',
   component: User,
},

```

2）路由跳转

```javascript
// 方法1：
<router-link :to="{ name: 'users', params: { uname: wade }}">按钮</router-link

// 方法2：
this.$router.push({name:'users',params:{uname:wade}})

// 方法3：
this.$router.push('/user/' + wade)

```

3）参数获取 通过 `$route.params.userid` 获取传递的值

**（2）query方式**

- 配置路由格式：`/router`，也就是普通配置
- 传递的方式：对象中使用query的key作为传递方式
- 传递后形成的路径：`/route?id=123`

1）路由定义

```javascript
//方式1：直接在router-link 标签上以对象的形式
<router-link :to="{path:'/profile',query:{name:'why',age:28,height:188}}">档案</router-link>

// 方式2：写成按钮以点击事件形式
<button @click='profileClick'>我的</button>    

profileClick(){
  this.$router.push({
    path: "/profile",
    query: {
        name: "kobi",
        age: "28",
        height: 198
    }
  });
}

```

2）跳转方法

```javascript
// 方法1：
<router-link :to="{ name: 'users', query: { uname: james }}">按钮</router-link>

// 方法2：
this.$router.push({ name: 'users', query:{ uname:james }})

// 方法3：
<router-link :to="{ path: '/user', query: { uname:james }}">按钮</router-link>

// 方法4：
this.$router.push({ path: '/user', query:{ uname:james }})

// 方法5：
this.$router.push('/user?uname=' + jsmes)

```

3）获取参数

```javascript
通过$route.query 获取传递的值

```

## Vue-router 路由钩子在生命周期的体现

一、Vue-Router导航守卫

有的时候，需要通过路由来进行一些操作，比如最常见的登录权限验证，当用户满足条件时，才让其进入导航，否则就取消跳转，并跳到登录页面让其登录。 为此有很多种方法可以植入路由的导航过程：全局的，单个路由独享的，或者组件级的

1、全局路由钩子

vue-router全局有三个路由钩子;

- router.beforeEach 全局前置守卫 进入路由之前
- router.beforeResolve 全局解析守卫（2.5.0+）在 beforeRouteEnter 调用之后调用
- router.afterEach 全局后置钩子 进入路由之后

具体使用∶

- beforeEach（判断是否登录了，没登录就跳转到登录页）

```javascript
router.beforeEach((to, from, next) => {  
    let ifInfo = Vue.prototype.$common.getSession('userData');  // 判断是否登录的存储信息
    if (!ifInfo) { 
        // sessionStorage里没有储存user信息    
        if (to.path == '/') { 
            //如果是登录页面路径，就直接next()      
            next();    
        } else { 
            //不然就跳转到登录      
            Message.warning("请重新登录！");     
            window.location.href = Vue.prototype.$loginUrl;    
        }  
    } else {    
        return next();  
    }
})

```

- afterEach （跳转之后滚动条回到顶部）

```javascript
router.afterEach((to, from) => {  
    // 跳转之后滚动条回到顶部  
    window.scrollTo(0,0);
});

```

2、单个路由独享钩子

**beforeEnter** 如果不想全局配置守卫的话，可以为某些路由单独配置守卫，有三个参数∶ to、from、next

```javascript
export default [    
    {        
        path: '/',        
        name: 'login',        
        component: login,        
        beforeEnter: (to, from, next) => {          
            console.log('即将进入登录页面')          
            next()        
        }    
    }
]

```

3、组件内钩子

beforeRouteUpdate、beforeRouteEnter、beforeRouteLeave

这三个钩子都有三个参数∶to、from、next

- beforeRouteEnter∶ 进入组件前触发
- beforeRouteUpdate∶ 当前地址改变并且改组件被复用时触发，举例来说，带有动态参数的路径foo/∶id，在 /foo/1 和 /foo/2 之间跳转的时候，由于会渲染同样的foa组件，这个钩子在这种情况下就会被调用
- beforeRouteLeave∶ 离开组件被调用

注意点，beforeRouteEnter组件内还访问不到this，因为该守卫执行前组件实例还没有被创建，需要传一个回调给 next来访问，例如：

```javascript
beforeRouteEnter(to, from, next) {      
    next(target => {        
        if (from.path == '/classProcess') {          
            target.isFromProcess = true        
        }      
    })    
}

```

二、Vue路由钩子在生命周期函数的体现

1. 完整的路由导航解析流程（不包括其他生命周期）

- 触发进入其他路由。
- 调用要离开路由的组件守卫beforeRouteLeave
- 调用局前置守卫∶ beforeEach
- 在重用的组件里调用 beforeRouteUpdate
- 调用路由独享守卫 beforeEnter。
- 解析异步路由组件。
- 在将要进入的路由组件中调用 beforeRouteEnter
- 调用全局解析守卫 beforeResolve
- 导航被确认。
- 调用全局后置钩子的 afterEach 钩子。
- 触发DOM更新（mounted）。
- 执行beforeRouteEnter 守卫中传给 next 的回调函数

4、触发钩子的完整顺序

路由导航、keep-alive、和组件生命周期钩子结合起来的，触发顺序，假设是从a组件离开，第一次进入b组件∶

- beforeRouteLeave：路由组件的组件离开路由前钩子，可取消路由离开。
- beforeEach：路由全局前置守卫，可用于登录验证、全局路由loading等。
- beforeEnter：路由独享守卫
- beforeRouteEnter：路由组件的组件进入路由前钩子。
- beforeResolve：路由全局解析守卫
- afterEach：路由全局后置钩子
- beforeCreate：组件生命周期，不能访问tAis。
- created;组件生命周期，可以访问tAis，不能访问dom。
- beforeMount：组件生命周期
- deactivated：离开缓存组件a，或者触发a的beforeDestroy和destroyed组件销毁钩子。
- mounted：访问/操作dom。
- activated：进入缓存组件，进入a的嵌套子组件（如果有的话）。
- 执行beforeRouteEnter回调函数next。

5、导航行为被触发到导航完成的整个过程

- 导航行为被触发，此时导航未被确认。
- 在失活的组件里调用离开守卫 beforeRouteLeave。
- 调用全局的 beforeEach守卫。
- 在重用的组件里调用 beforeRouteUpdate 守卫(2.2+)。
- 在路由配置里调用 beforeEnteY。
- 解析异步路由组件（如果有）。
- 在被激活的组件里调用 beforeRouteEnter。
- 调用全局的 beforeResolve 守卫（2.5+），标示解析阶段完成。
- 导航被确认。
- 调用全局的 afterEach 钩子。
- 非重用组件，开始组件实例的生命周期：beforeCreate&created、beforeMount&mounted
- 触发 DOM 更新。
- 用创建好的实例调用 beforeRouteEnter守卫中传给 next 的回调函数。
- 导航完成

## 什么是路由守卫？路由守卫有什么作用？

路由守卫（Route Guard）是 Vue Router 提供的一种机制，用于在导航到路由前、路由更新前、路由更新后、离开路由时等不同的阶段，对路由进行一些处理或控制。

路由守卫可以帮助我们实现很多常见的功能，例如：

- 用户登录状态控制：在用户未登录的情况下，禁止访问某些需要登录才能访问的页面。
- 权限控制：对于不同的用户，控制其可以访问的路由和页面。
- 路由重定向：对于某些路由，根据某些条件将其重定向到其他路由。
- 路由缓存：对于某些路由，进行缓存，以提升用户体验。
- 页面进度条：在路由切换时，显示一个进度条，提升用户体验等。

总之，路由守卫是一个非常有用的机制，可以帮助我们实现很多复杂的功能，让应用更加健壮和用户友好。

## 路由导航守卫有哪些？

Vue Router 提供了三种类型的导航守卫，可以在路由切换时执行相应的操作，这些导航守卫分别是：

1、全局导航守卫（Global Guard）：

对所有路由生效，即每次路由切换时都会触发。

- beforeResolve：在导航被确认之前，同时在所有组件内守卫和异步路由组件被解析之后调用。
- beforeEach：在导航被确认之前调用，可以用来进行身份验证等操作。
- afterEach：在导航被确认之后调用，可以用来进行页面统计等操作。

2、路由独享的守卫（Per-Route Guard）：

只对当前路由有效，即进入或离开该路由时才会触发。

- beforeEnter：在进入路由前调用，可以用来进行身份验证等操作。

3、组件内的守卫（Component Guard）：

只对当前路由匹配的组件有效，即进入或离开该组件时才会触发。

- beforeRouteEnter：在路由进入该组件前调用，该守卫无法访问组件实例，因此无法获取组件的数据等内容。
- beforeRouteUpdate：在当前路由复用该组件时调用，该守卫可以访问组件实例，因此可以进行更新操作。
- beforeRouteLeave：在路由离开该组件时调用，该守卫可以访问组件实例，因此可以进行保存数据等操作。

这些导航守卫可以让我们在路由切换前或切换后执行相应的操作，例如身份验证、页面统计、页面滚动等等。

# 📁 状态管理

## 什么是状态管理？如何理解“状态管理”？

**什么是状态管理？**

状态管理是指在复杂的应用程序中，通过统一的数据管理方式来管理应用程序中的状态。状态指的是应用程序中的数据和信息，如用户登录状态、应用程序的配置信息、用户的输入等等。在一个大型的应用程序中，状态管理可以让数据的变化和流动更加可控和可预测。

在状态管理中，通常采用集中式管理的方式来管理应用程序中的状态。这意味着所有的状态都被存储在一个集中的地方，并且可以被全局访问和修改。状态管理通常包括以下几个方面：

- 状态的定义：定义应用程序中的所有状态，并确定这些状态的初始值。
- 状态的修改：修改状态的值，通常是通过某种操作来触发状态的变化。
- 状态的获取：获取状态的值，通常是为了在应用程序的其他部分中使用该状态。

**有哪些状态管理工具**

在实现状态管理时，通常使用状态管理库，例如 Vue.js 中的 Vuex，React 中的 Redux 等。这些库提供了一些机制，如状态容器、状态更新的方式和状态订阅等，来帮助开发者管理应用程序中的状态。

**Vue中的状态管理**

在Vue.js中，状态管理模式的实现通常采用Vuex库。Vuex库的核心是store（仓库），store是一个容器，用于存储应用程序中的状态。Vuex中存储的数据是响应式的，当组件从store中读取状态时，如果数据发生变化，组件会自动更新。

要改变store中的状态，只能通过提交（commit）mutation的方式进行，mutation中只能有同步处理。如果需要进行异步处理，可以通过actions来实现，通过组件中dispatch的操作触发actions。这样就形成了一个生态圈，组件通过store来共享数据，通过mutation来改变数据，通过actions来处理异步操作。

## Vuex是单向数据流还是双向数据流？

在 Vuex 中，数据流是单向的从 State -> View -> Actions -> Mutations -> State。

也就是说，所有数据的流向都是单向的，不能直接修改 State 中的数据，需要通过提交 mutation 来修改。这种单向数据流的设计使得应用程序的状态变得可预测，易于调试和维护。

## Vuex 的原理

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

- Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
- 改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样可以方便地跟踪每一个状态的变化。

![b025e120ca3d0bd2ded3d038d58cacf4.jpg](E:\coder\09_OneNote\image\92fc4b2c6e414344b9b22bc057dcd39ctplv-k3u1fbpfcp-zoom-in-crop-mark1512000.webp) Vuex为Vue Components建立起了一个完整的生态圈，包括开发中的API调用一环。 

**（1)核心流程中的主要功能：**

- Vue Components 是 vue 组件，组件会触发（dispatch）一些事件或动作，也就是图中的 Actions;
- 在组件中发出的动作，肯定是想获取或者改变数据的，但是在 vuex 中，数据是集中管理的，不能直接去更改数据，所以会把这个动作提交（Commit）到 Mutations 中;
- 然后 Mutations 就去改变（Mutate）State 中的数据;
- 当 State 中的数据被改变之后，就会重新渲染（Render）到 Vue Components 中去，组件展示更新后的数据，完成一个流程。

**（2）各模块在核心流程中的主要功能：**

- `Vue Components`∶ Vue组件。HTML页面上，负责接收用户操作等交互行为，执行dispatch方法触发对应action进行回应。
- `dispatch`∶操作行为触发方法，是唯一能执行action的方法。
- `actions`∶ 操作行为处理模块。负责处理Vue Components接收到的所有交互行为。包含同步/异步操作，支持多个同名方法，按照注册的顺序依次触发。向后台API请求的操作就在这个模块中进行，包括触发其他action以及提交mutation的操作。该模块提供了Promise的封装，以支持action的链式触发。
- `commit`∶状态改变提交操作方法。对mutation进行提交，是唯一能执行mutation的方法。
- `mutations`∶状态改变操作方法。是Vuex修改state的唯一推荐方法，其他修改方式在严格模式下将会报错。该方法只能进行同步操作，且方法名只能全局唯一。操作之中会有一些hook暴露出来，以进行state的监控等。
- `state`∶ 页面状态管理容器对象。集中存储Vuecomponents中data对象的零散数据，全局唯一，以进行统一的状态管理。页面显示所需的数据从该对象中进行读取，利用Vue的细粒度数据响应机制来进行高效的状态更新。
- `getters`∶ state对象读取方法。图中没有单独列出该模块，应该被包含在了render中，Vue Components通过该方法读取全局state对象。

## Vuex的基本使用步骤是什么？

在Vue3中使用Vuex的基本步骤如下：

1、安装Vuex

```js
npm install vuex
```

2、在Vue中使用Vuex

在Vue3中，在组件中使用Vuex需要使用 `createStore` 方法来创建一个 store 实例。在组件中使用 `useStore` 方法来获取 store 实例，然后就可以在组件中访问 store 中的状态。

```js
import { createStore } from 'vuex'
import { useStore } from 'vuex'

const store = createStore({
  state () {
    return {
      count: 0
    }
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})

export default {
  setup () {
    const store = useStore()

    function incrementCount() {
      store.commit('increment')
    }

    return {
      incrementCount,
      count: store.state.count
    }
  }
}
```

3、在Vue应用中注入Vuex

```js
import { createApp } from 'vue'
import App from './App.vue'
import store from './store'

const app = createApp(App)
app.use(store)
app.mount('#app')
```

其中，`store` 对象是上一步创建的 store 实例。

4、在Vue应用中使用Vuex

在组件中，我们可以通过 `computed` 属性或 `methods` 方法来访问 store 中的状态或提交 mutations。例如：

```vue
<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="incrementCount">Increment</button>
  </div>
</template>

<script>
import { useStore } from 'vuex'

export default {
  setup () {
    const store = useStore()

    function incrementCount() {
      store.commit('increment')
    }

    return {
      incrementCount,
      count: store.state.count
    }
  }
}
</script>
```

以上是使用Vuex的基本步骤，其中包括创建 store、在组件中使用 store，以及在 Vue 应用中注入 store。在实际开发中，我们需要更深入地理解和使用 Vuex，以便更好地管理应用中的状态。

## 什么是单一状态树？

单一状态树是 Vuex 中的一个概念，指的是将整个应用的状态保存在一个单一的对象中，即 Vuex 的 state 对象。

Vuex 通过单一状态树来管理应用的状态，通过一个对象就包含了全部的应用层级的状态。将状态集中存储，方便开发者管理和维护，同时也方便调试和监控应用状态的变化。

**Vuex如何通过单一状态树管理诸多状态的？**

(modules)

当应用变得越来越复杂时，单一状态树的维护会变得比较困难，因为所有的状态都被存储在一个对象中。这时可以使用 Vuex 的 modules 来进行状态的拆分，将不同的状态存储在不同的模块中。

Vuex 的 modules 允许将 store 分割成多个小的 store，每个小的 store 都有自己的 state、mutation、action 和 getter。通过将 store 分割成多个模块，可以方便地管理和维护 store 中的状态。同时，modules 可以嵌套，因此可以创建更复杂的应用程序状态管理结构。

## Vuex有哪几种属性？

有五种，分别是 State、 Getter、Mutation 、Action、 Module

- state => 基本数据(数据源存放地)，类似于组件中data，存放数据，可以通过 this.$store.state 访问。
- getters => 从基本数据派生出来的数据，类型于组件中computed，可以通过 this.$store.getters 访问。
- mutations => 用于更改 State 中的数据，可以在里面进行同步操作，可以通过 this.$store.commit() 方法来调用 Mutation。
- actions => 用于包含任意异步操作，可以通过 this.$store.dispatch() 方法来调用 Action，在 Action 中可以调用 Mutation 中的方法来更改 State。
- modules => 用于将 State、Getter、Mutation、Action 模块化，更好地进行管理，使得大型应用更易于维护。

## Vuex和单纯的全局对象有什么区别？

- Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
- 不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样可以方便地跟踪每一个状态的变化，从而能够实现一些工具帮助更好地了解我们的应用。

## Vuex有哪些核心概念？以及作用？

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 包含以下核心概念：

**1、State（状态）：**

应用程序中需要管理的状态存储在一个单一的 state 对象中，所有组件都从该对象中读取状态数据。状态是响应式的，当状态发生改变时，所有依赖该状态的组件都会立即得到更新。

**2、Getter（派生状态）：**

Getter 用于从 state 中派生出一些状态，这些状态可以基于 store 中的 state 计算得到。Getter 类似于计算属性，当其依赖的 state 发生变化时，会重新计算。

Getter可以被多个组件共享和访问，也可以接受其他Getter作为依赖。

**3、Mutation（同步修改状态）：**

Mutation 是用来修改状态的唯一途径。Mutation 必须是同步函数，因为在 Vue.js 中，只有同步函数才能够被 DevTools 记录状态变更。这也保证了状态的可追踪性和可维护性。

**4、Action（异步修改状态）：**

Action 用来处理异步任务和复杂逻辑，Action 可以包含任意异步操作，并通过提交 Mutation 来修改状态。

例如API请求等，可以异步地修改状态，也可以触发其他Action。

**5、Module（模块）：**

Module 允许将 store 分割成模块，每个模块可以拥有自己的 state、mutation、action、getter，通过Module，可以将一个复杂的应用程序的状态树划分成多个小的状态树，方便维护和管理。从而使得 store 的结构更加清晰、易于维护。

这些核心概念组合在一起，构成了 Vuex 的基本架构。Vuex 的作用是简化 Vue.js 应用程序的状态管理。

通过 Vuex，我们可以将应用程序的状态存储在一个单一的 store 中，从而实现了状态的集中管理。

此外，Vuex 还提供了一系列工具和约束，可以帮助开发者更好地管理状态，避免状态的不合理修改，保证应用程序的状态变化是可预测的。

## Vuex中action和mutation的区别

mutation中的操作是一系列的同步函数，用于修改state中的变量的的状态。当使用vuex时需要通过commit来提交需要操作的内容。mutation 非常类似于事件：每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。这个回调函数就是实际进行状态更改的地方，并且它会接受 state 作为第一个参数：

```javascript
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      state.count++      // 变更状态
    }
  }
})

```

当触发一个类型为 increment 的 mutation 时，需要调用此函数：

```javascript
store.commit('increment')

```

而Action类似于mutation，不同点在于：

- Action 可以包含任意异步操作。
- Action 提交的是 mutation，而不是直接变更状态。

```javascript
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
})

```

Action 函数接受一个与 store 实例具有相同方法和属性的 context 对象，因此你可以调用 context.commit 提交一个 mutation，或者通过 context.state 和 context.getters 来获取 state 和 getters。 所以，两者的不同点如下：

- Mutation专注于修改State，理论上是修改State的唯一途径；Action业务代码、异步请求。
- Mutation：必须同步执行；Action：可以异步，但不能直接操作State。
- 在视图更新时，先触发actions，actions再触发mutation
- mutation的参数是state，它包含store中的数据；store的参数是context，它是 state 的父级，包含 state、getters

## 为什么 Vuex 的 mutation 中不能做异步操作？

- Vuex中所有的状态更新的唯一途径都是mutation，异步操作通过 Action 来提交 mutation实现，这样可以方便地跟踪每一个状态的变化，从而能够实现一些工具帮助更好地了解我们的应用。
- 每个mutation执行完成后都会对应到一个新的状态变更，这样devtools就可以打个快照存下来，然后就可以实现 time-travel 了。如果mutation支持异步操作，就没有办法知道状态是何时更新的，无法很好的进行状态的追踪，给调试带来困难。

## Vuex的严格模式是什么,有什么作用，如何开启？

在严格模式下，无论何时发生了状态变更且不是由mutation函数引起的，将会抛出错误。这能保证所有的状态变更都能被调试工具跟踪到。

在Vuex.Store 构造器选项中开启,如下

```php
const store = new Vuex.Store({
    strict:true,
})
```

## 如何在组件中批量使用Vuex的getter属性

使用mapGetters辅助函数, 利用对象展开运算符将getter混入computed 对象中

```javascript
import {mapGetters} from 'vuex'
export default{
    computed:{
        ...mapGetters(['total','discountTotal'])
    }
}
```

## 如何在组件中重复使用Vuex的mutation

使用mapMutations辅助函数,在组件中这么使用

```javascript
import { mapMutations } from 'vuex'
methods:{
    ...mapMutations({
        setNumber:'SET_NUMBER',
    })
}
```

然后调用`this.setNumber(10)`相当调用`this.$store.commit('SET_NUMBER',10)`

## Vuex 和 localStorage 的区别

**（1）最重要的区别**

- vuex存储在内存中
- localstorage 则以文件的方式存储在本地，只能存储字符串类型的数据，存储对象需要 JSON的stringify和parse方法进行处理。 读取内存比读取硬盘速度要快

**（2）应用场景**

- Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。vuex用于组件之间的传值。
- localstorage是本地存储，是将数据存储到浏览器的方法，一般是在跨页面传递数据时使用 。
- Vuex能做到数据的响应式，localstorage不能

**（3）永久性**

刷新页面时vuex存储的值会丢失，localstorage不会。

**注意：** 对于不变的数据确实可以用localstorage可以代替vuex，但是当两个组件共用一个数据源（对象或数组）时，如果其中一个组件改变了该数据源，希望另一个组件响应该变化时，localstorage无法做到，原因就是区别1。

## Redux 和 Vuex 有什么区别，它们的共同思想

**（1）Redux 和 Vuex区别**

- Vuex改进了Redux中的Action和Reducer函数，以mutations变化函数取代Reducer，无需switch，只需在对应的mutation函数里改变state值即可
- Vuex由于Vue自动重新渲染的特性，无需订阅重新渲染函数，只要生成新的State即可
- Vuex数据流的顺序是∶View调用store.commit提交对应的请求到Store中对应的mutation函数->store改变（vue检测到数据变化自动渲染）

通俗点理解就是，vuex 弱化 dispatch，通过commit进行 store状态的一次更变;取消了action概念，不必传入特定的 action形式进行指定变更;弱化reducer，基于commit参数直接对数据进行转变，使得框架更加简易;

**（2）共同思想**

- 单—的数据源
- 变化可以预测

本质上：redux与vuex都是对mvvm思想的服务，将数据从视图中抽离的一种方案; 形式上：vuex借鉴了redux，将store作为全局的数据中心，进行mode管理;

## 为什么要用 Vuex 或者 Redux

由于传参的方法对于多层嵌套的组件将会非常繁琐，并且对于兄弟组件间的状态传递无能为力。我们经常会采用父子组件直接引用或者通过事件来变更和同步状态的多份拷贝。以上的这些模式非常脆弱，通常会导致代码无法维护。

所以需要把组件的共享状态抽取出来，以一个全局单例模式管理。在这种模式下，组件树构成了一个巨大的"视图"，不管在树的哪个位置，任何组件都能获取状态或者触发行为。

另外，通过定义和隔离状态管理中的各种概念并强制遵守一定的规则，代码将会变得更结构化且易维护。

## Vuex是否可以用来管理组件的普通状态和代码逻辑？(思考)

可以 但是没必要！

在Vue.js应用程序中，组件状态和组件的业务逻辑通常是由组件自身来维护和管理的。vuex中一般用于一些公用的状态管理，只有当需要多个组件之间共享某些状态或者实现复杂的组件通信逻辑时，才会考虑使用Vuex来进行全局状态的管理。没有必要全都放在vuex中管理。

虽然可以使用Vuex来管理组件的普通状态和代码逻辑，但是这种做法会增加代码的复杂性和维护难度，同时也会导致组件的耦合度过高，降低代码的可维护性和可重用性。

因此，在大多数情况下，我们应该将组件的状态和业务逻辑限定在组件自身范围内，避免过度依赖Vuex来进行全局状态管理。

## Vuex中如何发送异步请求，以及组件如何知道异步请求的结果？

在Vuex中，异步请求应该放在action函数中发送。由于mutation函数必须是同步函数，如果直接在mutation函数中发送异步请求，会导致devtools无法进行数据追踪。

因此，我们需要在action函数中发送异步请求，请求到数据后再通过提交mutation的方式，将请求到的数据传递给mutation函数。mutation函数接收到action提交的数据后，可以直接修改state中的数据，修改完state数据后，数据就会被保存在state中。

为了让组件知道异步请求的结果，我们需要在action函数中返回一个Promise对象。在这个Promise对象中发送网络请求，在请求完成后，将数据通过提交mutation的方式传递给mutation函数。此时，在Promise对象中主动调用resolve函数，将请求到的数据传递给resolve函数。当我们在组件中派发action函数时，会返回一个Promise对象，我们可以通过调用then函数，拿到resolve函数中传递过来的结果，这样就可以知道异步请求的结果了。

组件可以通过直接在state中访问保存的数据，来获取异步请求的结果。例如，如果我们将请求到的数据保存在state的banners属性中，组件可以通过访问$store.state.banners来获取异步请求的结果。

## Vuex如何做持久化存储

在Vuex中实现持久化存储，可以使用第三方插件vuex-persistedstate，它可以将 Vuex 的 state 持久化到本地存储中，当页面刷新或重新打开时，可以从本地存储中恢复 state。

使用方法如下：

1.安装vuex-persistedstate插件

```
npm install vuex-persistedstate
```

2.在store/index.js中引入vuex-persistedstate并使用

```js
import createPersistedState from 'vuex-persistedstate'

const store = createStore({
  // ...
  plugins: [createPersistedState()]
})
```

这样就会将 Vuex 的 state 存储到本地存储中。如果需要将数据存储到 sessionStorage 而不是 localStorage 中，可以在 createPersistedState 的配置项中指定 storage 选项，例如：

```js
import createPersistedState from 'vuex-persistedstate'

const store = createStore({
  // ...
  plugins: [createPersistedState({
    storage: window.sessionStorage
  })]
})
```

这样就会将 Vuex 的 state 存储到 sessionStorage 中。

3.如果需要只存储部分 state 中的数据，可以在 createPersistedState 的配置项中指定 paths 选项，例如：

```js
import createPersistedState from 'vuex-persistedstate'

const store = createStore({
  // ...
  plugins: [createPersistedState({
    paths: ['user'] // 只存储 user 模块中的数据
  })]
})
```

这样就只会将 user 模块中的数据存储到本地存储中。

需要注意的是，由于使用了本地存储，需要对存储的数据进行管理，防止存储过多数据造成性能问题。另外，也需要注意本地存储的安全性问题。

## createPersistedState 是什么？

`createPersistedState` 是一个用于 Vuex 持久化存储的插件，可以将 Vuex 状态持久化到浏览器本地存储中。除了默认的配置项外，`createPersistedState` 还可以通过传入一个配置对象来进行配置。

以下是一些常用的配置选项：

- `key`: 存储在本地存储中的键名，默认为 `'vuex'`。
- `storage`: 存储方式，默认为 `window.localStorage`。可以设置为 `window.sessionStorage` 或其他实现了 `setItem` 和 `getItem` 方法的对象。
- `reducer`: 定义一个函数，用于定制持久化哪些 state，在函数中通过对象的键名来筛选出需要持久化的 state。
- `filter`: 与 `reducer` 类似，用于排除某些状态不需要被持久化。
- `subscriber`: 定义一个函数，用于订阅 Vuex store 的变化，在 store 变化时自动将变化的 state 进行持久化。
- `setState`: 定义一个函数，用于自定义将 state 写入本地存储的方式。例如可以对 state 进行加密后再进行存储。

下面是一个例子，展示了如何在创建 `createPersistedState` 插件时传入配置对象：

```js
import createPersistedState from 'vuex-persistedstate'

const persistedState = createPersistedState({
  key: 'my-app',
  storage: window.sessionStorage,
  reducer: state => ({
    user: state.user,
    settings: state.settings
  }),
  filter: mutation => mutation.type === 'LOGIN',
  subscriber: store => {
    store.subscribe((mutation, state) => {
      console.log('state changed', state)
    })
  },
  setState: (key, state, storage) => {
    const data = JSON.stringify(state)
    // 对 state 进行加密
    const encrypted = encrypt(data)
    storage.setItem(key, encrypted)
  }
})

export default new Vuex.Store({
  plugins: [persistedState],
  // ...
})
```

这里的配置选项中，定义了一个存储键名为 `'my-app'`，存储方式为 `window.sessionStorage`，持久化 `state` 中的 `user` 和 `settings`，过滤掉所有不是 `'LOGIN'` 的 mutation，定义了一个订阅者函数，并自定义了将 state 写入本地存储的方式。

## Vuex如何划分模块？什么是命名空间？

在Vuex中，模块可以通过将store对象分解为模块来划分。每个模块拥有自己的state、mutation、action、getter等属性，这些属性可以独立于其他模块进行管理。这样可以使得状态管理更加清晰，同时可以避免在大型应用中状态变得混乱和复杂。

在Vue 3中，模块定义方式和Vue 2稍有不同，需要使用`createStore`函数来创建store对象。具体定义方式如下：

```js
import { createStore } from 'vuex'

const moduleA = {
  state: {},
  mutations: {},
  actions: {},
  getters: {}
}

const moduleB = {
  state: {},
  mutations: {},
  actions: {},
  getters: {}
}

const store = createStore({
  modules: {
    moduleA,
    moduleB
  }
})
```

在上述例子中，我们定义了两个模块`moduleA`和`moduleB`，它们被包含在`modules`对象中，最终被传递给`createStore`函数，创建了一个包含这两个模块的store对象。

当我们在组件中访问模块中的状态或者提交模块中的mutation时，需要使用模块的命名空间。命名空间是一个可选项，它可以确保模块中的所有状态和操作都不会与全局命名空间冲突。在模块中定义命名空间可以通过`namespaced`属性来实现，具体示例如下：

```js
const moduleA = {
  namespaced: true,
  state: {},
  mutations: {},
  actions: {},
  getters: {}
}
```

在上述例子中，我们设置了`moduleA`模块的命名空间为true，因此在组件中访问该模块的状态或者提交该模块的mutation时，需要在前面加上命名空间，例如：

```js
this.$store.commit('moduleA/updateName', 'new name')
this.$store.state.moduleA.name
```

使用命名空间可以帮助我们更好地组织和管理Vuex的状态，避免状态冲突，并提高代码的可读性。

## 为什么需要加命名空间

在 Vuex 中使用模块时，每个模块都有自己的局部状态、getters、mutations 和 actions。当您在组件中访问模块中的状态或触发模块中的 mutations 或 actions 时，如果没有命名空间，Vuex 就无法确定这些操作应该应用于哪个模块。

通过添加命名空间，您可以指定该操作是针对哪个模块的。使用命名空间的方式有两种：

1、字符串方式命名空间：在 `mapState`、`mapGetters`、`mapMutations` 和 `mapActions` 辅助函数中使用字符串来指定命名空间，如下所示：

```
...mapState({
  someState: state => state.moduleName,someState
})
```

在这个例子中，`moduleName` 就是模块的命名空间。

2、对象方式命名空间：在组件中直接使用 `$store` 时，可以在提交 mutations 或触发 actions 时使用对象来指定命名空间，如下所示：

```
this.$store.commit("moduleName/someMutation", payload)
this.$store.dispatch("moduleName/someAction", payload)
```

在这个例子中，`moduleName` 就是模块的命名空间。


通过指定命名空间，您可以确保操作只针对特定的模块，从而避免状态或操作的名称冲突，使得代码更加清晰和易于维护。

## 什么是Pinia？和Vuex有什么区别？

pinia是一个用于对状态进行管理的库，跨组件跨页面对状态进行共享，与vuex和redux在作用上并无区别

1、区别

pinia没有mutations选项，因为mutations的出现解决的问题是让devtools进行状态追踪

- 但是随着技术的发展，pinia已经解决的这个没有mutation依然可以跟踪状态的问题

我们可以在任意组件中拿到store然后直接修改state中的任意值

不再需要modules这样的嵌套结构，取而代之的是可以创建一个个store

- 想要用时直接拿到store：const homeStore = useHome()，然后直接使用即可
- 想要拿到别的store，也是直接拿：const aboutStore = useAbout()，然后用就行
- 你可以在一个组件中拿任意数量的store
- 除此之外你还可以在某个store中拿另外的store，然后使用store中的任何东西
- 比如你想在某个store的某个getter函数中使用其他store的某个getter函数，在当前getter函数中可以这么写：
  - const aboutStore = useAbout();
  - aboutStore.某个about中getter函数

2、使用上的区别

- 我们在vuex中使用某个state时，需要$store.state.xxx
  - 在pinia中直接拿到store之后store.xxx即可

- 我们在vuex中使用某个getter函数时，需要$store.getters.xxx
  - 在pinia中拿到store后，store.xxx即可

- 在vuex中进行异步请求需要派发action函数
  - 在pinia中拿到store后，直接调用action函数即可

- 在getter函数中，第一个参数是state，可以通过这个参数拿state
  - 除了这个还可以通过this拿到当前的整个store，使用里面state、getter函数或者action函数

- 在action函数中，没有固定的参数，如果有参数，也是在调用action函数时传递过来的参数
  - 只能通过this拿到当前的store，再拿state进行赋值

## Pinia中有哪些核心概念，如何使用这些核心概念？

1、state

- state是一个选项，这个选项的值需要是一个函数，函数返回一个对象，对象中存储数据
- 在组件中拿到当前的store直接使用即可，store.xxx

2、getters

- getters也是一个选项，这个选项的值是一个对象，对象中存储着一个个函数，每个函数可以有一个参数state，通过state可以获取到当前store的state
- 除此之外每个函数还可以拿到一个this，这个this就是当前的整个store实例
- 通过这个this，可以想用谁就用谁
- 在组件中使用也是拿到store直接store.xxx即可

3、actions

- 在actions中，主要存放一个个函数，每个函数最主要的工作发送异步请求，获取到数据后直接修改state
- 每个action函数并不像getter函数一样，第一个参数是state，它可以没有参数
- 需要通过this拿到state然后再修改state中的值
- 在组件中拿到store后直接调用即可，store.xxx()
  - 如果你在此时传递参数，那么就可以在action中拿到参数

⭐没有模块的概念！！！

- 在vuex中会有modules的概念
- 但是在pinia中没有，想要有相同的概念，只需要多创建结构store即可
- store与store之前没有什么必然的联系
- 如果你想在某个store中使用另一个store中的内容，只需要拿到那个store使用里面的内容即可，灵活

## state三种写法的区别

以下是三种写法的具体示例：

第一种写法：

```js
export default {
  name: 'MyComponent',
  state: () => ({
    count: 0,
    message: 'Hello, world!'
  })
}
```

在这个示例中，`state` 使用了箭头函数，它返回一个对象字面量，其中包含两个属性：`count` 和 `message`。这个函数在组件被实例化时执行，并返回一个初始状态对象。

第二种写法：

```js
export default {
  name: 'MyComponent',
  state () {
    return {
      count: 0,
      message: 'Hello, world!'
    }
  }
}
```

在这个示例中，`state` 使用了普通函数，它返回一个对象字面量。这个函数在组件被实例化时执行，您可以在这个函数中编写任意 JavaScript 代码来动态计算状态对象。这个示例中，我们返回了一个具有两个属性的初始状态对象。

第三种写法：

```js
export default {
  name: 'MyComponent',
  state: {
    count: 0,
    message: 'Hello, world!'
  }
}
```

在这个示例中，`state` 直接使用了 ES6 对象字面量语法来定义初始状态对象。这个写法在语法上最简洁明了，但它只适用于定义简单的状态对象，并且不支持动态计算状态。

**三者用法上用什么区别**

这三种写法的用法上主要区别在于：

- 箭头函数写法适用于简单的状态对象，但不能在函数中进行复杂的计算，且无法访问组件实例。
- 普通函数写法适用于需要动态计算状态对象的情况。在函数中可以编写任意 JavaScript 代码来计算状态对象，但无法访问组件实例。
- 对象字面量写法适用于定义简单的状态对象。这种写法最简洁明了，但不支持动态计算状态，也无法访问组件实例。

在实际应用中，您可以根据组件的需求来选择适合的写法。如果您需要动态计算状态对象，可以使用普通函数写法；如果您只需要定义简单的状态对象，可以使用对象字面量写法或箭头函数写法。

## 对axios进行封装

```js
import axios from 'axios'
// 导入axios库

import { BASE_URL, TIMEOUT } from './config'
// 导入配置文件中的基础url和超时时间

class DQRequest {
  constructor(baseURL, timeout=10000) {
    // 构造函数，接收基础url和超时时间，如果没有超时时间，默认为10000毫秒
    this.instance = axios.create({
      baseURL,
      timeout
    })
    // 创建axios实例，将基础url和超时时间传递给axios实例
  }

  request(config) {
    // 发送请求的方法
    return new Promise((resolve, reject) => {
      // 返回一个promise对象，包含resolve和reject函数
      this.instance.request(config).then(res => {
        // 使用axios实例的request方法发送请求，当请求成功时，调用resolve函数，返回响应数据
        resolve(res.data)
      }).catch(err => {
        // 当请求失败时，调用reject函数，返回错误信息
        reject(err)
      })
    })
  }

  get(config) {
    // 发送get请求的方法，接收一个config对象
    return this.request({ ...config, method: "get" })
    // 调用request方法，将config对象和请求方法传递给request方法
  }

  post(config) {
    // 发送post请求的方法，接收一个config对象
    return this.request({ ...config, method: "post" })
    // 调用request方法，将config对象和请求方法传递给request方法
  }
}

export default new DQRequest(BASE_URL, TIMEOUT)
// 导出DQRequest类的实例，将基础url和超时时间传递给DQRequest的构造函数
```

> 这段代码定义了一个名为DQRequest的类，该类用于封装axios库，提供发送get和post请求的方法，并将请求结果以promise对象的形式返回。
> 在该类的构造函数中，使用axios.create方法创建了一个axios实例，并将基础url和超时时间传递给该实例。
> 该类的request方法使用axios实例发送请求，并在请求成功或失败时返回promise对象。
> 该类的get和post方法分别调用request方法，将请求方法设置为get或post，同时将config对象传递给request方法。最后，该类的实例被导出，并在实例化时传递了基础url和超时时间。

这段代码是一个用于封装 HTTP 请求的 JavaScript 类，使用了 axios 库进行网络请求。主要包括以下几个部分：

1. 导入 axios 库和配置参数：使用了 import 语法导入了 axios 库，并从 config.js 文件中导入了 BASE_URL 和 TIMEOUT 两个常量，分别表示请求的基础 URL 和超时时间。
2. 定义 DQRequest 类：使用了 class 关键字定义了一个名为 DQRequest 的类。在类的构造函数中，通过调用 axios.create 方法创建了一个 axios 实例，并将 baseURL 和 timeout 参数传递给该实例。在该类中，还定义了 request、get 和 post 三个方法。
3. request 方法：request 方法接受一个 config 参数，该参数包含了请求的各种配置信息，例如 URL、请求方法、请求头、请求体等等。该方法内部使用 axios 实例的 request 方法发起网络请求，并通过 Promise 对象返回响应数据或错误信息。
4. get 方法：get 方法接受一个 config 参数，该参数同样包含了请求的配置信息。该方法使用 request 方法发起一个 GET 请求，并将 method 参数设为 "get"。
5. post 方法：post 方法与 get 方法类似，不同之处在于使用 request 方法发起一个 POST 请求，并将 method 参数设为 "post"。
6. 导出 DQRequest 实例：使用了 export default 语法导出了一个 DQRequest 类的实例，并传递了 BASE_URL 和 TIMEOUT 两个参数。这意味着该实例可以在其他模块中被导入并使用，以发起网络请求。

> 在这段代码中，使用了axios库来发送HTTP请求。axios是一个基于Promise的HTTP客户端，可以用于浏览器和Node.js环境。使用axios库可以方便地进行HTTP请求，并且支持拦截器、请求和响应的转换、取消请求等功能。
>
> DQRequest类是对axios库的进一步封装，目的是将一些公共的配置封装在一个类中，避免重复代码和出错的风险。在构造函数中，使用axios.create方法创建了一个axios实例，并将基础url和超时时间传递给该实例。通过这种方式，每次发送请求时就可以直接使用该实例，无需重复设置基础url和超时时间。
>
> DQRequest类的request方法用于发送HTTP请求。该方法接收一个config对象，该对象包含了请求的相关配置，例如URL、请求方法、请求头、请求参数等。在该方法内部，使用axios实例的request方法发送HTTP请求，并在请求成功或失败时返回一个promise对象，该对象将请求的响应数据或错误信息作为参数传递给resolve或reject函数。
>
> DQRequest类的get和post方法分别用于发送GET和POST请求。这两个方法调用request方法，并将请求方法设置为get或post，同时将config对象传递给request方法。由于GET和POST请求是最常用的两种请求方式，因此这两个方法的封装可以大大简化发送HTTP请求的代码。
>
> 综上所述，DQRequest类的封装可以使得发送HTTP请求的代码更加简洁、易于维护和复用，并且可以方便地添加拦截器、统一处理错误信息等功能。

## GET请求和POST请求的区别

GET请求和POST请求是HTTP协议中常用的两种请求方式，它们之间的主要区别如下：

1、参数传递方式

- GET请求的参数通过URL的查询字符串(query string)传递，即参数会以"?key=value"的形式附在URL后面，多个参数之间使用"&"符号分隔。
- POST请求的参数则包含在请求体(body)中，而不是附在URL后面，因此在请求体中可以传递更大的数据量，且相对于GET请求更安全。

2、请求语义

- GET请求用于请求特定资源，通常用于获取资源，如获取文章列表或获取单篇文章详情等，它是幂等的，即多次重复的GET请求不会对服务器产生影响。
- POST请求则用于向服务器提交数据，通常用于创建或更新资源，如创建新的文章或修改文章详情等，它是非幂等的，即多次重复的POST请求会创建多个相同的资源。

3、缓存处理

- GET请求可以被缓存，因为它的请求参数直接附在URL后面，服务器可以直接根据URL来响应请求。
- POST请求不可以被缓存，因为它的请求参数包含在请求体中，服务器不能直接根据URL来响应请求，需要对请求头中的一些信息进行处理后才能响应请求。

> 综上所述，GET请求适用于请求数据量较小、安全性要求不高、请求幂等的场景，而POST请求适用于需要向服务器提交数据、请求数据量较大、安全性要求较高、请求非幂等的场景。

# 📁 Vue高级

## Vue中如何实现自定义指令？

在Vue 3中，可以使用 `directive` 函数来定义自定义指令。

下面是一个简单的例子，展示如何使用 `directive` 函数来创建一个名为 `highlight` 的自定义指令，它将文本的背景色设置为黄色：

```js
import { createApp } from 'vue';

const app = createApp({});

app.directive('highlight', {
  beforeMount(el, binding) {
    el.style.backgroundColor = binding.value;
  }
});

// 在模板中使用该指令
<template>
  <div v-highlight="'yellow'">这段文本的背景色将会变成黄色</div>
</template>
```

在这个例子中，`directive` 函数的第一个参数是指令名称 `highlight`，第二个参数是一个对象，包含了指令的钩子函数。在这个例子中，我们只定义了一个 `beforeMount` 钩子函数，该函数会在指令绑定的元素插入文档之前被调用。

`beforeMount` 钩子函数接收两个参数：指令绑定的元素 `el` 和指令的绑定值 `binding`。在这个例子中，我们从 `binding` 中获取了指令的值 `binding.value`，并将其作为背景色设置到了元素的样式中。

在模板中，我们可以通过 `v-highlight="'yellow'"` 将指令绑定到一个元素上。在这个例子中，我们将元素的背景色设置为黄色。

除了 `beforeMount` 钩子函数，Vue 3还提供了一系列其他的钩子函数，例如 `beforeUpdate`、`mounted`、`updated`、`beforeUnmount`、`unmounted` 等，开发者可以根据自己的需求来选择相应的钩子函数。

## 自定义指令的两种方式和生命周期？

在Vue 3中，有两种方式来定义自定义指令：全局注册和局部注册。

一、全局注册自定义指令

全局注册自定义指令是指在应用程序的入口处注册指令，然后在应用程序中的任何地方都可以使用该指令。可以使用 `app.directive()` 方法在全局范围内注册自定义指令。

下面是一个全局注册自定义指令的例子，展示了指令的常见生命周期钩子：

```js
import { createApp } from 'vue';

const app = createApp({});

app.directive('my-directive', {
  // 当绑定的元素插入到DOM中时调用
  mounted(el) {
    console.log('mounted');
  },
  // 当绑定的元素更新时调用
  updated(el) {
    console.log('updated');
  },
  // 当绑定的元素从DOM中移除时调用
  unmounted(el) {
    console.log('unmounted');
  }
});

export default app;
```

在这个例子中，我们使用 `app.directive()` 方法来全局注册了一个名为 `my-directive` 的自定义指令。指令对象包含了三个生命周期钩子：`mounted`、`updated`、`unmounted`。这些钩子函数将在指令绑定的元素插入到DOM中、更新、以及从DOM中移除时分别被调用。

二、局部注册自定义指令

局部注册自定义指令是指在组件中注册指令，该指令只能在该组件中使用。可以使用 `directives` 选项在组件中注册自定义指令。

下面是一个局部注册自定义指令的例子，展示了指令的常见生命周期钩子：

```js
import { defineComponent } from 'vue';

export default defineComponent({
  directives: {
    'my-directive': {
      // 当绑定的元素插入到DOM中时调用
      mounted(el) {
        console.log('mounted');
      },
      // 当绑定的元素更新时调用
      updated(el) {
        console.log('updated');
      },
      // 当绑定的元素从DOM中移除时调用
      unmounted(el) {
        console.log('unmounted');
      }
    }
  }
});
```

在这个例子中，我们使用 `directives` 选项在组件中注册了一个名为 `my-directive` 的自定义指令。指令对象包含了三个生命周期钩子：`mounted`、`updated`、`unmounted`。这些钩子函数将在指令绑定的元素插入到DOM中、更新、以及从DOM中移除时分别被调用。

## 描述下Vue自定义指令

在 Vue2.0 中，代码复用和抽象的主要形式是组件。然而，有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令。 一般需要对DOM元素进行底层操作时使用，尽量只用来操作 DOM展示，不修改内部的值。当使用自定义指令直接修改 value 值时绑定v-model的值也不会同步更新；如必须修改可以在自定义指令中使用keydown事件，在vue组件中使用 change事件，回调中修改vue数据;

**（1）自定义指令基本内容**

- 全局定义：`Vue.directive("focus",{})`

- 局部定义：`directives:{focus:{}}`

- 钩子函数：指令定义对象提供钩子函数

  o bind：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。

  o inSerted：被绑定元素插入父节点时调用（仅保证父节点存在，但不一定已被插入文档中）。

  o update：所在组件的VNode更新时调用，但是可能发生在其子VNode更新之前调用。指令的值可能发生了改变，也可能没有。但是可以通过比较更新前后的值来忽略不必要的模板更新。

  o ComponentUpdate：指令所在组件的 VNode及其子VNode全部更新后调用。

  o unbind：只调用一次，指令与元素解绑时调用。

- 钩子函数参数 o el：绑定元素

  o bing： 指令核心对象，描述指令全部信息属性

  o name

  o value

  o oldValue

  o expression

  o arg

  o modifers

  o vnode  虚拟节点

  o oldVnode：上一个虚拟节点（更新钩子函数中才有用）

**（2）使用场景**

- 普通DOM元素进行底层操作的时候，可以使用自定义指令
- 自定义指令是用来操作DOM的。尽管Vue推崇数据驱动视图的理念，但并非所有情况都适合数据驱动。自定义指令就是一种有效的补充和扩展，不仅可用于定义任何的DOM操作，并且是可复用的。

**（3）使用案例**

初级应用：

- 鼠标聚焦
- 下拉菜单
- 相对时间转换
- 滚动动画

高级应用：

- 自定义指令实现图片懒加载
- 自定义指令集成第三方插件

## Vue中如何安装插件，使用方法有哪些？

在 Vue 3 中，可以通过 `createApp` 函数的 `use` 方法来安装插件。`use` 方法接收一个插件对象或一个包含 `install` 方法的对象，并调用其 `install` 方法来安装插件。

下面是一个安装并使用插件的例子：

```javascript
import { createApp } from 'vue';
import MyPlugin from './my-plugin';

const app = createApp({...});

app.use(MyPlugin);

app.mount('#app');
```

在这个例子中，我们通过 `import` 引入一个名为 `MyPlugin` 的插件，然后在 `createApp` 实例上调用 `use` 方法来安装该插件。

插件对象需要实现一个名为 `install` 的静态方法，该方法接收应用实例作为第一个参数。除此之外，该方法还可以接收其他可选参数。

以下是一个简单的示例，演示了如何编写一个 Vue 插件：

```javascript
const MyPlugin = {
  install(app, options) {
    app.config.globalProperties.$myPlugin = options.value;
  }
};

export default MyPlugin;
```

在这个例子中，我们定义了一个名为 `MyPlugin` 的插件，它有一个名为 `install` 的静态方法。该方法将 `options.value` 注册为全局属性 `$myPlugin`，以便在应用程序的任何组件中使用。

另外，插件还可以通过全局 API 注册组件、指令或混入等功能。下面是一个例子，演示了如何在插件中注册全局组件：

```javascript
import MyComponent from './MyComponent.vue';

const MyPlugin = {
  install(app, options) {
    app.component('my-component', MyComponent);
  }
};

export default MyPlugin;
```

在这个例子中，我们定义了一个名为 `MyComponent` 的组件，然后在插件的 `install` 方法中使用 `app.component` 方法将该组件注册为全局组件。

总之，使用 Vue 3 中的 `use` 方法，我们可以轻松地安装和使用 Vue 插件，并且插件可以扩展应用程序的功能，使其更加灵活和易于开发。

## 什么是render函数、jsx语法是什么？(面试)

Vue 3 中的 `render` 函数是用于创建虚拟 DOM 的函数，它接收一个上下文对象作为参数，并返回一个虚拟 DOM 对象。这个函数可以手动编写，也可以使用 Vue 提供的 JSX 语法来编写。使用 `render` 函数的好处是可以直接操作虚拟 DOM，而不需要通过模板进行中间转换，从而提高了性能。

JSX 是一种 JavaScript 语法扩展，它允许开发者在 JavaScript 中编写类似于 HTML 的代码。在 Vue 3 中，可以使用 JSX 语法来编写 `render` 函数。通过在 JavaScript 中编写类似于 HTML 的代码，可以使代码更加直观和易于维护。

在使用 JSX 语法时，需要使用 `@vue/babel-plugin-jsx` 这个插件进行编译。在编写 `render` 函数时，需要使用 `createElement` 函数来创建虚拟 DOM 对象。`createElement` 函数接收三个参数，第一个参数表示要创建的元素类型，第二个参数是一个对象，表示该元素的属性和事件，第三个参数是元素的子元素。例如，可以使用以下代码来创建一个简单的 `render` 函数：

```js
import { h } from 'vue'

const App = {
  render() {
    return (
      <div id="app">
        <h1>Hello World</h1>
        <p>This is a paragraph.</p>
      </div>
    )
  }
}
```

在上面的代码中，使用了 `h` 函数来创建虚拟 DOM 对象，`h` 函数是 Vue 3 提供的一个别名，可以使用它来替代 `createElement` 函数。



`render`函数是React中的一个重要函数，它用于将React组件渲染为虚拟DOM元素，并最终渲染为实际的HTML元素，展示给用户。在React中，`render`函数是必须实现的函数。

JSX是一种语法扩展，它可以让我们在JavaScript代码中编写类似于HTML的标记，使得我们可以更加直观地描述UI组件的结构和样式。JSX语法本质上是一种语法糖，它被转换为`React.createElement()`函数调用，最终生成虚拟DOM元素。

在React中，我们通常使用JSX语法编写组件的UI代码，然后将其传递给`render`函数进行渲染。下面是一个使用JSX语法编写的React组件的例子：

```vue
import React from 'react';

function MyComponent(props) {
  return (
    <div className="my-component">
      <h1>{props.title}</h1>
      <p>{props.description}</p>
    </div>
  );
}
```

在这个例子中，我们定义了一个名为`MyComponent`的函数组件，它接收一个`props`参数。我们使用JSX语法来描述这个组件的UI结构，包括一个`div`元素、一个`h1`元素和一个`p`元素。我们使用`props`参数中的数据来填充`h1`和`p`元素中的内容。最终，当我们调用`render`函数并将`MyComponent`作为参数传递给它时，React将会根据我们的JSX代码生成虚拟DOM元素，并最终渲染为实际的HTML元素。

## Vue中实现动画的组件有哪些？实现动画的本质是什么？

一、Vue 3.0 中实现动画的组件主要有以下几种：

1、transition

可以在元素插入或移除时添加过渡效果；

2、transition-group

可以在多个元素同时插入或移除时添加过渡效果；

3、teleport

可以在不同的 DOM 节点之间移动元素，并且支持过渡效果；

4、keep-alive

可以将组件缓存起来，并在组件切换时触发过渡效果。

实现动画的本质是通过 CSS 过渡和动画来实现的。Vue 3 中通过在元素上添加 `transition`、`animation` 等 CSS 类名来触发动画效果，同时可以通过 JavaScript 配合 CSS 动态地添加或删除这些类名，从而实现过渡或动画效果。

二、具体来说，Vue 3 中通过以下几个步骤来实现动画效果：

1. 为需要添加动画效果的元素添加过渡或动画类名；
2. 监听元素的过渡或动画事件，例如 `transitionend`、`animationend` 等；
3. 在事件回调函数中添加或删除过渡或动画类名，以触发过渡或动画效果。

通过这些步骤，可以很方便地实现各种动画效果，例如淡入淡出、滑动、旋转等。同时，Vue 3 还提供了丰富的配置选项和钩子函数，可以进一步控制动画的细节。、

## Vue是如何收集依赖的？

在初始化 Vue 的每个组件时，会对组件的 data 进行初始化，就会将由普通对象变成响应式对象，在这个过程中便会进行依赖收集的相关逻辑，如下所示∶

```javascript
function defieneReactive (obj, key, val){
  const dep = new Dep();
  ...
  Object.defineProperty(obj, key, {
    ...
    get: function reactiveGetter () {
      if(Dep.target){
        dep.depend();
        ...
      }
      return val
    }
    ...
  })
}

```

以上只保留了关键代码，主要就是 `const dep = new Dep()`实例化一个 Dep 的实例，然后在 get 函数中通过 `dep.depend()` 进行依赖收集。 **（1）Dep** Dep是整个依赖收集的核心，其关键代码如下：

```javascript
class Dep {
  static target;
  subs;

  constructor () {
    ...
    this.subs = [];
  }
  addSub (sub) {
    this.subs.push(sub)
  }
  removeSub (sub) {
    remove(this.sub, sub)
  }
  depend () {
    if(Dep.target){
      Dep.target.addDep(this)
    }
  }
  notify () {
    const subs = this.subds.slice();
    for(let i = 0;i < subs.length; i++){
      subs[i].update()
    }
  }
}

```

Dep 是一个 class ，其中有一个关 键的静态属性 static，它指向了一个全局唯一 Watcher，保证了同一时间全局只有一个 watcher 被计算，另一个属性 subs 则是一个 Watcher 的数组，所以 Dep 实际上就是对 Watcher 的管理，再看看 Watcher 的相关代码∶

**（2）Watcher**

```javascript
class Watcher {
  getter;
  ...
  constructor (vm, expression){
    ...
    this.getter = expression;
    this.get();
  }
  get () {
    pushTarget(this);
    value = this.getter.call(vm, vm)
    ...
    return value
  }
  addDep (dep){
        ...
    dep.addSub(this)
  }
  ...
}
function pushTarget (_target) {
  Dep.target = _target
}

```

Watcher 是一个 class，它定义了一些方法，其中和依赖收集相关的主要有 get、addDep 等。

**（3）过程**

在实例化 Vue 时，依赖收集的相关过程如下∶ 初 始 化 状 态 initState ， 这 中 间 便 会 通 过 defineReactive 将数据变成响应式对象，其中的 getter 部分便是用来依赖收集的。 初始化最终会走 mount 过程，其中会实例化 Watcher ，进入 Watcher 中，便会执行 this.get() 方法，

```javascript
updateComponent = () => {
  vm._update(vm._render())
}
new Watcher(vm, updateComponent)

```

get 方法中的 pushTarget 实际上就是把 Dep.target 赋值为当前的 watcher。

```
this.getter.call（vm，vm），这里的 getter 会执行 vm._render() 方法，在这个过程中便会触发数据对象的 getter。那么每个对象值的 getter 都持有一个 dep，在触发 getter 的时候会调用 dep.depend() 方法，也就会执行 Dep.target.addDep(this)。刚才 Dep.target 已经被赋值为 watcher，于是便会执行 addDep 方法，然后走到 dep.addSub() 方法，便将当前的 watcher 订阅到这个数据持有的 dep 的 subs 中，这个目的是为后续数据变化时候能通知到哪些 subs 做准备。所以在 vm._render() 过程中，会触发所有数据的 getter，这样便已经完成了一个依赖收集的过程。
```

## 实现响应式原理代码，Vue2和Vue3响应式原理有什么区别？

响应式原理是 Vue 框架中的核心特性之一，它可以使数据和视图保持同步。在 Vue 2 和 Vue 3 中，响应式原理的实现方式略有不同。

在 Vue 2 中，响应式原理是通过 Object.defineProperty 来实现的。具体来说，当我们创建一个 Vue 实例时，Vue 会递归遍历对象的所有属性，并使用 Object.defineProperty 方法将每个属性转换为 getter 和 setter。这样，当我们访问或修改属性值时，就可以触发相应的 getter 和 setter 函数，从而更新视图。

在 Vue 3 中，响应式原理的实现方式发生了较大的变化。Vue 3 使用了 ES6 的 Proxy 对象来实现响应式。具体来说，当我们创建一个 Vue 实例时，Vue 会将数据对象包装成一个 Proxy 对象，并拦截其中的 get 和 set 操作。这样，当我们访问或修改属性值时，就可以触发相应的 get 和 set 操作，并更新视图。

## vue如何监听对象或者数组某个属性的变化

当在项目中直接设置数组的某一项的值，或者直接设置对象的某个属性值，这个时候，你会发现页面并没有更新。这是因为Object.defineProperty()限制，监听不到变化。

解决方式：

- this.$set(你要改变的数组/对象，你要改变的位置/key，你要改成什么value)

```javascript
this.$set(this.arr, 0, "OBKoro1"); // 改变数组this.$set(this.obj, "c", "OBKoro1"); // 改变对象

```

- 调用以下几个数组的方法

```javascript
splice()、 push()、pop()、shift()、unshift()、sort()、reverse()

```

vue源码里缓存了array的原型链，然后重写了这几个方法，触发这几个方法的时候会observer数据，意思是使用这些方法不用再进行额外的操作，视图自动进行更新。 推荐使用splice方法会比较好自定义,因为splice可以在数组的任何位置进行删除/添加操作

vm.`$set` 的实现原理是：

- 如果目标是数组，直接使用数组的 splice 方法触发相应式；
- 如果目标是对象，会先判读属性是否存在、对象是否是响应式，最终如果要对属性进行响应式处理，则是通过调用 defineReactive 方法进行响应式处理（ defineReactive 方法就是 Vue 在初始化对象时，给对象属性采用 Object.defineProperty 动态添加 getter 和 setter 的功能所调用的方法）

## Vue模版编译原理

vue中的模板template无法被浏览器解析并渲染，因为这不属于浏览器的标准，不是正确的HTML语法，所有需要将template转化成一个JavaScript函数，这样浏览器就可以执行这一个函数并渲染出对应的HTML元素，就可以让视图跑起来了，这一个转化的过程，就成为模板编译。模板编译又分三个阶段，解析parse，优化optimize，生成generate，最终生成可执行函数render。

- **解析阶段**：使用大量的正则表达式对template字符串进行解析，将标签、指令、属性等转化为抽象语法树AST。
- **优化阶段**：遍历AST，找到其中的一些静态节点并进行标记，方便在页面重渲染的时候进行diff比较时，直接跳过这一些静态节点，优化runtime的性能。
- **生成阶段**：将最终的AST转化为render函数字符串。

## 对SSR的理解

SSR也就是服务端渲染，也就是将Vue在客户端把标签渲染成HTML的工作放在服务端完成，然后再把html直接返回给客户端

SSR的优势：

- 更好的SEO
- 首屏加载速度更快

SSR的缺点：

- 开发条件会受到限制，服务器端渲染只支持beforeCreate和created两个钩子；
- 当需要一些外部扩展库时需要特殊处理，服务端渲染应用程序也需要处于Node.js的运行环境；
- 更多的服务端负载。

## Vue的性能优化有哪些

**（1）编码阶段**

- 尽量减少data中的数据，data中的数据都会增加getter和setter，会收集对应的watcher
- v-if和v-for不能连用
- 如果需要使用v-for给每项元素绑定事件时使用事件代理
- SPA 页面采用keep-alive缓存组件
- 在更多的情况下，使用v-if替代v-show
- key保证唯一
- 使用路由懒加载、异步组件
- 防抖、节流
- 第三方模块按需导入
- 长列表滚动到可视区域动态加载
- 图片懒加载

**（2）SEO优化**

- 预渲染
- 服务端渲染SSR

**（3）打包优化**

- 压缩代码
- Tree Shaking/Scope Hoisting
- 使用cdn加载第三方模块
- 多线程打包happypack
- splitChunks抽离公共文件
- sourceMap优化

**（4）用户体验**

- 骨架屏
- PWA
- 还可以使用缓存(客户端缓存、服务端缓存)优化、服务端开启gzip压缩等。

## template和jsx的有什么分别？

对于 runtime 来说，只需要保证组件存在 render 函数即可，而有了预编译之后，只需要保证构建过程中生成 render 函数就可以。在 webpack 中，使用`vue-loader`编译.vue文件，内部依赖的`vue-template-compiler`模块，在 webpack 构建过程中，将template预编译成 render 函数。与 react 类似，在添加了jsx的语法糖解析器`babel-plugin-transform-vue-jsx`之后，就可以直接手写render函数。

所以，template和jsx的都是render的一种表现形式，不同的是：JSX相对于template而言，具有更高的灵活性，在复杂的组件中，更具有优势，而 template 虽然显得有些呆滞。但是 template 在代码结构上更符合视图与逻辑分离的习惯，更简单、更直观、更好维护。

# 📁 Vue实战

## 总结整理一个新的项目需要完成哪些操作？

创建一个新的 Vue3 项目需要完成以下几个主要步骤：

1. 安装 Vue CLI 通过 npm 安装 Vue CLI，该工具提供了快速生成 Vue 项目的脚手架，方便开发者快速搭建项目。
2. 创建项目 在终端输入 `vue create [project-name]` 命令创建新项目，其中 `project-name` 为项目名称。
3. 选择特性 Vue CLI 会提示开发者选择需要的特性，包括路由、状态管理等，选择完毕后会根据选择的特性生成项目目录结构和相应的配置文件。
4. 安装依赖 项目创建完成后，需要进入项目根目录，运行 `npm install` 命令安装项目所依赖的第三方包。
5. 开发 在安装依赖完成后，就可以开始开发了，可以在 `src` 目录下编写 Vue 组件、样式和逻辑代码。
6. 编译和打包 在开发完成后，可以运行 `npm run build` 命令编译和打包项目代码，生成生产环境可用的代码。
7. 部署 将生成的代码部署到服务器上，通过配置服务器环境等步骤，使用户可以访问到部署好的 Vue 应用程序。

此外，还需要根据项目实际需求进行相关配置和优化，例如配置路由、状态管理、HTTP 请求等。

## vue初始化页面闪动问题

使用vue开发时，在vue初始化之前，由于div是不归vue管的，所以我们写的代码在还没有解析的情况下会容易出现花屏现象，看到类似于{{message}}的字样，虽然一般情况下这个时间很短暂，但是还是有必要让解决这个问题的。

首先：在css里加上以下代码：

```javascript
[v-cloak] {    display: none;}
```

如果没有彻底解决问题，则在根元素加上`style="display: none;" :style="{display: 'block'}"`

## assets和static的区别

**相同点：** `assets` 和 `static` 两个都是存放静态资源文件。项目中所需要的资源文件图片，字体图标，样式文件等都可以放在这两个文件下，这是相同点

**不相同点：**`assets` 中存放的静态资源文件在项目打包时，也就是运行 `npm run build` 时会将 `assets` 中放置的静态资源文件进行打包上传，所谓打包简单点可以理解为压缩体积，代码格式化。而压缩后的静态资源文件最终也都会放置在 `static` 文件中跟着 `index.html` 一同上传至服务器。`static` 中放置的静态资源文件就不会要走打包压缩格式化等流程，而是直接进入打包好的目录，直接上传至服务器。因为避免了压缩直接进行上传，在打包时会提高一定的效率，但是 `static` 中的资源文件由于没有进行压缩等操作，所以文件的体积也就相对于 `assets` 中打包后的文件提交较大点。在服务器中就会占据更大的空间。

**建议：** 将项目中 `template`需要的样式文件js文件等都可以放置在 `assets` 中，走打包这一流程。减少体积。而项目中引入的第三方的资源文件如`iconfoont.css` 等文件可以放置在 `static` 中，因为这些引入的第三方文件已经经过处理，不再需要处理，直接上传。

## 如何做动态图片

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

## new URL如何使用

`new URL()` 的语法如下：

```
const url = new URL(urlString[, baseString]);
```

其中，`urlString` 参数是要解析的 URL 字符串，`baseString` 是可选参数，是用来解析相对 URL 的基本 URL 字符串。如果省略 `baseString` 参数，则默认使用当前网页的 URL。

```js
const url = new URL('https://www.example.com/path?param=value#fragment');

console.log(url.href); // "*[https://www.example.com/path?param=value#fragment](https://www.example.com/path?param=value#fragment)"
console.log(url.protocol); // "https:"
console.log(url.host); // "[<a href="http://www.example.com](http:/www.example.com)">www.example.com](http://www.example.com)</a>"
console.log(url.pathname); // "/path"
console.log(url.search); // "?param=value"
console.log(url.hash); // "#fragment"
```

在这个示例中，`new URL()` 用于解析一个 URL 字符串，并创建一个包含各种 URL 组件的 URL 对象。你可以使用 URL 对象的属性来访问每个组件，例如 `protocol`、`host`、`pathname`、`search` 和 `hash`。

## 动态添加图片

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
> "../../assets/img/" +image是图像文件的相对路径。该image变量包含图像文件的名称。
> import.meta.url是当前模块的URL。它用作图像文件相对路径的基本 URL。
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

## 获取位置信息

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
> 定义了一个名为 `getPosition()` 的方法，用于获取设备的地理位置信息。
> `getPosition()` 方法返回了一个 Promise 对象，该对象在成功时会将获取的地理位置信息传递给 resolve() 方法，在失败时会将错误信息传递给 reject() 方法。
> 这种方式使用了 JavaScript 的 Promise API，可以使异步代码更易于编写和理解，并提供了更好的错误处理机制。
> 需要注意的是，在使用 `getCurrentPosition()` 方法获取地理位置信息时，浏览器会向用户显示一个请求位置的提示框，如果用户选择拒绝，将会触发错误回调函数并返回一个 `PermissionDeniedError` 错误。因此，如果您的应用程序需要获取位置信息，请确保向用户解释为什么需要该权限，并确保在代码中处理可能的错误情况。

## 发送网络请求文件模块

**网络请求工具封装**

`src/services/request/index.js`

**网址管理文件**

`src/services/request/config.js`

**分模块文件**

`src/services/modules/city.js`

**导出管理文件**

`src/services/index.js`用来在这里统一给

它做一个导出

## 发送网络请求操作流程

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

4、统一导出管理文件

`src/services/index.js`

```js
export * from './modules/city'
```

这段代码 `export * from './modules/city'` 的意思是将一个模块 `city` 中的所有导出`（export）`重新导出`（re-export）`到当前模块中。

更具体地说，这个语句会将 `./modules/city` 模块中的所有导出都作为当前模块的导出。这包括该模块中所有被导出的变量、函数、类等。这样，其他模块可以通过导入当前模块来访问这些导出。

需要注意的是，这里使用的是 * 通配符来表示要重新导出的所有内容。这相当于把 city 模块的所有导出都导出到当前模块中，而不是仅导出其中的一部分。另外，export * 必须放在当前模块的顶层，不能嵌套在函数或代码块中。

## 如何去修改UI组件库的样式？有哪些方式，各有什么优劣？(重要)

**方式一：使用插槽，插入自己的元素，然后在自己的作用域中直接修改这个元素**

```css
.tab-bar {
  img {
  height: 30px;
  }
}
```

**方式二：全局定义一个变量，覆盖它默认变量的值**

- 缺点：全局修改, 任何地方只要用到该变量都会被修改掉

```css
:root {
--primary-color: #ff9854;
--line-color: #f1f1f1;

*/* 全局修改：任何地方只要用到-van-tabbar-item-icon-size都会被修改掉 */*
*/* -- van-tabbar-item-icon-size: 30px; !important */*
*/* 搜索框搜索icon */*
--van-search-left-icon-color: var(--primary-color) !important
}
```

**方式三：局部定义一个变量，覆盖它默认变量的值**

- 优点：局部修改,只对自己以及自己的子元素会生效

```css
.tab-bar {
--van-tabbar-item-icon-size: 30px; !important
}
```

**方式四：直接找到对应的子组件选择器,进行修改**

- 通过:deep(.class) 找到子组件的类,让子组件的类也可以生效, 穿透到子组件
- :deep(子组件的元素的选择器)进行修改

```cs
.tab-bar {
:deep (.van-tabbar-item__icon) {
font-size:30px;
}
```

## 一个页面的数据请求和管理有哪些方式？各有什么特点

**方式一：保存在页面中**

- 如果网络请求太多, 那么页面组件中就包含大量的对于网络请求和数据的处理逻辑
- 如果页面封装了很多的子组件, 子组件需要这些数据, 我们必须一步步将数据传递过去(props)

**方式二：保存在store中**

- city.vue一个页面---对应stores/modules/city.js一个cityStore--- 对应services/modules/city.js 对于city的所有网络请求 , 这种分层架构结构清晰, 分工明确,效率高。

### 在一个页面中，数据请求和管理的方式有以下几种：

1、直接在页面组件中发送请求

将数据请求的逻辑写在页面组件的生命周期钩子函数中，例如 `created` 或 `mounted`，直接调用数据接口并处理响应数据。这种方式简单易懂，但不易于重用和维护，容易导致代码冗余和混乱。

2、使用 Vuex 管理数据状态

将数据状态统一管理在 Vuex 的 store 中，并通过 actions 和 mutations 进行数据请求和状态更新。这种方式可以有效地实现数据共享和组件解耦，提高代码复用和可维护性，但增加了一定的学习和开发成本。

3、使用 Axios 或其他 HTTP 库进行数据请求

使用 Axios 或其他 HTTP 库发送异步请求，处理响应数据，并将数据传递给页面组件或 Vuex store。这种方式可以方便地处理各种 HTTP 请求和响应类型，提高代码的可读性和可维护性，但需要额外的配置和学习成本。

4、使用 GraphQL 进行数据查询

使用 GraphQL 查询语言编写数据查询请求，通过 GraphQL API 请求数据，处理响应数据，并将数据传递给页面组件或 Vuex store。这种方式可以提高数据查询的效率和精度，减少不必要的数据传输，但需要额外的配置和学习成本。

不同的数据请求和管理方式各有优缺点，选择合适的方式取决于项目需求、团队技术水平和开发成本等因素。一般来说，对于简单的数据请求和处理，直接在页面组件中发送请求是最简单和直接的方式；对于复杂的应用程序，使用 Vuex 和 Axios 进行数据管理和请求可以提高代码的可维护性和可扩展性。

## 隐藏底部TabBar有什么方式？

### 方法一:通过v-if和useRoute(拿到当前活跃的路由对象)

第一步: 路由配置,自定义属性hideTabBar

```css
{
    path: "/city",
    component: () => important("@/views/city/city.vue"),
    meta: {
        hideTabBar: true
    }
} 
```

第二步: 通过useRoute拿到当前活跃的路由对象route,     通过当前路由对象的hideTabBar来控制TabBar的显示和隐藏

```js
<template>
  <div>
    <router-view></router-view>
    <!-- 当city页面,tabbar隐藏-->
    <tab-bar v-if="!route.meta.hideTabBer"></tab-bar>
  </div>
</template>
<script setup>
  import { useRoute } from "vue-router";
  import tabBar from "./components/tab-bar/tab-bar.vue"
  // 当city页面,tabbar隐藏
  const route = useRoute();
</script>
```

### 方法二：让city达到整个视口高度，把tab-bar给盖起来

```css
.top {
  position: relative;
  z-index: 9;
  height: 100vh;
  background-color: #fff;
  
  //  当内容超出元素高度时，显示垂直滚动条，以便用户可以滚动查看所有内容。
  over-flow-y: auto;
}
```

## 日期格式化工具使用

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

### 创建dayjs实例

```js
// 创建当前时间的dayjs实例
const now = dayjs();
console.log(now); // 输出当前时间的dayjs实例
javascriptCopy code// 通过传递日期字符串来创建dayjs实例
const dateStr = '2023-03-16';
const date = dayjs(dateStr);
console.log(date); // 输出指定日期的dayjs实例
```

### 格式化日期

```js
// 将dayjs实例格式化为字符串
const now = dayjs();
const formattedDate = now.format('YYYY-MM-DD HH:mm:ss');
console.log(formattedDate); // 输出格式化后的日期字符串，例如：2023-03-16 13:24:10
```

### 操作日期

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

### 获取日期信息

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

### 计算日期间隔

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

### 额外知识：

> vue3中控制台显示的RefImpl 是啥意思？
> 在Vue 3中，`RefImpl`是一个内部类，用于实现`ref`的具体实现细节。`ref`是一个响应式API，用于创建一个可变的、能够被响应式地监听的引用类型值。当我们使用`ref`创建一个引用类型值时，Vue会使用`RefImpl`来对该值进行封装，以便在该值被修改时能够触发相应的更新。
> 虽然`RefImpl`在Vue 3的内部实现中被使用，但在我们平时的开发过程中，我们通常不需要直接使用它。我们只需要使用`ref`来创建一个响应式的引用类型值即可。如果我们想要获取到`ref`的具体实现细节，可以通过在控制台中输出一个`ref`对象来查看它的原型链，从而找到它所使用的内部类`RefImpl`。

## 响应式动态日期创建

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
> 这段代码的作用是创建一个响应式的`endDate`变量，用于存储当前日期的下一天的日期，并将其格式化为指定的日期字符串格式。
> 具体来说，代码分为两行：
> 第一行代码通过`nowDate.setDate(nowDate.getDate() + 1)`获取当前日期对象`nowDate`的下一天日期，并将该日期的==毫秒数==存储在一个名为`afterDate`的常量中。
> 第二行代码使用`ref()`函数将`afterDate`格式化为指定的日期字符串格式，并将结果存储在一个名为`endDate`的响应式变量中。
> 在Vue 3中，使用`ref()`函数可以将一个普通的JavaScript对象或值转换为响应式的对象或值，使得当对象或值发生变化时，可以自动通知相关的组件进行重新渲染。
> 在这里，我们使用`ref()`函数将一个格式化后的日期字符串转换为响应式变量，以便在该日期发生变化时，相关的组件可以根据新的日期进行重新渲染。

## 动态时间格式

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
> 默认格式为“MM月DD日”，即函数返回格式为“月月日”的字符串。例如，如果输入日期为“2023-03-22”，则此函数的默认格式输出为“03 月 22 日”。

`src/components/searchBar/SearchBar.vue`

```js
import {useStore} from "vuex"
import { formatMothDay} from '@/utils/formatDate'
import {toRefs, computed} from 'vue' 

const mainStore = useStore()
const { startDate, endDate } = toRefs(mainStore.state.main)

const startDateStr = computed(() => formatMothDay(startDate.value， "MM.DD"))
const endDateStr = computed(() => formatMothDay(endDate.value, "MM.DD"))
```

## route 和 router 有什么区别？

`useRoute`和`useRouter`都是Vue Router提供的hook函数。

`useRoute`返回当前路由信息的对象，包括路由的路径、参数、查询参数等。

`useRouter`返回路由实例，可以用它来导航到其他路由或获取路由信息。

在你的代码中，`route`是通过`useRoute`获取到的当前路由信息对象，而`router`是通过`useRouter`获取到的Vue Router实例。

当你想要在代码中访问当前路由信息时，可以使用`useRoute`来获取；当你想要在代码中进行路由导航或获取路由信息时，可以使用`useRouter`来获取Vue Router实例。

## 文字省略号分行样式

```css
margin: 5px 0;
text-overflow: ellipsis;
overflow: hidden;
display: -webkit-box;
-webkit-line-clamp:2;
-webkit-box-orient: vertical;
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

## 百度地图的集成和使用过程

> 地图模块遇到会比较少，但是有可能~
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

## 动态绑定style样式

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

## undefined

ES6语法中，从`undefined`中取值时会报错，最新的vue支持添加`?`

对于存在很多数据嵌套的结构，获取数据时，会经常遇见这种问题

## 监听页面滚动到底部

### 12.5、监听页面滚动到底部

![metric-all](E:\coder\09_OneNote\image\metric-all.png)

> **页面为什么会滚动？区分清楚两种情况：**
> 1、window窗口
> 2、元素：overflow-y：auto

**思路：**

1、监听window窗口的滚动，当页面到达了底部时

==scrollTop + clientHeight >= scrollHeight==

`src/views/home/home.vue`

```js
// 监听页面到达了底部
window.addEventListener("scroll", () => {
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
> 在函数内部，我们首先定义了一个名为`scrollListenerHandler`的函数，用来处理滚动事件。在该函数中，我们获取了页面的滚动高度`scrollTop`、文档的总高度`scrollHeight`以及浏览器窗口的可视高度`clientHeight`。
> 如果`scrollTop + clientHeight >= scrollHeight`，则表示页面已经滚动到了底部。此时，我们执行回调函数`callback`，即调用传递进来的操作。同时，我们也打印出“滚动到了底部”的信息。
> 在`onMounted`和`onUnmounted`生命周期钩子中，我们分别调用`window.addEventListener`和`window.removeEventListener`函数来注册和取消滚动事件的监听器。这样可以确保在组件挂载和卸载时都能正确监听和取消滚动事件，避免内存泄漏和性能问题。
> 总之，这段代码是用来封装一个通用的页面滚动事件监听器，并且可以根据需要执行自定义操作的。
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

## 优化useScroll（一）

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
> `useScroll`函数使用`ref`创建了一个名为`isReachBottom`的响应式变量，并将其初始化为`false`。然后使用`throttle`函数创建了一个名为`scrollListenerHandler`的函数，这个函数将在滚动事件被触发时被调用。当滚动到页面底部时，将`isReachBottom`变量的值设置为`true`。
> `onMounted`和`onUnmounted`钩子分别在组件`挂载`和`卸载`时添加和移除了一个滚动监听器。监听器函数是`scrollListenerHandler`。
> `return { isReachBottom }`将一个对象返回，包含了`isReachBottom`属性，这个属性在组件中可以被使用。
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
> `const { isReachBottom } = useScroll()`是从`useScroll`函数返回的对象中提取`isReachBottom`属性的一种语法糖。它等价于`const isReachBottom = useScroll().isReachBottom`。
> `watch`函数用于监听`isReachBottom`变量的变化，并在`isReachBottom`变为`true`时，调用`homeStore.dispatch('home/fetchHouselist', currentPage.value)`方法。
> `homeStore`是一个Vuex Store对象，`fetchHouselist`是一个异步action。该异步action用于获取当前页面的房屋列表，并将`isReachBottom`变量重置为`false`，以便下次检测。
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

## 优化useScroll（二）

目前使用封装的`useScroll`函数不能正确监听到滚动的原因，是因为我们封装的`useScroll`是监听的`window`，而这个页面是块级元素`<div>`内部的滚动，因此需要优化之前封装的`useScroll`。

想监听元素的滚动，是需要传递参数的~+

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
> 在给定的代码中，将`tabRef`定义为`ref`是为了让Vue跟踪这个DOM元素的状态。通过将元素包装在`ref`中，Vue可以检测到何时该元素被创建、更新或销毁，从而允许我们执行相应的操作。
> 例如，在这个示例中，我们可以使用`$refs`属性访问`tabRef`，并且当在代码中更新`tabRef`时，Vue会自动重新渲染相关的DOM。
> 为什么不直接使用`useScroll(document.querySelector("detail-page"))`
> 因为setup中，这个div还没有被挂载，是传不进去的~

在进行封装监听页面滚动工具中，用了 Vue3的 onMounted 和 onUnmounted 生命周期以及 ref API 来实现组合式函数的编写；使用了 Lodash 库中的 throttle 函数来控制函数执行频率；

## 关于`toRefs`、`computed`

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
> 2. 第二种写法使用了 `computed` 函数，将解构出来的属性封装成了一个计算属性。这样，当依赖该计算属性的其他属性发生变化时，计算属性也会重新计算。如果你希望在获取属性值时进行一些计算操作，可以使用这种写法。

> 这两种写法在获取属性值方面都是等价的，只是在响应式更新和计算方面有所不同。❗❗❗一定不要忘记`.value`

## 节流、防抖

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

## 抽取Hook的好处

抽取hook的好处，在任何地方都可以调用，思想慢慢体会，Vue2没有这种方法，必须使用混入mixins，放入data中，虽然更难了，但是好处是大大的

不要纠结于你为什么想不到，做得少，但是你学会之后，在react中也是这种思想

那为什么不直接使用react？如果想更加灵活的话，在react中会更加更加的灵活，所以，这个问题也是社区一直讨论的。可能也会有一大部分人转手使用react。

vue有优势也优劣势

不要只知道api的使用，做一个opations API工程师，关键的点要掌握函数式编程的灵魂，这样才能学到精髓

## 页面跳转如何进行数据的传递

### 1、路由传参

在路由中使用`params`或者`query`来传递数据。`params`是通过`URL`传递参数，`query`是通过查询字符串传递参数。在源组件中通过`router.push`方法跳转到目标组件`route.params`或者`$route.query`获取传递的数据。

例如，在源组件中跳转到目标组件：

**源组件**

```
this.$router.push ({
    path: '/target',
    query: {
        name: 'vue',
        version: '3.2.1'
    }
} 
```

**目标组件获取参数**

```
this.$route.query.name // vue
this.$route.query.version // 3.2.1 
```

### 2、Vuex

Vuex 是一个专门为`Vue.js`设计的状态管理模式。在`Vuex`中，可以`定义全局的数据状态`，并且在`各个组件中共享这些状态`。当一个组件跳转到另一个组件时，可以将数据存储到`Vuex`的状态中，在目标组件中从状态中获取数据。

**在源组件中存储数据**

```
this.$store.commit('setData, { name: 'vue', version: '3.2.1' })
```

**目标组件中获取数据**

```
computed: {
    data() {
        return this.$route.state.data
    }
}
```

## 如何监听页面的滚动？

上拉加载更多很可能多个组件都需要用到  所以对其进行 `hooks` 的 `useScroll` 封装  用于方便使用

- 获取客户端  `scrollTop`  `scrollHeight`的高度  定义 `isReachBottom` 控制网络请求的再次的触发
- 当客户端的高度  `+`  上滑的高度  `>=`  内容滑块总高度时  就说明已经滚动到底部了  就可再次请求数据
- 当然这里为了提升性能   可用节流函数
- 事件需要在声明周期`onMounted`中进行(因为`setup`内部东西加载是处于(`beforeCreate`和`create`声明周期之间)  进行完成之后记得取消事件

```js
import { onMounted, onUnmounted, ref } from "vue";
import { throttle } from "lodash";

export default function useScroll() {
  const isReachBottom = ref(false)

  const clientHeight = ref(0)
  const scrollTop = ref(0)
  const scrollHeight = ref(0)
 // 获取各种高度(客户端  上滑高度   滑块内容总高度)
  const scrollListenerHandler = throttle(() => {
    clientHeight.value = document.documentElement.clientHeight
    scrollTop.value = document.documentElement.scrollTop
    scrollHeight.value = document.documentElement.scrollHeight

    if (clientHeight.value + scrollTop.value >= scrollHeight.value) {
      // 滚动到底部触发
      // console.log('gundao dibu l')
      isReachBottom.value = true
    }
  }, 150)
  // 监听事件
  onMounted(() => {
    window.addEventListener('scroll', scrollListenerHandler)
  })
  //移除事件
  onUnmounted(() => {
    window.removeEventListener('scroll', scrollListenerHandler)
  })

  return { isReachBottom, clientHeight, scrollTop, scrollHeight }
}
```

## 如何监控整个应用进行网络请求，并且显示动画界面？

在对`axios`的封装中  利用拦截器(`interceptors`)的请求和响应阶段可以进行很好的控制

- 对实例添加请求拦截和响应拦截
- 当请求成功  就利用变量(`isLoading=true`)来实现动画的加载
- 当请求响应成功  就把(`isLoading=false`)来结束动画的加载

```js
const mainStore = useMainStore()

class YORequest {
  constructor(baseURL, timeout=10000) {
    this.instance = axios.create({
      baseURL,
      timeout
    })

    this.instance.interceptors.request.use(config => {
      mainStore.isLoading = true
      return config
    }, err => {
      return err
    })
    this.instance.interceptors.response.use(res => {
      mainStore.isLoading = false
      return res
    }, err => {
      mainStore.isLoading = false
      return err
    })
  }
}
```

## 理解页面滚动和元素滚动之间的区别，如何实现？

重构`useScroll`对页面滚动和元素滚动做出不同的反应

- 如果是页面滚动  获取的是`document(文档)`客户端 高度(`clientHeight`)    文档上滑高度(`scrollTop`)    文档滑块内容总高度(`scrollHeight`)
- 如果是元素滚动  获取的不能是文档类的高度   而是元素的客户端的高度(`clientHeight`)   元素上滑高度(`scrollTop`)   元素滑块内容总高度(`scrollHeight`)

```js
// elRef决定的 useScroll 用于页面滚动还是元素的滚动
export default function useScroll(elRef) {
  let el = window

  const isReachBottom = ref(false)

  const clientHeight = ref(0)
  const scrollTop = ref(0)
  const scrollHeight = ref(0)

// 节流函数
  const scrollListenerHandler = throttle(() => {
    if (el === window) {
        
      clientHeight.value = document.documentElement.clientHeight
      scrollTop.value = document.documentElement.scrollTop
      scrollHeight.value = document.documentElement.scrollHeight
    } else {
      clientHeight.value = el.clientHeight
      scrollTop.value = el.scrollTop
      scrollHeight.value = el.scrollHeight
    }
    if (clientHeight.value + scrollTop.value >= scrollHeight.value) {
      console.log("滚动到底部了")
      isReachBottom.value = true
    }
  }, 150)
  
  onMounted(() => {
     // 判断是否传入的有元素  有就进入else  否则el = window
    if (elRef) el = elRef.value
    el.addEventListener("scroll", scrollListenerHandler)
  })
  
  onUnmounted(() => {
    el.removeEventListener("scroll", scrollListenerHandler)
  })

  return { isReachBottom, clientHeight, scrollTop, scrollHeight }
}
```

## 页面滚动位置显示正确的索引

```js
## watch(scrollTop, (newValue) => { // 使用Vue的watch函数监听scrollTop的变化，newValue为新的值
  const els = Object.values(sectionEl.value) // 获取所有需要匹配的元素
  const values = els.map(el => el.offsetTop) // 获取所有需要匹配的元素的offsetTop值
  let index = values.length - 1 // 初始化索引值为最后一个元素的索引
  for (let i = 0; i < values.length; i++) { // 遍历所有元素的offsetTop值
    if(values[i] < newValue + 44) { // 如果当前元素的offsetTop值大于newValue和tabber的和
      index= i-1 // 则将索引值设置为当前元素的前一个元素的索引
      break // 找到了符合条件的元素，退出循环
    }
  }
console.log(index) // 打印最终匹配到的索引值d
})
```

> 函数中的主要逻辑如下：
>
> 1. 获取所有需要匹配的元素的offsetTop值。这里使用了Vue 3的ref和reactive功能，通过sectionEl.value获取所有需要匹配的元素，然后通过Object.values方法将其转换为一个数组，最后通过map方法遍历获取每个元素的offsetTop值。
> 2. 遍历所有的offsetTop值，与当前的scrollTop值进行比较，找到第一个比scrollTop大的offsetTop值，对应的索引即为TabControl的索引。这里使用了一个for循环来遍历比较，如果找到第一个比scrollTop大的offsetTop值，则将其对应的索引减去1，这样就可以得到TabControl的索引了。
> 3. 注意处理一些边界情况。例如，如果scrollTop小于第一个offsetTop值，则默认为第一个TabControl的索引；如果scrollTop大于最后一个offsetTop值，则默认为最后一个TabControl的索引。
> 4. 最后，将找到的TabControl的索引打印出来，可以根据需要进行其他处理。

> 这个算法与网易云音乐中歌词的算法类似，都是根据值匹配到区间的问题。通过遍历比较的方式，找到第一个大于目标值的元素，即可确定匹配到的区间。
> 总的来说，这段代码实现了监听页面滚动事件，并根据当前的滚动位置匹配到对应的TabControl的索引。它使用了Vue 3的ref和reactive功能来获取需要匹配的元素的offsetTop值，并使用一个for循环来遍历比较。需要注意一些边界情况的处理，例如第一个和最后一个元素。

## 索引值匹配tabbar

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
> 或者大部分功能其实**别人也都是做过的**，都可以找到，
> 并且组件库的东西都是**可以自己实现的**，也可以去看源码是如何实现的！
> 自己实现，更加清晰自己的代码，组件库的有些BUG不好找原因~

## 移动端适配

### 一、禁止缩放

对于移动端项目，有可能用户会进行页面的缩放，但是不希望用户进行缩放怎么做？

**需要设置视口**

之前移动端适配有讲过

`index.html`

```
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0,user-scalable=no">
```

文档：

https://developer.mozilla.org/zh-CN/docs/Web/HTML/Viewport_meta_tag

### 二、Viewport 布局

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

## 在实际项目中如何使用Vue全家桶（Vue-router、Vuex等）？请分享一下你的经验。

Vue 全家桶包括 Vue.js、Vue Router 和 Vuex，它们是一套完整的解决方案，用于构建单页应用程序（SPA）和管理应用程序的状态。下面是一些在实际项目中使用 Vue 全家桶的示例：

1. 使用 Vue.js 构建应用程序界面

Vue.js 是一个用于构建用户界面的渐进式框架，它可以帮助我们将页面分解成可重用的组件，并使组件之间的数据传递更加简单。在实际项目中，我们可以使用 Vue.js 来构建应用程序的界面。

2. 使用 Vue Router 管理应用程序的路由

Vue Router 是一个官方的 Vue.js 路由管理器，它可以帮助我们管理应用程序的路由，实现单页应用程序（SPA）的页面切换。在实际项目中，我们可以使用 Vue Router 来定义应用程序的路由，并使用路由参数、路由导航守卫等功能来实现更加复杂的页面导航逻辑。

我会对路由进行懒加载，通过ES6的import，当然也可以用vue的动态组件~

3. 使用 Vuex 管理应用程序的状态

Vuex 是一个官方的 Vue.js 状态管理库，它可以帮助我们管理应用程序的状态，实现组件之间的数据共享。在实际项目中，我们可以使用 Vuex 来定义应用程序的状态，并使用状态变化、状态订阅等功能来实现更加复杂的数据管理逻辑。

Vuex的核心包括state、getter、mutation和action，通过mutation去更改state的值，要注意异步操作只能放在action里。

除此之外，还有一些其他的 Vue 全家桶相关的工具和库，例如 Vue CLI、Vue Test Utils 等，它们可以帮助我们更加高效地开发和测试 Vue 应用程序。

总的来说，使用 Vue 全家桶可以帮助我们构建更加可维护和高效的应用程序，但也需要考虑到全家桶的体积和学习成本等问题。因此，在选择使用 Vue 全家桶时，需要根据具体的项目需求和团队技能水平进行评估和选择。