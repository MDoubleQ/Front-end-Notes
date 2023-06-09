![手写代码面试题.png](E:\coder\09_OneNote\image\6fd41339dfd14200bb006815eab31324tplv-k3u1fbpfcp-zoom-in-crop-mark1512000.webp)

## 零、其他

### 1、1️⃣ instanceof 方法

#### instanceof 运算符

在 JavaScript 中，instanceof 运算符用于检查一个对象是否属于某个构造函数的实例。它的语法如下：

```js
object instanceof constructor
```

其中，object 是要检查的对象，constructor 是要检查的构造函数。如果 object 是 constructor 的实例，则返回 true，否则返回 false。

#### 手动实现 instanceof 方法的思路如下：

- 获取 object 的原型链（即 object 的 **proto** 属性），并保存在一个变量中。
- 获取 constructor 的原型（即 constructor.prototype 属性），并保存在一个变量中。
- 判断 object 的原型链中是否存在 constructor 的原型。如果存在，则返回 true；否则，继续沿着 object 的原型链向上查找，直到找到 Object.prototype 为止。如果还没有找到，则返回 false。

下面是手动实现 instanceof 方法的代码实现：

```js
function myInstanceOf(object, constructor) {
  let proto = object.__proto__;
  let prototype = constructor.prototype;
  while (proto) {
    if (proto === prototype) {
      return true;
    }
    proto = proto.__proto__;
  }
  return false;
}

// 使用示例
class Person {}
const p = new Person();
console.log(myInstanceOf(p, Person)); // true
console.log(myInstanceOf(p, Object)); // true
console.log(myInstanceOf(p, Array)); // false
```

在这个实现中，我们首先定义了一个名为 myInstanceOf 的函数，它接受两个参数：object 和 constructor。在函数内部，我们首先获取 object 的原型链，并将其保存在变量 proto 中。然后，我们获取 constructor 的原型，并将其保存在变量 prototype 中。接下来，我们使用 while 循环遍历 object 的原型链，如果在原型链中找到了 constructor 的原型，则返回 true；否则，继续向上查找。如果最终没有找到 constructor 的原型，就返回 false。

在使用示例中，我们首先定义了一个 Person 类，并创建了一个 Person 的实例 p。然后，我们使用 myInstanceOf 方法检查 p 是否是 Person 类的实例。由于 p 是通过 new Person() 创建的，因此 myInstanceOf(p, Person) 返回 true。我们还使用 myInstanceOf 方法检查 p 是否是 Object 和 Array 类的实例，分别返回 true 和 false，这符合我们的预期。

#### 其他方式

除了上面手动实现 instanceof 的方式之外，还可以使用其他方式来实现 instanceof 的功能。下面介绍一些常见的方法：

#### 使用 Object.prototype.isPrototypeOf()

可以使用 Object.prototype.isPrototypeOf() 方法来判断一个对象是否是另一个对象的原型。具体实现方法如下：

```js
function myInstanceOf(object, constructor) {
  return constructor.prototype.isPrototypeOf(object);
}
```

#### 使用 Function.prototype.call()

可以使用 Function.prototype.call() 方法来改变 this 的指向，从而判断一个对象是否是另一个构造函数的实例。具体实现方法如下：

```js
function myInstanceOf(object, constructor) {
  return constructor.call(object) === object;
}
```

#### 使用 ES6 中的 Symbol.hasInstance

ES6 中为每个构造函数定义了一个 Symbol.hasInstance 属性，该属性是一个方法，用于检查一个对象是否是该构造函数的实例。具体实现方法如下：

```js
function myInstanceOf(object, constructor) {
  return constructor[Symbol.hasInstance](object);
}
```

以上三种方法的实现原理都是基于原型链的概念，都可以判断一个对象是否是另一个构造函数的实例。不同之处在于实现方式略有不同，有些使用了 ES6 的新特性，有些使用了原型方法或函数调用方式等。根据具体情况可以选择不同的实现方式。

#### 使用原型链来判断对象是否是构造函数的实例：

其思路与使用 Object.prototype.isPrototypeOf() 方法的方式类似，只是具体实现方法略有不同。这个方案也是常见的实现方式之一，比较简单易懂。

具体实现方法如下：

```js
function myInstanceOf(left, right) {
  let proto = Object.getPrototypeOf(left); // 获取对象的原型
  let prototype = right.prototype; // 获取构造函数的 prototype 对象

  // 判断构造函数的 prototype 对象是否在对象的原型链上
  while (true) {
    if (!proto) return false;
    if (proto === prototype) return true;

    proto = Object.getPrototypeOf(proto);
  }
}
```

这里使用了一个 while 循环来遍历对象的原型链，直到找到构造函数的 prototype 对象，或者原型链为空时返回 false。具体流程如下：

- 首先获取对象的原型，使用 Object.getPrototypeOf() 方法。
- 获取构造函数的 prototype 对象，即 right.prototype。
- 使用 while 循环遍历对象的原型链。
- 在循环中，首先判断原型链是否为空，如果为空则返回 false。
- 然后判断当前原型对象是否等于构造函数的 prototype 对象，如果相等则返回 true。
- 如果当前原型对象不等于构造函数的 prototype 对象，则将原型对象改为当前原型对象的原型，继续循环判断。

需要注意的是，如果构造函数的 prototype 对象不存在或者不是对象类型，那么将会抛出 TypeError 错误。

### 2、手写 new 操作符

（1）首先创建了一个新的空对象

（2）设置原型，将对象的原型设置为函数的 prototype 对象。

（3）让函数的 this 指向这个对象，执行构造函数的代码（为这个新对象添加属性）

（4）判断函数的返回值类型，如果是值类型，返回创建的对象。如果是引用类型，就返回这个引用类型的对象。

```js
function objectFactory() {
  let newObject = null;
  let constructor = Array.prototype.shift.call(arguments);
  let result = null;
  // 判断参数是否是一个函数
  if (typeof constructor !== "function") {
    console.error("type error");
    return;
  }
  // 新建一个空对象，对象的原型为构造函数的 prototype 对象
  newObject = Object.create(constructor.prototype);
  // 将 this 指向新建对象，并执行函数
  result = constructor.apply(newObject, arguments);
  // 判断返回对象
  let flag = result && (typeof result === "object" || typeof result === "function");
  // 判断返回结果
  return flag ? result : newObject;
}
// 使用方法
objectFactory(构造函数, 初始化参数);
```

实现`new`操作符的方法，其实现方式与我之前给出的第一种方法类似，但是在细节上有所不同。下面是这段代码的解释：

1.首先，我们声明了一个变量`newObject`，表示我们将要创建的新对象，以及一个变量`constructor`，用于存储我们传递给`objectFactory()`函数的第一个参数（即构造函数）。

2.接着，我们使用`Array.prototype.shift.call(arguments)`将`arguments`对象中的第一个参数（即构造函数）移除，并将其赋值给`constructor`变量。这样，`arguments`对象中就只剩下初始化参数了。

3.我们对`constructor`参数进行类型检查，确保它是一个函数。如果不是，就抛出一个错误并返回。

4.我们使用`Object.create()`方法创建一个空对象`newObject`，并将其原型设置为构造函数的原型对象。

5.我们使用`Function.prototype.apply()`方法调用构造函数，将`newObject`作为`this`参数传递给它，并将剩余的参数作为初始化参数传递给它。这样，构造函数就可以初始化`newObject`了。

6.我们检查构造函数的返回值。如果返回值是一个对象或者函数，就将其作为结果返回。否则，就返回`newObject`对象。

总的来说，这段代码与我之前给出的方法实现`new`操作符的思路是一致的。它们的主要区别在于实现的细节上，这些细节可能会对性能、可读性和代码风格产生影响。

#### Chat-Gpt实现

在JavaScript中，`new`操作符是用来创建一个新对象并将其绑定到一个构造函数上的。下面是几种手写`new`操作符的方法：

#### 方法一：使用Object.create()

```js
function myNew(constructor, ...args) {
  let obj = Object.create(constructor.prototype);
  let result = constructor.apply(obj, args);
  return result instanceof Object ? result : obj;
}
```

#### 方法二：使用Object.setPrototypeOf()

```js
function myNew(constructor, ...args) {
  let obj = {};
  Object.setPrototypeOf(obj, constructor.prototype);
  let result = constructor.apply(obj, args);
  return result instanceof Object ? result : obj;
}
```

#### 方法三：使用函数字面量

```js
function myNew(constructor, ...args) {
  let obj = {};
  obj.__proto__ = constructor.prototype;
  let result = constructor.apply(obj, args);
  return result instanceof Object ? result : obj;
}
```

这些方法都使用了JavaScript中的原型继承来创建新对象并将其与构造函数绑定。在实现`new`操作符时，我们首先创建一个新对象，然后将其原型设置为构造函数的原型，接着我们通过调用构造函数并将新对象和参数传递给它来初始化对象。最后，我们检查构造函数的返回值是否是一个对象，如果不是，就返回新对象。

### 3、1️⃣ 手写apply-call_coderwhy

```js
// new Function()
// foo.__proto__ === Function.prototype
function foo(name, age) {
  console.log(this, name, age)
}

// foo函数可以通过apply/call
// foo.apply("aaa", ["why", 18])
// foo.call("bbb", "kobe", 30)

// 1.给函数对象添加方法: hyapply
Function.prototype.hyapply = function(thisArg, otherArgs) {
  // this -> 调用的函数对象
  // thisArg -> 传入的第一个参数, 要绑定的this
  // console.log(this) // -> 当前调用的函数对象
  // this.apply(thisArg)

  thisArg.fn = this

  // 1.获取thisArg, 并且确保是一个对象类型
  thisArg = (thisArg === null || thisArg === undefined)? window: Object(thisArg)

  // thisArg.fn = this
  Object.defineProperty(thisArg, "fn", {
    enumerable: false,
    configurable: true,
    value: this
  })
  thisArg.fn(...otherArgs)

  delete thisArg.fn
}

// foo.hyapply({ name: "why" }, ["james", 25])
// foo.hyapply(123, ["why", 18])
// foo.hyapply(null, ["kobe", 30])

// 2.给函数对象添加方法: hycall
Function.prototype.hycall = function(thisArg, ...otherArgs) {
  // 1.获取thisArg, 并且确保是一个对象类型
  thisArg = (thisArg === null || thisArg === undefined)? window: Object(thisArg)

  // thisArg.fn = this
  Object.defineProperty(thisArg, "fn", {
    enumerable: false,
    configurable: true,
    value: this
  })
  thisArg.fn(...otherArgs)

  delete thisArg.fn
}

foo.hycall({ name: "why", fn: "abc" }, "james", 25)
foo.hycall(123, "why", 18)
foo.hycall(null, "kobe", 30)
```

> 代码解释

这段代码是在 `Function` 原型上添加了两个新的方法 `hyapply` 和 `hycall`，用来模拟 `apply` 和 `call` 方法的效果。下面是对代码的详细解释：

