==如何一句话解释 this：它就是一个变量，指向了某个对象保存在堆中的数据。==

# 从原理角度理解 this

我们知道在 JS 中，对象的变量名保存在栈(Stack)中，对象的数据保存在堆(Heap)中，像这样：

![Pasted image 20230515161604.png](E:\coder\09_OneNote\image\da5da87df56349459e384ceb75517888tplv-k3u1fbpfcp-zoom-in-crop-mark1512000.webp)

一句话解释 this，它就是一个变量，引用了某个对象保存在堆中的数据，就这么简单。 比如在上图中，`personA` 的 `this` 引用了 `{name: "LB", age:20}`

# this 有什么用？

既然 `this` 指向的堆中某个对象的数据，那我们可以通过 `this` 来灵活的操作对象在堆中的数据呀。

比如下面的代码，可以把一个`sayHi`函数放在两个对象身上使用，代码可复用性这不就上来了么：

```javascript
const user = { name: "john" };
const admin = { name: "admin" };

function sayHi() {
  console.log(this.name); // this 可以指向 user，也可以指向 admin
}

user.f = sayHi;
admin.f = sayHi;

user.f();  // john
admin.f();  // admin
```

# 把 this 掌握在自己手里

只有掌握好 `this` 的指向规则，才能让我们使用 this 的时候可以指哪打哪。

## 如何操纵普通函数的 this ？

普通函数的 `this` 的指向可以通过下面几种规则来判断，优先级从高到低：

1. 看是不是 `new` 调用。函数是否在 `new` 中调用? 如果是的话 ，`this` 绑定的是新创建的对象。

   ```csharp
   csharp
   复制代码var bar = new foo()
   ```

2. 看是不是**显示绑定**。函数是否通过 `call、apply、bind` 调用? 如果是的话，`this` 绑定的是 指定的对象。

   ```ini
   ini
   复制代码 var bar = foo.call(obj2)
   ```

3. 看是不是**隐式绑定**。函数是否在某个上下文对象中调用? 如果是的话，`this` 绑定的是那个上下文对象。

   ```ini
   ini
   复制代码 var bar = obj1.foo()
   ```

4. 如果**都不是**的话，使用默认绑定。如果在严格模式下，就绑定到 undefined，否则绑定到 全局对象。

   ```ini
   ini
   复制代码 var bar = foo()
   ```

普通函数的 `this` 绑定是动态的，也就是在运行时才知道 `this` 绑定的是谁的 context，再具体一点来说，`this` 所在的函数被谁调用了，`this` 就绑定了谁的上下文。如果这个谁也没有上下文，就再往上看上一层调用者，直到找到有上下文的函数 (最顶层就是拥有全局上下文的全局函数)。

从调用栈的角度来说，一个普通函数出栈后，就有一个新的栈顶函数，然后被调用，这个函数的 `this` 绑定的是新的栈顶函数的上下文。

## 如何操纵箭头函数的 this ？

箭头函数可以理解为轻量级的普通函数，它压根就没有 `this`，所以普通函数的 `this` 规则不适用于它。它的 `this` 在创建函数的时候，从外层的 `this` 继承而来，而且一旦继承了 `this`，就不会再变了。

在创建箭头函数的时候，`this` 继承自外部，而且 `this` 确定之后不会变：

```javascript
function foo() {
  return (a) => {
    // this 继承自 foo()
    // this 继承之后不会变
    console.log(this.a);
  };
}
var obj1 = { a: 2 };
var obj2 = { a: 3 };
var bar = foo.call(obj1); // 调用 foo，foo 的 this 指向 obj1
bar.call(obj2); // 2
```

因为不用担心 `this` 的指向会被三方库修改，所以常用在创建回调函数：

```javascript
function foo() {
  setTimeout(() => {
    // 这里的 this 继承自 foo，不用担心 setTimeout 会修改它
    console.log(this.a);
  }, 100);
}
var obj = { a: 2 };
foo.call(obj); // 2
```

下面的代码和上面的一样，把回调函数的声明抽出来了，更好理解：

```javascript
function foo() {
  const cb = () => {
    // 这里的 this 继承自 foo
    console.log(this.a);
  };
  setTimeout(cb, 100);
}
var obj = { a: 2 };
foo.call(obj); // 2
```

# 代码实操

下面的例子，如果没有额外说明 use strict，都是没有 use strict 的。 推荐你配合着上面的 `this` 绑定规则一起看下面的代码。

默认绑定：

```javascript
function makeUser() {
  return {
    name: "John",
    ref: this
  };
}

// this 的指向只和 function 在哪里 call 有关系
let user = makeUser();

console.log( user.ref.name ); // Error: Cannot read property 'name' of undefinedoo
```

隐式绑定：

```javascript
"use strict";
function makeUser() {
  return {
    name: "John",
    ref() {
      return this;  // 拿的是 makeUser 的 this
    },
  };
}

let user = makeUser();

// user 是一个对象，user.ref() 相当于隐式绑定了 this
console.log(user.ref().name); // John
```

箭头函数的 `this` 继承自外层:

```javascript
obj = {
  count: 0,
  cool: function coolFn() {
    if (this.count < 1) {
      setTimeout(() => {   // 箭头函数的 this 就是 coolFn() 的 this
        console.log("awesome");
      }, 100);
    }
  },
};

obj.cool(); // awesome

// 下面代码是一样的
obj = {
  count: 0,
  cool: function coolFn() {
    if (this.count < 1) {
      let foo = () => {
	    // 箭头函数的 this 就是 coolFn() 的 this

        console.log("awesome");
      };
      setTimeout(foo, 100);
    }
  },
};

obj.cool(); // awesome
```



作者：Kz
链接：https://juejin.cn/post/7233307834456064057
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。