```js
// 定义一个函数 foo，用来测试 hyapply 和 hycall 方法的效果
function foo(name, age) {
  console.log(this, name, age)
}
// 定义 hyapply 方法
Function.prototype.hyapply = function(thisArg, otherArgs) {
  // 将调用 hyapply 方法的函数对象赋值给 this
  thisArg.fn = this

  // 获取 thisArg 并确保它是一个对象
  thisArg = (thisArg === null || thisArg === undefined) ? window : Object(thisArg)

  // 将函数对象 this 绑定到 thisArg.fn 属性上
  Object.defineProperty(thisArg, "fn", {
    enumerable: false,
    configurable: true,
    value: this
  })

  // 调用 thisArg.fn，传入参数 otherArgs
  thisArg.fn(...otherArgs)

  // 删除绑定到 thisArg.fn 上的函数对象
  delete thisArg.fn
}
```

`hyapply` 方法的作用是模拟 `apply` 方法的效果，它的参数是一个对象 `thisArg` 和一个数组 `otherArgs`，其中 `thisArg` 是需要绑定到函数对象的 `this` 上的对象，`otherArgs` 则是函数调用时传入的其他参数。这个方法首先将调用 `hyapply` 方法的函数对象赋值给 `thisArg.fn`，然后获取 `thisArg` 并确保它是一个对象，接着将函数对象 `this` 绑定到 `thisArg.fn` 属性上，最后调用 `thisArg.fn`，传入参数 `otherArgs`。在调用结束后，将绑定到 `thisArg.fn` 上的函数对象删除。

```js
// 定义 hycall 方法
Function.prototype.hycall = function(thisArg, ...otherArgs) {
  // 获取 thisArg 并确保它是一个对象
  thisArg = (thisArg === null || thisArg === undefined) ? window : Object(thisArg)

  // 将函数对象 this 绑定到 thisArg.fn 属性上
  Object.defineProperty(thisArg, "fn", {
    enumerable: false,
    configurable: true,
    value: this
  })

  // 调用 thisArg.fn，传入参数 otherArgs
  thisArg.fn(...otherArgs)

  // 删除绑定到 thisArg.fn 上的函数对象
  delete thisArg.fn
}
```

`hycall` 方法的作用是模拟 `call` 方法的效果，它的参数与函数调用时传入的参数一样，但是第一个参数不再是一个数组，而是直接绑定到函数对象的 `this` 上的对象。这个方法首先获取 `thisArg` 并确保它是一个对象，然后将函数对象 `this` 绑定到 `thisArg.fn` 属性上，最后调用 `thisArg.fn`，传入参数 `otherArgs`。在调用结束后，将绑定到 `thisArg.fn` 上的函数对象

### 4、1️⃣ apply-call 封装_coderwhy

```js
// new Function()
// foo.__proto__ === Function.prototype
function foo(name, age) {
  console.log(this, name, age)
}

// foo函数可以通过apply/call
// foo.apply("aaa", ["why", 18])
// foo.call("bbb", "kobe", 30)

// 1.封装思想
// 1.1.封装到独立的函数中
function execFn(thisArg, otherArgs, fn) {
  // 1.获取thisArg, 并且确保是一个对象类型
  thisArg = (thisArg === null || thisArg === undefined)? window: Object(thisArg)

  // thisArg.fn = this
  Object.defineProperty(thisArg, "fn", {
    enumerable: false,
    configurable: true,
    value: fn
  })

  // 执行代码
  thisArg.fn(...otherArgs)

  delete thisArg.fn
}

// 1.2. 封装原型中
Function.prototype.hyexec = function(thisArg, otherArgs) {
  // 1.获取thisArg, 并且确保是一个对象类型
  thisArg = (thisArg === null || thisArg === undefined)? window: Object(thisArg)

  // thisArg.fn = this
  Object.defineProperty(thisArg, "fn", {
    enumerable: false,
    configurable: true,
    value: this
  })
  thisArg.fn(...otherArgs)

  delete thisArg.fn
}


// 1.给函数对象添加方法: hyapply
Function.prototype.hyapply = function(thisArg, otherArgs) {
  this.hyexec(thisArg, otherArgs)
}
// 2.给函数对象添加方法: hycall
Function.prototype.hycall = function(thisArg, ...otherArgs) {
  this.hyexec(thisArg, otherArgs)
}

foo.hyapply({ name: "why" }, ["james", 25])
foo.hyapply(123, ["why", 18])
foo.hyapply(null, ["kobe", 30])

foo.hycall({ name: "why" }, "james", 25)
foo.hycall(123, "why", 18)
foo.hycall(null, "kobe", 30)
```

1. 首先定义了一个函数 `execFn`，该函数接受三个参数 `thisArg`、`otherArgs`、`fn`，分别表示执行函数时的上下文对象、函数的参数数组、待执行的函数。
2. 在 `execFn` 函数中，首先对 `thisArg` 进行判断，如果 `thisArg` 是 `null` 或 `undefined`，则将其设置为全局对象 `window`；否则，将其转换为对象类型。这样做是为了确保 `thisArg` 是一个对象，因为只有对象才能作为函数的上下文对象。
3. 接下来，使用 `Object.defineProperty()` 方法给 `thisArg` 对象添加一个不可枚举、可配置、值为待执行的函数的属性 `fn`。这样做是为了将待执行的函数绑定到 `thisArg` 上下文对象上。
4. 然后，使用 `...` 拓展运算符将 `otherArgs` 数组中的元素作为参数传递给函数，并执行该函数。这里使用 `thisArg.fn(...otherArgs)` 的形式来调用函数，即通过 `fn` 属性来访问待执行的函数。
5. 最后，使用 `delete` 操作符将 `fn` 属性从 `thisArg` 对象上删除，以避免对 `thisArg` 对象的污染。
6. 接着，定义了函数原型上的 `hyexec` 方法，该方法与 `execFn` 函数的功能相同，但是将待执行的函数绑定到该函数对象上，而不是绑定到 `thisArg` 上下文对象上。该方法的实现方式与 `execFn` 函数基本相同。
7. 接下来，使用原型继承的方式，将 `hyapply` 和 `hycall` 方法添加到 `Function` 构造函数的原型上。这两个方法分别对应 JavaScript 中的 `apply` 和 `call` 方法，其实现方式都是通过调用 `hyexec` 方法来实现。
8. 最后，调用 `foo` 函数，并使用 `hyapply` 和 `hycall` 方法对其进行了多次调用，验证了封装方法的正确性。

### 5、1️⃣ bind 封装_coderwhy

```js
// apply/call
function foo(name, age, height, address) {
  console.log(this, name, age, height, address)
}

// Function.prototype
// var newFoo = foo.bind({ name: "why" }, "why", 18)
// newFoo(1.88)

// 实现hybind函数
Function.prototype.hybind = function(thisArg, ...otherArgs) {
  // console.log(this) // -> foo函数对象

  // 1. 对传入的 thisArg 进行判断，如果是 null 或 undefined，将其指向全局对象 window
  thisArg = thisArg === null || thisArg === undefined ? window: Object(thisArg)
  // 2. 将当前函数对象作为一个不可枚举、不可配置、不可写的属性添加到 thisArg 上，并将其命名为 fn
  Object.defineProperty(thisArg, "fn", {
    enumerable: false,
    configurable: true,
    writable: false,
    value: this
  })

  // 3. 返回一个新的函数，该函数可以接收任意个参数
  return (...newArgs) => {
    // 4. 将 otherArgs 和 newArgs 合并为一个新数组 allArgs
    var allArgs = [...otherArgs, ...newArgs]
    // 5. 调用 thisArg 上的 fn 函数，并传入合并后的 allArgs 数组作为参数
    thisArg.fn(...allArgs)
  }
}

// 6. 使用 hybind 函数将 foo 函数的 this 绑定到字符串 "abc" 上，并传入 "kobe" 和 30 两个参数
var newFoo = foo.hybind("abc", "kobe", 30)

// 7. 多次调用 newFoo 函数，每次传入不同的参数
newFoo(1.88, "广州市")
newFoo(1.88, "广州市")
newFoo(1.88, "广州市")
newFoo(1.88, "广州市")
```

这段代码实现了一个自定义的bind函数，用于改变函数内部this指向。

1. 首先定义了一个普通的函数foo，该函数用于打印传入的参数及函数内部的this值。
2. 接着在Function.prototype对象上定义了一个hybind方法，该方法可以用于绑定函数内部的this值。该方法的第一个参数为需要绑定的this值，后面的其他参数将被传递给绑定后的函数。
3. 在hybind函数内部，首先需要判断传入的thisArg是否为null或undefined，如果是的话则将其设置为window对象，否则将其强制转换为对象类型。
4. 接着使用Object.defineProperty方法定义了一个名为fn的属性，将其值设置为当前函数对象。这里将fn设置为不可枚举、不可重写、不可修改的属性。
5. 最后返回一个箭头函数，该函数用于接收新的参数并执行绑定后的函数。在箭头函数内部，使用展开语法将otherArgs和newArgs合并为一个数组allArgs，并将其传递给thisArg对象上的fn方法，以执行绑定后的函数。
6. 最后使用该自定义的hybind函数，将需要绑定的this值和其他参数传递给它，即可得到一个新的函数newFoo。调用newFoo函数时，传递的参数将被合并后传递给原始函数foo，并改变了函数内部的this值。



### 6、3️⃣ Object.create手写

> Object.create() 是一种创建新对象并将其原型设置为指定对象的方法。下面是几种手写实现 Object.create() 方法的代码：

**手写 Object.create() 方法的思路：**

在 JavaScript 中，每个对象都有一个原型（prototype）对象。原型对象包含该对象继承的属性和方法。可以使用 Object.create() 方法手动创建一个对象并指定其原型对象。

1. 创建一个空函数（称之为 F），该函数的作用是用来作为一个中间层，它不具有任何的属性和方法。
2. 将传入的参数作为 F 函数的原型对象。
3. 返回一个新的对象，这个新对象的原型指向 F 函数的原型对象。

**手写 Object.create() 方法的代码实现：**

```js
function createObject(proto) {
  function F() {}
  F.prototype = proto;
  return new F();
}

// 使用示例
const obj1 = {name: 'obj1'};
const obj2 = createObject(obj1);
console.log(obj2.name); // 'obj1'
```

在这个实现中，我们首先定义了一个名为 createObject 的函数，它接受一个参数 proto。在函数内部，我们创建了一个空函数 F，并将它的原型对象设置为 proto。最后，我们返回一个新对象，这个对象的原型指向 F 函数的原型对象，这样新对象就继承了 proto 对象的属性和方法。

在使用示例中，我们首先创建了一个对象 obj1，然后使用 createObject 方法创建了另一个对象 obj2，它的原型指向 obj1。因此，我们可以通过 obj2 访问 obj1 的属性。

### 7、Promise

Promise 是 JavaScript 中常用的一种异步编程的解决方案，用于处理异步操作的结果。在 ES6 中，Promise 已经被标准化，成为了原生对象，简化了异步操作的代码编写。

下面是手写 Promise 的详细实现过程：

#### 1）. 创建 Promise 类

首先我们需要创建一个 Promise 类，该类需要有以下几个属性：

- status：表示当前 Promise 的状态，有三种状态：pending（进行中）、fulfilled（已成功）和 rejected（已失败）。
- value：表示异步操作成功时的返回值。
- reason：表示异步操作失败时的错误信息。
- onFulfilledCallbacks：表示成功时的回调函数队列。
- onRejectedCallbacks：表示失败时的回调函数队列。

```js
class MyPromise {
  constructor(executor) {
    this.status = 'pending';
    this.value = undefined;
    this.reason = undefined;
    this.onFulfilledCallbacks = [];
    this.onRejectedCallbacks = [];

    // 执行异步操作
    try {
      executor(this.resolve.bind(this), this.reject.bind(this));
    } catch (error) {
      this.reject(error);
    }
  }

  resolve(value) {
    if (this.status === 'pending') {
      this.status = 'fulfilled';
      this.value = value;
      this.onFulfilledCallbacks.forEach((callback) => callback(value));
    }
  }

  reject(reason) {
    if (this.status === 'pending') {
      this.status = 'rejected';
      this.reason = reason;
      this.onRejectedCallbacks.forEach((callback) => callback(reason));
    }
  }
}
```

#### 2）\. 实现 then 方法

Promise 的 then 方法用于注册异步操作成功和失败时的回调函数，需要返回一个新的 Promise 对象。

```js
then(onFulfilled, onRejected) {
  const promise2 = new MyPromise((resolve, reject) => {
    if (this.status === 'fulfilled') {
      // 当前 Promise 已经成功，执行成功回调
      try {
        const x = onFulfilled(this.value);
        this.resolvePromise(promise2, x, resolve, reject);
      } catch (error) {
        reject(error);
      }
    } else if (this.status === 'rejected') {
      // 当前 Promise 已经失败，执行失败回调
      try {
        const x = onRejected(this.reason);
        this.resolvePromise(promise2, x, resolve, reject);
      } catch (error) {
        reject(error);
      }
    } else {
      // 当前 Promise 还在进行中，将回调函数加入队列中等待执行
      this.onFulfilledCallbacks.push((value) => {
        try {
          const x = onFulfilled(value);
          this.resolvePromise(promise2, x, resolve, reject);
        } catch (error) {
          reject(error);
        }
      });
      this.onRejectedCallbacks.push((reason) => {
        try {
          const x = onRejected(reason);
          this.resolvePromise(promise2, x, resolve, reject);
        } catch (error) {
          reject(error);
        }
      });
    }
  });

  return promise2;
}
```

#### 3）\. 实现 resolvePromise 方法

resolvePromise 方法用于处理 then 方法返回的结果，将其转化为一个新的 Promise 对象。resolvePromise 方法需要处理以下情况：

- 如果 then 方法返回的是当前 Promise 对象，直接 reject 一个 TypeError 错误。
- 如果 then 方法返回的是一个 Promise 对象，将其作为 promise2 的结果。
- 如果 then 方法返回的是一个普通值，将其作为 promise2 的成功结果。
- 如果 then 方法执行出错，将错误作为 promise2 的失败结果。

```js
resolvePromise(promise2, x, resolve, reject) {
  if (promise2 === x) {
    return reject(new TypeError('Chaining cycle detected for promise'));
  }

  let called = false; // 防止多次调用

  if (x instanceof MyPromise) {
    // 如果 x 是一个 Promise 对象，调用 then 方法
    x.then(
      (value) => {
        if (called) return;
        called = true;
        this.resolvePromise(promise2, value, resolve, reject);
      },
      (reason) => {
        if (called) return;
        called = true;
        reject(reason);
      }
    );
  } else if (x && (typeof x === 'object' || typeof x === 'function')) {
    // 如果 x 是一个对象或者函数，判断其是否具有 then 方法
    try {
      const then = x.then;
      if (typeof then === 'function') {
        then.call(
          x,
          (value) => {
            if (called) return;
            called = true;
            this.resolvePromise(promise2, value, resolve, reject);
          },
          (reason) => {
            if (called) return;
            called = true;
            reject(reason);
          }
        );
      } else {
        resolve(x);
      }
    } catch (error) {
      if (called) return;
      called = true;
      reject(error);
    }
  } else {
    resolve(x);
  }
}
```

这样，一个简单的 Promise 类就被实现出来了。我们可以使用该类来进行异步操作。

例如，我们可以使用该 Promise 类来封装一个简单的异步计时器：

```js
function timer(delay) {
  return new MyPromise((resolve) => {
    setTimeout(() => {
      resolve(delay);
    }, delay);
  });
}
```

然后，我们就可以使用 Promise 对象进行链式调用：

```js
timer(1000)
  .then((value) => {
    console.log(`第一次计时完成，耗时 ${value} 毫秒`);
    return timer(2000);
  })
  .then((value) => {
    console.log(`第二次计时完成，耗时 ${value} 毫秒`);
    return timer(3000);
  })
  .then((value) => {
    console.log(`第三次计时完成，耗时 ${value} 毫秒`);
  });
```

输出结果为：

```js
第一次计时完成，耗时 1000 毫秒
第二次计时完成，耗时 2000 毫秒
第三次计时完成，耗时 3000 毫秒
```

### 8、深拷贝

```js
function isObject(obj) {
     return obj !== null && (typeof obj === "object" || typeof obj === "function")
   }
 
   function deepClone(originValue) {
     // Symbol类型
     if (typeof originValue === "symbol") {
       return Symbol(originValue.description)
     }
 
     // 判断是否是对象
     if (!isObject(originValue)) return originValue;
 
     // set类型
     if (originValue instanceof Set) {
       const newSet = new Set()
       for (const setItem of originValue) {
         newSet.add(deepClone(setItem))
       }
       return newSet
     }
 
     // 判断是函数
     if (typeof originValue === "function") {
       return originValue
     }
 
     // 判断返回值是数组还是对象
     const newObj = Array.isArray(originValue) ? [] : {}
     if (Reflect) {
       for (let key of Reflect.ownKeys(originValue)) {
         {
           let value = originValue[key]
           // 让 SymbolKey的值不同
           if (typeof key === "symbol") {
             const newSymbolKey = Symbol(key.description)
             // 将原来的值赋值给新生成的Symbol key
             value = originValue[key]
             key = newSymbolKey
           }
           newObj[key] = deepClone(value)
         }
       }
     } else {
       for (const key in originValue) {
         const value = originValue[key]
         newObj[key] = deepClone(value)
       }
 
       // 对于Symbol类型的key forin 无法便利出来
       const symbolKeys = Object.getOwnPropertySymbols(originValue)
        for (const symbolKey in symbolKeys) {
        const originSymbolValue = symbolKeys[symbolKey]
        const newSymbol = Symbol(originSymbolValue.description)
        newObj[newSymbol] = deepClone(originValue[originSymbolValue])
      }
    }
return newObj
}
```

### 9、循环引用

```js

  function isObject(obj) {
    return obj !== null && (typeof obj === "object" || typeof obj === "function")
  }

  function deepClone(originValue, map = new WeakMap()) {
    // Symbol类型
    if (typeof originValue === "symbol") {
      return Symbol(originValue.description)
    }

    // 判断是否是对象
    if (!isObject(originValue)) return originValue;

    if (map.has(originValue)) {
      return map.get(originValue)
    }
    // set类型
    if (originValue instanceof Set) {
      const newSet = new Set()
      for (const setItem of originValue) {
        newSet.add(deepClone(setItem, map))
      }
      return newSet
    }

    // 判断是函数
    if (typeof originValue === "function") {
      return originValue
    }

    // 判断返回值是数组还是对象
    const newObj = Array.isArray(originValue) ? [] : {}
    map.set(originValue, newObj)
    if (Reflect) {
      for (let key of Reflect.ownKeys(originValue)) {
        {
          let value = originValue[key]
          // 让 SymbolKey的值不同
          if (typeof key === "symbol") {
            const newSymbolKey = Symbol(key.description)
            // 将原来的值赋值给新生成的Symbol key
            value = originValue[key]
            key = newSymbolKey
          }
          newObj[key] = deepClone(value, map)
        }
      }
    } else {
      for (const key in originValue) {
        const value = originValue[key]
        newObj[key] = deepClone(value, map)
      }

      // 对于Symbol类型的key forin 无法便利出来
      const symbolKeys = Object.getOwnPropertySymbols(originValue)


      for (const symbolKey in symbolKeys) {
        const originSymbolValue = symbolKeys[symbolKey]
        const newSymbol = Symbol(originSymbolValue.description)
        newObj[newSymbol] = deepClone(originValue[originSymbolValue], map)
      }
    }

    return newObj
  }
```

### 10、事件总线的基本实现和使用(重点)

```js
class myEventBus {
  constructor() {
    this.eventBus = {};
  }

  on(eventName, eventFn) {
    let eventSet = this.eventBus[eventName];
    if (!eventSet) {
      eventSet = new Set();
      this.eventBus[eventName] = eventSet;
    }
    this.eventBus[eventName].add(eventFn);
  }

  off(eventName, eventFn) {
    if (!this.eventBus[eventName]) {
      return;
    }
    const eventSet = this.eventBus[eventName];
    if (eventSet.has(eventFn)) this.eventBus[eventName].delete(eventFn);

    // 如果删除函数后 该事件对应的set为空 则删除该事件
    if (!this.eventBus[eventName].size) {
      delete this.eventBus[eventName];
    }
  }

  emit(eventName, ...payload) {
    if (!this.eventBus[eventName]) {
      return;
    }
    for (const item of this.eventBus[eventName]) {
      item(...payload);
    }
  }
}

const mitt = new myEventBus();
mitt.on("wmm", () => {
  console.log("123");
});
const fn = () => {
  console.log("456");
};
mitt.on("wmm", fn);
mitt.on("wmm", () => {
  console.log("789");
});

setTimeout(() => {
  // 移除事件
  mitt.off("wmm", fn);
}, 1000);
setTimeout(() => {
  mitt.emit("wmm");
}, 2000);
// 123
// 789
```

### 11、总结手写Promise

一. Promise规范

https://promisesaplus.com/

二. Promise类设计

```js
class HYPromise {}
```

```js
function HYPromise() {}
```

三. 构造函数的规划

```js
class HYPromise {
  constructor(executor) {
           // 定义状态
    // 定义resolve、reject回调
    // resolve执行微任务队列：改变状态、获取value、then传入执行成功回调
    // reject执行微任务队列：改变状态、获取reason、then传入执行失败回调
    
    // try catch
    executor(resolve, reject)
  }
}
```

四. then方法的实现

```js
class HYPromise {
  then(onFulfilled, onRejected) {
    // this.onFulfilled = onFulfilled
    // this.onRejected = onRejected
    
    // 1.判断onFulfilled、onRejected，会给默认值
    
    // 2.返回Promise resolve/reject
    
    // 3.判断之前的promise状态是否确定
    // onFulfilled/onRejected直接执行（捕获异常）
    
    // 4.添加到数组中push(() => { 执行 onFulfilled/onRejected 直接执行代码})
  }
}
```

五. catch方法

```js
class HYPromise {
  catch(onRejected) {
    return this.then(undefined, onRejected)
  }
}
```

六. finally

```js
class HYPromise {
  finally(onFinally) {
    return this.then(() => {onFinally()}, () => {onFinally()})
  }
}
```

七. resolve/reject

八. all/allSettled

核心：要知道new Promise的resolve、reject在什么情况下执行

all：

- 情况一：所有的都有结果
- 情况二：有一个reject

allSettled：

- 情况：所有都有结果，并且一定执行resolve

九.race/any

race:

- 情况：只要有结果

any:

- 情况一：必须等到一个resolve结果
- 情况二：都没有resolve，所有的都是reject

## 一、JavaScript 基础

### 1. 手写 Object.create

思路：将传入的对象作为原型

```javascript
function create(obj) {
  function F() {}
  F.prototype = obj
  return new F()
}

```

### 2. 手写 instanceof 方法

instanceof 运算符用于判断构造函数的 prototype 属性是否出现在对象的原型链中的任何位置。

实现步骤：

1. 首先获取类型的原型
2. 然后获得对象的原型
3. 然后一直循环判断对象的原型是否等于类型的原型，直到对象原型为 `null`，因为原型链最终为 `null`

具体实现：

```javascript
function myInstanceof(left, right) {
  let proto = Object.getPrototypeOf(left), // 获取对象的原型
      prototype = right.prototype; // 获取构造函数的 prototype 对象

  // 判断构造函数的 prototype 对象是否在对象的原型链上
  while (true) {
    if (!proto) return false;
    if (proto === prototype) return true;

    proto = Object.getPrototypeOf(proto);
  }
}

```

### 3. 手写 new 操作符

在调用 `new` 的过程中会发生以上四件事情：

（1）首先创建了一个新的空对象

（2）设置原型，将对象的原型设置为函数的 prototype 对象。

（3）让函数的 this 指向这个对象，执行构造函数的代码（为这个新对象添加属性）

（4）判断函数的返回值类型，如果是值类型，返回创建的对象。如果是引用类型，就返回这个引用类型的对象。

```javascript
function objectFactory() {
  let newObject = null;
  let constructor = Array.prototype.shift.call(arguments);
  let result = null;
  // 判断参数是否是一个函数
  if (typeof constructor !== "function") {
    console.error("type error");
    return;
  }
  // 新建一个空对象，对象的原型为构造函数的 prototype 对象
  newObject = Object.create(constructor.prototype);
  // 将 this 指向新建对象，并执行函数
  result = constructor.apply(newObject, arguments);
  // 判断返回对象
  let flag = result && (typeof result === "object" || typeof result === "function");
  // 判断返回结果
  return flag ? result : newObject;
}
// 使用方法
objectFactory(构造函数, 初始化参数);

```

### 4. 手写 Promise

```javascript
const PENDING = "pending";
const RESOLVED = "resolved";
const REJECTED = "rejected";

function MyPromise(fn) {
  // 保存初始化状态
  var self = this;

  // 初始化状态
  this.state = PENDING;

  // 用于保存 resolve 或者 rejected 传入的值
  this.value = null;

  // 用于保存 resolve 的回调函数
  this.resolvedCallbacks = [];

  // 用于保存 reject 的回调函数
  this.rejectedCallbacks = [];

  // 状态转变为 resolved 方法
  function resolve(value) {
    // 判断传入元素是否为 Promise 值，如果是，则状态改变必须等待前一个状态改变后再进行改变
    if (value instanceof MyPromise) {
      return value.then(resolve, reject);
    }

    // 保证代码的执行顺序为本轮事件循环的末尾
    setTimeout(() => {
      // 只有状态为 pending 时才能转变，
      if (self.state === PENDING) {
        // 修改状态
        self.state = RESOLVED;

        // 设置传入的值
        self.value = value;

        // 执行回调函数
        self.resolvedCallbacks.forEach(callback => {
          callback(value);
        });
      }
    }, 0);
  }

  // 状态转变为 rejected 方法
  function reject(value) {
    // 保证代码的执行顺序为本轮事件循环的末尾
    setTimeout(() => {
      // 只有状态为 pending 时才能转变
      if (self.state === PENDING) {
        // 修改状态
        self.state = REJECTED;

        // 设置传入的值
        self.value = value;

        // 执行回调函数
        self.rejectedCallbacks.forEach(callback => {
          callback(value);
        });
      }
    }, 0);
  }

  // 将两个方法传入函数执行
  try {
    fn(resolve, reject);
  } catch (e) {
    // 遇到错误时，捕获错误，执行 reject 函数
    reject(e);
  }
}

MyPromise.prototype.then = function(onResolved, onRejected) {
  // 首先判断两个参数是否为函数类型，因为这两个参数是可选参数
  onResolved =
    typeof onResolved === "function"
      ? onResolved
      : function(value) {
          return value;
        };

  onRejected =
    typeof onRejected === "function"
      ? onRejected
      : function(error) {
          throw error;
        };

  // 如果是等待状态，则将函数加入对应列表中
  if (this.state === PENDING) {
    this.resolvedCallbacks.push(onResolved);
    this.rejectedCallbacks.push(onRejected);
  }

  // 如果状态已经凝固，则直接执行对应状态的函数

  if (this.state === RESOLVED) {
    onResolved(this.value);
  }

  if (this.state === REJECTED) {
    onRejected(this.value);
  }
};

```

### 5. 手写 Promise.then

`then` 方法返回一个新的 `promise` 实例，为了在 `promise` 状态发生变化时（`resolve` / `reject` 被调用时）再执行 `then` 里的函数，我们使用一个 `callbacks` 数组先把传给then的函数暂存起来，等状态改变时再调用。

**那么，怎么保证后一个 \**`\*\*then\*\*`\** 里的方法在前一个 \**`\*\*then\*\*`\**（可能是异步）结束之后再执行呢？** 我们可以将传给 `then` 的函数和新 `promise` 的 `resolve` 一起 `push` 到前一个 `promise` 的 `callbacks` 数组中，达到承前启后的效果：

- 承前：当前一个 `promise` 完成后，调用其 `resolve` 变更状态，在这个 `resolve` 里会依次调用 `callbacks` 里的回调，这样就执行了 `then` 里的方法了
- 启后：上一步中，当 `then` 里的方法执行完成后，返回一个结果，如果这个结果是个简单的值，就直接调用新 `promise` 的 `resolve`，让其状态变更，这又会依次调用新 `promise` 的 `callbacks` 数组里的方法，循环往复。。如果返回的结果是个 `promise`，则需要等它完成之后再触发新 `promise` 的 `resolve`，所以可以在其结果的 `then` 里调用新 `promise` 的 `resolve`

```javascript
then(onFulfilled, onReject){
    // 保存前一个promise的this
    const self = this; 
    return new MyPromise((resolve, reject) => {
      // 封装前一个promise成功时执行的函数
      let fulfilled = () => {
        try{
          const result = onFulfilled(self.value); // 承前
          return result instanceof MyPromise? result.then(resolve, reject) : resolve(result); //启后
        }catch(err){
          reject(err)
        }
      }
      // 封装前一个promise失败时执行的函数
      let rejected = () => {
        try{
          const result = onReject(self.reason);
          return result instanceof MyPromise? result.then(resolve, reject) : reject(result);
        }catch(err){
          reject(err)
        }
      }
      switch(self.status){
        case PENDING: 
          self.onFulfilledCallbacks.push(fulfilled);
          self.onRejectedCallbacks.push(rejected);
          break;
        case FULFILLED:
          fulfilled();
          break;
        case REJECT:
          rejected();
          break;
      }
    })
   }

```

**注意：**

- 连续多个 `then` 里的回调方法是同步注册的，但注册到了不同的 `callbacks` 数组中，因为每次 `then` 都返回新的 `promise` 实例（参考上面的例子和图）
- 注册完成后开始执行构造函数中的异步事件，异步完成之后依次调用 `callbacks` 数组中提前注册的回调

### 6. 手写 Promise.all

**1) 核心思路**

1. 接收一个 Promise 实例的数组或具有 Iterator 接口的对象作为参数
2. 这个方法返回一个新的 promise 对象，
3. 遍历传入的参数，用Promise.resolve()将参数"包一层"，使其变成一个promise对象
4. 参数所有回调成功才是成功，返回值数组与参数顺序一致
5. 参数数组其中一个失败，则触发失败状态，第一个触发失败的 Promise 错误信息作为 Promise.all 的错误信息。

**2）实现代码**

一般来说，Promise.all 用来处理多个并发请求，也是为了页面数据构造的方便，将一个页面所用到的在不同接口的数据一起请求过来，不过，如果其中一个接口失败了，多个请求也就失败了，页面可能啥也出不来，这就看当前页面的耦合程度了

```javascript
function promiseAll(promises) {
  return new Promise(function(resolve, reject) {
    if(!Array.isArray(promises)){
        throw new TypeError(`argument must be a array`)
    }
    var resolvedCounter = 0;
    var promiseNum = promises.length;
    var resolvedResult = [];
    for (let i = 0; i < promiseNum; i++) {
      Promise.resolve(promises[i]).then(value=>{
        resolvedCounter++;
        resolvedResult[i] = value;
        if (resolvedCounter == promiseNum) {
            return resolve(resolvedResult)
          }
      },error=>{
        return reject(error)
      })
    }
  })
}
// test
let p1 = new Promise(function (resolve, reject) {
    setTimeout(function () {
        resolve(1)
    }, 1000)
})
let p2 = new Promise(function (resolve, reject) {
    setTimeout(function () {
        resolve(2)
    }, 2000)
})
let p3 = new Promise(function (resolve, reject) {
    setTimeout(function () {
        resolve(3)
    }, 3000)
})
promiseAll([p3, p1, p2]).then(res => {
    console.log(res) // [3, 1, 2]
})

```

### 7. 手写 Promise.race

该方法的参数是 Promise 实例数组, 然后其 then 注册的回调方法是数组中的某一个 Promise 的状态变为 fulfilled 的时候就执行. 因为 Promise 的状态**只能改变一次**, 那么我们只需要把 Promise.race 中产生的 Promise 对象的 resolve 方法, 注入到数组中的每一个 Promise 实例中的回调函数中即可.

```javascript
Promise.race = function (args) {
  return new Promise((resolve, reject) => {
    for (let i = 0, len = args.length; i < len; i++) {
      args[i].then(resolve, reject)
    }
  })
}

```

### 8. 手写防抖函数

函数防抖是指在事件被触发 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。这可以使用在一些点击请求的事件上，避免因为用户的多次点击向后端发送多次请求。

```javascript
// 函数防抖的实现
function debounce(fn, wait) {
  let timer = null;

  return function() {
    let context = this,
        args = arguments;

    // 如果此时存在定时器的话，则取消之前的定时器重新记时
    if (timer) {
      clearTimeout(timer);
      timer = null;
    }

    // 设置定时器，使事件间隔指定事件后执行
    timer = setTimeout(() => {
      fn.apply(context, args);
    }, wait);
  };
}

```

### 9. 手写节流函数

函数节流是指规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。节流可以使用在 scroll 函数的事件监听上，通过事件节流来降低事件调用的频率。

```javascript
// 函数节流的实现;
function throttle(fn, delay) {
  let curTime = Date.now();

  return function() {
    let context = this,
        args = arguments,
        nowTime = Date.now();

    // 如果两次时间间隔超过了指定时间，则执行函数。
    if (nowTime - curTime >= delay) {
      curTime = Date.now();
      return fn.apply(context, args);
    }
  };
}

```

### 10. 手写类型判断函数

```javascript
function getType(value) {
  // 判断数据是 null 的情况
  if (value === null) {
    return value + "";
  }
  // 判断数据是引用类型的情况
  if (typeof value === "object") {
    let valueClass = Object.prototype.toString.call(value),
      type = valueClass.split(" ")[1].split("");
    type.pop();
    return type.join("").toLowerCase();
  } else {
    // 判断数据是基本数据类型的情况和函数的情况
    return typeof value;
  }
}

```

### 11. 手写 call 函数

call 函数的实现步骤：

1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
2. 判断传入上下文对象是否存在，如果不存在，则设置为 window 。
3. 处理传入的参数，截取第一个参数后的所有参数。
4. 将函数作为上下文对象的一个属性。
5. 使用上下文对象来调用这个方法，并保存返回结果。
6. 删除刚才新增的属性。
7. 返回结果。

```javascript
// call函数实现
Function.prototype.myCall = function(context) {
  // 判断调用对象
  if (typeof this !== "function") {
    console.error("type error");
  }
  // 获取参数
  let args = [...arguments].slice(1),
      result = null;
  // 判断 context 是否传入，如果未传入则设置为 window
  context = context || window;
  // 将调用函数设为对象的方法
  context.fn = this;
  // 调用函数
  result = context.fn(...args);
  // 将属性删除
  delete context.fn;
  return result;
};

```

### 12. 手写 apply 函数

apply 函数的实现步骤：

1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
2. 判断传入上下文对象是否存在，如果不存在，则设置为 window 。
3. 将函数作为上下文对象的一个属性。
4. 判断参数值是否传入
5. 使用上下文对象来调用这个方法，并保存返回结果。
6. 删除刚才新增的属性
7. 返回结果

```javascript
// apply 函数实现
Function.prototype.myApply = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  let result = null;
  // 判断 context 是否存在，如果未传入则为 window
  context = context || window;
  // 将函数设为对象的方法
  context.fn = this;
  // 调用方法
  if (arguments[1]) {
    result = context.fn(...arguments[1]);
  } else {
    result = context.fn();
  }
  // 将属性删除
  delete context.fn;
  return result;
};

```

### 13. 手写 bind 函数

bind 函数的实现步骤：

1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
2. 保存当前函数的引用，获取其余传入参数值。
3. 创建一个函数返回
4. 函数内部使用 apply 来绑定函数调用，需要判断函数作为构造函数的情况，这个时候需要传入当前函数的 this 给 apply 调用，其余情况都传入指定的上下文对象。

```javascript
// bind 函数实现
Function.prototype.myBind = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  // 获取参数
  var args = [...arguments].slice(1),
      fn = this;
  return function Fn() {
    // 根据调用方式，传入不同绑定值
    return fn.apply(
      this instanceof Fn ? this : context,
      args.concat(...arguments)
    );
  };
};

```

### 14. 函数柯里化的实现

函数柯里化指的是一种将使用多个参数的一个函数转换成一系列使用一个参数的函数的技术。

```javascript
function curry(fn, args) {
  // 获取函数需要的参数长度
  let length = fn.length;

  args = args || [];

  return function() {
    let subArgs = args.slice(0);

    // 拼接得到现有的所有参数
    for (let i = 0; i < arguments.length; i++) {
      subArgs.push(arguments[i]);
    }

    // 判断参数的长度是否已经满足函数所需参数的长度
    if (subArgs.length >= length) {
      // 如果满足，执行函数
      return fn.apply(this, subArgs);
    } else {
      // 如果不满足，递归返回科里化的函数，等待参数的传入
      return curry.call(this, fn, subArgs);
    }
  };
}

// es6 实现
function curry(fn, ...args) {
  return fn.length <= args.length ? fn(...args) : curry.bind(null, fn, ...args);
}

```

### 15. 实现AJAX请求

AJAX是 Asynchronous JavaScript and XML 的缩写，指的是通过 JavaScript 的 异步通信，从服务器获取 XML 文档从中提取数据，再更新当前网页的对应部分，而不用刷新整个网页。

创建AJAX请求的步骤：

- **创建一个 XMLHttpRequest 对象。**
- 在这个对象上**使用 open 方法创建一个 HTTP 请求**，open 方法所需要的参数是请求的方法、请求的地址、是否异步和用户的认证信息。
- 在发起请求前，可以为这个对象**添加一些信息和监听函数**。比如说可以通过 setRequestHeader 方法来为请求添加头信息。还可以为这个对象添加一个状态监听函数。一个 XMLHttpRequest 对象一共有 5 个状态，当它的状态变化时会触发onreadystatechange 事件，可以通过设置监听函数，来处理请求成功后的结果。当对象的 readyState 变为 4 的时候，代表服务器返回的数据接收完成，这个时候可以通过判断请求的状态，如果状态是 2xx 或者 304 的话则代表返回正常。这个时候就可以通过 response 中的数据来对页面进行更新了。
- 当对象的属性和监听函数设置完成后，最后调**用 sent 方法来向服务器发起请求**，可以传入参数作为发送的数据体。

```javascript
const SERVER_URL = "/server";
let xhr = new XMLHttpRequest();
// 创建 Http 请求
xhr.open("GET", SERVER_URL, true);
// 设置状态监听函数
xhr.onreadystatechange = function() {
  if (this.readyState !== 4) return;
  // 当请求成功时
  if (this.status === 200) {
    handle(this.response);
  } else {
    console.error(this.statusText);
  }
};
// 设置请求失败时的监听函数
xhr.onerror = function() {
  console.error(this.statusText);
};
// 设置请求头信息
xhr.responseType = "json";
xhr.setRequestHeader("Accept", "application/json");
// 发送 Http 请求
xhr.send(null);

```

### 16. 使用Promise封装AJAX请求

```javascript
// promise 封装实现：
function getJSON(url) {
  // 创建一个 promise 对象
  let promise = new Promise(function(resolve, reject) {
    let xhr = new XMLHttpRequest();
    // 新建一个 http 请求
    xhr.open("GET", url, true);
    // 设置状态的监听函数
    xhr.onreadystatechange = function() {
      if (this.readyState !== 4) return;
      // 当请求成功或失败时，改变 promise 的状态
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
    // 设置错误监听函数
    xhr.onerror = function() {
      reject(new Error(this.statusText));
    };
    // 设置响应的数据类型
    xhr.responseType = "json";
    // 设置请求头信息
    xhr.setRequestHeader("Accept", "application/json");
    // 发送 http 请求
    xhr.send(null);
  });
  return promise;
}

```

### 17. 实现浅拷贝

浅拷贝是指，一个新的对象对原始对象的属性值进行精确地拷贝，如果拷贝的是基本数据类型，拷贝的就是基本数据类型的值，如果是引用数据类型，拷贝的就是内存地址。如果其中一个对象的引用内存地址发生改变，另一个对象也会发生变化。

#### （1）Object.assign()

`Object.assign()`是ES6中对象的拷贝方法，接受的第一个参数是目标对象，其余参数是源对象，用法：`Object.assign(target, source_1, ···)`，该方法可以实现浅拷贝，也可以实现一维对象的深拷贝。

**注意：**

- 如果目标对象和源对象有同名属性，或者多个源对象有同名属性，则后面的属性会覆盖前面的属性。
- 如果该函数只有一个参数，当参数为对象时，直接返回该对象；当参数不是对象时，会先将参数转为对象然后返回。
- 因为`null` 和 `undefined` 不能转化为对象，所以第一个参数不能为`null`或 `undefined`，会报错。

```javascript
let target = {a: 1};
let object2 = {b: 2};
let object3 = {c: 3};
Object.assign(target,object2,object3);  
console.log(target);  // {a: 1, b: 2, c: 3}

```

#### （2）扩展运算符

使用扩展运算符可以在构造字面量对象的时候，进行属性的拷贝。语法：`let cloneObj = { ...obj };`

```javascript
let obj1 = {a:1,b:{c:1}}
let obj2 = {...obj1};
obj1.a = 2;
console.log(obj1); //{a:2,b:{c:1}}
console.log(obj2); //{a:1,b:{c:1}}
obj1.b.c = 2;
console.log(obj1); //{a:2,b:{c:2}}
console.log(obj2); //{a:1,b:{c:2}}

```

#### （3）数组方法实现数组浅拷贝

###### **1）Array.prototype.slice**

- `slice()`方法是JavaScript数组的一个方法，这个方法可以从已有数组中返回选定的元素：用法：`array.slice(start, end)`，该方法不会改变原始数组。
- 该方法有两个参数，两个参数都可选，如果两个参数都不写，就可以实现一个数组的浅拷贝。

```javascript
let arr = [1,2,3,4];
console.log(arr.slice()); // [1,2,3,4]
console.log(arr.slice() === arr); //false

```

###### **2）Array.prototype.concat**

- `concat()` 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。
- 该方法有两个参数，两个参数都可选，如果两个参数都不写，就可以实现一个数组的浅拷贝。

```javascript
let arr = [1,2,3,4];
console.log(arr.concat()); // [1,2,3,4]
console.log(arr.concat() === arr); //false

```

#### （4）手写实现浅拷贝

```javascript
// 浅拷贝的实现;

function shallowCopy(object) {
  // 只拷贝对象
  if (!object || typeof object !== "object") return;

  // 根据 object 的类型判断是新建一个数组还是对象
  let newObject = Array.isArray(object) ? [] : {};

  // 遍历 object，并且判断是 object 的属性才拷贝
  for (let key in object) {
    if (object.hasOwnProperty(key)) {
      newObject[key] = object[key];
    }
  }

  return newObject;
}// 浅拷贝的实现;

function shallowCopy(object) {
  // 只拷贝对象
  if (!object || typeof object !== "object") return;

  // 根据 object 的类型判断是新建一个数组还是对象
  let newObject = Array.isArray(object) ? [] : {};

  // 遍历 object，并且判断是 object 的属性才拷贝
  for (let key in object) {
    if (object.hasOwnProperty(key)) {
      newObject[key] = object[key];
    }
  }

  return newObject;
}// 浅拷贝的实现;
function shallowCopy(object) {
  // 只拷贝对象
  if (!object || typeof object !== "object") return;
  // 根据 object 的类型判断是新建一个数组还是对象
  let newObject = Array.isArray(object) ? [] : {};
  // 遍历 object，并且判断是 object 的属性才拷贝
  for (let key in object) {
    if (object.hasOwnProperty(key)) {
      newObject[key] = object[key];
    }
  }
  return newObject;
}

```

### 18. 实现深拷贝

- **浅拷贝：** 浅拷贝指的是将一个对象的属性值复制到另一个对象，如果有的属性的值为引用类型的话，那么会将这个引用的地址复制给对象，因此两个对象会有同一个引用类型的引用。浅拷贝可以使用  Object.assign 和展开运算符来实现。
- **深拷贝：** 深拷贝相对浅拷贝而言，如果遇到属性值为引用类型的时候，它新建一个引用类型并将对应的值复制给它，因此对象获得的一个新的引用类型而不是一个原有类型的引用。深拷贝对于一些对象可以使用 JSON 的两个函数来实现，但是由于 JSON 的对象格式比 js 的对象格式更加严格，所以如果属性值里边出现函数或者 Symbol 类型的值时，会转换失败

#### （1）JSON.stringify()

- `JSON.parse(JSON.stringify(obj))`是目前比较常用的深拷贝方法之一，它的原理就是利用`JSON.stringify` 将`js`对象序列化（JSON字符串），再使用`JSON.parse`来反序列化(还原)`js`对象。
- 这个方法可以简单粗暴的实现深拷贝，但是还存在问题，拷贝的对象中如果有函数，undefined，symbol，当使用过`JSON.stringify()`进行处理之后，都会消失。

```javascript
let obj1 = {  a: 0,
              b: {
                 c: 0
                 }
            };
let obj2 = JSON.parse(JSON.stringify(obj1));
obj1.a = 1;
obj1.b.c = 1;
console.log(obj1); // {a: 1, b: {c: 1}}
console.log(obj2); // {a: 0, b: {c: 0}}

```

#### （2）函数库lodash的_.cloneDeep方法

该函数库也有提供_.cloneDeep用来做 Deep Copy

```javascript
var _ = require('lodash');
var obj1 = {
    a: 1,
    b: { f: { g: 1 } },
    c: [1, 2, 3]
};
var obj2 = _.cloneDeep(obj1);
console.log(obj1.b.f === obj2.b.f);// false

```

#### （3）手写实现深拷贝函数

```javascript
// 深拷贝的实现
function deepCopy(object) {
  if (!object || typeof object !== "object") return;

  let newObject = Array.isArray(object) ? [] : {};

  for (let key in object) {
    if (object.hasOwnProperty(key)) {
      newObject[key] =
        typeof object[key] === "object" ? deepCopy(object[key]) : object[key];
    }
  }

  return newObject;
}

```

## 二、数据处理

### 1. 实现日期格式化函数

输入：

```javascript
dateFormat(new Date('2020-12-01'), 'yyyy/MM/dd') // 2020/12/01
dateFormat(new Date('2020-04-01'), 'yyyy/MM/dd') // 2020/04/01
dateFormat(new Date('2020-04-01'), 'yyyy年MM月dd日') // 2020年04月01日

const dateFormat = (dateInput, format)=>{
    var day = dateInput.getDate() 
    var month = dateInput.getMonth() + 1  
    var year = dateInput.getFullYear()   
    format = format.replace(/yyyy/, year)
    format = format.replace(/MM/,month)
    format = format.replace(/dd/,day)
    return format
}

```

### 2. 交换a,b的值，不能用临时变量

巧妙的利用两个数的和、差：

```javascript
a = a + b
b = a - b
a = a - b

```

### 3. 实现数组的乱序输出

主要的实现思路就是：

- 取出数组的第一个元素，随机产生一个索引值，将该第一个元素和这个索引对应的元素进行交换。
- 第二次取出数据数组第二个元素，随机产生一个除了索引为1的之外的索引值，并将第二个元素与该索引值对应的元素进行交换
- 按照上面的规律执行，直到遍历完成

```javascript
var arr = [1,2,3,4,5,6,7,8,9,10];
for (var i = 0; i < arr.length; i++) {
  const randomIndex = Math.round(Math.random() * (arr.length - 1 - i)) + i;
  [arr[i], arr[randomIndex]] = [arr[randomIndex], arr[i]];
}
console.log(arr)

```

还有一方法就是倒序遍历：

```javascript
var arr = [1,2,3,4,5,6,7,8,9,10];
let length = arr.length,
    randomIndex,
    temp;
  while (length) {
    randomIndex = Math.floor(Math.random() * length--);
    temp = arr[length];
    arr[length] = arr[randomIndex];
    arr[randomIndex] = temp;
  }
console.log(arr)

```

### 4. 实现数组元素求和

- arr=[1,2,3,4,5,6,7,8,9,10]，求和

```javascript
let arr=[1,2,3,4,5,6,7,8,9,10]
let sum = arr.reduce( (total,i) => total += i,0);
console.log(sum);

```

- arr=[1,2,3,[[4,5],6],7,8,9]，求和

```javascript
var = arr=[1,2,3,[[4,5],6],7,8,9]
let arr= arr.toString().split(',').reduce( (total,i) => total += Number(i),0);
console.log(arr);

```

递归实现：

```javascript
let arr = [1, 2, 3, 4, 5, 6] 

function add(arr) {
    if (arr.length == 1) return arr[0] 
    return arr[0] + add(arr.slice(1)) 
}
console.log(add(arr)) // 21

```

### 5. 实现数组的扁平化

**（1）递归实现**

普通的递归思路很容易理解，就是通过循环递归的方式，一项一项地去遍历，如果每一项还是一个数组，那么就继续往下遍历，利用递归程序的方法，来实现数组的每一项的连接：

```javascript
let arr = [1, [2, [3, 4, 5]]];
function flatten(arr) {
  let result = [];

  for(let i = 0; i < arr.length; i++) {
    if(Array.isArray(arr[i])) {
      result = result.concat(flatten(arr[i]));
    } else {
      result.push(arr[i]);
    }
  }
  return result;
}
flatten(arr);  //  [1, 2, 3, 4，5]

```

**（2）reduce 函数迭代**

从上面普通的递归函数中可以看出，其实就是对数组的每一项进行处理，那么其实也可以用reduce 来实现数组的拼接，从而简化第一种方法的代码，改造后的代码如下所示：

```javascript
let arr = [1, [2, [3, 4]]];
function flatten(arr) {
    return arr.reduce(function(prev, next){
        return prev.concat(Array.isArray(next) ? flatten(next) : next)
    }, [])
}
console.log(flatten(arr));//  [1, 2, 3, 4，5]

```

**（3）扩展运算符实现**

这个方法的实现，采用了扩展运算符和 some 的方法，两者共同使用，达到数组扁平化的目的：

```javascript
let arr = [1, [2, [3, 4]]];
function flatten(arr) {
    while (arr.some(item => Array.isArray(item))) {
        arr = [].concat(...arr);
    }
    return arr;
}
console.log(flatten(arr)); //  [1, 2, 3, 4，5]

```

**（4）split 和 toString**

可以通过 split 和 toString 两个方法来共同实现数组扁平化，由于数组会默认带一个 toString 的方法，所以可以把数组直接转换成逗号分隔的字符串，然后再用 split 方法把字符串重新转换为数组，如下面的代码所示：

```javascript
let arr = [1, [2, [3, 4]]];
function flatten(arr) {
    return arr.toString().split(',');
}
console.log(flatten(arr)); //  [1, 2, 3, 4，5]

```

通过这两个方法可以将多维数组直接转换成逗号连接的字符串，然后再重新分隔成数组。

**（5）ES6 中的 flat**

我们还可以直接调用 ES6 中的 flat 方法来实现数组扁平化。flat 方法的语法：`arr.flat([depth])`

其中 depth 是 flat 的参数，depth 是可以传递数组的展开深度（默认不填、数值是 1），即展开一层数组。如果层数不确定，参数可以传进 Infinity，代表不论多少层都要展开：

```javascript
let arr = [1, [2, [3, 4]]];
function flatten(arr) {
  return arr.flat(Infinity);
}
console.log(flatten(arr)); //  [1, 2, 3, 4，5]

```

可以看出，一个嵌套了两层的数组，通过将 flat 方法的参数设置为 Infinity，达到了我们预期的效果。其实同样也可以设置成 2，也能实现这样的效果。在编程过程中，如果数组的嵌套层数不确定，最好直接使用 Infinity，可以达到扁平化。 **（6）正则和 JSON 方法** 在第4种方法中已经使用 toString 方法，其中仍然采用了将 JSON.stringify 的方法先转换为字符串，然后通过正则表达式过滤掉字符串中的数组的方括号，最后再利用 JSON.parse 把它转换成数组：

```javascript
let arr = [1, [2, [3, [4, 5]]], 6];
function flatten(arr) {
  let str = JSON.stringify(arr);
  str = str.replace(/(\[|\])/g, '');
  str = '[' + str + ']';
  return JSON.parse(str); 
}
console.log(flatten(arr)); //  [1, 2, 3, 4，5]

```

### 6. 实现数组去重

给定某无序数组，要求去除数组中的重复数字并且返回新的无重复数组。

ES6方法（使用数据结构集合）：

```javascript
const array = [1, 2, 3, 5, 1, 5, 9, 1, 2, 8];

Array.from(new Set(array)); // [1, 2, 3, 5, 9, 8]

```

ES5方法：使用map存储不重复的数字

```javascript
const array = [1, 2, 3, 5, 1, 5, 9, 1, 2, 8];

uniqueArray(array); // [1, 2, 3, 5, 9, 8]

function uniqueArray(array) {
  let map = {};
  let res = [];
  for(var i = 0; i < array.length; i++) {
    if(!map.hasOwnProperty([array[i]])) {
      map[array[i]] = 1;
      res.push(array[i]);
    }
  }
  return res;
}

```

### 7. 实现数组的flat方法

```javascript
function _flat(arr, depth) {
  if(!Array.isArray(arr) || depth <= 0) {
    return arr;
  }
  return arr.reduce((prev, cur) => {
    if (Array.isArray(cur)) {
      return prev.concat(_flat(cur, depth - 1))
    } else {
      return prev.concat(cur);
    }
  }, []);
}

```

### 8. 实现数组的push方法

```javascript
let arr = [];
Array.prototype.push = function() {
	for( let i = 0 ; i < arguments.length ; i++){
		this[this.length] = arguments[i] ;
	}
	return this.length;
}
```

### 9. 实现数组的filter方法

```javascript
Array.prototype._filter = function(fn) {
    if (typeof fn !== "function") {
        throw Error('参数必须是一个函数');
    }
    const res = [];
    for (let i = 0, len = this.length; i < len; i++) {
        fn(this[i]) && res.push(this[i]);
    }
    return res;
}

```

### 10. 实现数组的map方法

```javascript
Array.prototype._map = function(fn) {
   if (typeof fn !== "function") {
        throw Error('参数必须是一个函数');
    }
    const res = [];
    for (let i = 0, len = this.length; i < len; i++) {
        res.push(fn(this[i]));
    }
    return res;
}

```

### 11. 实现字符串的repeat方法

输入字符串s，以及其重复的次数，输出重复的结果，例如输入abc，2，输出abcabc。

```javascript
function repeat(s, n) {
    return (new Array(n + 1)).join(s);
}

```

递归：

```javascript
function repeat(s, n) {
    return (n > 0) ? s.concat(repeat(s, --n)) : "";
}

```

### 12. 实现字符串翻转

在字符串的原型链上添加一个方法，实现字符串翻转：

```javascript
String.prototype._reverse = function(a){
    return a.split("").reverse().join("");
}
var obj = new String();
var res = obj._reverse ('hello');
console.log(res);    // olleh

```

需要注意的是，必须通过实例化对象之后再去调用定义的方法，不然找不到该方法。

### 13. 将数字每千分位用逗号隔开

**数字有小数版本：**

```javascript
let format = n => {
    let num = n.toString() // 转成字符串
    let decimals = ''
        // 判断是否有小数
    num.indexOf('.') > -1 ? decimals = num.split('.')[1] : decimals
    let len = num.length
    if (len <= 3) {
        return num
    } else {
        let temp = ''
        let remainder = len % 3
        decimals ? temp = '.' + decimals : temp
        if (remainder > 0) { // 不是3的整数倍
            return num.slice(0, remainder) + ',' + num.slice(remainder, len).match(/\d{3}/g).join(',') + temp
        } else { // 是3的整数倍
            return num.slice(0, len).match(/\d{3}/g).join(',') + temp 
        }
    }
}
format(12323.33)  // '12,323.33'

```

**数字无小数版本：**

```javascript
let format = n => {
    let num = n.toString() 
    let len = num.length
    if (len <= 3) {
        return num
    } else {
        let remainder = len % 3
        if (remainder > 0) { // 不是3的整数倍
            return num.slice(0, remainder) + ',' + num.slice(remainder, len).match(/\d{3}/g).join(',') 
        } else { // 是3的整数倍
            return num.slice(0, len).match(/\d{3}/g).join(',') 
        }
    }
}
format(1232323)  // '1,232,323'

```

### 14. 实现非负大整数相加

JavaScript对数值有范围的限制，限制如下：

```javascript
Number.MAX_VALUE // 1.7976931348623157e+308
Number.MAX_SAFE_INTEGER // 9007199254740991
Number.MIN_VALUE // 5e-324
Number.MIN_SAFE_INTEGER // -9007199254740991

```

如果想要对一个超大的整数(`> Number.MAX_SAFE_INTEGER`)进行加法运算，但是又想输出一般形式，那么使用 + 是无法达到的，一旦数字超过 `Number.MAX_SAFE_INTEGER` 数字会被立即转换为科学计数法，并且数字精度相比以前将会有误差。

实现一个算法进行大数的相加：

```javascript
function sumBigNumber(a, b) {
  let res = '';
  let temp = 0;
  
  a = a.split('');
  b = b.split('');
  
  while (a.length || b.length || temp) {
    temp += ~~a.pop() + ~~b.pop();
    res = (temp % 10) + res;
    temp  = temp > 9
  }
  return res.replace(/^0+/, '');
}

```

其主要的思路如下：

- 首先用字符串的方式来保存大数，这样数字在数学表示上就不会发生变化
- 初始化res，temp来保存中间的计算结果，并将两个字符串转化为数组，以便进行每一位的加法运算
- 将两个数组的对应的位进行相加，两个数相加的结果可能大于10，所以可能要仅为，对10进行取余操作，将结果保存在当前位
- 判断当前位是否大于9，也就是是否会进位，若是则将temp赋值为true，因为在加法运算中，true会自动隐式转化为1，以便于下一次相加
- 重复上述操作，直至计算结束

### 13. 实现 add(1)(2)(3)

函数柯里化概念： 柯里化（Currying）是把接受多个参数的函数转变为接受一个单一参数的函数，并且返回接受余下的参数且返回结果的新函数的技术。

1）粗暴版

```javascript
function add (a) {
return function (b) {
 	return function (c) {
      return a + b + c;
 	}
}
}
console.log(add(1)(2)(3)); // 6

```

2）柯里化解决方案

- 参数长度固定

```javascript
var add = function (m) {
  var temp = function (n) {
    return add(m + n);
  }
  temp.toString = function () {
    return m;
  }
  return temp;
};
console.log(add(3)(4)(5)); // 12
console.log(add(3)(6)(9)(25)); // 43

```

对于add(3)(4)(5)，其执行过程如下：

1. 先执行add(3)，此时m=3，并且返回temp函数；
2. 执行temp(4)，这个函数内执行add(m+n)，n是此次传进来的数值4，m值还是上一步中的3，所以add(m+n)=add(3+4)=add(7)，此时m=7，并且返回temp函数
3. 执行temp(5)，这个函数内执行add(m+n)，n是此次传进来的数值5，m值还是上一步中的7，所以add(m+n)=add(7+5)=add(12)，此时m=12，并且返回temp函数
4. 由于后面没有传入参数，等于返回的temp函数不被执行而是打印，了解JS的朋友都知道对象的toString是修改对象转换字符串的方法，因此代码中temp函数的toString函数return m值，而m值是最后一步执行函数时的值m=12，所以返回值是12。

- 参数长度不固定

```javascript
function add (...args) {
    //求和
    return args.reduce((a, b) => a + b)
}
function currying (fn) {
    let args = []
    return function temp (...newArgs) {
        if (newArgs.length) {
            args = [
                ...args,
                ...newArgs
            ]
            return temp
        } else {
            let val = fn.apply(this, args)
            args = [] //保证再次调用时清空
            return val
        }
    }
}
let addCurry = currying(add)
console.log(addCurry(1)(2)(3)(4, 5)())  //15
console.log(addCurry(1)(2)(3, 4, 5)())  //15
console.log(addCurry(1)(2, 3, 4, 5)())  //15

```

### 14. 实现类数组转化为数组

类数组转换为数组的方法有这样几种：

- 通过 call 调用数组的 slice 方法来实现转换

```javascript
Array.prototype.slice.call(arrayLike);

```

- 通过 call 调用数组的 splice 方法来实现转换

```javascript
Array.prototype.splice.call(arrayLike, 0);

```

- 通过 apply 调用数组的 concat 方法来实现转换

```javascript
Array.prototype.concat.apply([], arrayLike);

```

- 通过 Array.from 方法来实现转换

```javascript
Array.from(arrayLike);

```

### 15. 使用 reduce 求和

arr = [1,2,3,4,5,6,7,8,9,10]，求和

```javascript
let arr = [1,2,3,4,5,6,7,8,9,10]
arr.reduce((prev, cur) => { return prev + cur }, 0)

```

arr = [1,2,3,[[4,5],6],7,8,9]，求和

```javascript
let arr = [1,2,3,4,5,6,7,8,9,10]
arr.flat(Infinity).reduce((prev, cur) => { return prev + cur }, 0)

```

arr = [{a:1, b:3}, {a:2, b:3, c:4}, {a:3}]，求和

```javascript
let arr = [{a:9, b:3, c:4}, {a:1, b:3}, {a:3}] 

arr.reduce((prev, cur) => {
    return prev + cur["a"];
}, 0)

```

### 16. 将js对象转化为树形结构

```javascript
// 转换前：
source = [{
            id: 1,
            pid: 0,
            name: 'body'
          }, {
            id: 2,
            pid: 1,
            name: 'title'
          }, {
            id: 3,
            pid: 2,
            name: 'div'
          }]
// 转换为: 
tree = [{
          id: 1,
          pid: 0,
          name: 'body',
          children: [{
            id: 2,
            pid: 1,
            name: 'title',
            children: [{
              id: 3,
              pid: 1,
              name: 'div'
            }]
          }
        }]

```

代码实现：

```javascript
function jsonToTree(data) {
  // 初始化结果数组，并判断输入数据的格式
  let result = []
  if(!Array.isArray(data)) {
    return result
  }
  // 使用map，将当前对象的id与当前对象对应存储起来
  let map = {};
  data.forEach(item => {
    map[item.id] = item;
  });
  // 
  data.forEach(item => {
    let parent = map[item.pid];
    if(parent) {
      (parent.children || (parent.children = [])).push(item);
    } else {
      result.push(item);
    }
  });
  return result;
}

```

### 17. 使用ES5和ES6求函数参数的和

ES5：

```javascript
function sum() {
    let sum = 0
    Array.prototype.forEach.call(arguments, function(item) {
        sum += item * 1
    })
    return sum
}

```

ES6：

```javascript
function sum(...nums) {
    let sum = 0
    nums.forEach(function(item) {
        sum += item * 1
    })
    return sum
}

```

### 18. 解析 URL Params 为对象

```javascript
let url = 'http://www.domain.com/?user=anonymous&id=123&id=456&city=%E5%8C%97%E4%BA%AC&enabled';
parseParam(url)
/* 结果
{ user: 'anonymous',
  id: [ 123, 456 ], // 重复出现的 key 要组装成数组，能被转成数字的就转成数字类型
  city: '北京', // 中文需解码
  enabled: true, // 未指定值得 key 约定为 true
}
*/

function parseParam(url) {
  const paramsStr = /.+\?(.+)$/.exec(url)[1]; // 将 ? 后面的字符串取出来
  const paramsArr = paramsStr.split('&'); // 将字符串以 & 分割后存到数组中
  let paramsObj = {};
  // 将 params 存到对象中
  paramsArr.forEach(param => {
    if (/=/.test(param)) { // 处理有 value 的参数
      let [key, val] = param.split('='); // 分割 key 和 value
      val = decodeURIComponent(val); // 解码
      val = /^\d+$/.test(val) ? parseFloat(val) : val; // 判断是否转为数字
      if (paramsObj.hasOwnProperty(key)) { // 如果对象有 key，则添加一个值
        paramsObj[key] = [].concat(paramsObj[key], val);
      } else { // 如果对象没有这个 key，创建 key 并设置值
        paramsObj[key] = val;
      }
    } else { // 处理没有 value 的参数
      paramsObj[param] = true;
    }
  })
  return paramsObj;
}

```

### 19. 实现Array.of 方法

Array.of 方法是用于创建一个新的数组，它接受任意数量的参数，并将这些参数作为数组元素，返回新的数组。如果只传递一个参数，那么这个参数就是数组的长度。

下面是一个简单的实现示例：

```javascript
Array.of = function() {
  return Array.prototype.slice.call(arguments);
};
```

这个实现方法首先将参数转换成一个类数组对象，然后通过调用 Array.prototype.slice 方法，将其转换成一个真正的数组并返回。这个方法可以接受任意数量的参数，并且可以正确处理单个参数的情况。

下面是一个使用 Array.of 方法创建新数组的示例：

```javascript
let arr1 = Array.of(1, 2, 3); // [1, 2, 3]
let arr2 = Array.of(5); // [5]
let arr3 = Array.of(); // []
```

## 三、场景应用

### 1. 循环打印红黄绿

下面来看一道比较典型的问题，通过这个问题来对比几种异步编程方法：**红灯 3s 亮一次，绿灯 1s 亮一次，黄灯 2s 亮一次；如何让三个灯不断交替重复亮灯？**

三个亮灯函数：

```javascript
function red() {
    console.log('red');
}
function green() {
    console.log('green');
}
function yellow() {
    console.log('yellow');
}

```

这道题复杂的地方在于**需要“交替重复”亮灯**，而不是“亮完一次”就结束了。

#### （1）用 callback 实现

```javascript
const task = (timer, light, callback) => {
    setTimeout(() => {
        if (light === 'red') {
            red()
        }
        else if (light === 'green') {
            green()
        }
        else if (light === 'yellow') {
            yellow()
        }
        callback()
    }, timer)
}
task(3000, 'red', () => {
    task(2000, 'green', () => {
        task(1000, 'yellow', Function.prototype)
    })
})

```

这里存在一个 bug：代码只是完成了一次流程，执行后红黄绿灯分别只亮一次。该如何让它交替重复进行呢？

上面提到过递归，可以递归亮灯的一个周期：

```javascript
const step = () => {
    task(3000, 'red', () => {
        task(2000, 'green', () => {
            task(1000, 'yellow', step)
        })
    })
}
step()

```

**注意看黄灯亮的回调里又再次调用了 step 方法** 以完成循环亮灯。

#### （2）用 promise 实现

```javascript
const task = (timer, light) => 
    new Promise((resolve, reject) => {
        setTimeout(() => {
            if (light === 'red') {
                red()
            }
            else if (light === 'green') {
                green()
            }
            else if (light === 'yellow') {
                yellow()
            }
            resolve()
        }, timer)
    })
const step = () => {
    task(3000, 'red')
        .then(() => task(2000, 'green'))
        .then(() => task(2100, 'yellow'))
        .then(step)
}
step()

```

这里将回调移除，在一次亮灯结束后，resolve 当前 promise，并依然使用递归进行。

#### （3）用 async/await 实现

```javascript
const taskRunner =  async () => {
    await task(3000, 'red')
    await task(2000, 'green')
    await task(2100, 'yellow')
    taskRunner()
}
taskRunner()

```

### 2. 实现每隔一秒打印 1,2,3,4

```javascript
// 使用闭包实现
for (var i = 0; i < 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}
// 使用 let 块级作用域
for (let i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, i * 1000);
}

```

### 3. 小孩报数问题

有30个小孩儿，编号从1-30，围成一圈依此报数，1、2、3 数到 3 的小孩儿退出这个圈， 然后下一个小孩 重新报数 1、2、3，问最后剩下的那个小孩儿的编号是多少?

```javascript
function childNum(num, count){
    let allplayer = [];    
    for(let i = 0; i < num; i++){
        allplayer[i] = i + 1;
    }
    
    let exitCount = 0;    // 离开人数
    let counter = 0;      // 记录报数
    let curIndex = 0;     // 当前下标
    
    while(exitCount < num - 1){
        if(allplayer[curIndex] !== 0) counter++;    
        
        if(counter == count){
            allplayer[curIndex] = 0;                 
            counter = 0;
            exitCount++;  
        }
        curIndex++;
        if(curIndex == num){
            curIndex = 0               
        };           
    }    
    for(i = 0; i < num; i++){
        if(allplayer[i] !== 0){
            return allplayer[i]
        }      
    }
}
childNum(30, 3)

```

### 4. 用Promise实现图片的异步加载

```javascript
let imageAsync=(url)=>{
            return new Promise((resolve,reject)=>{
                let img = new Image();
                img.src = url;
                img.οnlοad=()=>{
                    console.log(`图片请求成功，此处进行通用操作`);
                    resolve(image);
                }
                img.οnerrοr=(err)=>{
                    console.log(`失败，此处进行失败的通用操作`);
                    reject(err);
                }
            })
        }
        
imageAsync("url").then(()=>{
    console.log("加载成功");
}).catch((error)=>{
    console.log("加载失败");
})

```

### 5. 实现发布-订阅模式

```javascript
class EventCenter{
  // 1. 定义事件容器，用来装事件数组
	let handlers = {}

  // 2. 添加事件方法，参数：事件名 事件方法
  addEventListener(type, handler) {
    // 创建新数组容器
    if (!this.handlers[type]) {
      this.handlers[type] = []
    }
    // 存入事件
    this.handlers[type].push(handler)
  }

  // 3. 触发事件，参数：事件名 事件参数
  dispatchEvent(type, params) {
    // 若没有注册该事件则抛出错误
    if (!this.handlers[type]) {
      return new Error('该事件未注册')
    }
    // 触发事件
    this.handlers[type].forEach(handler => {
      handler(...params)
    })
  }

  // 4. 事件移除，参数：事件名 要删除事件，若无第二个参数则删除该事件的订阅和发布
  removeEventListener(type, handler) {
    if (!this.handlers[type]) {
      return new Error('事件无效')
    }
    if (!handler) {
      // 移除事件
      delete this.handlers[type]
    } else {
      const index = this.handlers[type].findIndex(el => el === handler)
      if (index === -1) {
        return new Error('无该绑定事件')
      }
      // 移除事件
      this.handlers[type].splice(index, 1)
      if (this.handlers[type].length === 0) {
        delete this.handlers[type]
      }
    }
  }
}

```

### 6. 查找文章中出现频率最高的单词

```javascript
function findMostWord(article) {
  // 合法性判断
  if (!article) return;
  // 参数处理
  article = article.trim().toLowerCase();
  let wordList = article.match(/[a-z]+/g),
    visited = [],
    maxNum = 0,
    maxWord = "";
  article = " " + wordList.join("  ") + " ";
  // 遍历判断单词出现次数
  wordList.forEach(function(item) {
    if (visited.indexOf(item) < 0) {
      // 加入 visited 
      visited.push(item);
      let word = new RegExp(" " + item + " ", "g"),
        num = article.match(word).length;
      if (num > maxNum) {
        maxNum = num;
        maxWord = item;
      }
    }
  });
  return maxWord + "  " + maxNum;
}

```

### 7. 封装异步的fetch，使用async await方式来使用

```javascript
(async () => {
    class HttpRequestUtil {
        async get(url) {
            const res = await fetch(url);
            const data = await res.json();
            return data;
        }
        async post(url, data) {
            const res = await fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            });
            const result = await res.json();
            return result;
        }
        async put(url, data) {
            const res = await fetch(url, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                data: JSON.stringify(data)
            });
            const result = await res.json();
            return result;
        }
        async delete(url, data) {
            const res = await fetch(url, {
                method: 'DELETE',
                headers: {
                    'Content-Type': 'application/json'
                },
                data: JSON.stringify(data)
            });
            const result = await res.json();
            return result;
        }
    }
    const httpRequestUtil = new HttpRequestUtil();
    const res = await httpRequestUtil.get('http://golderbrother.cn/');
    console.log(res);
})();

```

### 8. 实现prototype继承

所谓的原型链继承就是让新实例的原型等于父类的实例：

```javascript
//父方法
function SupperFunction(flag1){
    this.flag1 = flag1;
}

//子方法
function SubFunction(flag2){
    this.flag2 = flag2;
}

//父实例
var superInstance = new SupperFunction(true);

//子继承父
SubFunction.prototype = superInstance;

//子实例
var subInstance = new SubFunction(false);
//子调用自己和父的属性
subInstance.flag1;   // true
subInstance.flag2;   // false

```

### 9. 实现双向数据绑定

```javascript
let obj = {}
let input = document.getElementById('input')
let span = document.getElementById('span')
// 数据劫持
Object.defineProperty(obj, 'text', {
  configurable: true,
  enumerable: true,
  get() {
    console.log('获取数据了')
  },
  set(newVal) {
    console.log('数据更新了')
    input.value = newVal
    span.innerHTML = newVal
  }
})
// 输入监听
input.addEventListener('keyup', function(e) {
  obj.text = e.target.value
})

```

### 10. 实现简单路由

```javascript
// hash路由
class Route{
  constructor(){
    // 路由存储对象
    this.routes = {}
    // 当前hash
    this.currentHash = ''
    // 绑定this，避免监听时this指向改变
    this.freshRoute = this.freshRoute.bind(this)
    // 监听
    window.addEventListener('load', this.freshRoute, false)
    window.addEventListener('hashchange', this.freshRoute, false)
  }
  // 存储
  storeRoute (path, cb) {
    this.routes[path] = cb || function () {}
  }
  // 更新
  freshRoute () {
    this.currentHash = location.hash.slice(1) || '/'
    this.routes[this.currentHash]()
  }
}

```

### 11. 实现斐波那契数列

```javascript
// 递归
function fn (n){
    if(n==0) return 0
    if(n==1) return 1
    return fn(n-2)+fn(n-1)
}
// 优化
function fibonacci2(n) {
    const arr = [1, 1, 2];
    const arrLen = arr.length;

    if (n <= arrLen) {
        return arr[n];
    }

    for (let i = arrLen; i < n; i++) {
        arr.push(arr[i - 1] + arr[ i - 2]);
    }

    return arr[arr.length - 1];
}
// 非递归
function fn(n) {
    let pre1 = 1;
    let pre2 = 1;
    let current = 2;

    if (n <= 2) {
        return current;
    }

    for (let i = 2; i < n; i++) {
        pre1 = pre2;
        pre2 = current;
        current = pre1 + pre2;
    }

    return current;
}

```

### 12. 字符串出现的不重复最长长度

用一个滑动窗口装没有重复的字符，枚举字符记录最大值即可。用 map 维护字符的索引，遇到相同的字符，把左边界移动过去即可。挪动的过程中记录最大长度：

```javascript
var lengthOfLongestSubstring = function (s) {
    let map = new Map();
    let i = -1
    let res = 0
    let n = s.length
    for (let j = 0; j < n; j++) {
        if (map.has(s[j])) {
            i = Math.max(i, map.get(s[j]))
        }
        res = Math.max(res, j - i)
        map.set(s[j], j)
    }
    return res
};

```

### 13. 使用 setTimeout 实现 setInterval

setInterval 的作用是每隔一段指定时间执行一个函数，但是这个执行不是真的到了时间立即执行，它真正的作用是每隔一段时间将事件加入事件队列中去，只有当当前的执行栈为空的时候，才能去从事件队列中取出事件执行。所以可能会出现这样的情况，就是当前执行栈执行的时间很长，导致事件队列里边积累多个定时器加入的事件，当执行栈结束的时候，这些事件会依次执行，因此就不能到间隔一段时间执行的效果。

针对 setInterval 的这个缺点，我们可以使用 setTimeout 递归调用来模拟 setInterval，这样我们就确保了只有一个事件结束了，我们才会触发下一个定时器事件，这样解决了 setInterval 的问题。

实现思路是使用递归函数，不断地去执行 setTimeout 从而达到 setInterval 的效果

```javascript
function mySetInterval(fn, timeout) {
  // 控制器，控制定时器是否继续执行
  var timer = {
    flag: true
  };
  // 设置递归函数，模拟定时器执行。
  function interval() {
    if (timer.flag) {
      fn();
      setTimeout(interval, timeout);
    }
  }
  // 启动定时器
  setTimeout(interval, timeout);
  // 返回控制器
  return timer;
}

```

### 14. 实现 jsonp

```javascript
// 动态的加载js文件
function addScript(src) {
  const script = document.createElement('script');
  script.src = src;
  script.type = "text/javascript";
  document.body.appendChild(script);
}
addScript("http://xxx.xxx.com/xxx.js?callback=handleRes");
// 设置一个全局的callback函数来接收回调结果
function handleRes(res) {
  console.log(res);
}
// 接口返回的数据格式
handleRes({a: 1, b: 2});

```

### 15. 判断对象是否存在循环引用

循环引用对象本来没有什么问题，但是序列化的时候就会发生问题，比如调用`JSON.stringify()`对该类对象进行序列化，就会报错: `Converting circular structure to JSON.`

下面方法可以用来判断一个对象中是否已存在循环引用：

```javascript
const isCycleObject = (obj,parent) => {
    const parentArr = parent || [obj];
    for(let i in obj) {
        if(typeof obj[i] === 'object') {
            let flag = false;
            parentArr.forEach((pObj) => {
                if(pObj === obj[i]){
                    flag = true;
                }
            })
            if(flag) return true;
            flag = isCycleObject(obj[i],[...parentArr,obj[i]]);
            if(flag) return true;
        }
    }
    return false;
}


const a = 1;
const b = {a};
const c = {b};
const o = {d:{a:3},c}
o.c.b.aa = a;

console.log(isCycleObject(o)

```

查找有序二维数组的目标值：

```javascript
var findNumberIn2DArray = function(matrix, target) {
    if (matrix == null || matrix.length == 0) {
        return false;
    }
    let row = 0;
    let column = matrix[0].length - 1;
    while (row < matrix.length && column >= 0) {
        if (matrix[row][column] == target) {
            return true;
        } else if (matrix[row][column] > target) {
            column--;
        } else {
            row++;
        }
    }
    return false;
};


```

二维数组斜向打印：

```javascript
function printMatrix(arr){
  let m = arr.length, n = arr[0].length
	let res = []
  
  // 左上角，从0 到 n - 1 列进行打印
  for (let k = 0; k < n; k++) {
    for (let i = 0, j = k; i < m && j >= 0; i++, j--) {
      res.push(arr[i][j]);
    }
  }

  // 右下角，从1 到 n - 1 行进行打印
  for (let k = 1; k < m; k++) {
    for (let i = k, j = n - 1; i < m && j >= 0; i++, j--) {
      res.push(arr[i][j]);
    }
  }
  return res
}
```



作者：CUGGZ
链接：https://juejin.cn/post/6946136940164939813
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

