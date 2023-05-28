

# 📁 this、箭头函数


## this的面试题解析

面试题一

```js
var name = "window";
var person = {
  name: "person",
  sayName: function () {
    console.log(this.name);
  }
};
function sayName() {
  var sss = person.sayName;
  sss();                          // window
  person.sayName();               // person
  (person.sayName)();             // person
  (b = person.sayName)();         // window 
}
sayName();
```

面试题二

```js
var name = 'window'
var person1 = {
  name: 'person1',
  foo1: function () {
    console.log(this.name)
  },
  foo2: () => console.log(this.name),
  foo3: function () {
    return function () {
      console.log(this.name)
    }
  },
  foo4: function () {
    return () => {
      console.log(this.name)
    }
  }
}

var person2 = { name: 'person2' }

// person1.foo1(); // 隐式绑定: person1
// person1.foo1.call(person2); // person2

// person1.foo2(); // 上层作用域: window
// person1.foo2.call(person2); // window

// person1.foo3()(); // window
// person1.foo3.call(person2)(); // window
// person1.foo3().call(person2); // person2

// person1.foo4()(); // person1
// person1.foo4.call(person2)(); // person2
// person1.foo4().call(person2); // person1
```

面试题三

```js
var name = 'window'
function Person (name) {
  this.name = name
  this.foo1 = function () {
    console.log(this.name)
  },
  this.foo2 = () => console.log(this.name),
  this.foo3 = function () {
    return function () {
      console.log(this.name)
    }
  },
  this.foo4 = function () {
    return () => {
      console.log(this.name)
    }
  }
}
var person1 = new Person('person1')
var person2 = new Person('person2')

// person1.foo1() // person1
// person1.foo1.call(person2) // person2

// person1.foo2() // person1
// person1.foo2.call(person2) // person1

// person1.foo3()() // window
// person1.foo3.call(person2)() // window
// person1.foo3().call(person2) // person2

// person1.foo4()() // person1
// person1.foo4.call(person2)() // person2
// person1.foo4().call(person2) // person1
```

面试题四

```js
var name = 'window'
function Person (name) {
  this.name = name
  this.obj = {
    name: 'obj',
    foo1: function () {
      return function () {
        console.log(this.name)
      }
    },
    foo2: function () {
      return () => {
        console.log(this.name)
      }
    }
  }
}
var person1 = new Person('person1')
var person2 = new Person('person2')

// person1.obj.foo1()() // window
// person1.obj.foo1.call(person2)() // window
// person1.obj.foo1().call(person2) // person2

// person1.obj.foo2()() // obj
// person1.obj.foo2.call(person2)() // person2
// person1.obj.foo2().call(person2) // obj
```

## this的绑定规则

1、默认绑定规则：

如果一个函数默认被调用，那么“this”指向全局对象（在浏览器是window对象，在node.js是global对象）；

在默认绑定规则下， "this" 关键字将绑定到全局对象。这是因为当在函数中没有显式指定 "this" 关键字时，JavaScript 引擎会在调用栈中查找最近的函数调用，然后将 "this" 绑定到该调用的上下文中。如果没有找到任何函数调用，则 "this" 将默认绑定到全局对象。

```js
function myFunction() {
	console.log(this); // window
}

myFunction();
```

2、隐式绑定规则：

在隐式绑定规则下， "this" 关键字将绑定到调用该函数的对象。当函数作为对象的方法被调用时，JavaScript 引擎会将该函数作为对象的属性进行访问，然后在函数内部使用 "this" 关键字引用该对象。

```js
const person = {
  name: 'John',
  age: 30,
  sayName: function() {
 	 console.log(this.name);
  }
};

person.sayName(); // John
```

3、显示绑定规则：

使用 call() 或 apply() 方法，可以显式地指定函数在调用时所绑定的 "this" 关键字。这是通过在调用函数时将需要绑定到 "this" 关键字的对象作为第一个参数传递来实现的。

使用 bind() 方法可以创建一个新函数，该函数在调用时将永久绑定到指定的对象。这是通过返回一个新函数，该函数的 "this" 关键字将永久绑定到指定对象来实现的。

```
const person1 = {
  name: "John",
  age: 30,
};

const person2 = {
  name: "Mike",
  age: 35,
};

function sayName() {
  console.log(this.name);
}

sayName.call(person1); // John
sayName.call(person2); // Mike
```

4、new绑定规则：

当使用new操作符调用一个函数时，会按照以下步骤执行：

1. 在内存中创建一个新对象；
2. 将这个新对象内部的 \[\[Prototype\]\] 属性赋值为构造函数的 prototype 属性；
3. 将构造函数内部的 this 赋值为这个新对象（即 this 指向新对象）；
4. 执行构造函数内部的代码（给新对象添加属性）；
5. 如果构造函数返回了非空对象，则返回该对象；否则，返回刚创建的新对象；

这样，"this" 关键字就被绑定到新创建的对象上了。

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.sayHello = function () {
  console.log(\`Hello, my name is ${this.name} 
                            and I am ${this.age} years old.`);
};
const john = new Person('John', 30);
john.sayHello(); // 输出 "Hello, my name is John and I am 30 years old."
```

在这个例子中，构造函数Person创建一个新的对象，并将name和age属性添加到该对象中。同时，它的原型对象上也定义了一个sayHello方法。然后，使用new操作符调用构造函数来创建一个新的Person对象，并将它赋值给变量john。最后，调用john的sayHello方法来输出一句问候语。

5、箭头函数绑定：

箭头函数的“this”是在创建时静态绑定的，它继承了它所处的词法作用域中的“this”。

```js
const person = {
  name: 'Alice',
  sayHello: () => {
    console.log(`Hello, my name is ${this.name}.`);
  }
};
person.sayHello(); // 输出：Hello, my name is undefined.
```

## apply、call、bind函数的用法和区别

`apply()`, `call()`, 和 `bind()`是 JavaScript 中的三种函数调用方式，它们的作用都是改变函数的执行上下文（context）。这意味着它们可以更改函数内部的 this 指向，并传递参数。

- `call()`和 `apply()`可以立即调用函数，而 `bind()`则返回一个新的函数，该函数可以稍后调用。
- `call()`和 `apply()`方法的参数列表可以不同，`call()`方法接受一系列单独的参数，而 `apply()`方法接受一个参数数组。

如果你已经有了要传递的实参，那么你可以使用 `call()`或 `apply()`方法。如果你想先绑定 this 值，并稍后再传递实参，那么你可以使用 `bind()`方法。

好的，让我们更详细地了解 `call()`、`apply()`和 `bind()`方法的用法和区别。

1、call()

`call()`方法是在一个对象上调用一个方法时，指定该对象作为调用方法的 this 值。它接受一个参数列表，第一个参数是要绑定的 this 值，之后是函数的实参。语法如下：

```js
function.call(thisArg, arg1, arg2, ...)
```

其中，`thisArg`是要绑定的 this 值，`arg1`、`arg2`等是函数的实参。下面是一个例子：

```js
function sayHello() {
	console.log(`Hello, ${this.name}!`);
}

const person = {
	name: 'John'
};

sayHello.call(person); // 输出 Hello, John!
```

2、apply()

`apply()`方法也是在一个对象上调用一个方法时，指定该对象作为调用方法的 this 值。与 `call()`方法不同的是，`apply()`方法接受一个数组作为参数，该数组包含了要传递给函数的实参。语法如下：

```js
function.apply(thisArg, [arg1, arg2, ...])
```

其中，`thisArg`是要绑定的 this 值，`[arg1, arg2, ...]`是要传递给函数的实参数组。下面是一个例子：

```js
function sayHello(name) {
	`console.log(`Hello, ${name}! My name is ${this.name}.`);`
}

const person = {
	name: 'John'
};

sayHello.apply(person, ['Bob']); // 输出 Hello, Bob! My name is John.
```

3、bind()

`bind()`方法是在一个对象上调用一个方法时，创建一个新的函数，并将该函数绑定到指定的对象上。与 `call()`和 `apply()`方法不同的是，`bind()`方法不会立即调用函数，而是返回一个新的函数，该函数可以稍后调用。语法如下：

```js
function.bind(thisArg, arg1, arg2, ...)
```

其中，`thisArg`是要绑定的 this 值，`arg1`、`arg2`等是要传递给函数的实参。下面是一个例子：

```js
function sayHello(name) {
	console.log(`Hello, ${name}! My name is ${this.name}.`);
}

const person = {
	name: 'John'
};

const sayHelloToBob = sayHello.bind(person, 'Bob');
sayHelloToBob(); // 输出 Hello, Bob! My name is John.
```
在使用 `bind` 方法传递参数时，需要注意参数的顺序：

1.  首先是绑定函数的执行上下文（`this` 值），它是 `bind` 方法的第一个参数。
2.  接下来是要传递给函数的参数，它们依次按照参数列表的顺序传递给函数。

## 箭头函数的各种用法和简写

1、基本写法

()：函数的参数

{}：函数的执行体

```js
var foo3 = (name, age) => {
  console.log("箭头函数的函数体")
  console.log(name, age)
}
```

2、优化写法

- 只有一个参数时, 可以省略()


```js
names.forEach(item => {
   console.log(item)
})
```

- 只有一行代码时, 可以省略{}


```js
names.forEach(item => console.log(item))
```

- 只要一行代码时, 表达式的返回值会作为箭头函数默认返回值, 所以可以省略return


```js
var newNums = nums.filter(item => item % 2 === 0)
var newNums = nums.filter(item => item % 2 === 0)
```

- 如果箭头函数默认返回的是对象, 在省略{}的时候, 对象必须使用()包裹 () => ({name: "why"})


```js
var arrFn = () => ["abc", "cba"]
var arrFn = () => {} // 注意: 这里是{}执行体
var arrFn = () => ({ name: "why" })
console.log(arrFn())
```


## apply() , call() , 和 bind() 如何改变函数的执行上下文

在 JavaScript 中，函数执行上下文（context）是指在函数执行时，函数所处的环境，包括函数内部的 this 值、当前作用域链、变量对象以及 this 值的指向等信息。apply()、call()、和 bind() 都是用于改变函数执行上下文的方法。

1、apply() 方法：

apply() 方法是**函数对象的方法**，用于改变函数的执行上下文。apply() 方法的第一个参数是要绑定给 this 的值，第二个参数是一个数组，包含了要传递给函数的参数列表。

这个方法会在函数调用时，将函数内部的 this 指向第一个参数，将第二个参数中的参数传递给函数。

例如：

```js
function greeting() {
  console.log("Hello, " + this.name);
}

var person = { name: "John" };
greeting.apply(person); // 输出 "Hello, John"
```

在上面的代码中，通过 apply() 方法将 greeting 函数的执行上下文从全局对象切换到了 person 对象。

2、call() 方法：

call() 方法与 apply() 方法类似，也是用于改变函数的执行上下文。不同的是，call() 方法接收的是一系列单独的参数，而不是一个数组。

例如：

```js
function greeting() {
  console.log("Hello, " + this.name);
}

var person = { name: "John" };
greeting.call(person); // 输出 "Hello, John"
```

在上面的代码中，通过 call() 方法将 greeting 函数的执行上下文从全局对象切换到了 person 对象。

3、bind() 方法：

bind() 方法也可以改变函数的执行上下文，但是与 apply() 和 call() 不同的是，bind() 方法返回的是一个新函数，而不是立即执行原函数。

例如：

```js
function greeting() {
  console.log("Hello, " + this.name);
}

var person = { name: "John" };
var greetJohn = greeting.bind(person);
greetJohn(); // 输出 "Hello, John"
```

在上面的代码中，通过 bind() 方法将 greeting 函数的执行上下文从全局对象切换到了 person 对象，并返回了一个新函数 greetJohn。调用 greetJohn() 时，执行上下文仍然是 person 对象。


## 箭头函数和普通函数有什么区别？

一、语法

箭头函数使用箭头（`=>`）来定义，而普通函数使用 `function` 关键字来定义。例如，一个简单的箭头函数可以写成这样：

```js
const add = (a, b) => a + b;
```

而相应的普通函数写法如下：

```js
function add(a, b) {
  return a + b;
}
```

二、返回关键字return

如果箭头函数只有一个表达式，它将自动返回该表达式的结果，而无需使用 `return` 关键字。例如，上面的 `add` 函数可以写成这样：

```js
const add = (a, b) => a + b;
```

普通函数必须使用 `return` 关键字来返回值。例如，相应的 `add` 函数将如下所示：

```js
function add(a, b) {
  return a + b;
}
```

三、this 值

箭头函数和普通函数的作用域也不同。箭头函数没有自己的 `this` 值，而是继承了它们的父级作用域的 `this` 值。这意味着，在箭头函数内部使用 `this` 关键字时，它将指向其定义时的外部作用域。相比之下，普通函数的this值是可变的。例如：

```js
const person = {
  name: 'Alice',
  sayName: function() {
    console.log(this.name);
  },
  sayNameArrow: () => {
    console.log(this.name);
  }
};

person.sayName(); // "Alice"
person.sayNameArrow(); // undefined
```

在上面的例子中，`sayName` 方法是一个普通函数，`sayNameArrow` 方法是一个箭头函数。在 `sayName` 方法中，`this` 关键字指向 `person` 对象，因为它是通过对象调用的。但是在 `sayNameArrow` 方法中，`this` 关键字指向其定义时的外部作用域，因此它的值是 `undefined`。

四、arguments 对象

在箭头函数中，没有自己的 `arguments` 对象，这意味着无法通过 `arguments` 对象来访问函数参数的列表。如果需要访问函数参数，必须使用命名参数或使用 `...rest` 语法来获取剩余参数列表。例如：

```javascript
const sum = (...args) => {
  return args.reduce((a, b) => a + b, 0);
}

console.log(sum(1, 2, 3)); // 6
```

在上面的例子中，`sum` 函数使用 `...rest` 语法来获取所有的参数列表，然后使用 `reduce` 方法来计算它们的总和。

五、构造函数

箭头函数不能用作构造函数，因为它们没有自己的 `this` 值。如果尝试在箭头函数中使用 `new` 关键字创建一个实例，则会抛出错误。例如：

```javascript
const Person = (name) => {
  this.name = name;
};

const person = new Person('Alice'); // TypeError: Person is not a constructor
```

在上面的例子中，`Person` 函数是一个箭头函数，但是尝试使用 `new` 关键字创建一个实例会抛出错误。

六、原型

箭头函数没有自己的原型对象，也不能使用 `new` 关键字来创建对象。由于箭头函数没有原型，因此不能向其添加方法。例如：

```js
const add = (a, b) => a + b;

add.prototype; // undefined

const obj = new add(); // TypeError: add is not a constructor
```

在上面的例子中，`add` 函数是一个箭头函数，因此无法访问其原型对象，也不能使用 `new` 关键字来创建对象。

七、递归

由于箭头函数没有自己的 `this` 值，因此不能在函数内部递归调用自身。如果尝试在箭头函数中递归调用自身，则会出现错误。例如：

```javascript
const countdown = (n) => {
  if (n > 0) {
    console.log(n);
    countdown(n - 1);
  }
};

countdown(3); // TypeError: countdown is not a function
```

在上面的例子中，`countdown` 函数是一个箭头函数，尝试在函数内部递归调用自身时会抛出错误。

八、使用场景

箭头函数通常用于简化函数表达式的语法和提高代码可读性，特别是在使用回调函数时更为常见。普通函数则适用于更多的场景，例如在构造函数中创建对象，定义方法，定义具有多个参数的函数等。此外，由于箭头函数没有 `this` 值和自己的 `arguments` 对象，因此在需要访问这些对象的情况下，应使用普通函数。

九、函数名称

箭头函数没有自己的名称，因此在调用堆栈跟踪中可能不太容易识别。如果需要给函数命名，应使用普通函数，或者在箭头函数外部使用变量来存储函数。例如：

```javascript
const add = (a, b) => a + b;

console.log(add.name); // ""
```

在上面的例子中，`add` 函数是一个箭头函数，没有自己的名称，因此无法通过 `name` 属性获取函数名称。

综上所述，箭头函数和普通函数在多个方面存在区别，包括语法、返回值、作用域、参数传递、构造函数、原型、递归、arguments 对象、this 值、使用场景和函数名称等方面。在使用函数时应根据具体需求选择合适的类型。

## 箭头函数的不适用场合

第一个场合是定义对象的方法，且该方法内部包括`this`。

```javascript
const cat = {
  lives: 9,
  jumps: () => {
    this.lives--;
  }
}
```

上面代码中，`cat.jumps()`方法是一个箭头函数，这是错误的。调用`cat.jumps()`时，如果是普通函数，该方法内部的`this`指向`cat`；如果写成上面那样的箭头函数，使得`this`指向全局对象，因此不会得到预期结果。这是因为对象不构成单独的作用域，导致`jumps`箭头函数定义时的作用域就是全局作用域。

第二个场合是需要动态`this`的时候，也不应使用箭头函数。

```javascript
var button = document.getElementById('press');
button.addEventListener('click', () => {
  this.classList.toggle('on');
});
```

上面代码运行时，点击按钮会报错，因为`button`的监听函数是一个箭头函数，导致里面的`this`就是全局对象。如果改成普通函数，`this`就会动态指向被点击的按钮对象。

另外，如果函数体很复杂，有许多行，或者函数内部有大量的读写操作，不单纯是为了计算值，这时也不应该使用箭头函数，而是要使用普通函数，这样可以提高代码可读性。

# 📁 JavaScript_运行原理

## 如何理解执行上下文

执行上下文（Execution Context）是 JavaScript 中一个非常重要的概念，它是 JavaScript 引擎用来管理代码执行的机制。

简单来说，执行上下文就是当前 JavaScript 代码的执行环境。每当 JavaScript 引擎开始执行一段代码时，都会创建一个新的执行上下文，并将其推入执行上下文栈中。当代码执行完毕后，该执行上下文会被弹出栈。

执行上下文包含三个重要的组成部分：

1. 变量环境（Variable Environment）：用于存储变量和函数的声明，并确定它们的作用域。在变量环境中，还包含了 this 的指向。

2. 词法环境（Lexical Environment）：用于处理当前执行上下文中的标识符和变量，包括变量的声明、函数的声明、块级作用域等。词法环境可以理解为一个查找标识符的结构体。

3. 外部环境（Outer Environment）：指向该执行上下文所在的外部执行上下文。在函数执行上下文中，外部环境指向该函数被调用的执行上下文。在全局执行上下文中，外部环境指向 null。

在每个执行上下文中，还有一个重要的属性，叫做作用域链（Scope Chain）。作用域链是由当前执行上下文的变量环境和其外部环境的词法环境组成的，用于决定变量的访问权限。

当代码中使用一个变量时，JavaScript 引擎会首先在当前执行上下文的变量环境中查找该变量。如果找不到，就会沿着作用域链向上查找，直到找到该变量或者到达全局执行上下文。如果仍然找不到该变量，就会抛出一个 ReferenceError 异常。

虽然执行上下文的概念比较抽象，但是理解执行上下文是非常重要的，因为它关系到 JavaScript 中很多特性的实现，比如作用域、闭包、this 等。掌握执行上下文的机制可以帮助我们更好地理解 JavaScript 的运行时行为，从而编写出更加高效和健壮的代码。


## 还能如何理解执行上下文

JavaScript 中的执行上下文可以看作是一个堆栈，每当一个新的执行上下文被创建时，它就被推入堆栈的顶部。当执行上下文执行完毕后，它就会从堆栈中弹出，控制权返回给上一个执行上下文。

执行上下文栈的底部是全局执行上下文，它是最先创建的执行上下文。当遇到函数调用时，会创建一个新的函数执行上下文，它被推入执行上下文栈的顶部。函数执行完毕后，该执行上下文就会从堆栈中弹出，控制权回到上一个执行上下文。

每个执行上下文都有自己的变量环境、词法环境和作用域链。其中，变量环境用于存储变量和函数声明，词法环境用于存储标识符和作用域链，作用域链用于查找变量和函数的定义。

在执行上下文中，this 关键字用于指向当前执行上下文所属的对象。在全局执行上下文中，this 指向全局对象；在函数执行上下文中，this 取决于函数的调用方式；在块级执行上下文中，this 指向 undefined；在模块执行上下文中，this 指向模块本身。


## 在执行上下文创建时，会经历什么

两个阶段：创建阶段和执行阶段。

1、创建阶段，会做如下操作：

1. 创建变量对象：变量对象包括函数的形参、函数声明和变量声明，初始化为 undefined。
2. 建立作用域链：将变量对象添加到作用域链的最前端，然后将外部函数的变量对象添加到作用域链中，直至全局执行上下文。
3. 确定 this 指向：在函数执行时，会根据函数的调用方式来确定 this 对象的指向。

2、执行阶段

执行代码，JavaScript 引擎会按照代码的顺序执行代码，具体执行的过程会根据代码的类型而有所不同，比如函数调用、变量赋值、条件语句等。

在执行过程中，会根据作用域链查找标识符的值，如果在当前执行上下文中找不到，则会继续向上查找，直至全局执行上下文。

## 执行上下文有哪些？

JavaScript 中有以下类型的执行上下文：

1、全局执行上下文：在代码开始执行时，首先创建全局执行上下文。全局执行上下文只有一个，它是默认的、最外层的执行上下文。在浏览器环境中，全局执行上下文的变量对象是 window 对象，在 Node.js 环境中则是 global 对象。

2、函数执行上下文：每当一个函数被调用时，都会创建一个新的函数执行上下文。函数执行上下文与全局执行上下文类似，但它们的变量对象和作用域链可能不同。

3、eval 函数执行上下文：当代码执行 eval 函数时，会创建一个新的 eval 函数执行上下文。eval 函数执行上下文也有自己的变量对象和作用域链。

4、块级执行上下文（Block Execution Context）：块级执行上下文是在 ES6 中引入的新特性，它是在代码块内部创建的执行上下文。代码块可以是包含在函数内部的一段代码，也可以是一个块级语句，比如 if、for、while 等。

5、模块执行上下文（Module Execution Context）：模块执行上下文是在 ES6 中引入的新特性，它是用于处理 JavaScript 模块的执行上下文。模块执行上下文与函数执行上下文有些类似，但是它具有一些独特的特性，比如模块级别的 this 对象和 import、export 语句等。

这几种执行上下文都有自己的变量环境、词法环境和作用域链，它们会影响到当前执行上下文中标识符的查找和访问。同时，每个执行上下文都有自己的 this 对象，用于指向当前执行上下文所属的对象。

## 浏览器的渲染原理

**一、浏览器的渲染步骤**

是指当用户访问网页时，浏览器如何将HTML、CSS、JavaScript等资源转换为用户可见的网页的过程。该过程通常可以分为以下几个步骤：

1、DNS服务器进行域名解析

DNS服务器会将输入的网址解析成对应的IP地址，然后我们就可以向这个IP地址发送HTTP请求，获取对应的静态资源。如果我们没有输入具体的文件名，服务器会默认返回index.html文件。

2、解析HTML文档：

当用户在浏览器地址栏中输入一个URL或者点击页面中的链接时，浏览器会向服务器发送请求，然后服务器会响应HTML文件。浏览器会先将HTML解析成DOM树（Document Object Model），解析过程中，浏览器会对HTML标签进行解析，将标签转化为DOM节点，并确定它们之间的关系。

3、解析CSS文档：

浏览器将CSS文档解析成CSSOM树（CSS Object Model），用于表示文档的样式信息。与DOM树类似，CSSOM树是由多个CSS规则构成的，每个规则又包含多个CSS属性。

4、构建渲染树：

浏览器将DOM树和CSSOM树合并，生成渲染树（Render Tree），渲染树只包含需要显示的节点和样式信息，而不包含不需要显示的节点，例如head或display:none的节点。

5、布局（Layout）：

浏览器根据渲染树的结构和样式信息，计算每个节点在屏幕上的位置和大小。

6、绘制（Painting）：

在计算布局之后，浏览器会将渲染树节点绘制到屏幕上。渲染树节点的绘制顺序是从上到下、从左到右。由于一个节点可能会遮挡其他节点，因此浏览器还需要对它们进行合成，以便正确显示。

7、重排和重绘：

如果浏览器需要更新渲染树的布局信息，例如当窗口大小改变时，它就需要进行重排和重绘。重排是指浏览器需要重新计算布局，而重绘是指浏览器只需要重新绘制节点而不需要重新计算布局。

在网页渲染过程中，回流和重绘是两个常见的性能瓶颈。

> 以上就是浏览器渲染页面的主要流程。当然，实际的情况可能会更加复杂，因为在这个过程中还涉及到JavaScript的执行、网络请求的优化等方面。但是，了解了这些基本流程之后，我们就可以更好地理解网页是如何呈现在我们眼前的了。

**二、其他补充**

除了上述步骤，还有一些其他的过程会影响网页的渲染效果，这里再补充一下：

1、JavaScript的执行：

在解析HTML和CSS的同时，浏览器内核也会执行JavaScript代码。如果JavaScript代码中有对DOM树或CSSOM树的修改，那么这些修改会影响到渲染树的生成和布局，进而影响到网页的渲染效果。

2、网络请求的优化：

为了提高网页的加载速度，浏览器内核会对网络请求进行优化。例如，它会使用HTTP缓存来避免重复下载已经缓存的资源，使用预加载来提前下载一些可能需要的资源等等。

3、GPU加速：

为了提高渲染速度，现代的浏览器内核会利用GPU来加速绘制。它们会将渲染树中的一些节点分配给GPU进行处理，从而减轻CPU的负担，提高渲染效率。

4、响应式设计：

现在的网页往往需要在不同的设备上呈现不同的样式，这就需要使用响应式设计。在这种设计中，网页的布局和样式会随着设备屏幕大小的改变而改变，从而适应不同的屏幕尺寸和分辨率。浏览器内核会根据当前设备的屏幕大小和分辨率来动态调整网页的渲染效果，从而让用户获得更好的使用体验。

> 总之，浏览器渲染网页的过程非常复杂，它需要同时处理HTML、CSS、JavaScript等多种语言和技术，还需要考虑网络请求、GPU加速、响应式设计等多个方面的因素。只有理解了这些基本概念和流程，我们才能更好地了解网页的渲染效果和性能表现，从而更好地进行网站开发和优化。

## 说出从输入URL到页面渲染完成的整个过程？

1. URL 输入：用户在浏览器地址栏输入URL，浏览器会对URL进行解析，判断输入的URL是否合法，若不合法，浏览器会进行自动纠错或者自动搜索。
2. DNS 解析：浏览器向 DNS 服务器查询输入的域名对应的IP地址，获取目标服务器的IP地址。
3. 建立 TCP 连接：浏览器与目标服务器通过TCP协议建立连接，包括TCP的三次握手，建立连接后，数据就可以在浏览器与服务器之间传输。
4. 发送 HTTP 请求：浏览器向服务器发送HTTP请求报文，请求服务器返回数据，HTTP请求可以是GET、POST等。
5. 服务器响应请求：服务器收到请求后，会根据请求返回HTTP响应报文，响应报文包含HTTP状态码、响应头以及响应体。
6. 浏览器解析渲染页面：浏览器根据HTML和CSS等资源构建DOM树和CSSOM树，再将DOM树和CSSOM树合并成渲染树，计算每个节点的位置和大小，最后渲染页面并呈现给用户。
7. HTTP请求结束，断开TCP连接：浏览器从服务器获取完所有资源后，关闭TCP连接，页面呈现完毕。

## 回流和重绘

一、回流（reflow）

元素的位置发生变动时发生重排，也叫回流。此时在关键渲染路径中的 Layout 阶段，计算每一个元素在设备视口内的确切位置和大小。当一个元素位置发生变化时，其父元素及其后边的元素位置都可能发生变化，代价极⾼。

指浏览器根据DOM树和样式计算每个节点的大小和位置信息，并在页面上布局这些节点的过程。

注意: 第一次确定节点的大小位置 称之为布局(Layout) 之后对节点大小位置改变后的重新计算称之为回流。

二、重绘（repaint）

指浏览器根据节点的样式重新绘制节点的过程。元素的样式发生变动，但是位置没有改变。此时在关键渲染路径中的 Paint 阶段，将渲染树中的每个节点转换成屏幕上的实际像素，这一步通常称为绘制或栅格化。

由于回流和重绘都需要重新计算和渲染节点，因此会消耗大量的CPU资源，降低网页性能。

**引起回流的情况:**

- DOM结构发生改变。当增删节点时，浏览器需要重新计算节点的位置和大小信息，因此会引起回流。
- 修改了节点的布局。例如，修改节点的宽度、高度、字体大小、边距等样式，都会引起节点的位置和大小信息发生改变，从而引起回流。
- 修改窗口的尺寸。当窗口尺寸发生改变时，所有节点的位置和大小信息都需要重新计算，因此会引起回流。
- 调用getComputedStyle获取位置信息。当我们获取某个节点的位置信息时，浏览器需要重新计算节点的位置和大小信息，因此会引起回流。

第一次绘制节点渲染到页面上称之为绘制(paint)，之后重新绘制称之为重绘

**引起重绘情况:**

- 修改背景色、颜色等不影响布局的样式。

回流一定会引起重绘，所以回流非常消耗性能！

**如何避免回流：**

由于回流的计算量比重绘大得多，因此我们应该尽量避免回流的发生。下面是一些避免回流的方法：

- 尽量一次性的修改样式。例如，我们可以将多个样式的修改放到一个CSS类中，然后使用JavaScript一次性地将这个CSS类添加到节点上，这样可以避免多次修改样式引起的多次回流。
- 避免频繁的操作DOM。因为DOM的增删会引起回流，所以我们应该尽量减少DOM的操作次数。
- 避免通过getComputedStyle获取尺寸位置信息等。因为获取节点的位置信息会引起回流，所以我们应该尽量避免频繁获取这些信息。
- 对于某些元素使用position:absolute/fixed。因为这些元素的位置不会影响其他元素的位置，所以对它们的修改不会引起回流。
- 使用CSS3的transform属性代替修改节点的位置信息。因为transform属性不会影响节点的位置信息，所以可以避免回流。

> 总之，减少回流和重绘对于提高网页性能非常重要。我们应该尽可能地减少DOM的操作次数，一次性地修改样式，避免频繁获取节点的位置信息等，以提高网页的响应速

## async和defer的使用以及区别？

浏览器在解析HTML文件构建DOM树的过程中，如果遇到`<script>`标签，会先停止构建DOM树，然后下载并执行JavaScript代码。如果JavaScript代码中涉及到对DOM节点的操作，而此时DOM树还没有构建完成，就会出现大量的回流和重绘，从而降低页面的性能。

使用`async`和`defer`属性可以解决这个问题。`async`属性用于异步加载脚本，它会在下载完成后立即执行脚本，不会阻塞HTML文件的解析和DOM树的构建。而`defer`属性也是用于异步加载脚本，但是它会等待HTML文件解析完成和DOM树构建完成后再执行脚本，确保脚本的执行顺序和文档的顺序一致。

1、defer

立即下载，延迟执行

```html
<script async src="script.js"></script>
```

defer属性也是用于异步加载脚本的属性，但它与async属性有一些不同。与async属性不同的是，使用defer属性加载的脚本会在下载完成后等待页面的渲染完成再执行，这样可以确保脚本的执行顺序和文档的顺序一致。

- 脚本的下载会与DOM树的构建同时进行
- 如果脚本提前下载好了，则会等到DOM树构建完成之后，在DOMContentLoaded事件之前执行defer中的代码
- 如果多个defer脚本存在依赖关系，可以通过在父级script标签中指定defer属性，并在其内部按照顺序引入多个子级脚本的方式来保证它们的执行顺序。
- 推荐放到head标签中，可以早解析
- 对于script默认的内容，会忽略
- 只对外部脚本文件生效

2、async

```html
<script defer src="script.js"></script>
```

立即下载，完成下载后执行

async属性是HTML5中新增的一个脚本属性，它用于告诉浏览器该脚本可以异步加载，不会阻塞页面的渲染和其他资源的加载。使用async属性加载的脚本会在下载完成后立即执行，而不需要等待其他资源的加载完成。

- 脚本的下载会与DOM树的构建同时进行
- 让一个脚本完全独立，脚本的解析运行于DOM的构建无关
- 多个async属性的脚本不保证运行顺序

使用async属性加载的脚本会在页面的渲染过程中执行，因此它们不能保证按照编写的顺序执行。如果多个async脚本之间存在依赖关系，那么就需要通过其他方式来确保它们正确的执行顺序。

**区别**

综上所述，async和defer属性的主要区别在于脚本的执行时机。使用async属性加载的脚本会在下载完成后立即执行，而使用defer属性加载的脚本会在下载完成后等待页面的渲染完成再执行。因此，如果脚本的执行不需要等待页面渲染完成，可以使用async属性来提高性能；如果需要保证脚本的执行顺序和文档的顺序一致，可以使用defer属性。

**注意**

需要注意的是，虽然async和defer属性可以提高页面的加载性能，但是它们并不适用于所有的脚本。例如，如果一个脚本需要在页面加载过程中对DOM进行大量的操作，那么使用async或defer属性可能会导致页面出现闪烁或渲染不完整的情况。在这种情况下，最好将脚本放到页面底部，以确保在DOM构建完成后再执行。

## 写出v8引擎执行代码的大致流程

V8引擎执行JavaScript代码的完整流程如下：

1、词法分析(Scanner)：

V8引擎将JavaScript源代码转换为一系列有意义的代码块，这些代码块被称为词法单元(Token)。

2、语法分析(Parser)：

V8引擎将词法单元分析成一个元素逐级嵌套的树形结构，称为抽象语法树(Abstract Syntax Tree，AST)。这个过程还包括预处理器(Pre-parser)的处理，例如函数声明和变量声明等。

3、解释器(Ignition)：

V8引擎将AST转换为字节码(Bytecode)，并使用解释器(Ignition)将字节码解释执行。同时，Ignition还会收集TurboFan优化需要的信息，例如函数调用的频率和参数类型。

4、编译器(TurboFan)：

如果Ignition发现某个函数被多次调用，则会将这个函数标记为热点函数(Hot Function)，并将其字节码交给编译器(TurboFan)进行编译。TurboFan会将字节码编译成CPU可以直接执行的机器码(Machine Code)，以提高代码的性能。

5、逆优化(Deoptimization)：

如果后续执行代码过程中，函数调用的参数类型发生了改变，TurboFan会将优化后的机器码逆向转换成字节码，交给解释器(Ignition)重新解释执行。这个过程称为逆优化(Deoptimization)。

6、垃圾回收：

V8引擎会定期检查内存中不再使用的对象，并进行垃圾回收(Garbage Collection)。这个过程可以避免内存泄漏(Memory Leak)和内存溢出(Memory Overflow)等问题，提高程序的稳定性。

7、其他优化：

V8引擎还有其他一些优化策略，例如内联(Inline)，函数去抖(Throttle)，以及快速属性访问等，这些优化策略可以进一步提高代码的性能。

> 总的来说，V8引擎通过将JavaScript代码转换为字节码并使用高效的编译器进行优化，以提高代码的性能。同时，垃圾回收和其他优化策略可以进一步提高代码的效率和稳定性。

## instanceof 和 typeof

`instanceof` 和 `typeof` 都是 JavaScript 中的运算符，用于判断一个值的类型。但是它们的用途和实现方式有所不同。

`typeof` 运算符用于检查一个值的类型，它会返回一个字符串，表示该值的数据类型。例如：

```javascript
typeof 123;  // "number"
typeof "hello";  // "string"
typeof true;  // "boolean"
typeof undefined;  // "undefined"
typeof null;  // "object"
typeof {};  // "object"
typeof [];  // "object"
typeof function(){};  // "function"
```

需要注意的是，`typeof null` 的结果是 `"object"`，这是一个历史遗留问题，因为在 JavaScript 的早期版本中，`null` 被错误地标记为了一个对象类型。

`instanceof` 运算符用于检查一个对象是否属于某个类或构造函数的实例。它需要两个操作数，左操作数是要检查的对象，右操作数是目标类或构造函数。例如：

```javascript
const arr = [1, 2, 3];
arr instanceof Array;  // true

function Person(name) {
  this.name = name;
}
const person = new Person("Alice");
person instanceof Person;  // true
```

需要注意的是，`instanceof` 运算符只能用于检查对象类型，无法用于检查基本数据类型（如数字、字符串、布尔值等）的类型。

## JavaScript的代码的执行流程

一、执行流程

在执行代码时，JavaScript 引擎会逐行解析代码，将其转换为可执行的指令。解析完成后，会按照以下顺序执行代码：

1、创建全局执行上下文(GEC)并将其推入执行上下文栈(ECS)的顶部。全局执行上下文是在代码执行前自动创建的，它包含全局变量、函数、this 等信息。

2、开始执行代码，遇到变量和函数声明时，在当前执行上下文的变量对象(VO)中创建变量并赋值为 undefined。函数会被存储为函数对象(Function Object)。

- 需要注意的是，变量对象（VO）在ES6之后被废弃，取而代之的是词法环境（Lexical Environment）。变量和函数声明会被存储在词法环境中。

3、遇到函数调用时，创建函数执行上下文(ExecutionContext)，并将其推入执行上下文栈的顶部。函数执行上下文包含该函数的参数、局部变量、this 等信息。

- 在创建函数执行上下文时，还会建立函数的私有作用域（Private Scope），用于存储函数内部的变量和函数声明。

4、执行函数体内的代码，解析和执行函数体内的语句。

- 在执行函数体内的代码时，JavaScript引擎会根据作用域链（Scope Chain）查找变量的值。作用域链是一个由词法环境组成的链表，用于解析变量的引用。

5、如果在函数中遇到了`return`语句，则返回值将被传递给调用方，并将函数执行上下文从执行上下文栈(ECS)中弹出。

- 如果在函数中没有遇到`return`语句，则函数会返回`undefined`。

6、如果函数执行完毕或者遇到了异常，则将函数执行上下文从执行上下文栈(ECS)中弹出。

- 如果在执行代码过程中发生了异常，JavaScript引擎会中止执行，并将异常信息抛出到执行上下文栈的顶层。

7、当代码执行完成后，全局执行上下文也将从执行上下文栈(ECS)中弹出。

二、其他

在执行过程中，每个执行上下文都有自己的变量对象(VO)和作用域链(scope chain)，用于存储变量和查找变量。作用域链的顶端指向当前执行上下文的变量对象(VO)，底端指向全局执行上下文的变量对象(VO)。

JavaScript引擎还会进行变量提升、作用域链查找、this指针的绑定等操作，以确保代码的正确执行。

JavaScript还支持异步编程模型，如事件驱动、回调函数等，这些异步操作会被添加到任务队列（task queue）中，并在合适的时机被执行。因此，JavaScript代码的执行流程并不是线性的，而是可以被打断和延迟的。

此外，JavaScript 中还有闭包(closure)的概念，即函数内部可以访问其外部函数的变量。在函数创建时，会将函数内部引用的外部变量存储在函数对象的作用域链中，当函数被调用时，可以通过作用域链访问这些外部变量。

## 创建全局执行上下文的步骤

一、步骤

1、创建全局对象：JavaScript 引擎会在执行全局代码前创建一个全局对象（global object）并将其保存在执行上下文栈的底部。

  - 在浏览器环境中，全局对象是 window 对象。
  - 在 Node.js 环境中，全局对象是 global 对象。

2、创建 this 对象：JavaScript 引擎会创建一个 this 对象，它指向全局对象。

  - 在浏览器环境中，this 对象指向 window 对象。
  - 在 Node.js 环境中，this 对象指向 global 对象。

3、创建作用域链：JavaScript 引擎会创建一个作用域链(scope chain)。

  - 全局执行上下文的作用域链只包含全局对象。
  - 作用域链是一个数组，用来存储当前执行上下文中的变量对象（variable     object）以及所有父级执行上下文的变量对象。
  - 全局执行上下文的作用域链只包含全局对象。

4、初始化变量：JavaScript 引擎会扫描代码，将所有变量的声明提升到作用域的顶部，但是变量的赋值不会被提升。

  - 在全局执行上下文中，JavaScript 引擎会初始化全局变量和函数，并将它们添加到全局对象和作用域链中。
  - `let` 和 `const` 声明的变量也会被提升，但是它们和 `var` 有所不同。与 `var` 不同的是，`let` 和 `const` 声明的变量被提升到了所在块级作用域的顶部，而不是函数作用域的顶部。

5、执行代码：最后，JavaScript 引擎会按照从上到下的顺序执行全局代码。

二、特殊操作

在创建全局执行上下文的过程中，JavaScript 引擎会执行一些特殊操作，例如：

1. 将变量和函数声明提升：在创建变量对象时，JavaScript 引擎会将所有变量和函数的声明提升到作用域的顶部。
2. 绑定 this 指针：在全局执行上下文中，this 指针会被绑定到全局对象。
3. 进行初始化：在创建变量对象后，JavaScript 引擎会为变量和函数分配内存空间，并将变量初始化为 undefined，函数则被初始化为函数对象。
4. 设置特殊变量值：JavaScript 引擎会为一些特殊变量设置初始值，例如 arguments等。
    a. `arguments` 是 JavaScript 中的一个特殊对象，它代表了函数调用时传入的参数列表。它类似于一个数组，但并不是一个真正的数组，它没有数组的方法，只有 `length` 属性和下标访问。

> 总之，创建全局执行上下文是在执行 JavaScript 代码前自动进行的，它会创建全局对象、作用域链、初始化变量等，并执行一些特殊操作，以确保代码的正确执行。

## 对GO/AO/VO的理解

一、Global Object（全局对象）：

- 全局对象是一个特殊的对象，通常在JavaScript环境的启动时就创建好了。
- 在浏览器中，全局对象是window对象；在Node.js中，全局对象是global对象。
- 全局对象是全局作用域的顶级对象，也是所有内置对象和函数的容器。
- 全局对象中包含了一些JavaScript语言内置的对象和函数，如Date、Array、String、Number、setTimeout、setInterval等等。开发者可以向全局对象添加自定义的属性和方法。
- 在解析JavaScript代码时，全局变量和函数声明会被添加到全局对象中，初始值为undefined。
- 在浏览器中，全局对象有一个window属性指向自己，在Node.js中没有这个属性。

二、Activation Object（活动对象）：

- 活动对象是在进入一个执行上下文（比如函数）时创建的对象，存储着该执行上下文中的arguments、对应函数的形参、局部变量、函数声明、和其它对象；
- 变量的初始值为undefined；
- 活动对象是当前执行上下文的变量对象（Variable Object），也是当前作用域的顶级对象。
- 活动对象在函数执行结束后会被销毁，其中的变量值也会被释放。

三、Variable Object（变量对象）：

- Variable Object 是当前执行上下文的数据对象，可以是全局对象或活动对象：
- 在函数执行期间，Variable Object就是Activation Object；
- 当全局代码被执行的时候，Variable Object就是Global Object ；
- 变量对象是在函数执行期间创建的，并包含当前函数中的所有变量和函数声明；其中，变量声明会被初始化为 undefined，而函数声明会被提升到变量对象的顶部。

## 作用域和作用域链的理解

一、作用域：

在 JavaScript 中，作用域是指变量、函数和对象的可访问范围。每个作用域都有一个相关联的变量对象（VO）。

JavaScript 采用词法作用域，即在编译阶段确定变量的作用域。一个变量的作用域可以是全局作用域，函数作用域，块级作用域。

- 全局作用域是指在程序的任何地方都能访问到的变量和函数。在浏览器中，全局作用域是 window 对象。

- 函数作用域是指变量和函数只能在函数内部访问。当函数执行完毕后，函数作用域中的变量和函数就会被销毁。

- 在ES6中，代码块、let、const等都会有属于自己的作用域。块级作用域是指在代码块中定义的变量和函数只能在该块内部访问。在 ES6 之前，JavaScript 没有块级作用域，但可以通过立即执行函数表达式 (IIFE) 来模拟块级作用域。


二、作用域链：

作用域链是由当前执行上下文的变量对象和其父级作用域的变量对象组成的链。当函数被创建时，JavaScript 引擎会在该函数对象中创建一个 [[Scope]] 属性。

作用域链（scope chain）是一个对象列表，当JavaScript执行代码时，用于变量标识符的求值；该作用域链是在函数定义时创建的，而不是在函数执行时创建的。它指向该函数的作用域链对象列表，将函数的活动对象添加到作用域链的顶部。这样，函数就可以访问其父级作用域中的变量和函数。

当 JavaScript 执行代码时，它会按照作用域链的顺序查找变量和函数。如果在当前作用域中找不到标识符，它会继续向上查找直到找到为止。如果在整个作用域链中都找不到标识符，就会抛出“未定义的”错误。

作用域链的顺序是由函数的定义位置决定的，而不是由函数的调用位置决定的。这意味着，如果一个函数被定义在另一个函数内部，它就可以访问外部函数的变量和函数，但外部函数不能访问内部函数的变量和函数。

三、作用域链的作用：

1、变量查找 

作用域链的主要作用是解析变量的作用域和访问权限，当访问一个变量时，JavaScript引擎会沿着作用域链一级一级地向上查找变量，直到找到变量的定义位置或者到达全局作用域，如果一直找不到，则抛出一个ReferenceError异常。

2、变量保护 

作用域链的另一个作用是保护变量，变量在作用域内是私有的，外部无法访问。通过作用域链，函数可以访问自身作用域内的变量，但无法访问其他函数作用域内的变量，从而保护了变量的安全性。

3、闭包实现 

作用域链还被广泛应用于JavaScript中的闭包（Closure）实现。在JavaScript中，函数内部定义的变量可以被外部函数访问，这种能力被称为“闭包”。通过作用域链机制，JavaScript引擎可以在函数返回后仍然保留函数内部的变量，使其在函数外部继续访问。

> 总结
>
> - 当进入到一个执行上下文时，执行上下文会关联一个作用域链。
> - 通常作用域链在解析时就被确定，作用域链与函数的定义位置有关，与它的调用位置无关

# 📁 JavaScript_内存管理、闭包

## V8引擎的内存管理以及垃圾回收器

V8引擎是一款用于执行JavaScript代码的引擎，主要用于Google Chrome浏览器和Node.js等应用程序中。V8引擎具有先进的内存管理和垃圾回收机制，以提高JavaScript代码的性能和稳定性。

### 内存管理

V8引擎使用的是动态内存管理，它会在运行时根据需要动态分配和释放内存。在V8中，内存被分为两个主要部分：堆和栈。

1、堆是用于存储JavaScript对象的一块内存区域。

在V8中，堆的大小是动态的，并且可以根据需要自动增长或收缩。

V8引擎将堆分为两个部分：新生代和老年代。新生代用于存储生存时间较短的对象，而老年代用于存储生存时间较长的对象。

2、栈是用于存储函数调用和变量等数据的一块内存区域。

V8引擎使用栈来管理函数调用和变量分配。栈的大小是固定的，通常比堆小得多。

每个函数调用都会在栈上创建一个新的栈帧，并在函数返回时删除该栈帧。栈帧中存储了函数参数、局部变量和返回地址等信息。

### 垃圾回收(GC)

因为内存大小是有限的，所以在内存不需要的时候，需要进行释放，用于腾出空间

GC对于内存管理有着对应的算法

### 常见的算法

1、引用计数(Reference Count)

- 当一个对象有引用指向它时，对应的引用计数+1
- 当没有对象指向它时，则为0，此时进行回收
- 但是有一个严重的问题 - 会产生循环引用

2、标记清除(Mark-Sweep)

核心思路: 可达性

有一个根对象，从该对象出发，开始引用到所用到的对象，对于根对象没有引用到的对象，认为是不可用的对象。

对于不可用的对象，则进行回收，该算法有效的解决了循环引用的问题，目前V8引擎采用的就是该算法。

### V8引擎优化

在采用标记清除的过程中也引用了其他的算法

1、标记整理

和标记清除相似，不同的是回收时，会将保留下来的存储对象整合到连续的内存空间，避免内存碎片化

2、分代收集(Generational Collection)

将堆分为两个部分：新生代和老生代。

a、新生代

存储的是年轻的、短寿的对象，而老生代中存储的是经过多次垃圾回收后仍然存在的对象。

在新生代中，V8使用了一种称为Scavenge的垃圾回收器。Scavenge垃圾回收器使用了一种称为“复制”算法的技术，将新生代分为两个区域：From空间和To空间。当From空间满了之后，V8将会执行垃圾回收，并将存活的对象复制到To空间中。然后，V8会将From空间和To空间交换，使得To空间成为新的From空间，重新开始垃圾回收。

b、老生代

V8使用了一种称为标记清除（Mark-Sweep）垃圾回收器的算法。

Mark-Sweep垃圾回收器会首先标记所有存活的对象，然后清除所有未被标记的对象。这种垃圾回收算法可能会导致内存碎片的问题，因此V8还使用了一种称为“压缩”算法的技术来解决这个问题。

在压缩算法中，V8会将存活的对象移动到堆的一端，然后释放堆的另一端的空间，从而解决了内存碎片的问题。

3、增量收集(Increment Collection)

如果有许多对象，并且我们试图一次遍历并标记整个对象集，则可能需要一些时间，并在执行过程中带来明显的延迟。因此，引擎将现有的整个对象集拆分为多个部分，然后将这些部分逐一清除。这样就会有很多小型的垃圾收集，而不是一个大型的。这需要它们之间有额外的标记来追踪变化，但是这样会带来许多微小的延迟而不是一个大的延迟。

4、闲时收集(IdIe-time Collection)

垃圾收集器只会在 CPU 空闲时尝试运行，以减少可能对代码执行的影响。

[https://jayconrod.com/posts/55/a-tour-of-v8-garbage-collection](https://jayconrod.com/posts/55/a-tour-of-v8-garbage-collection)

<https://v8.dev/>

## 什么是闭包？谈谈你的了解

> JS闭包指的是**一个函数能够访问并操作其外部作用域的变量**，即使这个函数在外部作用域已经执行完毕，这些变量依然可以被访问和修改。
>
> 也就是延长了其生命周期

**闭包的实现方式是在一个函数内部定义另一个函数，并将其作为返回值返回。这个内部函数可以访问外部函数的局部变量，而外部函数的局部变量则被保存在返回的内部函数中，形成了一个闭包。**

```js
function outerFunction() {    
  var privateMethod = function() {    
    console.log("This is a private method");    
  };  
  
  return privateMethod;    
}  
  
const privateMethod = outerFunction();    
privateMethod(); // 输出 "This is a private method"

```

> 从代码我们可以看出，闭包的一种形式就是很简单的函数里面在套一个函数，调用上层函数获取下面的函数的东西

### 闭包的高级操作

**闭包实现高并发**

```js
// 在函数内部创建一个新的闭包，用于存储线程对象
var thread = null;
function addNumbers(a, b, callback) {  
    function worker() {  
var result = a + b; callback(result); 
    }  
    if (!thread) { 
thread = new Thread(worker); 
thread.start(); 
    } 
    else thread.run(worker); 
}
// 在函数外部创建一个新的线程，并使用闭包创建一个新的线程对象
addNumbers(1, 1, function(result) { 
console.log(result); 
});

```

> 在这个例子中，**addNumbers 函数返回了一个闭包**，该闭包在内部创建了一个**新线程**，该线程执行的任务是加法运算。新线程执行的任务是**在闭包内部完成**的，因此可以**避免竞争条件**。最后，闭包返回的结果被返回到调用它的上下文中，并通过线程对象被其他线程访问。

### 闭包的作用

实现私有变量和方法，以及实现高阶函数等功能。但是过度使用闭包也可能导致内存泄漏和性能问题，因此需要慎重使用。

## 如何理解闭包？闭包到底是什么?

广义上讲，JavaScript中的所有函数都是闭包，因为它们都有一个`[[Scope]]`属性，指向它们的作用域链。这个作用域链包括当前函数的活动对象和所有父级函数的变量对象。

狭义上讲，只有当函数访问了外层作用域中的变量或参数时，它才被称为闭包。这是因为只有在这种情况下，JavaScript引擎才会创建一个闭包来保存外部变量的引用。

**闭包的组成**

闭包是由函数和它能够访问到的外部变量的引用组成的。

实现上，闭包是一个对象，它包含了一个函数和一个环境（一个对象，其中包含了该函数能够访问的所有变量和参数）。

闭包是由于函数嵌套而产生的一种特殊的函数作用域，内部函数可以访问外部函数中的变量和参数，因为它们在同一作用域链上。

当内部函数访问外部函数中的变量或参数时，JavaScript引擎会在内存中创建一个闭包，以保存这些变量和参数的引用。这个闭包会一直存在，直到没有任何引用指向它，才会被垃圾回收机制清理掉。

闭包可以用来实现许多有用的功能，如创建私有变量和方法，保存函数状态，避免变量污染等。但是，使用不当可能会导致内存泄漏和性能问题，因此需要谨慎使用。

```js
function createAdder(count) {
  function adder(num) {
    return count + num
  }
  return adder
}
var adder5 = createAdder(5)
adder5(100)
adder5(55)
adder5(12)
```

> 这段代码定义了一个名为createAdder的函数，它接受一个参数count，并返回一个名为adder的函数。adder函数接受一个参数num，并将count和num相加后返回结果。
> 接下来，代码创建了一个名为adder5的变量，它被赋值为createAdder(5)的返回值，也就是一个具有闭包的adder函数，其中count被绑定为5。
> 最后，代码调用adder5三次，每次传入不同的参数。由于adder函数具有闭包，它能够记住之前的count值，并将每次调用的num参数加上count返回。
> 因此，第一次调用adder5(100)会返回105，第二次调用adder5(55)会返回60，第三次调用adder5(12)会返回17。

## 闭包是如何产生的？

由于在JavaScript中，函数是我们的头等公民，因此函数自身就可以作为另一个函数的参数来使用。

当一个函数返回另一个函数时，内部函数就可以访问外部函数中的变量和参数，这种函数嵌套的特性就是闭包。

简单来说，当内部函数引用了外部函数的变量时，这个变量就会被保存在一个特殊的内部数据结构中，该结构被称为闭包。当外部函数执行完毕后，其作用域会被销毁，但是闭包中的变量仍然会存在于内存中，因为内部函数引用了它们。这样，即使外部函数已经执行完毕，内部函数仍然可以访问这些变量。

闭包可以用来创建私有变量和函数，以及实现函数式编程中的柯里化、惰性求值等技术。但是，使用不当可能会导致内存泄漏等问题，因为闭包会持有外部变量的引用，这些变量可能会占用大量内存。因此，在使用闭包时需要注意内存管理，及时释放不再需要的变量。

## 闭包、原型和作用域

**问题：闭包、原型和作用域等 JavaScript 基础知识在您的项目中发挥了什么作用？请结合实际项目案例，谈谈您如何运用这些知识解决实际问题。**

我曾经参与过一个电商网站的开发，其中有一个功能是实现购物车的增删改查。在实现这个功能时，我使用了闭包、原型和作用域等 JavaScript 知识。

首先，我使用了闭包来实现购物车数据的存储。在用户加入商品到购物车时，我使用了一个立即执行函数来创建一个闭包，将商品信息保存在闭包中的数组中。这样，即使用户在浏览网站的其他页面时，购物车数据也不会丢失。

```js
var shoppingCart = (function() {
  var cartItems = [];

  return {
    addItem: function(item) {
      cartItems.push(item);
    },
    removeItem: function(index) {
      cartItems.splice(index, 1);
    },
    getItems: function() {
      return cartItems;
    }
  }
})();
```

其次，我使用原型来封装购物车操作的方法，以便在代码中复用。在上面的代码中，我们可以看到 `addItem`、`removeItem` 和 `getItems` 这些方法都被定义在对象上，并且使用了闭包来访问 `cartItems` 数组。这些方法可以在代码的其他部分中被调用，以实现购物车的增删改查操作。

最后，我使用了作用域来避免命名冲突和提高代码的可读性。在上面的代码中，我使用了立即执行函数来创建了一个独立的作用域，将购物车的实现细节隐藏在这个作用域中。这样，可以避免全局变量的污染，同时提高了代码的可读性和可维护性。

综上所述，闭包、原型和作用域等 JavaScript 基础知识在我的项目中发挥了重要作用。通过使用这些知识，我能够实现购物车功能，并提高了代码的可读性、可维护性和性能。

## 闭包、原型和作用域（二）

一、闭包

闭包是 JavaScript 中一种非常重要的概念，它可以用于创建私有变量和函数。在实际项目中，闭包常常被用于封装代码，避免全局变量的污染和命名冲突。

例如，我们可以使用闭包创建一个计数器函数，每次调用这个函数都会返回一个新的计数器：

```js
function createCounter() {
  let count = 0;
  return function() {
    count++;
    console.log(count);
  };
}

const counter1 = createCounter();
counter1(); // 1
counter1(); // 2

const counter2 = createCounter();
counter2(); // 1
```

在这个示例中，**createCounter** 函数返回一个闭包，它包含一个私有变量 **count** 和一个内部函数，每次调用内部函数都会增加 **count** 的值并输出结果。通过使用闭包，我们可以创建多个计数器实例，每个实例都有自己的私有变量 **count**，互相独立。

二、原型

原型是 JavaScript 中一种面向对象编程的基本机制，它可以用于共享代码和属性。在实际项目中，原型常常被用于创建可复用的对象和方法，以避免代码重复。

例如，我们可以使用原型创建一个可复用的方法，用于格式化日期：

```js
Date.prototype.format = function(format) {
	// 实现日期格式化逻辑
}

const date = new Date();
console.log(date.format('yyyy-MM-dd')); // 输出格式化后的日期
```

在这个示例中，我们通过修改 **Date** 对象的原型，添加了一个 **format** 方法，用于格式化日期。通过使用原型，我们可以在所有 **Date** 实例中共享这个方法，避免了代码的重复和冗余。

三、作用域

作用域是 JavaScript 中管理变量和函数可访问性的机制，它可以用于控制代码的可见性和安全性。在实际项目中，作用域常常被用于封装代码和避免变量的命名冲突。

例如，我们可以使用作用域创建一个模块，封装代码并避免命名冲突：

```js
// 模块1
(function (module) {
  let count = 0;

  module.increment = function () {
    count++;
    console.log(count);
  };
})((window.module1 = {}));

// 模块2
(function (module) {
  let count = 0;

  module.increment = function () {
    count++;
    console.log(count);
  };
})((window.module2 = {}));

// 调用模块1和模块2
module1.increment(); // 1
module2.increment(); // 1
```

在这个示例中，我们使用自执行函数创建了两个模块 **module1** 和 **module2**，每个模块都有一个私有变量 **count** 和一个公开方法 **increment**，用于增加 **count** 的值并输出结果。通过使用作用域，我们可以封装模块中的变量和方法，避免了变量的命名冲突。

总的来说，闭包、原型和作用域等 JavaScript 基础知识在实际项目中发挥了重要作用，它们可以用于封装代码、避免命名冲突、共享属性和方法等，帮助我们编写更加简洁、高效和可维护的代码。

## 什么是内存泄漏

内存泄漏是指程序在申请内存后，无法释放已经申请的内存空间，导致系统的有效内存空间逐渐减少，最终耗尽系统的所有内存资源，导致程序崩溃。

JavaScript 中的内存泄漏通常是指在代码中错误地创建了不再需要的对象，但却未能及时地将其从内存中删除。这些对象通常会被存储在变量、数组、缓存中，或者被添加到 DOM 中等等。

**一些常见的 JavaScript 内存泄漏的情形包括：**

1、意外的全局变量

如果没有使用 var、let 或 const 关键字，或者在全局作用域中定义了变量或对象，那么它将成为全局对象的属性，从而无法被垃圾回收。

2、未清除的定时器或回调函数

如果未及时清除定时器或回调函数，那么它们会一直存在于内存中，并阻止与之相关的对象被垃圾回收。

3、闭包

由于闭包会保留其外部函数的作用域，所以可能会阻止垃圾回收机制回收这些对象。

4、DOM 节点

如果使用了大量的 DOM 节点，并且未正确地清除或删除它们，那么它们会一直占用内存，直到页面被卸载。

5、循环引用：

当两个或多个对象相互引用时，如果它们之间的引用关系没有被正确地打破，就会导致内存泄漏。

**解决内存泄漏的方法包括**：

使用变量和对象时，要确保其在不再需要时能够被垃圾回收；及时清除不需要的定时器和回调函数；避免使用不必要的闭包；在页面卸载前，确保删除所有不再需要的 DOM 节点。

## 在 Web 开发中，IE 浏览器常见的内存泄漏问题主要有

在 Web 开发中，IE 浏览器常见的内存泄漏问题主要有以下几种：

1.循环引用：在 IE 浏览器中，如果一个对象被其他对象引用，而这个对象又引用了其他对象，形成了一个循环引用的结构，这时候即使没有其他地方再引用这些对象，它们也无法被 JavaScript 引擎自动回收，会导致内存泄漏。

2.DOM 清理不彻底：在 IE 浏览器中，如果没有正确清理 DOM 元素，或者使用 innerHTML 来替换 DOM 元素，可能会导致元素与事件的绑定无法释放，从而导致内存泄漏。

3.XMLHttpRequest 对象未释放：在 IE 浏览器中，如果没有正确释放 XMLHttpRequest 对象，会导致这些对象一直驻留在内存中，从而导致内存泄漏。

4.大量字符串操作：在 IE 浏览器中，如果使用字符串拼接的方式来操作大量数据，会导致内存占用过高，从而导致内存泄漏。

需要注意的是，IE 浏览器对 JavaScript 的内存管理实现方式与现代浏览器存在巨大差异，因此在编写兼容 IE 的代码时，需要特别注意内存泄漏问题。但随着 IE 浏览器的逐渐淘汰，这些问题的影响也会逐渐减小。

## 闭包为什么会产生内存泄露如何解决

**产生原因**

闭包会使外部函数中的变量，在函数执行结束后仍然存在于内存中，因为闭包会持有对外部函数中变量的引用，即使外部函数已经执行完毕，这些变量仍然存在于内存中，直到闭包被销毁。

例如，如果一个闭包被赋值给一个全局变量或者被保存在一个数组中，并且这个闭包中引用了一些大型的对象或者DOM节点，那么这些对象或节点可能不会被及时释放，导致内存泄漏。

另外，如果一个闭包中引用了一些循环变量，而这些循环变量在外部函数执行结束后还会被使用，那么闭包中引用的这些变量也不会被释放，导致内存泄漏。

**导致结果**

如果闭包创建的变量占用大量内存，这可能会导致内存占用过高，影响页面性能。

如果闭包被错误地使用，例如在循环中创建多个闭包，可能会导致内存泄漏。

虽然闭包可能会导致内存泄漏，但使用闭包仍然是  JavaScript 中非常有用的编程模式。只要注意使用和管理闭包，就可以避免这个问题。  

**解决闭包导致的内存泄漏**

1、避免创建不必要的闭包

在编写代码时，应尽量避免创建不必要的闭包。例如，在循环中创建闭包可能会导致性能问题和内存泄漏。可以将循环中的闭包提取到循环外部，避免重复创建闭包。

2、显示释放引用

在使用完闭包后，可以显式地将其引用置为null，以便垃圾回收机制回收它所占用的内存。

3、使用 let 和 const

使用 let 和 const 声明变量，这样变量的作用域只在块级内，当块级结束后，变量就会被垃圾回收机制清除。

4、使用WeakMap

WeakMap 是一种特殊的 Map，它可以自动删除无用的键值对，因此可以用来解决闭包导致的内存泄漏问题。在使用 WeakMap 时，可以将需要引用的外部变量存储在 WeakMap 中，这样当外部变量不再需要时，WeakMap 会自动将其删除。

5、避免循环引用

如果闭包中引用了外部对象，并且外部对象也引用了闭包，就会出现循环引用。这种情况下，垃圾回收机制无法回收这些对象，从而导致内存泄漏。可以通过避免循环引用的方式解决这个问题，例如使用事件代理来处理事件处理程序，避免在事件处理程序中创建闭包。

6、及时释放事件监听器

如果在闭包中添加了事件监听器，当元素被移除时，应该及时将事件监听器移除，避免闭包持续存在导致内存泄漏。

> 综上所述，要解决闭包导致的内存泄漏问题，需要在编写代码时注意避免创建不必要的闭包，显式释放引用，使用  WeakMap，避免循环引用等方法。  

## 闭包的应用场景（一）

闭包在 JavaScript 中有很多实际的应用场景，可以帮助我们更好地封装、组织和管理代码，提高程序的可维护性和可扩展性。以下是一些常见的应用场景：

1、封装变量和方法：

闭包可以用来封装私有变量和方法，从而隐藏实现细节，避免外部访问和修改。

```js
function Counter() {
  var count = 0;
  
  function increase() {
    count++;
    console.log(count);
  }
  
  function decrease() {
    count--;
    console.log(count);
  }
  
  return {
    increase: increase,
    decrease: decrease
  }
}

var counter1 = Counter();
counter1.increase(); // 输出 1
counter1.increase(); // 输出 2
counter1.decrease(); // 输出 1

var counter2 = Counter();
counter2.increase(); // 输出 1
counter2.increase(); // 输出 2
counter2.increase(); // 输出 3
```

> 在这个示例中，我们定义了一个名为 Counter 的函数，它返回一个对象，包含了两个方法 increase 和 decrease。这些方法都可以访问和修改 count 变量，但是 count 变量是被封装在 Counter 函数的作用域内部，外部无法访问和修改，从而实现了变量的私有化。通过这种方式，我们可以避免外部直接修改 count 变量，保证了代码的安全性和可靠性。

2、模块化开发：

通过闭包可以实现模块化开发，将一些相关的功能封装在一个闭包内部，从而避免命名冲突和全局变量的污染。

```js
var myModule = (function() {
  var privateVar = 0;
  
  function privateMethod() {
    console.log("private method");
  }
  
  return {
    publicVar: "public",
    publicMethod: function() {
      privateVar++;
      console.log(privateVar);
    }
  };
})();

myModule.publicMethod(); // 输出 1
myModule.publicMethod(); // 输出 2
console.log(myModule.publicVar); // 输出 "public"
```

> 在这个示例中，我们使用立即执行函数来创建一个模块化的对象，该对象包含了两个方法 publicMethod 和 publicVar，外部可以通过访问这些方法和属性来获取模块的功能。在模块内部，我们定义了一个私有变量和私有方法，外部无法访问和修改，从而避免了命名冲突和全局变量的污染。

3、实现回调函数：

闭包可以用来实现回调函数，将一个函数作为参数传递给另一个函数，并在内部使用闭包来保存上下文，从而实现异步编程。

```js
function delay(fn, time) {
  return function() {
    var args = arguments;
    setTimeout(function() {
      fn.apply(null, args);
    }, time);
  }
}

function sayHello(name) {
  console.log("Hello, " + name);
}

var delayedSayHello = delay(sayHello, 1000);
delayedSayHello("John"); // 延迟 1 秒后输出 "Hello, John"
```

> 在这个示例中，我们定义了一个 delay 函数，它接受一个函数和一个时间参数，返回一个函数。该函数使用 setTimeout 函数来延迟执行传入的函数，并将传入的参数传递给该函数。这样，我们就可以使用闭包来保存上下文和参数，实现了回调函数的功能。

4、缓存数据：

通过闭包可以实现缓存数据，避免频繁的计算和重复的网络请求，提高程序的性能。

```js
function memoize(fn) {
  var cache = {};
  return function() {
    var args = JSON.stringify(arguments);
    if (cache[args]) {
      return cache[args];
    }
    var result = fn.apply(null, arguments);
    cache[args] = result;
    return result;
  }
}

function fibonacci(n) {
  if (n < 2) {
    return n;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}

var memoizedFibonacci = memoize(fibonacci);
console.log(memoizedFibonacci(10)); // 输出 55
console.log(memoizedFibonacci(10)); // 输出 55（从缓存中获取）
```

> 在这个示例中，我们定义了一个 memoize 函数，它接受一个函数作为参数，并返回一个新的函数。该函数使用一个对象 cache 来缓存函数的计算结果，如果参数已经在缓存中，则直接返回缓存中的结果，否则计算函数的结果，并将结果保存到缓存中。

5、实现迭代器：

闭包可以用来实现迭代器，通过保存状态和数据结构的引用，实现对集合元素的遍历和访问。

```js
function makeIterator(array) {
  var index = 0;
  return function() {
    if (index >= array.length) {
      return { done: true };
    }
    return {
      value: array[index++],
      done: false
    };
  }
}

var array = [1, 2, 3];
var iterator = makeIterator(array);
console.log(iterator.next()); // 输出 { value: 1, done: false }
console.log(iterator.next()); // 输出 { value: 2, done: false }
console.log(iterator.next()); // 输出 { value: 3, done: false }
console.log(iterator.next()); // 输出 { done: true }
```

> 在这个示例中，我们定义了一个 makeIterator 函数，它接受一个数组作为参数，并返回一个新的函数。该函数使用闭包来保存数组的下标 index，每次调用返回数组中的下一个元素，直到遍历完所有元素，返回一个 done 属性表示遍历结束。

6、实现单例模式：

闭包可以用来实现单例模式，从而保证一个类只有一个实例，避免资源浪费和状态不一致的问题。

```js
var Singleton = (function() {
  var instance;
  function init() {
    return {
      publicMethod: function() {
        console.log("public method");
      },
      publicVar: "public"
    };
  }
  return {
    getInstance: function() {
      if (!instance) {
        instance = init();
      }
      return instance;
    }
  };
})();

var singleton1 = Singleton.getInstance();
var singleton2 = Singleton.getInstance();
console.log(singleton1 === singleton2); // 输出 true
```

> 在这个示例中，我们使用立即执行函数来创建一个单例模式，该模式包含一个 getInstance 方法，用来获取单例对象。在模式内部，我们使用一个变量 instance 来保存单例对象，当第一次调用 getInstance 方法时，如果 instance 不存在，则创建一个新的实例，否则返回已有的实例。这样，我们就可以保证一个类只有一个实例。

## 闭包的应用场景（二）

闭包是JavaScript中一种非常重要的概念，它可以将函数内部的数据与外部隔离开来，同时又可以让这些数据在函数外部被访问和使用。闭包的应用场景非常广泛，以下是几个常见的应用场景和相应的代码案例：

1、防抖

防抖是指在一定时间内，如果有连续的事件触发，则只执行最后一次，以达到减少频繁操作的效果。防抖的代码实现通常使用闭包来保存定时器的状态。

```js
function debounce(func, delay) {
  let timer = null;
  return function() {
    let context = this;
    let args = arguments;
    clearTimeout(timer);
    timer = setTimeout(function() {
      func.apply(context, args);
    }, delay);
  };
}
```

2、节流

节流是指在一定时间内，如果有连续的事件触发，则只执行一次，以达到减少频繁操作的效果。节流的代码实现通常使用闭包来保存时间戳的状态。

```js
function throttle(func, delay) {
  let timer = null;
  let lastTime = 0;
  return function() {
    let context = this;
    let args = arguments;
    let now = Date.now();
    if (now - lastTime >= delay) {
      func.apply(context, args);
      lastTime = now;
    }
  };
}
```

3、立即执行函数

立即执行函数是指在定义后立即执行的函数，常用于定义模块等场景，可以防止变量污染全局作用域。立即执行函数的代码实现通常使用闭包来将函数作为一个表达式进行执行。

```js
let result = (function() {
  let x = 0;
  return x + 1;
})();
console.log(result); // 1
```

4、组合函数

组合函数是指将多个函数组合起来，形成一个新的函数，以达到代码复用的效果。组合函数的代码实现通常使用闭包来保存函数链。

```js
function compose(...funcs) {
  return function(arg) {
    return funcs.reduceRight((acc, func) => func(acc), arg);
  };
}

function add(x) {
  return x + 1;
}

function mul(x) {
  return x * 2;
}

let result = compose(add, mul)(1);
console.log(result); // 3
```

以上是闭包在常见应用场景中的代码案例，它们都利用了闭包的特性来实现相应的功能。

# 📁 函数、对象增强

## 理解纯函数以及编写自己的纯函数

一、什么是纯函数？

在函数式编程中，纯函数是一种没有副作用、并且输出只由输入决定的函数。这意味着纯函数不会修改传入的参数，也不会改变全局变量或发起 I/O 操作，而且相同的输入始终会得到相同的输出。

二、纯函数的特点

- 确定的输入一定会有确定的输出（外部环境的任何变化不会影响函数内部的操作产生的结果）
- 纯函数的执行不会产生副作用。（函数内部的操作也不会对函数外部产生任何影响）

三、纯函数的优点？

纯函数的好处在于它们非常容易测试和理解，并且可以被组合使用以构建更复杂的程序。由于纯函数不会修改状态，因此它们对并发执行和多线程执行是安全的，这是一些并行和分布式计算模型所必需的。

四、纯函数示例

纯函数在react和redux中应用比较多。

下面是一个简单的纯函数示例：

```js
function add(a, b) {
  return a + b;
}
```

这个函数不会修改传入的参数，也不会访问全局变量或发起 I/O 操作，因此它是一个纯函数。

**编写自己的纯函数时，可以考虑以下几点：**

1. 不要修改传入的参数。纯函数应该只依赖于它的输入，而不应该改变它的输入。如果需要修改参数的值，请使用副本。
2. 避免访问全局变量。纯函数应该只依赖于它的输入，而==不应该依赖于全局变量==。如果需要访问全局变量，请将它们作为参数传递给函数。
3. 避免发起 I/O 操作。纯函数应该只关心输入和输出，而不应该对外部环境产生任何影响。如果需要进行 I/O 操作，请将它们封装到单独的函数中。

**下面是一个更复杂的纯函数示例：**

```js
function getDiscountedPrices(prices, discount) {
  return prices.map(function(price) {
    return price * (1 - discount);
  });
}
```

这个函数不会修改传入的参数（即 prices 和 discount），也不会访问全局变量或发起 I/O 操作。它只是根据输入计算输出，并且始终会返回相同的输出，因此它是一个纯函数。

```js
//一般的数学方法可以写成纯函数,例如相加
function sum(...args) {
  var result = args.reduce((perValue, item) => {
    return preValue + item
  }, 0)
  return result
}
```

> 总之，纯函数是一种非常有用的函数式编程范式，可以帮助我们构建更清晰、更可靠和更易于测试的程序。在编写自己的纯函数时，应该遵循一些基本原则，以确保函数的纯洁性和可重用性。

## 什么是副作用

在计算机科学中，副作用（side effect）指的是在执行一个函数或操作时，除了返回一个值之外，还对程序的状态或环境产生了可观察的变化。换句话说，副作用是函数或操作对于函数外部环境产生的影响。

常见的副作用包括但不限于：

1. 修改全局变量或静态变量：函数修改了在函数外部定义的全局变量或静态变量的值。

2. 修改传入的参数：函数修改了作为参数传递的变量的值。

3. 修改对象属性或数组元素：函数修改了对象的属性或数组的元素的值。

4. I/O 操作：函数进行了文件读写、网络请求、数据库操作等 I/O 操作。

5. 异常抛出：函数抛出了异常，改变了正常的程序执行流程。

副作用可能会对程序的可靠性、可维护性和可测试性产生影响。由于副作用的存在，同样的输入可能会导致不同的输出，使得程序的行为变得不可预测。此外，副作用也增加了程序的复杂性，使得代码的理解和调试更加困难。

函数式编程中的一个重要原则就是尽可能地减少副作用，使得函数的行为只依赖于输入，输出仅仅取决于输入参数，而不依赖于外部状态或环境。这样可以使代码更加可靠、可复用和易于测试。纯函数（Pure Function）是指没有副作用的函数，对于相同的输入始终返回相同的输出，不依赖于外部状态。

在编写函数时，我们应该注意副作用的产生，尽量将副作用限制在必要的范围内，遵循函数的单一职责原则，减少副作用对系统的影响，提高代码的可维护性和可测试性。

## 理解函数柯里化以及说出柯里化的作用

函数柯里化是一种将具有多个参数的函数转化为一系列接受单个参数的函数的技术。柯里化过程中，函数首先接受一个参数，并返回一个新函数，该新函数接受下一个参数，依次类推，直到所有参数都被传递完毕，最终返回最终的结果。

```js
function add(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    }
  }
}

const sum = add(1)(2)(3);
console.log(sum); // 6
```

**柯里化的作用**

1、单一职责：

每一个函数只用处理传入的单个参数，每个函数的职责单一而且确定

2、参数复用：

柯里化使得函数可以更方便地复用参数。例如，在上面的示例中，我们可以使用 add(1) 创建一个新的 add 函数，它将一直使用 1 作为第一个参数，而不需要每次都传递它。

3、延迟执行：

柯里化可以将一个多参数函数转换为一系列单参数函数，这使得函数的执行可以被延迟到后面的某个时刻。这在一些特定的应用场景中非常有用，例如需要构建高效的、惰性的函数链。

4、函数组合：

柯里化可以将多个函数组合在一起，以实现更复杂的行为。例如，在函数式编程中，我们可以使用柯里化来将一些简单的函数组合成一个更复杂的函数，以实现复杂的行为逻辑。

## 单一职责原则

（Single Responsibility Principle, SRP）是指每个对象或函数都应该只负责完成一个单一的职责或功能，而不应该有多个职责或功能，这样可以提高代码的可读性、可维护性和可测试性。

在函数编程中，单一职责原则通常表现为每个函数只处理单个参数或数据类型，且函数的功能单一而且明确。这种思想也被称为“一次只做一件事”的原则。

**实现**

具体来说，单一职责原则可以通过以下几个方面来实现：

1. 函数的功能要单一：每个函数应该只完成一个单一的功能，而不应该处理过多的逻辑。
2. 函数的参数要简单：每个函数应该只接收一个或少量的简单参数，而不应该接收过多的参数或复杂的数据结构。
3. 函数的命名要准确：每个函数的命名应该准确地反映出它的功能和职责，以方便代码的理解和维护。
4. 函数的复用性要高：每个函数应该尽可能地被设计成可复用的，以减少代码冗余和提高代码的可维护性。

**总结**

总之，单一职责原则是函数式编程中非常重要的一条原则，它可以帮助我们更好地组织代码、提高代码的可读性和可维护性，使得代码更加健壮、可靠和高效。

## 理解组合函数以及组合函数的作用

**组合函数的概念**

将多个函数组合成一个新函数的技术。组合函数将一个或多个函数作为输入，并返回一个新函数，该新函数将这些函数组合在一起以实现复杂的行为。

通常，组合函数可以使用函数柯里化来实现，通过将多个函数拆分成接受单一参数的函数，然后将这些函数组合在一起。

举个例子，假设有两个函数 f(x) 和 g(x)，我们可以使用组合函数将它们组合成一个新函数 h(x)：

```js
function compose(f, g) {
  return function(x) {
    return f(g(x));
  };
}

const h = compose(f, g);
```

这里，compose 函数接受两个函数 f 和 g 作为输入，然后返回一个新函数，该新函数将先执行 g 函数，并将其结果传递给 f 函数进行处理，最终返回 f(g(x))。

**组合函数的作用**

1、代码复用：

组合函数可以将多个简单的函数组合成一个更复杂的函数，这样可以减少代码冗余和重复。

2、代码简洁性：

组合函数可以使代码更加简洁和易于理解，因为它将多个函数组合成一个整体，从而使代码更加易于阅读和维护。

3、抽象层次：

组合函数可以将多个简单的函数组合成一个更高级的、抽象的函数，从而更好地实现了面向对象编程中的“抽象层次”的概念。

4、增强代码可读性：

组合函数可以使代码更加可读，因为它将多个函数组合成一个整体，从而使代码更加清晰和易于理解。

> 总之，组合函数是一种非常有用的函数式编程技术，可以帮助我们更好地组织和组合代码，减少冗余和重复，并提高代码的可读性和可维护性。

## 说说你对严格模式的理解

严格模式是一种JavaScript的限制模式，因为种种历史原因，JavaScript语言在非严格模式下是比较松散的。在JavaScript不断优化和加入新特性的过程中，为了兼容早期的JavaScript，一些错误和不规范的写法也被保留了下来。这些错误也不会被抛出。在开启了严格模式后，js引擎会以一种更严格的规范执行JavaScript代码，一些不规范的写法和错误也会直接抛出。

**目的：**

提供更加严格的 JavaScript 代码执行环境，以消除 JavaScript 中的一些不安全或不合理的语法行为，并提高代码的健壮性和可维护性。

**历史：**

严格模式最初于 ECMAScript 5 中被引入，并在 ES6、ES7 和以后的版本中继续得到支持和推广。目前，严格模式已经成为 JavaScript 开发中的标准和最佳实践之一。

**局限性：**

严格模式的局限性和设计缺陷在于，==它无法完全解决 JavaScript 中的所有问题==

它并不能防止一些常见的错误，如变量名拼写错误、类型错误等。此外，在某些情况下，严格模式可能会导致性能问题，因为它要求更多的代码检查和类型转换。

它无法防止原型污染、闭包内存泄漏等一些常见的问题。此外，严格模式还可能影响一些 JavaScript 库和框架的兼容性，因为这些库和框架可能不支持严格模式。

**目前解决了什么问题：**

严格模式可以解决一些常见的 JavaScript 问题，如全局变量污染、变量声明不规范、this 指向不明确等问题。此外，严格模式还可以帮助开发者更好地调试和优化 JavaScript 代码，提高代码的健壮性和可维护性。

**开启严格模式的方法：**

1、对文件开启：在文件的开头写上"use strict"

2、对函数开启：在函数的开头写上"use strict"

**严格模式下的语法限制：**

- 不允许意外创建全局变量（不写var、let、const这种声明变量的关键字）
- 会对静默失败的赋值操作抛出异常
- 试图删除不可删除的属性
- 不允许函数参数有相同的名称
- 不允许只有0开头的八进制语法
- 不允许使用with
- 无法获取eval中定义的变量
- this绑定不会默认转成对象

> 总之，严格模式可以帮助开发人员更好地避免一些常见的 JavaScript 问题和陷阱，提高代码的可靠性和安全性。虽然严格模式会增加一些限制和约束，但它也会带来一些好处，例如更好的代码质量、更好的可维护性和更好的可读性。因此，建议在开发过程中启用严格模式，以提高代码质量和可靠性。

## toLocalString() 方法

`toLocaleString()` 方法是JavaScript中的一个内置方法，用于将数字、日期或时间转换为本地格式的字符串表示形式。它根据当前用户的本地化设置，返回适合其语言和地区的字符串表示。

# 📁 继承

## 什么是原型、原型链？

**原型：**

在JavaScript中，每一个对象都会有一个属性`[[prototype]]`，这个属性就是对象的原型，这个属性的值也是一个对象，是原对象的原型对象。访问对象中属性时，会先在对象自身进行查找，如果没有找到，那么会去对象的原型对象上查找。

**原型链：**

每个对象都有自己的原型对象，原型对象也有自己的原型对象。在访问对象的属性时，会沿着对象自身——>自身的原型对象——>原型对象的原型对象......这样的链条一路查找上去，这条链式结构就叫做原型链。原型链的尽头是Object的原型对象的`[[prototype]]`属性，值为null。

## 简述原型链（prototype chain）的概念

JavaScript 中的原型链（prototype chain）是一种机制，用于实现对象之间的继承。每个对象都有一个内部属性 `[[Prototype]]`，它指向另一个对象，也就是该对象的原型。如果在当前对象上访问一个属性或方法，但该属性或方法不存在，则 JavaScript 引擎会沿着原型链向上查找，直到找到该属性或方法为止。

## 原型链的应用有哪些

原型链是 JavaScript 中的重要概念之一，它可以帮助我们实现一些有用的应用，例如：

1. 继承：JavaScript 中的继承是通过原型链来实现的。可以通过将一个对象的原型设置为另一个对象，从而实现继承。这种方式比传统的基于类的继承更加灵活。

2. 方法共享：由于 JavaScript 中的所有对象都是基于原型的，因此可以在原型对象上定义方法，从而实现方法共享。这种方式可以提高代码的重用性和性能。

3. 多态：由于 JavaScript 中的对象是动态类型的，因此可以在运行时动态修改对象的原型，从而实现多态。这种方式可以提高代码的灵活性和可扩展性。

4. 类库的实现：很多 JavaScript 类库都是基于原型链实现的。通过在原型上定义方法和属性，可以实现一些通用的功能，从而提高代码的复用性。

总之，原型链是 JavaScript 中的一个重要概念，可以帮助我们实现很多有用的应用。需要注意的是，在使用原型链时，需要注意避免出现不必要的内存泄漏和性能问题。

## 隐式原型和显式原型？

隐式原型和显示原型是 JavaScript 中的两个概念，它们都与对象和原型链有关。

一、隐式原型

（也称为 `[[Prototype]]`）是一个指向其父对象的内部链接，用于继承父对象的属性和方法。当我们创建一个对象时，它会自动包含一个指向其构造函数的原型对象，该原型对象又会包含一个指向其父对象的原型对象，以此类推，最终形成一个原型链。

二、 显式原型

（也称为 `prototype`）是一个属性，**只存在于函数对象中**。它指向一个对象，该对象被用作新对象的隐式原型。当我们使用 `new` 关键字来创建一个对象时，该对象的隐式原型就会指向该函数的显示原型。

例如，下面是一个使用构造函数和原型链创建对象的例子：

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
}

const john = new Person('John', 30);
john.greet(); // 输出 "Hello, my name is John and I am 30 years old."
```

在上面的例子中，`Person` 函数的显示原型对象包含一个 `greet` 方法，它可以被 `john` 对象继承并调用。

**显式原型的作用：**

显式原型的作用是作为构造函数创建的对象的原型对象。在 JavaScript 中，构造函数创建的对象都可以访问构造函数的 prototype 属性，通过这个属性，可以访问到构造函数的原型对象。当我们通过构造函数创建一个对象时，这个对象会继承构造函数的原型对象上的所有属性和方法，这就实现了 JavaScript 中的基于原型的继承。

> 通过显式原型，我们可以在原型对象上定义一些属性和方法，从而让构造函数创建的所有对象都可以共享这些属性和方法。这样做可以有效地节省内存，提高代码的效率。

## `getprototypeof` 和 `__proto__` 的区别

`Object.getPrototypeOf()`和`__proto__`都是用于获取对象原型的方法，但它们有一些区别：

1. 语法不同：`__proto__`是一个属性，是一个非标准的方法，使用点号或方括号访问；`Object.getPrototypeOf()`是一个方法，标准的ECMAScript 5方法，它是一个静态方法，接受一个对象作为参数，并返回该对象的原型。它不会去访问对象的`__proto__`属性，而是通过内部的`[[Prototype]]`属性来获取对象的原型。。
2. `__proto__`属性可以让我们直接访问和修改对象的原型链。它是一个访问器属性，通过它可以读取和写入对象的原型。它是一个动态的属性，可以在运行时进行修改。而`Object.getPrototypeOf()`方法只能用于获取对象的原型。
3. `__proto__`属性在ECMAScript 6标准中已经被弃用，不再建议使用；而`Object.getPrototypeOf()`方法是一个标准方法，推荐使用。

下面是一些使用`Object.getPrototypeOf()`和`__proto__`的例子：

```javascript
let obj = {};
let proto1 = Object.getPrototypeOf(obj);
let proto2 = obj.__proto__;

console.log(proto1 === proto2); // true
```

在这个例子中，我们首先使用`Object.getPrototypeOf()`方法获取`obj`的原型，然后使用`__proto__`属性获取`obj`的原型。由于它们都指向同一个原型对象，所以它们是相等的。

然而，我们不推荐使用`__proto__`属性来访问和修改对象的原型，因为它是一个非标准的方法，不是所有的JavaScript引擎都支持它，并且它可能会影响代码的可读性和可维护性。因此，我们建议使用`Object.getPrototypeOf()`方法来获取对象的原型。

## 如何理解构造函数和constructor

在 JavaScript 中，构造函数是一种用于创建对象的特殊函数。当使用 new 操作符调用构造函数时，会创建一个新对象，并将该对象作为 this 关键字的值传递给构造函数。构造函数通常用来初始化对象的属性和方法。

例如，以下代码定义了一个名为 Person 的构造函数，用于创建人的对象：

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

var person1 = new Person('Alice', 25);
console.log(person1.name); // 输出 "Alice"
console.log(person1.age); // 输出 25
```

在这个例子中，Person 是一个构造函数。当我们使用 new 操作符创建 person1 对象时，JavaScript 引擎会执行 Person 函数并将 this 关键字指向一个新的空对象，然后将该对象赋值给 person1 变量。

constructor 是一个属性，用于指向构造函数。每个 JavaScript 对象都有一个 constructor 属性，该属性指向创建该对象的构造函数。例如，person1 对象的 constructor 属性指向 Person 函数：

```js
console.log(person1.constructor); // 输出 "Person"
```

constructor 属性在许多情况下很有用。例如，可以使用它来检查对象的类型：

```js
console.log(person1.constructor === Person); // 输出 true
```

另外，如果我们想要创建一个与 person1 对象相同的新对象，可以使用构造函数和 new 操作符来创建一个新的对象：

```js
var person2 = new person1.constructor('Bob', 30);
console.log(person2.name); // 输出 "Bob"
console.log(person2.age); // 输出 30
```

在这个例子中，person2 对象是通过 person1.constructor（即 Person 函数）创建的，因此它具有相同的属性和方法。

## new操作符具体做了什么

在 JavaScript 中，`new` 操作符用于创建一个对象实例。当你使用 `new` 关键字来调用一个函数时，以下步骤将被执行：

1. 创建一个新的空对象
2. 将这个空对象的原型指向构造函数的原型对象（也就是 `Constructor.prototype`）
3. 将构造函数中的 `this` 指向这个新创建的空对象
4. 执行构造函数中的代码
5. 如果构造函数中有返回值，并且返回值是一个对象，则返回该对象；否则返回创建的新对象。

## 如何通过原型链实现继承？

**原型链继承**：

重写子类的显式原型对象，让子类的显式原型对象的隐式原型指向父类的显式原型对象。

**ES5中继承的演变过程：**

原型链继承=> 构造函数继承=> 组合继承（原型链+构造函数继承）=> 寄生组合继承(原型链+寄生式函数+构造函数继承)

```javascript
function createObject(o) {
  function F() {}
  F.prototype = o
  return new F()
}
function inherit(Subtype, Supertype) {
  Subtype.prototype = Object.create(Supertype.prototype)
  Object.defineProperty(Subtype.prototype, "constructor", {
    enumerable: false,
    configurable: true,
    writable: true,
    value: Subtype
  })
}
function Person() {}
function Student() {
  Person.call(this)
}
inherit(Student, Person)
```

## 继承的各个方案以及优缺点

JavaScript中各种继承方式的原理、案例、优缺点以及使用场景。

### 1、原型链继承

原理：

原型链继承是通过将一个对象的实例作为另一个对象的原型来实现继承的。子类的原型对象指向父类的实例，从而使子类可以共享父类原型对象的属性和方法。

案例：

```javascript
// 定义一个 Animal 构造函数
function Animal(name) {
  this.name = name;
  this.colors = ['black', 'white'];
}

// 在 Animal 的原型上添加方法
Animal.prototype.sayName = function() {
  console.log(`My name is ${this.name}.`);
};

// 定义一个 Dog 构造函数
function Dog(breed) {
  this.breed = breed;
}

// 将 Dog 的原型指向 Animal 的实例，从而实现原型链继承
Dog.prototype = new Animal('Lassie');

// 实例化一个 Dog 对象
const dog = new Dog('Collie');

// 调用从 Animal 继承来的方法和属性
dog.sayName(); // My name is Lassie.
console.log(dog.colors); // ["black", "white"]
```

优点：

- 子类可以共享父类原型对象的属性和方法。

缺点：

- 在子类实例中修改继承来的属性和方法也会影响到父类和其他子类的实例。
- 子类不能向父类构造函数传参。

使用场景：

- 适用于单一继承的场景。

### 2、构造函数继承

原理：

构造函数继承是通过在子类中调用父类的构造函数来实现继承的。通过该方式，子类可以继承父类的实例属性和方法。

案例：

```javascript
// 定义一个 Animal 构造函数
function Animal(name) {
  this.name = name;
}

// 在 Animal 的原型上添加方法
Animal.prototype.sayName = function() {
  console.log(`My name is ${this.name}.`);
};

// 定义一个 Dog 构造函数，利用 call 方法调用父类 Animal 的构造函数
function Dog(name, breed) {
  Animal.call(this, name);
  this.breed = breed;
}

// 实现 Dog 对象继承 Animal 对象的方法
Dog.prototype = Object.create(Animal.prototype);

// 在 Dog 的原型上添加方法
Dog.prototype.sayBreed = function() {
  console.log(`I'm a ${this.breed} dog.`);
};

// 实例化一个 Dog 对象
const dog = new Dog('Lassie', 'Collie');

// 调用从 Animal 继承来的方法和自身添加的方法
dog.sayName(); // My name is Lassie.
dog.sayBreed(); // I'm a Collie dog.
```

优点：

- 子类可以继承父类的实例属性和方法。

缺点：

- 子类不能继承父类原型对象上的属性和方法。

使用场景：

- 适用于需要继承父类的实例属性和方法，而不需要继承父类原型对象上的属性和方法的场景。

### 3、组合继承

原理：

组合继承是将原型链继承和构造函数继承结合起来使用的一种方式。通过该方式，子类可以继承父类的实例属性和方法，也可以继承父类原型对象上的属性和方法。在该方式中，子类的构造函数调用了父类的构造函数，同时将子类的原型对象指向一个新的父类实例。

案例：

```js
// 定义一个 Animal 构造函数
function Animal(name) {
  this.name = name;
  this.colors = ['black', 'white'];
}

// 在 Animal 的原型上添加方法
Animal.prototype.sayName = function() {
  console.log(`My name is ${this.name}.`);
};

// 定义一个 Dog 构造函数
function Dog(name, breed) {
  // 使用 call 方法调用父类 Animal 的构造函数，从而继承父类的属性
  Animal.call(this, name);
  this.breed = breed;
}

// 将 Dog 的原型指向 Animal 的实例，从而继承父类的方法
Dog.prototype = new Animal();

// 修正 Dog 的原型对象的 constructor 属性
Dog.prototype.constructor = Dog;

// 在 Dog 的原型上添加方法
Dog.prototype.sayBreed = function() {
  console.log(`I'm a ${this.breed} dog.`);
};

// 实例化一个 Dog 对象
const dog = new Dog('Lassie', 'Collie');

// 调用从 Animal 继承来的方法和自身添加的方法
dog.sayName(); // My name is Lassie.
dog.sayBreed(); // I'm a Collie dog.
console.log(dog.colors); // ["black", "white"]
```

优点：

- 子类可以继承父类的实例属性和方法，也可以继承父类原型对象上的属性和方法。

缺点：

- 该方式会调用两次父类构造函数，一次是在创建子类原型对象时调用，另一次是在创建子类实例时调用，导致性能较差。

使用场景：

- 适用于需要继承父类的实例属性和方法，同时需要继承父类原型对象上的属性和方法的场景。

### 4、原型式继承

原理：

原型式继承是通过克隆一个已有的对象来创建一个新对象，并将新对象的原型对象指向已有对象，从而实现继承的。该方式可以通过`Object.create()`方法实现。

案例：

```javascript
// 定义一个 Person 构造函数
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// 在 Person 的原型上添加方法
Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}.`);
};

// 使用 Object.create() 方法来实现继承
const student = Object.create(Person.prototype);

// 给 student 对象添加自身属性
student.name = 'Tom';
student.grade = 6;

// 添加自身方法
student.study = function() {
  console.log(`${this.name} is studying in grade ${this.grade}.`);
};

// 调用从 Person 继承来的方法和自身添加的方法
student.sayHello(); // Hello, my name is Tom.
student.study(); // Tom is studying in grade 6.
```

优点：

- 可以动态的创建对象，而不需要定义具体的构造函数。

缺点：

- 不能实现复杂的继承关系。

使用场景：

- 适用于需要创建对象，并且该对象需要从多个对象中继承属性和方法的场景。

### 5、寄生式继承

原理：

寄生式继承是在原型式继承的基础上，增加了一个创建包含继承属性和方法的新对象的函数，并将新对象返回的方式，从而实现继承的。该方式可以通过封装原型式继承的代码来实现。

案例：

```javascript
// 定义父类
var person = {
  name: "default",
  sayHello: function() {
    console.log("Hello, " + this.name);
  }
};

// 定义子类
function createStudent(obj) {
  var student = Object.create(obj);
  student.grade = 5;
  return student;
}

// 创建子类实例
var s = createStudent(person);
s.name = "Tom";

// 调用父类方法
s.sayHello(); // Hello, Tom
```

优点：

- 可以动态的创建对象，而不需要定义具体的构造函数。
- 可以在不改变原型的情况下，增强对象。

缺点：

- 对象之间的关系比较模糊，不易于理解和维护。
- 函数复用性不高。

使用场景：

- 适用于需要创建一个新对象，同时需要从一个已有对象继承属性和方法的场景。
- 适用于一些特殊的情况，如对已有对象进行扩展等。

### 6、寄生组合式继承

原理：

寄生组合式继承是在组合继承的基础上，通过 Object.create() 方法来优化父类实例的创建，并且不会调用两次父类构造函数。通过这种方式，子类既可以继承父类的实例属性和方法，又可以继承父类原型对象上的属性和方法，而且不会调用两次父类构造函数。

案例：

```javascript
// 定义一个 Animal 构造函数
function Animal(name) {
  this.name = name;
}

// 在 Animal 的原型上添加方法
Animal.prototype.sayName = function() {
  console.log(`My name is ${this.name}.`);
};

// 定义一个 Dog 构造函数，利用 call 方法调用父类 Animal 的构造函数
function Dog(name, breed) {
  Animal.call(this, name);
  this.breed = breed;
}

// 实现 Dog 对象继承 Animal 对象的方法，但不直接使用 new Animal()
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

// 在 Dog 的原型上添加方法
Dog.prototype.sayBreed = function() {
  console.log(`I'm a ${this.breed} dog.`);
};

// 实例化一个 Dog 对象
const dog = new Dog('Lassie', 'Collie');

// 调用从 Animal 继承来的方法和自身添加的方法
dog.sayName(); // My name is Lassie.
dog.sayBreed(); // I'm a Collie dog.
```

优点：

- 既可以继承父类的实例属性和方法，又可以继承父类原型对象上的属性和方法。
- 不会调用两次父类构造函数。

缺点：

- 代码比较复杂，需要理解原型和构造函数的继承方式。

使用场景：

- 适用于需要继承父类的实例属性和方法，同时需要继承父类原型对象上的属性和方法的场景。

### 7、ES6 的 class 继承

```js
// 定义一个 Animal 类
class Animal {
  constructor(name) {
    this.name = name;
  }

  // 添加方法
  sayName() {
    console.log(`My name is ${this.name}.`);
  }
}

// 定义一个 Dog 类，并将其继承自 Animal
class Dog extends Animal {
  constructor(name, breed) {
    super(name);
    this.breed = breed;
  }

  // 添加方法
  sayBreed() {
    console.log(`I'm a ${this.breed} dog.`);
  }
}

// 实例化一个 Dog 对象
const dog = new Dog('Lassie', 'Collie');

// 调用从 Animal 继承来的方法和自身添加的方法
dog.sayName(); // My name is Lassie.
dog.sayBreed(); // I'm a Collie dog.
```

优点：

- 语法简洁易懂，符合直觉；
- 可以继承父类构造函数中的属性和方法，也可以继承父类原型上的属性和方法。

缺点：

- 仍然会创建父类构造函数中的属性和方法，每个实例都会拥有一份，可能造成内存浪费；
- 与原型继承方式一样，所有实例都会共享原型对象中的属性和方法，可能造成属性污染和命名冲突。

> 不同的继承方案各有优缺点，在实际开发中需要根据具体情况进行选择。需要注意的是，JavaScript的继承机制是基于原型链的，而不是基于类。即使使用类的概念，底层的实现仍然是基于原型的继承。因此，在使用继承时需要注意原型链的相关知识，以避免出现一些奇怪的问题。

## 最终ES5实现继承的方案_coderwhy

### 方案一：

直接将父类的prototype赋值给子类的prototype，父类和子类共享原型对象

缺点：

在子类原型对象上添加方法和属性会影响到父类

```javascript
function Person() {}
function Student() {}
Student.prototype = Pesrson.prototype
```

### 方案二：

通过new操作符创建一个新的对象，将这个对象作为子类的原型对象(显式原型)

缺点：

- 子类的实例对象继承过来的属性是在原型上的，无法打印
- 没有完美的实现属性的继承（子类的实对象可以从父类继承属性，也可以拥有自己的属性）

```javascript
function Person() {}
function Student() {}
var p = new Person()
Student.prototype = p
```

### 方案三：

通过new操作符创建一个新的对象，将这个对象作为子类的原型对象(显式原型)，并且在子类的内部通过借用构造函数的方法实现属性的继承

缺点：

父类构造函数会被调用两次，并且子类的实例对象总是有两份相同的属性，一份在自身，一份在其原型对象上

```javascript
function Person(arg1, arg2) {}
function Student() {
  Person.call(this, arg1, arg2)
}
var p = new Person()
Student.prototype = p
```

### 方案四：

让子类的原型对象(显式原型)的原型对象(隐式原型)指向父类的原型对象(显式原型)

缺点：

存在兼容性问题,`__proto__`属性只有部分游览器支持

```javascript
function Person() {}
function Student() {}
Student.prototype.__proto__ = Person.prototype
```

### 方案五：

寄生组合式继承(ES5中实现继承的最终方案)

```javascript
function createObject(o) {
  function F() {}
  F.prototype = o
  return new F()
}
function inherit(Subtype, Supertype) {
  Subtype.prototype = createObject(Supertype.prototype)
  Object.defineProperty(Subtype.prototype, "constructor", {
    enumerable: false,
    configurable: true,
    writable: true,
    value: Subtype
  })
}
function Person() {}
function Student() {
  Person.call(this)
}
inherit(Student, Person)
```

## 继承关系图中的各个关系

下图所有对象之间的关系？

![image-20230430224601115](E:\coder\09_OneNote\image\image-20230430224601115.png)

一、Function、Object、函数对象Foo的关系

- Function/Object/Foo 都是Function的实例对象
- Object是Function/Foo的父类
- 函数的`__proto__`都指向Function的显示原型,包括Function自己的`__proto__`

```js
var obj = {}; //相当于new Object()  ---> function Object(){}
function Foo() {} //相当于 new Function() ---> function Function(){}
function Person() {}

console.log(obj.__proto__ === Object.prototype);

console.log(Foo.__proto__ === Function.prototype);
console.log(Person.__proto__ === Function.prototype);
console.log(Foo.__proto__ === Person.__proto__);

console.log(Object.__proto__ === Function.prototype);
console.log(Function.__proto__ === Function.prototype);

console.log(Foo.prototype.__proto__ === Object.prototype);
console.log(Function.prototype.__proto__ === Object.prototype);

var p1 = new Person();
console.log(p1.__proto__ === Person.prototype);
```

二、普通对象、Foo创建出来的对象之间的关系

普通对象的父类和Foo创建出来的对象的父类都是Object

## 编写ES6的类并且实现继承

```js
class Person{
    constructor(name,age,height) {
        this.name = name
        this.age = age
        this.height = height
    }
    running() {
        console.log("running~")
    }
    eating() {
        console.log("eating~")
    }
}
class Coder extends Person{
    constructor(name,age,height){
        super(name,age,height)
    }
    running() {
        console.log("在健身房")
        super.running()
    }
    code() {
        console.log("Write code~")
    }
    static work() {
        console.log("Working overtime every day~")
    }
}

var coderwhy = new Coder()
coderwhy.code()
Coder.work()
```

## 使用babel进行ES6转ES5操作，并且阅读源码

## 对面向对象多态的理解

多态是面向对象编程中的一个重要概念，它指的是**在不同的对象上调用相同的方法时，可以产生不同的结果。**换句话说，多态是指一个方法可以根据不同的对象类型而表现出不同的行为。在JavaScript中，这通常通过使用继承来实现。子类可以继承父类的方法，并且可以重写这些方法以实现不同的行为。

例如，如果有一个基类Animal，它有一个speak方法：

```js
class Animal {
  speak() {
    console.log('Animal speaks');
  }
}
```

然后有一个子类Dog，它重写了speak方法：

```js
class Dog extends Animal {
  speak() {
    console.log('Dog barks');
  }
}
```

现在，当我们调用speak方法时，它会根据对象的类型执行不同的操作：

```js
const animal = new Animal();
animal.speak(); // 输出 "Animal speaks"

const dog = new Dog();
dog.speak(); // 输出 "Dog barks"
```

这就是多态的一个例子。不同的对象类型调用相同的方法，但它们的行为却不同。这种多态性允许我们以更灵活的方式设计代码，并且可以在不同的情况下以不同的方式使用相同的接口。

# 📁 JavaScript_ES6+

## 整理词法环境、环境记录等概念

一、词法环境概念

词法环境（Lexical Environment）是在JavaScript中管理标识符（Identifier）的一种机制，用于确定标识符在代码执行期间的作用域和值。词法环境是在代码编写时就已经确定的，而不是在代码执行时动态生成的。

二、组成部分

每个词法环境都由两部分组成：

1. 环境记录（Environment Record）：用于存储标识符和对应的值，以及一些用于管理标识符的方法。环境记录有两种类型：声明式环境记录和对象式环境记录。
2. 外部词法环境（Outer Lexical Environment）：指向包含当前词法环境的外层词法环境，用于实现作用域链（Scope Chain）。

**环境记录**

- 声明式环境记录（Declarative Environment Record）用于处理变量声明和函数声明等语法元素。在声明式环境记录中，会创建一个绑定（Binding），绑定将标识符和对应的值或函数体关联起来。当代码执行时，标识符会沿着作用域链逐级向外查找，直到找到绑定的值或函数体。


- 对象式环境记录（Object Environment Record）用于处理with语句和catch语句中的标识符。在对象式环境记录中，标识符和对应的值被存储在一个对象中，该对象被称为环境对象（Environment Object）。当代码执行时，标识符会在环境对象中查找对应的值。


三、作用

在JavaScript中，词法环境常常用于关联函数声明、代码块语句、try-catch语句等语法结构。当这些语法结构被执行时，JavaScript引擎会创建一个新的词法环境，并将其作为当前执行上下文的一部分。在这个词法环境中，会存储相应的变量、函数等标识符，以及它们的值。当函数执行完毕后，其词法环境会被销毁，其中存储的标识符也会随之消失。

四、作用域链

作用域链是一种机制，用于确定标识符在代码执行期间的作用域。作用域链由当前词法环境的环境记录和外部词法环境的作用域链构成，形成了一个链式结构。在查找标识符时，会从当前词法环境的环境记录开始，沿着作用域链逐级向外查找，如果在全局环境中还没有找到，就会报出“未定义”的错误。

## let、const和var的区别

在JavaScript中，let、const和var是用来声明变量的关键字。它们之间的区别主要体现在以下几个方面：

1、变量作用域：

var声明的变量作用域为函数作用域或全局作用域，而let和const声明的变量作用域为块级作用域（即{}内部的作用域）。

2、变量提升：

var声明的变量会存在变量提升（Hoisting）现象，即在代码执行前就已经被声明，但是值为undefined。

而let和const声明的变量不会存在变量提升。这意味着，在变量声明之前引用该变量会导致引用错误（即“暂时性死区”）。

3、暂时性死区

指在代码块内使用 `let` 或 `const` 声明变量时，该变量在声明前无法被访问或使用。使用它们会导致暂时性死区错误。为了确保代码中变量的正确性和可预测性。

例如，下面的代码会抛出暂时性死区错误：

```js
console.log(a); // ReferenceError: a is not defined
let a = 10;
```

在这个例子中，使用 `let` 声明变量 `a` 后，代码块内的 `console.log(a)` 尝试在 `a` 声明前使用它，因此会导致暂时性死区错误。

4、变量重复声明：

var声明的变量可以被重复声明，而let和const声明的变量不允许重复声明。

5、初始值：

var声明的变量可以不用赋初始值，如果不赋值，则变量的值为undefined。而let和const声明的变量必须在声明时就赋值。

6、可变性：

let声明的变量的值可以修改，而const声明的变量的值不可修改（即为常量），但是如果赋值的是引用类型，那么可以通过引用找到对应的对象，修改对象的内容。

**案例演示**

下面是一个简单的例子，演示let、const和var的区别：

```js
function test() {
  var a = 10;
  let b = 20;
  const c = 30;

  if (true) {
    var a = 1; // 可以重复声明
    let b = 2; // 不会影响外层的b
    const c = 3; // 不会影响外层的c
    console.log(a); // 1
    console.log(b); // 2
    console.log(c); // 3
  }

  console.log(a); // 1
  console.log(b); // 20
  console.log(c); // 30

  b = 40; // 可以修改值
  // c = 50; // 不允许修改值，会报错
}

test();
```

在这个例子中，使用var声明的变量a可以被重复声明，并且其作用域为整个函数，所以在if语句块中修改a的值后，外部也会受到影响。而使用let和const声明的变

## 写出案例进行字面量增强、解构练习

1.数组的解构

```js
var arr = ["张三", "李四", "王五"]
// 数组的解构，按顺序
var [item1, item2, item3] = arr
console.log(item1);
// 解构后面的元素
var [, , item] = arr
console.log(item);
// 默认值,原本是undefined
var [a, b, d, c = "eee"] = arr
console.log(c);
// 解构出一个元素，后面的元素放在一个新数组里
var [e, ...newArr] = arr
console.log(newArr);
```

2.对象的解构

```js
var obj = {
  name: "张三",
  age: 12,
  address: "上海"
}
// 对象的解构，没有顺序
// var { name, address, age } = obj
// console.log(name, age, address);
// 只解构一个元素
var { age } = obj
console.log(age);
//重命名
var { name: newName } = obj
console.log(newName);
// name没有被定义，报错
// console.log(name);
// 默认值
var { height = 89 } = obj
console.log(height);
console.log(obj);
// 重命名＋默认值
var { sex: newSex = "女" } = obj
// sex没有被定义，报错
// console.log(sex);
console.log(newSex);
// 之前不用对象的解构
function foo(info) {
  console.log(info.name, info.age);
}
foo(obj)
// 用对象的解构
function bar({ name, age, address }) {
  console.log(name, age, address);
}
bar(obj)
// 常见的用法
function foo(info) {
  console.log(info.name, info.age);
}
```

3.字面量增强

```js
var message = "hello";
var age = 90;
var obj = {
  // 属性的简写
  message,
  age,
  // 方法的简写
  eating() {
    console.log("eat");
  },
  running: () => {
    console.log(this);
  },
  //计算属性名
  [message + "abc"]: "helloword",
};
console.log(obj);
```

## 暂时性死区的本质是什么

暂时性死区是指在代码块内，使用 let 或 const 声明变量之前，该变量是不存在的，如果尝试访问该变量，就会产生一个引用错误。这种行为是 JavaScript 引擎的特性，而非语法错误。

该特性的本质在于 JavaScript 的变量提升机制发生了改变。在早期的 JavaScript 版本中，使用 var 声明变量时，变量会被提升至作用域顶部，因此在声明之前就可以访问和使用该变量，但此时变量的值为 undefined。

> 例如，以下代码中，变量 x 在声明之前就被使用了：
>
> ```js
> console.log(x); // 输出 undefined
> var x = 10;
> ```
>
> 在上述代码中，虽然 x 在声明之前就被使用了，但是由于变量提升的作用，x 已经被声明了，只是值为 undefined。如果没有使用 var 声明变量，就会出现引用错误。
>

但是，在 ES6 引入 let 和 const 后，这种行为发生了变化，使用 let 和 const 声明的变量，只有在声明语句执行之后，才能被访问到，否则会产生暂时性死区的错误。

这种机制的存在，可以避免在变量未声明时就使用变量的错误，同时也让代码的可读性和可维护性得到了提高。

## 理解let的块级作用域以及作用

一、概念

在 JavaScript 中，`let` 是一种块级作用域的变量声明方式，它可以在指定的作用域内声明一个变量，并且该变量只在该作用域内可用。块级作用域是指由一对花括号 `{}` 括起来的代码块，比如 `if` 语句、`for` 循环、函数等。

二、特点

使用 `let` 声明的变量具有以下特点：

1. 块级作用域：在使用 `let` 声明的变量所在的代码块内，该变量只在该代码块内可用，超出该作用域范围就无法访问。
2. 没有变量提升：和 `var` 声明的变量不同，`let` 声明的变量不存在变量提升，也就是说，在声明变量之前访问该变量会抛出一个暂时性死区错误。
3. 可以重新赋值：使用 `let` 声明的变量可以被重新赋值。

三、举例

下面是一个使用 `let` 声明的变量的例子：

```js
let x = 10;
if (true) {
  let x = 20;
  console.log(x); // 输出 20
}
console.log(x); // 输出 10
```

在这个例子中，我们首先使用 `let` 声明了变量 `x`，然后在一个 `if` 语句的代码块内又使用 `let` 声明了一个同名变量 `x`，这个变量只在该代码块内可用。在代码块外部再次访问变量 `x`，则访问到的是代码块外部声明的变量 `x`。这说明了 `let` 声明的变量具有块级作用域的特点。

## 为什么需要块级作用域？

> - 内层变量可能会覆盖外层变量
> - 用来计数的循环变量泄露为全局变量
>
> ——《ES6标准入门》

在 JavaScript 中，变量的作用域通常是函数级别的，也就是说，在函数内声明的变量只在函数内部可见，函数外部无法访问。但是，在代码块中使用 var 声明的变量具有全局作用域，这就会导致变量污染和命名冲突等问题。

为了解决这个问题，ES6 引入了 let 和 const 关键字，用于声明块级作用域的变量。块级作用域中的变量只在当前代码块内部可见，不会污染全局作用域，也不会与其他代码块中的变量产生命名冲突。

块级作用域的引入，使得代码的可读性和可维护性得到了提高。在较大的代码块中，使用块级作用域可以明确变量的作用域范围，减少代码的副作用，避免错误发生。同时，块级作用域还可以用于创建闭包，让变量在函数外部依然可以访问。

总之，块级作用域是 JavaScript 中一个重要的特性，它使得变量的作用域变得更加清晰明了，减少了代码中变量污染和命名冲突等问题，提高了代码的可读性和可维护性。

## 块级作用域的作用

1. 避免变量污染和命名冲突：在代码块内部声明的变量只在该代码块内部可见，不会影响到其他作用域中的同名变量，从而减少了变量污染和命名冲突的问题。
2. 控制变量的生命周期：在块级作用域内声明的变量，只有在该代码块内部存在，当代码块执行完毕后，这些变量也会被销毁，从而避免了变量长时间存在而导致的内存浪费问题。
3. 创建闭包：块级作用域可以用于创建闭包，使得函数内部的变量在函数外部仍然可以访问，从而实现一些高级的编程技巧。
4. 增加代码的可读性和可维护性：使用块级作用域可以明确变量的作用域范围，使得代码更加易读和易于维护。

## 函数能否在块级作用域中声明

在 ES6（ECMAScript 2015）之前，JavaScript 中的函数只能在全局作用域和函数作用域中声明，无法在块级作用域（例如 if 语句、for 循环等）中声明。在块级作用域中声明的函数会被提升到它所在的函数或全局作用域中，而不是该块级作用域中。

例如，以下代码中，虽然函数 foo 是在 if 代码块中声明的，但实际上它是在全局作用域中声明的：

```js
if (true) {
  function foo() {
    console.log('Hello, world!');
  }
}
foo(); // 输出 "Hello, world!"
```

然而，ES6 引入了 `let` 和 `const` 关键字，它们可以在块级作用域中声明变量，并且在这些块级作用域中声明的函数也有了新的行为。

在 ES6 中，使用 `let` 或 `const` 声明函数时，该函数的作用域就被限制在块级作用域内，而不是像 var 关键字那样在函数作用域或全局作用域内。这意味着在块级作用域内声明的函数不会被提升到函数或全局作用域，而是在声明位置被创建。

举个例子，以下代码演示了在块级作用域中使用 `let` 声明函数的例子：

```js
{
  let foo = function() {
    console.log("foo");
  };
  
  foo(); // 输出 "foo"
}

foo(); // Uncaught ReferenceError: foo is not defined
```

可以看到，`foo()` 函数在块级作用域中被定义，并在该块级作用域内被调用，输出了 "foo"。而在该块级作用域之外，尝试调用 `foo()` 函数会抛出 `ReferenceError`，因为该函数不在当前作用域中声明。

> 考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也应该写成函数表达式，而不是函数声明语句。

## ES6声明变量的六种方式

ES6 (ECMAScript 2015) 提供了六种新的声明变量的方式，它们分别是：

1. let：用于声明一个块级作用域的变量，它的作用域是在代码块内部，且不能重复声明同一个变量。

2. const：用于声明一个常量，其值不能被重新赋值，但是可以修改其内部属性。也是块级作用域的。

3. var：ES5 中已经存在的关键字，用于声明一个变量，但它是函数级作用域或全局作用域，容易引起变量提升问题。

4. function：ES6 中函数也可以被视为一种变量声明方式，具有块级作用域。

5. class：ES6 中引入了类的概念，可以用 class 关键字来声明一个类，也可以看做一种特殊的函数声明方式。

6. import：ES6 中的模块化机制使用 import 关键字来导入其他模块中的变量，也是一种声明变量的方式。

## 对象进行合并

### 1、Object.assign

利用assign合并多个对象，第一个参数为目标对象，后面可以有多个源对象。

- 首先我们需要知道的是assign实行的是浅拷贝，也就是说如果源对象的某个属性值是对象，那么assign拷贝的是它的引用。
- assign是将源对象的可枚举属性复制到目标对象，如果属性名相同后面的属性会覆盖前面属性，只有一个参数assign会直接返回该参数。
- 如果参数不是对象，assign会先将其转为对象，再进行操作
- assign可以处理数组，但数组会被视为对象

```js
let obj1 = {
    name: 'dk',
    age: '99',
    feature: 'stronge'
}

let obj2 = {
    name: 'tk',
    age: '99',
    feature1: 'noStronge',
    address: {
        city: '广州',
        address: {
      	  city: '深圳'
        }
    },
    skills: ['JavaScript', 'React', 'Node']
}

let res = Object.assign(obj1, obj2);
res.address.address.city = '广州';
console.log(obj2);
console.log(res);
/* {
  name: 'tk',
  age: '99',
  feature1: 'noStronge',
  address: { city: '广州', address: { city: '广州' } },
  skills: [ 'JavaScript', 'React', 'Node' ]
}
{
  name: 'tk',
  age: '99',
  feature: 'stronge',
  feature1: 'noStronge',
  address: { city: '广州', address: { city: '广州' } },
  skills: [ 'JavaScript', 'React', 'Node' ]
}
*/
```

### 2、利用扩展运算符

需要注意的是利用扩展运算符`...`合并对象，同样是进行浅拷贝

```js
let obj1 = {
    name: 'dk',
    age: '99',
    feature: 'stronge'
}

let obj2 = {
    name: 'tk',
    age: '99',
    feature1: 'noStronge',
    address: {
        city: '广州',
        address: {
        city: '深圳'
        }
    },
    skills: ['JavaScript', 'React', 'Node']
}

let res = {...obj1, ...obj2};
res.address.address.city = '杭州';
console.log(obj2);
console.log(res);
```

### 3、手写函数（浅拷贝实现）

```js
let merger = (...opts) => {
    let res = {};

    let combine = (opt) => {
        for(let prop in opt) {
            if(opt.hasOwnProperty(prop)) {
                res[prop] = opt[prop];
            }
        }
    }

    //扩张运算符将两个对象合并到一个数组里，因此opts可以调用length方法
    for (let i = 0; i < opts.length; i++) {
        combine(opts[i]);
    
    return res;
}


let obj1 = {
    name: 'dk',
    age: '99',
    feature: 'stronge'
}

let obj2 = {
    name: 'tk',
    age: '99',
    feature1: 'noStronge',
    address: {
        city: '广州',
        address: {
        city: '深圳'
        }
    },
    skills: ['JavaScript', 'React', 'Node']
}

let res = merger(obj1, obj2);

//查看是否是浅拷贝
res.address.address.city = '杭州';
console.log(res);
console.log(obj2);
```

**上面实现的函数主要的知识点有**

- Object对象的hasOwnProperty方法，主要用于判断实例对象是否有该属性。
- for in循环主要用于遍历对象属性。不管是自身的还是继承的属性。

### 4、手写函数（实现深拷贝）

下面实现深拷贝的函数思路和浅拷贝差不多，就是多出了一个递归，如果有不了解递归的小伙伴，可以去了解一下。

```js
let merger = (...opts) => {
    let res = {};

    let combine = (opt) => {
        for(let prop in opt) {
            if(opt.hasOwnProperty(prop)) {

                //下面是深拷贝与浅拷贝的区别，用到了递归的思想
                if(Object.prototype.toString.call(opt[prop]) === '[object Object]') {

                    res[prop] = merger(res[prop], opt[prop]);

                }else {

                    res[prop] = opt[prop];

                }

            }
        }
    }

    //扩张运算符将两个对象合并到一个数组里因此可以调用length方法
    for (let i = 0; i < opts.length; i++) {
        combine(opts[i]);
    }
    return res;
}


let obj1 = {
    name: 'dk',
    age: '99',
    feature: 'stronge'
}

let obj2 = {
    name: 'tk',
    age: '99',
    feature1: 'noStronge',
    address: {
        city: '广州',
        address: {
        city: '深圳'
        }
    },
    skills: ['JavaScript', 'React', 'Node']
}

let res = merger(obj1, obj2);

//查看是否是浅拷贝
res.address.address.city = '杭州';
console.log(obj2);
console.log(res);
```

Object.prototype.toString.call() 用于判断类型，他其实是toString( )方法和call( )方法结合使用，toString( ) 方法用于返回对象类型字符串，而call( )方法就是绑定this嘛。

上面在merger中调用merger就是递归的思想，有兴趣的小伙伴可以去学学递归的思想。

### 5、merge( )方法

最后介绍最后一种办法Lodash's中的merge( )方法。Lodash's是node中的库。它也是一种深拷贝的办法。

```js
const _ = require('lodash');

let obj1 = {
    name: 'dk',
    age: '99',
    feature: 'stronge'
}

let obj2 = {
    name: 'tk',
    age: '99',
    feature1: 'noStronge',
    address: {
        city: '广州',
        address: {
        city: '深圳'
        }
    },
    skills: ['JavaScript', 'React', 'Node']
}

const res = _.merge(obj1, obj2);
console.log(res);
```

## 弱引用和强引用的区别

一、JavaScript弱引用和强引用的区别

JavaScript中的引用（reference）是指对内存中某个对象的指向，可以让开发者通过一个变量来访问该对象。而引用可以分为强引用（strong reference）和弱引用（weak reference）两种类型。

强引用是最常见的引用类型，如果一个对象有强引用指向它，那么该对象不会被垃圾回收器回收，直到这个强引用被删除或者置为null。

弱引用是指不能阻止引用对象被垃圾回收的引用，当一个对象只被弱引用指向时，如果内存不足，该对象可能会被垃圾回收器回收。可以使用WeakMap和WeakSet来创建弱引用。

二、通常使用弱引用的场景包括：

- 缓存数据，当内存不足时可以自动释放不常用的数据。
- 监听对象的生命周期，当被监听对象被回收时，相应的监听器也可以自动释放。

> 需要注意的是，由于弱引用不能保证被引用对象一定存在，所以在使用弱引用时需要注意对被引用对象的判空处理。

三、举例说明

以下是使用强引用和弱引用的两个例子：

1、强引用的例子：

```js
let obj = { name: "Tom" }; // obj是对对象{ name: "Tom" }的强引用
let objRef = obj; // objRef也是对同一对象的强引用

obj = null; // 对象{ name: "Tom" }的强引用被删除

// 对象{ name: "Tom" }仍然存在，因为还有一个强引用objRef指向它
console.log(objRef); // 输出 { name: "Tom" }
```

2、弱引用的例子：

```js
let weakMap = new WeakMap();
let obj = { name: "Tom" };
weakMap.set(obj, "some data"); // 对象obj与字符串"some data"建立弱引用关系

obj = null; // 对象{ name: "Tom" }的强引用被删除

// 此时weakMap中的键值对会被垃圾回收器回收，因为对象obj只有一个弱引用与之关联
console.log(weakMap.get(obj)); // 输出undefined
```

在这个例子中，当对象`obj`被赋值为`null`时，虽然`weakMap`中还存在对`obj`的弱引用，但是由于没有强引用指向该对象，该对象会被垃圾回收器回收，同时`weakMap`中的键值对也会被回收。因此在获取`obj`对应的值时，会输出`undefined`。

## js 中 `<%...%>`是干嘛的

<% ... %> 是 JavaScript 中的一种模板语法，通常用于嵌入 JavaScript 代码到 HTML 模板中。

在使用模板引擎（如 EJS、Pug 等）时，我们可以使用 <% ... %> 标记来嵌入 JavaScript 代码。例如，以下是一个简单的 EJS 模板示例：

```html
<ul>
  <% for (var i = 0; i < fruits.length; i++) { %>
    <li><%= fruits[i] %></li>
  <% } %>
</ul>
```

在上面的例子中， <% ... %> 标记用于嵌入 for 循环，而 <%= ... %> 标记用于输出 fruits 数组中的每个元素。

需要注意的是，<% ... %> 标记中的代码会被执行，而 <%= ... %> 标记中的代码会被解析成字符串并输出到模板中。因此，在使用 <% ... %> 标记时需要注意不要在其中包含会产生副作用的代码，比如赋值语句或函数调用。

## Array.prototype.slice.call()

`Array.prototype.slice.call()` 是将类数组对象（例如 `arguments` 对象或 `NodeList` 对象）转换为数组的一种常见方法。它的实现基于 `slice()` 方法和 `Function.prototype.call()` 方法。

`slice()` 方法是一个数组方法，用于从数组中提取一部分元素并返回一个新数组。当该方法的参数为空时，它会将整个数组复制到新数组中。而 `Function.prototype.call()` 方法是 JavaScript 中的函数方法，可以用来调用一个函数并指定函数中 `this` 关键字的值。当我们将 `slice()` 方法应用于类数组对象时，我们可以使用 `call()` 方法将类数组对象作为 `slice()` 方法的 `this` 参数传递。这会将类数组对象转换为数组，并将其作为 `slice()` 方法的参数使用。

以下是一个示例，将 `arguments` 对象转换为数组：

```javascript
function myFunction() {
  const argsArray = Array.prototype.slice.call(arguments);
  // 现在 argsArray 是一个数组，包含传递给 myFunction() 的所有参数
  console.log(argsArray);
}

myFunction(1, "two", { three: 3 });
// 输出: [1, "two", { three: 3 }]
```

在上面的示例中，我们使用 `slice()` 方法和 `call()` 方法将 `arguments` 对象转换为数组，并将其保存在 `argsArray` 变量中。然后，我们在控制台中打印该数组，以证明它已成功转换为数组。

## js 中 tag函数 是干嘛的

标签模板字符串：

在 JavaScript 中，`tag函数`是一种特殊类型的函数，它可以被用来处理 `模板字符串`。

`模板字符串`是一种包含在反引号(\`)的字符串字面量，它可以包含占位符（\`${expression}\`）来嵌入任意 JavaScript 表达式。当 `模板字符串`被传递给 `tag函数` 时，该函数会将其解析成一个标记化的字符串数组和相应的表达式值，然后通过函数的参数来进行处理并返回最终结果。

例如，以下是一个简单的 `tag函数` 示例：

```js
function tag(strings, ...values) {
  console.log(strings);  // ["Hello, ", "!"]
  console.log(values);   // ["World"]
  
  return strings[0] + values[0] + strings[1];
}

const message = tag`Hello, ${"World"}!`;
console.log(message);  // "Hello, World!"
```

在上面的例子中，`tag函数` 接收两个参数：`strings` 和 `values`。`strings` 参数是一个字符串数组，它包含了 `模板字符串` 中所有静态文本的部分。`values` 参数是一个包含了所有占位符表达式的数组，它的长度与 `strings` 的长度相同，且对应位置的元素是相应占位符表达式的值。

在这个 `tag函数` 的实现中，它会将 `strings` 和 `values` 中的元素按照一定的逻辑进行处理，最终返回一个新的字符串。

由于 `tag函数` 可以灵活地处理 `模板字符串`，因此它在实现一些高级功能，比如模板字符串的本地化、代码注入等方面都有着广泛的应用。

## includs 和 contains 的区别？

在JavaScript中，`includes()`和`contains()`都是用于检查字符串或数组是否包含另一个字符串或元素的方法。但是，`contains()`并不是JavaScript中的一个内置方法。

在ES6中，`includes()`是新增的字符串和数组的原型方法。它接受一个参数，表示要查找的字符串或元素，并返回一个布尔值，表示是否找到了该字符串或元素。

例如，在字符串中使用`includes()`方法可以这样写：

```js
const str = 'Hello, world!';
console.log(str.includes('world')); // true
console.log(str.includes('foo')); // false
```

在数组中使用`includes()`方法可以这样写：

```js
const arr = [1, 2, 3, 4, 5];
console.log(arr.includes(3)); // true
console.log(arr.includes(6)); // false
```

相反，`contains()`不是JavaScript中的内置方法，可能是自定义函数或第三方库提供的方法。

因此，在JavaScript中，`includes()`是更为常见和标准的方法，应该优先使用。

## 变量的解构赋值用途有哪些？

变量的解构赋值是ES6中新增的语法，它可以将数组或对象的值解构成单独的变量，并赋值给它们。变量的解构赋值在实际开发中有以下几个常见的用途：

1、交换变量的值

使用解构赋值可以非常简洁地交换两个变量的值。例如：

```js
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a); // 2
console.log(b); // 1
```

2、提取函数返回的值

在JavaScript中，函数可以返回多个值，使用解构赋值可以方便地提取这些返回值。例如：

```js
function getValues() {
  return [1, 2, 3];
}

const [x, y, z] = getValues();
console.log(x); // 1
console.log(y); // 2
console.log(z); // 3
```

3、函数参数的默认值

在函数的参数列表中使用解构赋值可以提供默认值。例如：

```js
function foo({ x = 0, y = 0 }) {
  console.log(x, y);
}

foo({ x: 1 }); // 1 0
```

在上面的代码中，函数foo的参数是一个对象，使用解构赋值可以提供默认值。

4、函数参数的传递

在调用函数时使用解构赋值可以方便地将一个对象作为参数传递给函数。例如：

```js
function foo({ x, y, z }) {
  console.log(x, y, z);
}

const obj = { x: 1, y: 2, z: 3 };
foo(obj); // 1 2 3
```

5、提取对象中的属性值

使用解构赋值可以方便地提取对象中的属性值，从而避免使用点运算符访问属性。例如：

```js
const obj = { x: 1, y: 2, z: 3 };
const { x, y } = obj;
console.log(x); // 1
console.log(y); // 2
```

6、提取数组中的元素

使用解构赋值可以方便地提取数组中的元素。例如：

```js
const arr = [1, 2, 3];
const [x, y] = arr;
console.log(x); // 1
console.log(y); // 2
```

7、遍历map结构

Map 结构原生支持 Iterator 接口，配合变量的解构赋值，获取键名和键值就非常方便。

```javascript
const map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world
```

如果只想获取键名，或者只想获取键值，可以写成下面这样。

```javascript
// 获取键名
for (let [key] of map) {
  // ...
}

// 获取键值
for (let [,value] of map) {
  // ...
}
```

8、输入模块的指定方法

加载模块时，往往需要指定输入哪些方法。解构赋值使得输入语句非常清晰。

```javascript
const { SourceMapConsumer, SourceNode } = require("source-map");
```

总之，变量的解构赋值在实际开发中有很多用途，它可以让代码更简洁、更易读、更易维护。

## bigint解决了什么问题

`BigInt` 是 JavaScript 中的一种新数据类型，它被用来表示任意精度的整数。在 JavaScript 之前，整数的范围被限制在 `Number` 数据类型的 `-2^53` 到 `2^53` 之间，超出这个范围的整数将失去精度。这意味着对于需要使用超过这个范围的整数的应用程序，JavaScript 是无法满足要求的。

`BigInt` 数据类型的出现解决了这个问题。它可以表示比 `Number` 更大的整数，因为它不受 `Number` 范围的限制。`BigInt` 可以表示任意精度的整数，因此它非常适合处理需要非常大的整数的应用程序，例如密码学、金融和科学计算。

`BigInt` 可以像其他 JavaScript 数据类型一样进行运算和比较，但需要使用新的运算符和函数。例如，与 `Number` 数据类型相比，`BigInt` 不支持常规的算术运算符和比较运算符，需要使用新的运算符和函数。以下是一些示例：

```javascript
const a = 123456789012345678901234567890n; // 使用 "n" 后缀创建一个 BigInt 常量
const b = 987654321098765432109876543210n;

// BigInt 运算
const c = a + b;
const d = a * b;
const e = a > b;

console.log(c); // 1111111110111111111011111111110n
console.log(d); // 121932631137021795730507004601707445423262718120853083482001384524559390n
console.log(e); // false
```

### BigInt的特点

1. 任意精度：`BigInt` 可以表示任意大小的整数，不受 `Number` 数据类型范围的限制。它可以精确表示非常大的整数，例如用于密码学、金融和科学计算等领域。

2. 非常量：`BigInt` 是一种非常量数据类型，这意味着它不能用作对象属性名、数组索引、常量等。

3. 与 Number 的交互：`BigInt` 可以与 `Number` 类型进行交互，但需要注意一些行为。例如，在 `BigInt` 和 `Number` 之间执行运算时，`Number` 类型将被自动转换为 `BigInt` 类型。但是，将 `BigInt` 转换为 `Number` 时，如果 `BigInt` 大于 `Number` 数据类型的最大值，则会丢失精度。

4. 运算符和函数：与其他 JavaScript 数据类型一样，`BigInt` 有自己的一套运算符和函数。例如，`+` 和 `-` 运算符可以用于 `BigInt` 运算，但是它们的行为与 `Number` 运算不同。

5. 不可变性：`BigInt` 是不可变的，这意味着它们的值在创建后不能更改。如果需要更改一个 `BigInt` 值，必须创建一个新的 `BigInt` 值。

6. 语法：`BigInt` 值可以使用 `n` 后缀创建。例如，`123456789012345678901234567890n` 表示一个 `BigInt` 值。

7. 不能用于位运算：`BigInt` 不能用于位运算，例如按位与、按位或等，因为这些运算符只能用于 `Number` 类型。如果需要执行位运算，可以将 `BigInt` 转换为 `Number`，但是这可能会导致精度丢失。

8. 不能用于比较运算符：`BigInt` 不能与 `Number` 或其他 `BigInt` 进行比较运算，例如 `<`、`>`、`<=`、`>=` 等，因为它们的值类型不同。但是，可以使用 `===` 和 `!==` 运算符进行相等性比较。

9. 不能用于模运算：`BigInt` 不能用于 `%` 运算符，因为 JavaScript 规范规定 `%` 运算符只能用于 `Number` 数据类型。

10. 转换为字符串：`BigInt` 可以使用 `toString()` 方法将其转换为字符串。例如，`123n.toString()` 将返回字符串 `"123"`。

11. 可以使用递归方式进行运算：由于 `BigInt` 是不可变的，因此不能通过更改现有值来进行运算。但是，可以使用递归方式计算 `BigInt` 值。例如，可以使用递归方式实现阶乘函数：

    ```javascript
    function factorial(n) {
      if (n === 0n) {
        return 1n;
      } else {
        return n * factorial(n - 1n);
      }
    }
    
    console.log(factorial(10n)); // 输出 3628800n
    ```


需要注意的是，`BigInt` 在某些情况下可能会比 `Number` 更慢，因为它需要更多的内存和处理能力来处理。此外，`BigInt` 在某些情况下也不兼容某些 API 和库，因此需要谨慎使用。

## 整理ES6~ES13新增知识点

### 一、ES6 :

**⭐⭐⭐默写ES6新增了哪些新特性**

- 使用class用来定义类
  - constructor构造器
  - extends实现继承
  - super关键字代表继承的父类

- 对象字面量的增强
  - 属性的简写
  - 方法的简写
  - 计算属性名

- 解构
- let/const的使用
  - 不能重复声明变量
  - 不存在作用域提升
  - 存在暂时性死区
  - 不添加window
  - 存在块级作用域

- 字符串模板
  - 在模板字符串中，我们可以通过`${expression}`来嵌入动态的内容
  - 标签模板字符串

- 函数的默认参数
- 函数的剩余参数
- 箭头函数
  - 没有显式原型prototype
  - 不绑定this、arguments、super参数

- 展开语法
  - 在函数调用时使用；
  - 在数组构造时使用；
  - 展开运算符其实是一种浅拷贝
  - 在构建对象字面量时，也可以使用展开运算符，这个是在ES2018（ES9）中添加的新特性；

- 规范了二进制和八进制的写法
- 新增Symbol
- Set、WeakSet、Map、WeakMap

### 二、ES7 :

- Array Includes
  - 通过`includes`来判断一个数组中是否包含一个指定的元素，根据情况，包含返回`true`，否则返回`false`。

- 指数exponentiation运算符
  - `**`,对数字来计算乘方。

### 三、ES8 :

- Object values
  - 通过`Object.values`来获取所有的value值

- Object entries
  - 通过`Object.entries`可以获取到一个数组，数组中会存放可枚举属性的键值对数组

- String Padding
  - `padStart` 和 `padEnd` 方法，分别对字符串的首尾进行填充的。

- Trailing Commas
  - 允许在函数定义和调用时多加一个逗号：

- Object.getOwnPropertyDescriptors

### 四、ES9 :

- 构建对象字面量时，可以使用展开运算符

### 五、ES10 :

- flat
  - `flat()` 方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。

- flatMap
  - `flatMap`是先进行`map`操作，再做`flat`的操作
  - `flatMap`中的`flat`相当于深度为`1`

- Object fromEntries
  - `Object.formEntries`将`entries`转换成一个对象

- trimStart trimEnd
  - 去除字符串前面或者后面的空格

### 六、ES11 :

- BigInt
  - `BigInt`，用于表示大的整数(超过最大安全整数)
  - `BitInt`，表示方法是在数值的后面加上`n`

- 空值合并操作符
  - `??`当前面的值为null或者`undefined`时，显示`??`后面的值

- Optional Chaining
  - 可选链`?.`
  - 当`?.`前面的值为空时返回`undefined`

- Global This
  - JavaScript环境的全局对象

- for..in标准化
  - `for...in...`遍历对象时遍历的是`key`

## Symbol的用法和作用

### 用法

- Symbol值是通过Symbol函数来生成的
- Symbol()表示生成一个独一无二的值
- 我们也可以在创建Symbol值的时候,在`()`里面传入一个`description`,描述当前的Symbol
- 获取Symbol,使用`Object.getOwnPropertySymbols()`获取当前对象的Symbol,结果为一个数组

### 作用

- 用于对象的属性名,表示一个唯一的属性名

### 相同值的Symbol:

- 使用`Symbol.for()`生成,当`key`一样的时候,生成表示相同的Symbol
- `Symbol.keyFor(Symbol.for())`获取对应的`key`

JavaScript 中的 Symbol 是一种基本数据类型，用于表示独一无二的值。它们通常用作对象的属性名，以确保属性名称不会与其他属性名称冲突。

### 以下是几个关于 Symbol 的常见用法和作用：

#### 1、“隐藏” 对象属性

可以使用 Symbol 来“隐藏”对象属性，使其不可被枚举、不可被访问，从而实现类似于私有属性的效果。这种做法的原理是，Symbol 值在对象中是唯一的，因此无法被外部直接访问到。

例如，下面的代码定义了一个叫做 "hidden" 的 Symbol，用来作为一个私有属性：

```js
const hidden = Symbol('hidden');

const myObject = {
  publicProperty: 'public value',
  [hidden]: 'hidden value'
};
```

在这个例子中，myObject 对象具有两个属性，一个是公共属性 publicProperty，另一个是私有属性 hidden。由于 hidden 是一个 Symbol 值，因此它不会出现在对象的属性列表中，也不能直接被访问到。但是，我们可以使用属性访问器来访问 hidden 属性，例如：

```js
console.log(myObject.publicProperty); // 'public value'
console.log(myObject[hidden]); // 'hidden value'
```

需要注意的是，使用 Symbol 来“隐藏”对象属性并不是一种真正的安全措施，因为可以使用 `Object.getOwnPropertySymbols() `方法来获取对象中所有的 Symbol 属性，从而间接地访问到被“隐藏”的属性。但是，这种做法可以有效地防止属性名冲突和无意中修改私有属性。

#### 2、声明一个独特的常量

Symbol 可以用来声明一个独特的常量，以确保其值不会被意外更改。例如：

```js
const MY_SYMBOL = Symbol('my symbol');
```

在这个例子中，MY_SYMBOL 是一个具有唯一标识符 'my symbol' 的 Symbol，它被声明为一个常量。

#### 3、防止属性名冲突

Symbol 可以用来作为对象属性名，以确保属性名不会与其他属性名冲突。例如：

```js
const obj = {
  [Symbol('property1')]: 'value1',
  [Symbol('property2')]: 'value2'
};

console.log(obj); // { Symbol(property1): 'value1', Symbol(property2): 'value2' }
```

在这个例子中，obj 对象具有两个 Symbol 属性，每个 Symbol 都具有唯一的标识符。

#### 4、实现迭代器

Symbol 可以用来实现可迭代对象的迭代器。例如：

```js
const myIterable = {
  [Symbol.iterator]: function* () {
    yield 1;
    yield 2;
    yield 3;
  }
};

for (const value of myIterable) {
  console.log(value); // 1, 2, 3
}
```

在这个例子中，myIterable 对象具有一个 Symbol.iterator 属性，该属性是一个生成器函数，返回一个迭代器对象。当使用 for...of 循环遍历 myIterable 时，迭代器对象依次返回 1、2、3。

#### 5、创建私有属性和方法

由于 Symbol 具有唯一性，可以使用它们来创建私有属性和方法。例如：

```js
const MyClass = (function () {
  const privateProperty = Symbol('privateProperty');

  class MyClass {
    constructor() {
      this[privateProperty] = 'private value';
    }

    getPrivateValue() {
      return this[privateProperty];
    }
  }

  return MyClass;
})();

const myObject = new MyClass();

console.log(myObject.getPrivateValue()); // 'private value'
console.log(myObject.privateProperty); // undefined
```

在这个例子中，MyClass 类具有一个私有属性 privateProperty，该属性是一个 Symbol。在 MyClass 的构造函数中，私有属性被初始化为 'private value'。MyClass 还具有一个公共方法 getPrivateValue，该方法返回私有属性的值。由于 privateProperty 是一个 Symbol，它无法从外部访问。

#### 6、创建枚举类型

在 JavaScript 中，通常使用对象字面量来表示枚举类型，例如：

```
const COLOR_RED = 0;
const COLOR_GREEN = 1;
const COLOR_BLUE = 2;
```

这种方法有一个缺点，即枚举值可以被随意更改。使用 Symbol 可以创建真正的枚举类型，例如：

```js
const COLOR_RED = Symbol('RED');
const COLOR_GREEN = Symbol('GREEN');
const COLOR_BLUE = Symbol('BLUE');
```

在这个例子中，COLOR_RED、COLOR_GREEN 和 COLOR_BLUE 都是具有唯一标识符的 Symbol，它们表示三种不同的颜色。

#### 7、扩展对象功能

在 JavaScript 中，对象可以拥有一些内置的方法，例如 toString 和 valueOf。我们可以使用 Symbol 来创建自定义方法，例如：

```js
const mySymbol = Symbol('my symbol');

const myObject = {
  [mySymbol]: function() {
    console.log('hello from mySymbol');
  }
};

myObject[mySymbol](); // 'hello from mySymbol'
```

在这个例子中，myObject 对象具有一个 Symbol 属性 mySymbol，它的值是一个函数。我们可以通过对象的属性访问语法来调用这个函数。

总之，Symbol 是 JavaScript 中非常有用的一种数据类型，它可以用来创建唯一的值、防止属性名冲突、实现迭代器、创建私有属性和方法、创建枚举类型，以及扩展对象的功能。

## 什么是枚举类型

在 JavaScript 中，没有内置的枚举类型，但可以通过对象、数组或 ES6 的 Symbol 来模拟枚举类型。

枚举类型是一种特殊的数据类型，它定义了一组有限的命名值。通常用于表示一组相关的常量。枚举类型的值通常是不可修改的，因此它们通常用于表示某些固定的状态或选项。

以下是用对象来模拟枚举类型的示例：

```javascript
const Colors = {
  Red: 'RED',
  Green: 'GREEN',
  Blue: 'BLUE'
};

console.log(Colors.Red); // "RED"
console.log(Colors.Green); // "GREEN"
console.log(Colors.Blue); // "BLUE"
```

在此示例中，`Colors` 对象定义了三个属性，分别代表三种颜色。这些属性的值可以作为常量使用，因为它们是固定的且不可修改的。

ES6 中的 Symbol 可以用来模拟一个更加严格的枚举类型。使用 Symbol，可以确保枚举值是唯一的，并且不能被修改。以下是一个使用 Symbol 的示例：

```javascript
const Colors = {
  Red: Symbol('RED'),
  Green: Symbol('GREEN'),
  Blue: Symbol('BLUE')
};

console.log(Colors.Red); // Symbol(RED)
console.log(Colors.Green); // Symbol(GREEN)
console.log(Colors.Blue); // Symbol(BLUE)
```

在此示例中，`Colors` 对象的属性使用 Symbol 来表示每种颜色。这些 Symbol 对象是唯一的，并且不能被修改，因此它们可以用作固定的枚举值。

## Set、WeakSet、Map、WeakMap的特点

**一、Set:**

- 用来存储数据，类似于数组,
- 与数组的区别是元素不能重复,
- 可以使用forEach方法和使用for...of...遍历

**常见属性和方法**

- `size`：返回Set中元素的个数
- `add(value)`：添加某个元素，返回Set对象本身
- `delete(value)`：从set中删除和这个值相等的元素，返回boolean类型
- `has(value)`：判断set中是否存在某个元素，返回boolean类型
- `clear()`：清空set中所有的元素
- `forEach(callback, [ ,thisArg])`：通过`forEach`遍历set

**使用场景**

Set主要用于存储一组不重复的值，可以用来去除数组中的重复元素。一些场景包括：

- 去重：从一个数组中去掉重复的元素。
- 数组元素筛选：将一个数组中满足某个条件的元素筛选出来。
- ES6中的新特性：使用Set来处理ES6中新增的类似于集合的数据类型。

**二、WeakSet:**

- 只能存储对象类型，不能存放基本数据类型,
- 对对象的引用是一个弱引用，如果没有其他对对象的引用，那么相应对象会被GC进行清除，
- 不能遍历

**常见的方法**

- `add(value)`：添加某个元素，返回WeakSet对象本身
- `delete(value)`：从WeakSet中删除和这个值相等的元素，返回boolean类型
- `has(value)`：判断WeakSet中是否存在某个元素，返回boolean类型

**使用场景**

WeakSet与Set相似，但是它只能存储对象类型的值，且存储的是弱引用。当对象被垃圾回收时，对应的键值对也会被自动删除。一些场景包括：

- 存储临时的对象数据：当一些对象不再被使用时，WeakSet可以帮助自动清除对应的键值对，避免内存泄漏。

**三、Map:**

- 用于存储映射关系，存储的为键值对，
- 每个键值对为一个数组，
- 与对象的区别是存储的key可以为一个对象
- 可以使用`forEach`方法和使用`for...of...`遍历

**常见属`性和方法**

- `size`：返回Set中元素的个数
- `set(key, value)`：在Map中添加key、value，并且返回整个Map对象
- `get(key)`：根据key获取Map中的value
- `has(key)`：判断是否包括某一个key，返回Boolean类型
- `delete(key)`：根据key删除一个键值对，返回Boolean类型
- `clear()`：清空所有的元素
- `forEach(callback, [ ,thisArg])`：通过`forEach`遍历`Map`

**使用场景**

Map主要用于存储一组键值对，可以用于实现字典、哈希表等数据结构。一些场景包括：

- *存储配置信息：例如，可以使用Map来存储应用程序的配置信息，如数据库连接配置、日志配置等。
- 缓存数据：例如，可以使用Map来存储缓存数据，以提高应用程序的性能。

**四、WeakMap:**

- 存储的key只能为对象，不允许是其他类型
- 对对象的引用是一个弱引用，如果没有其他对对象的引用，那么相应对象会被GC进行清除，
- 不能进行遍历

**常见的方法**

- `set(key, value)`：在Map中添加key、value，并且返回整个Map对象
- `get(key)`：根据key获取Map中的value
- `has(key)`：判断是否包括某一个key，返回Boolean类型
- `delete(key)`：根据key删除一个键值对，返回Boolean类型

**使用场景**

WeakMap是一种特殊的Map，它只能存储对象类型的键，且键是弱引用。当对象被垃圾回收时，它对应的键值对也会被自动删除。一些场景包括：

- 存储临时的对象数据：当一些对象不再被使用时，WeakMap可以帮助自动清除对应的键值对，避免内存泄漏。
- 私有属性：由于WeakMap中的键是弱引用，因此可以将WeakMap用于实现对象的私有属性，避免属性被外部访问到。等。

## Difference between Set and Map

Set和Map的区别？

简述：

- Set 和 Map 主要的应用场景在于==数据重组==和==数据储存==。
- Set 是一种叫做集合的数据结构，Map 是一种叫做字典的数据结构。

集合 与 字典 的区别：

- 共同点：集合、字典 可以储存不重复的值
- 不同点：集合 是以 [value, value]的形式储存元素，字典 是以 [key, value] 的形式储存

一、集合（Set）：

[ES6](https://so.csdn.net/so/search?q=ES6&spm=1001.2101.3001.7020) 新增的一种新的数据结构，类似于数组，成员唯一（内部元素没有重复的值）。且使用键对数据排序即顺序存储。

Set 本身是一种构造函数，用来生成 Set 数据结构。

Set 对象允许你储存任何类型的唯一值，无论是原始值或者是对象引用。

```js
const s = new Set()
[1, 2, 3, 4, 3, 2, 1].forEach(x => s.add(x))
for (let i of s) {
    console.log(i)        // 1 2 3 4
}

// 去重数组的重复对象
let arr = [1, 2, 3, 2, 1, 1]
[... new Set(arr)]        // [1, 2, 3]
```

注意：向 Set 加入值的时候，不会发生类型转换，所以`5`和`"5"`是两个不同的值。Set 内部判断两个值是否不同，使用的算法叫做“Same-value-zero equality”，它类似于**精确相等**运算符（`===`），主要的区别是`NaN`等于自身，而精确相等运算符认为`NaN`不等于自身。另外，`NaN`和`undefined`都可以被存储在Set 中， `NaN`之间被视为相同的值（NaN被认为是相同的，尽管 NaN !== NaN）。

```js
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b);
set // Set {NaN}
 
let set1 = new Set()
set1.add(5)
set1.add('5')
console.log([...set1])        // [5, "5"]
```

操作方法：

- add(value)：新增，相当于 array里的push。
- delete(value)：删除集合中value。
- has(value)：判断集合中是否存在 value。
- clear()：清空集合。

遍历方法（遍历顺序为插入顺序）

- keys()：返回一个包含集合中所有键的迭代器。
- values()：返回一个包含集合中所有值得迭代器。
- entries()：返回一个包含Set对象中所有元素得键值对迭代器。
- forEach(callbackFn, thisArg)：用于对集合成员执行callbackFn操作，如果提供了 thisArg 参数，回调中的this会是这个参数，**没有返回值。**

二、WeakSet：

WeakSet 对象允许你将**弱引用对象**储存在一个集合中。

WeakSet 与 Set 的区别：

- WeakSet 只能储存对象引用，不能存放值，而 Set 都可以。
- WeakSet 对象中储存的对象值都是被弱引用的，即垃圾回收机制不考虑 WeakSet 对该对象的应用，如果没有其他的变量或属性引用这个对象值，则这个对象将会被垃圾回收掉（不考虑该对象还存在于 WeakSet 中），所以，WeakSet 对象里有多少个成员元素，取决于垃圾回收机制有没有运行，运行前后成员个数可能不一致，遍历结束之后，有的成员可能取不到了（被垃圾回收了），WeakSet 对象是无法被遍历的（ES6 规定 WeakSet 不可遍历），也没有办法拿到它包含的所有元素。

方法

- add(value)：在WeakSet 对象中添加一个元素value。
- has(value)：判断 WeakSet 对象中是否包含value。
- delete(value)：删除元素 value。

三、字典（Map）：

是一组键值对的结构，具有极快的查找速度。

```
const m = new Map()
const o = {p: 'haha'}
m.set(o, 'content')
m.get(o)        // content
 
m.has(o)        // true
m.delete(o)        // true
m.has(o)        // false
```

操作方法：

- set(key, value)：向字典中添加新元素。
- get(key)：通过键查找特定的数值并返回。
- has(key)：判断字典中是否存在键key。
- delete(key)：通过键 key 从字典中移除对应的数据。
- clear()：将这个字典中的所有元素删除。

遍历方法：

- Keys()：将字典中包含的所有键名以迭代器形式返回。
- values()：将字典中包含的所有数值以迭代器形式返回。
- entries()：返回所有成员的迭代器。
- forEach()：遍历字典的所有成员。

四、WeakMap：

WeakMap 对象是一组键值对的集合，其中的**键是弱引用对象，而值可以是任意**。

**注意，WeakMap 弱引用的只是键名，而不是键值。键值依然是正常引用。**

WeakMap 中，每个键对自己所引用对象的引用都是弱引用，在没有其他引用和该键引用同一对象，这个对象将会被垃圾回收（相应的key则变成无效的），所以，WeakMap 的 key 是不可枚举的。

方法：

- has(key)：判断是否有 key 关联对象。
- get(key)：返回key关联对象（没有则则返回 undefined）。
- set(key)：设置一组key关联对象。
- delete(key)：移除 key 的关联对象。

五、总结：

Set：

- 成员唯一、有序且不重复。
- [value, value]，键值与键名是一致的（或者说只有键值，没有键名）。
- 可以遍历，方法有：add、delete、has。

WeakSet：

- 成员都是对象。
- 成员都是弱引用，可以被垃圾回收机制回收，可以用来保存DOM节点，不容易造成内存泄漏。
- 不能遍历，方法有add、delete、has。

Map：

- 本质上是键值对的集合，类似集合。
- 可以遍历，方法很多可以跟各种数据格式转换。

WeakMap：

- 只接受对象作为键名（null除外），不接受其他类型的值作为键名。
- 键名是弱引用，键值可以是任意的，键名所指向的对象可以被垃圾回收，此时键名是无效的。
- 不能遍历，方法有get、set、has、delete。

## Difference between Object and Map?

在JavaScript中，Map和Object都是用键值对来存储数据，但它们有以下不同点：

1、key类型：

在Object中，key必须是简单数据类型（整数、字符串或symbol），而在Map中可以是JavaScript支持的所有数据类型，也就是说可以用一个Object当做一个Map元素的key。

2、元素顺序：

Map元素的顺序遵循插入的顺序，而Object的则没有这一特性。

3、继承：

Map继承自Object对象。

4、新建实例：

Object支持以下几种方法来创建新的实例：

```js
var obj = {...};
var obj = new Object();
var obj = Object.create(null);
```

Map仅支持下面这一种构建方法：

```js
var map = new Map([[1, 2], [2, 3]]); // map = {1 => 2, 2 => 3}
```

5、数据访问：

Map想要访问元素，可以使用Map本身的原生方法，如：

```js
map.get(1); // 2 访问元素
map.has(1); // 判断某个元素是否在Map中可以使用
map.set(key, value); // 新增一个数据
map.delete(1); // 删除指定数据
map.clear(); //全部删除
```

Object可以通过`.`和`[]`来访问，如：

```js
// 获取数据
obj.id;
obj['id'];
 
// 新增/修改数据
obj['key'] = value;
obj.key = value;
 
// 删除数据
delete obj.id;
// 下面这种做法效率更高
obj.id = undefined
```

需要注意的是，使用delete会真正地将属性从对象中删除，而使用赋值undefined的方式，仅仅是值变成了undefined。属性仍然在对象上，也就意味着在使用for...in...去遍历的时候，仍然会访问到该属性。判断某个元素是否在Object中需要以下操作：

```js
obj.id === undefined;
// 或者
'id' in obj;
```

另外需要注意的一点是，Object可以使用Object.prototype.hasOwnProperty()来判断某个key是否是这个对象本身的属性，从原型链继承的属性不包括在内。

6、获取size：

Map自身有size属性，可以自己维护size的变化。Object则需要借助Object.keys()来计算。

```js
console.log(Object.keys(obj).length); 
```

7、Iterating：

Map自身支持迭代，Object不支持。可以使用以下方法确定一个类型是否支持迭代：

```js
console.log(typeof obj[Symbol.iterator]); // undefined
console.log(typeof map[Symbol.iterator]); // function
```

## 何时使用Map，何时使用Object？

虽然Map在很多时候优于Object，但作为JavaScript最基础的数据类型，还是有很多情景更适合使用Object。

当所要存储的是简单数据类型，并且 key 都为字符串或整数或 symbol 的时候，优先使用 Object，因为 Object 可以使用字符变量的方式创建，更加高效。

此外，Object 也有更为丰富的方法和属性，如 Object.keys()、Object.values() 等，可以方便地操作对象的属性。

在需要在单独的逻辑中访问属性或元素时，也应该使用 Object。

例如，以下代码使用 Object 定义了一个包含 id、name 和 print 方法的对象，并可以通过 obj.print() 访问对象的属性和方法：

```js
var obj = {
    id: 1,
    name: "It's Me!",
    print: function() {
        return `Object Id: ${this.id}, with Name: ${this.name}`;
    }
}
console.log(obj.print()); // Object Id: 1, with Name: It's Me.
```

另外，由于 JSON 直接支持 Object，但不支持 Map，在需要将数据转换为 JSON 格式的场景中，也应该使用 Object。

不过，如果代码执行时无法确定 key 的类型，或者需要存储大量元素，且需要频繁地执行写入和删除操作，那么使用 Map 会更为合适。

## Set、WeaeSet、Map、WeakMap的基本用法

Set、WeakSet、Map、WeakMap都是ES6中新增的数据结构，它们有着不同的特点和用途。

Set

Set是一种类似于数组的数据结构，它的特点是存储的值是唯一的，可以用来去除数组中的重复元素。Set的基本使用如下：

```js
// 创建一个Set
const mySet = new Set();

// 添加元素
mySet.add(1);
mySet.add(2);
mySet.add(3);

// 删除元素
mySet.delete(2);

// 判断元素是否存在
mySet.has(1); // true

// 获取Set的大小
mySet.size; // 2

// 遍历Set中的元素
mySet.forEach((value) => console.log(value));

// 将Set转换成数组
const myArray = [...mySet];
```

WeakSet

WeakSet是一种特殊的Set，它只能存储对象类型的值，且值是弱引用。当对象被垃圾回收时，它对应的值也会被自动删除。WeakSet的基本使用如下：

```js
// 创建一个WeakSet
const myWeakSet = new WeakSet();

// 添加对象
const obj = {};
myWeakSet.add(obj);

// 判断对象是否存在
myWeakSet.has(obj); // true

// 删除对象
myWeakSet.delete(obj);
```

需要注意的是，WeakSet没有size属性，也不能遍历它的元素。

Map

Map是一种键值对的数据结构，可以用来存储一组键值对，其中的键和值可以是任何类型。Map的基本使用如下：

```js
// 创建一个Map
const myMap = new Map();

// 添加键值对
myMap.set('name', 'Alice');
myMap.set('age', 30);

// 获取值
myMap.get('name'); // 'Alice'

// 删除键值对
myMap.delete('age');

// 判断键是否存在
myMap.has('name'); // true

// 获取Map的大小
myMap.size; // 1

// 遍历Map中的键值对
myMap.forEach((value, key) => console.log(key, value));

// 将Map转换成数组
const myArray = [...myMap];
```

WeakMap

WeakMap是一种特殊的Map，它只能存储对象类型的键，且==键是弱引用==。当对象被垃圾回收时，它对应的键值对也会被自动删除。WeakMap的基本使用如下：

```js
// 创建一个WeakMap
const myWeakMap = new WeakMap();

// 添加键值对
const key = {};
myWeakMap.set(key, 'value');

// 获取值
myWeakMap.get(key); // 'value'

// 删除键值对
myWeakMap.delete(key);

// 判断键是否存在
myWeakMap.has(key); // false
```

需要注意的是，WeakMap没有size属性，也没有forEach方法，也不能将其转换成数组。它主要用于存储一些临时的对象数据，比如缓存对象等。

## 引用赋值、浅拷贝、深拷贝的内存情况

### 变量的赋值：

在 JavaScript 中，变量的赋值有两种不同的方式：引用赋值和值赋值。

1、引用赋值

- 将一个变量中存储的对象的引用地址赋值给另一个变量

引用赋值是指当将一个对象赋值给变量时，变量将引用该对象的内存地址。换句话说，变量指向的是原始对象在内存中的位置，而不是该对象的值本身。当你对该变量进行操作时，实际上是在操作该对象。

2、值赋值

值赋值是指当将一个简单值（如字符串、数字或布尔值）赋值给变量时，变量将存储该值的副本，而不是该值在内存中的位置。

### 浅拷贝、深拷贝

1、浅拷贝

浅拷贝是一种复制对象的方法，它会创建一个新的对象，但是这个新对象只复制了原对象的一层属性，而不是复制原对象中的所有子属性。当对浅拷贝对象进行操作时，它实际上是对原始对象的引用，即两个对象指向同一个内存地址。这意味着如果你更改浅拷贝对象的属性，原始对象的属性也会更改。

在 JavaScript 中，有几种实现浅拷贝的方法，例如使用扩展运算符 `...`、`Object.assign()` 方法等。这些方法都只会复制对象的第一层属性，而不会复制对象中的所有子属性。如果原始对象中的属性值是一个对象，那么浅拷贝对象中对应的属性值也将是对这个对象的引用。这就是所谓的“浅拷贝”。

2、深拷贝

深拷贝是一种复制对象的方法，它可以完整地创建一个和原来的对象有相同结构的新的对象，包括对象中的子对象和数组中的元素，而不是只复制对象或数组的引用。这意味着，当你对深拷贝对象进行操作时，它不会影响原始对象。

在 JavaScript 中，对象和数组都是引用赋值的，所以当你将一个对象或数组赋值给另一个变量时，该变量将引用原始对象的内存地址。这意味着，当你改变一个对象或数组的属性时，原始对象或数组也会被改变。而深拷贝可以避免这种问题，因为它会复制对象或数组的所有属性，包括子对象或数组，而不是只复制它们的引用。

需要注意的是，深拷贝可能会比浅拷贝慢，并且在拷贝过程中可能会丢失一些原始对象的信息，比如函数、正则表达式、循环引用等，因此需要谨慎使用。常见的深拷贝方法包括递归复制、使用 JSON 序列化和反序列化等。

**案例**

以下是一个示例代码，展示了引用赋值、浅拷贝和深拷贝的不同情况：

```js
// 引用赋值
const obj1 = { a: 1, b: 2 };
const obj2 = obj1;
obj2.a = 3;
console.log(obj1); // { a: 3, b: 2 }

// 浅拷贝
const obj3 = { a: 1, b: { c: 2 } };
const obj4 = Object.assign({}, obj3);
obj4.b.c = 3;
console.log(obj3); // { a: 1, b: { c: 3 } }

// 深拷贝
const obj5 = { a: 1, b: { c: 2 } };
const obj6 = JSON.parse(JSON.stringify(obj5));
obj6.b.c = 3;
console.log(obj5); // { a: 1, b: { c: 2 } }
```

在上述代码中，当我们将 `obj1` 赋值给 `obj2` 时，`obj2` 实际上是 `obj1` 的引用，所以当我们更改 `obj2` 的属性时，`obj1` 的属性也会更改。

当我们使用 `Object.assign()` 对对象进行浅拷贝时，我们创建了一个新对象 `obj4`，该对象包含了 `obj3` 的所有属性和值。然而，`obj4` 中的 `b` 属性仍然是 `obj3` 的引用，因此当我们更改 `obj4.b.c` 时，`obj3` 的属性 `b.c` 也会更改，因为它们指向同一内存地址。

当我们使用 `JSON.parse(JSON.stringify())` 对对象进行深拷贝时，我们首先将对象转换为字符串，然后将字符串再次转换为对象，这将创建一个与原始对象相同但不同内存地址的新对象。因此，当我们更改 `obj6.b.c` 时，`obj5` 的属性 `b.c` 不会受到影响。

需要注意的是，使用 `JSON.parse(JSON.stringify())` 进行深拷贝也有一些限制，例如该方法无法复制函数、循环引用等特殊情况。

在处理复杂对象时，可能需要使用专业的库（如 Lodash、Underscore.js 等）来进行深拷贝。

## ES5监听对象的方式

==Object.defineProperty()==

在ES5中，可以使用Object.defineProperty()方法对对象的属性进行监听，从而实现对对象的监听。Object.defineProperty()方法可以定义对象的新属性或修改对象的现有属性，并返回修改后的对象。

1、该方法的语法如下：

```js
Object.defineProperty(obj, prop, descriptor)
```

其中，obj是要定义属性的对象，prop是要定义或修改的属性的名称，descriptor是属性的描述符对象，包含了该属性的各种特性。

2、在descriptor对象中，常用的特性有：

- value：属性的值
- writable：属性是否可写
- enumerable：属性是否可枚举
- configurable：属性是否可配置
- get：属性的 getter 函数
- set：属性的 setter 函数

在使用Object.defineProperty()方法时，可以通过定义getter和setter函数来监听对象的属性。getter函数在访问属性时自动调用，setter函数在设置属性时自动调用。

一、案例演示（一）：

下面是一个使用Object.defineProperty()方法监听对象的示例：

```js
let obj = {
  name: 'Alice',
  age: 18
}

Object.defineProperty(obj, 'name', {
  get() {
    console.log(`Get name`)
    return this._name
  },
  set(value) {
    console.log(`Set name to ${value}`)
    this._name = value
  }
})

console.log(obj.name) // 输出 Get name \n Alice
obj.name = 'Bob' // 输出 Set name to Bob
```

> 代码解释在上面的代码中，我们首先定义了一个名为obj的对象，该对象有两个属性：name和age。然后，我们使用Object.defineProperty()方法对obj对象的name属性进行监听，并定义了get和set方法。在get方法中，我们打印了对应的信息，并返回该属性的值。在set方法中，我们打印了对应的信息，并设置该属性的值。最后，我们通过obj.name和obj.name = 'Bob'对name属性进行访问和修改，分别触发了get和set方法，并输出了对应的信息。

二、案例演示（二）：

以下是一个稍微复杂一些的案例，演示了如何使用Object.defineProperty()方法对对象的多个属性进行监听：

```js
let obj = {
  name: 'Alice',
  age: 18
}

function watch(obj, prop, callback) {
  let value = obj[prop]
  Object.defineProperty(obj, prop, {
    get() {
      console.log(`Get ${prop}`)
      return value
    },
    set(newValue) {
      console.log(`Set ${prop} to ${newValue}`)
      const oldValue = value
      value = newValue
      callback(newValue, oldValue)
    }
  })
}

watch(obj, 'name', (newValue, oldValue) => {
  console.log(`name changed from ${oldValue} to ${newValue}`)
})

watch(obj, 'age', (newValue, oldValue) => {
  console.log(`age changed from ${oldValue} to ${newValue}`)
})

console.log(obj.name) // 输出 Get name \n Alice
obj.name = 'Bob' // 输出 Set name to Bob \n name changed from Alice to Bob
console.log(obj.age) // 输出 Get age \n 18
obj.age = 20 // 输出 Set age to 20 \n age changed from 18 to 20
```

> 在上面的代码中，我们首先定义了一个名为obj的对象，该对象有两个属性：name和age。然后，我们定义了一个名为watch的函数，该函数可以对指定对象的指定属性进行监听。在watch函数中，我们使用Object.defineProperty()方法对指定属性进行监听，并定义了get和set方法。在set方法中，我们首先保存该属性的旧值，然后设置新值，并调用回调函数，将新值和旧值作为参数传递给回调函数。回调函数中，我们打印了属性值的变化信息。
>
> 接着，我们通过watch函数分别对obj对象的name和age属性进行监听，并指定了相应的回调函数。最后，我们通过obj.name和obj.age对name和age属性进行访问和修改，分别触发了相应的get和set方法，并输出了对应的信息。
>
> 需要注意的是，在使用Object.defineProperty()方法时，我们将每个属性的旧值保存在了一个闭包变量value中，并在set方法中对该变量进行更新。这是因为在set方法中，this指向的是描述符对象，而不是实际的对象，无法直接访问对象的属性值。
>

## ES5监听对象的缺点

需要注意的是，在使用Object.defineProperty()方法时，需要对每个属性单独进行监听，且只能监听已经存在的属性，无法监听新添加的属性。

同时，该方法只能监听对象的属性，无法监听对象本身的变化。如果需要监听整个对象的变化，需要使用第三方库或手动实现递归遍历对象的方法。

## Proxy 的使用方式

**Proxy 干什么用的**

当我们需要对一个对象进行拦截或定制操作时，可以使用ES6中提供的Proxy对象。

Proxy对象可以代理另一个对象，拦截并处理对该对象的访问和操作。

在使用Proxy对象时，需要定义一个handler对象，该对象中包含了拦截和处理对==被代理对象==的**访问和操作**的方法。

**下面是Proxy对象的基本使用方式：**

```javascript
let target = {
  name: 'Alice',
  age: 18
}

let handler = {
  get(target, property, receiver) {
    console.log(`Get ${property}`)
    return Reflect.get(target, property, receiver)
  },
  set(target, property, value, receiver) {
    console.log(`Set ${property} to ${value}`)
    return Reflect.set(target, property, value, receiver)
  }
}

let proxy = new Proxy(target, handler)

console.log(proxy.name) // 输出 Get name \n Alice
proxy.age = 20 // 输出 Set age to 20
```

> 在上面的代码中，我们首先定义了一个名为target的对象，该对象有两个属性：name和age。然后，我们定义了一个名为handler的对象，该对象包含了对get和set方法的拦截和处理。在get方法中，我们打印了对应的信息，并使用Reflect.get方法获取原对象的属性。在set方法中，我们打印了对应的信息，并使用Reflect.set方法设置原对象的属性。最后，我们使用new Proxy()创建了一个名为proxy的Proxy对象，并将target和handler作为参数传入。
>
> 在使用Proxy对象时，当我们通过proxy对象访问或操作target对象的属性时，会自动触发handler对象中对应的方法。例如，当我们使用proxy.name访问target对象的name属性时，会触发handler对象中的get方法，并输出对应的信息。当我们使用proxy.age = 20设置target对象的age属性时，会触发handler对象中的set方法，并输出对应的信息。
>
> 需要注意的是，使用Proxy对象进行代理时，原对象target和代理对象proxy并不是同一个对象。对proxy对象的操作并不会直接影响到原对象target。因此，当我们使用Proxy对象时，需要通过handler对象和Reflect方法对原对象进行相应的操作。

## 说出Proxy和Object.defineProperty的区别

`Proxy` 和 `Object.defineProperty` 都是 JavaScript 中用于拦截对象属性操作的 API，但它们有以下几个区别：

### 1、功能不同（主要），Vue2、Vue3 响应式区别

**Object.defineProperty**

的设计初衷是定义对象的属性，所以它主要用于定义对象属性的特性（比如可写性、可枚举性和可配置性）以及属性的 `getter` 和 `setter` 方法。它仅能对单个属性进行拦截，无法对整个对象进行拦截。

- 该属性设计初衷是定义对象的属性,所以有些监听操作是监听不到的
- 对于复杂的对象,层级很深的话,需要深度监听
- 删除属性,添加属性是不能被监听的
- 不能监听数组的变化
  - 本质上是数组的length属性的数据属性描述符:
  - configurable: false 意味着length属性不能被修改,不能将length属性修改为存取属性描述符
  - 所以数组长度的变化的不能被监听的

**1.2.Proxy**

的设计初衷是监听对象的变化，并提供了13种方法来监听对象的操作，从而方便了对对象的监听和操作。它可以对整个对象进行拦截，并支持多个拦截器（称为“陷阱”），拦截的操作包括属性访问、赋值、删除、函数调用等。`Proxy` 支持的拦截操作更加丰富，包括了 `Object.defineProperty` 不支持的操作，比如监听数组的变化。

- 拦截和监视外部对对象的访问
- 可以直接监听数组的变化

### 2、兼容性不同

`Object.defineProperty` 的兼容性比 `Proxy` 更好，因为它是 ES5 中的 API，几乎所有现代浏览器都支持它。而 `Proxy` 是 ES6 中的 API，旧版本的浏览器不支持它，需要使用 polyfill 或者转译成 ES5 代码来兼容。

### 3、性能不同

由于 `Proxy` 是一个通用的拦截器机制，它的性能相对于 `Object.defineProperty` 来说要慢一些。尤其是在对每个属性进行访问时，由于要经过拦截器的处理，所以 `Proxy` 的性能可能比 `Object.defineProperty` 差一些。

### 4、应用场景不同

`Object.defineProperty` 适用于对已有对象的单个属性进行拦截，常用于对一些数据模型进行限制，比如限制对象的某个属性只读、禁止删除等。

`Proxy` 适用于对整个对象进行拦截，常用于在框架和库中实现数据绑定、数据校验、缓存等功能。它还可以用于实现代理模式、远程调用等高级用途。同时，由于 `Proxy` 支持监听数组的变化，所以它在处理数组操作的场景中比 `Object.defineProperty` 更加实用。

> 需要注意的是，由于 `Object.defineProperty` 是用于定义对象属性的 API，所以它的监听操作受到一定的限制，比如不能监听整个对象的变化、不能深度监听对象属性的变化、不能监听属性的添加和删除等。
> 而 `Proxy` 作为一个通用的拦截器机制，提供了对对象的拦截和定制行为的能力。它可以代理 JavaScript 中的任何对象，包括函数、数组和类实例等。
> 通过 Proxy，我们可以拦截并重写对象上的默认操作，例如获取属性、设置属性、删除属性、函数调用等，这让我们有了更大的灵活性去控制对象的行为。

与 Object.defineProperty 相比，Proxy 的功能更加强大、灵活，支持监听数组变化、深度监听、监听动态新增的属性等操作，而 Object.defineProperty 只能监听对象的属性。此外，使用 Proxy 可以避免直接操作目标对象，从而增加了代码的可维护性和安全性。

### 案例说明

举个例子，假设我们要对一个对象进行访问控制，只允许对其中一些属性进行访问，而另外一些属性则需要进行加密或者其他特殊处理，我们可以通过 Proxy 实现这个需求。具体来说，我们可以使用 `get` 拦截器来限制访问，使用 `set` 拦截器来对属性值进行加密或者其他处理，从而达到我们的目的。

```js
const data = {
  name: 'Alice',
  age: 18,
  address: 'New York'
}

const proxy = new Proxy(data, {
  get(target, key) {
    if (key === 'address') {
      console.log('Access to address is not allowed')
      return undefined
    }
    console.log(`Accessing ${key}`)
    return target[key]
  },
  set(target, key, value) {
    if (key === 'name') {
      console.log(`Setting ${key} is not allowed`)
      return false
    }
    console.log(`Setting ${key} to ${value}`)
    target[key] = value
    return true
  }
})

console.log(proxy.name) // Alice
console.log(proxy.age) // Accessing age 18
console.log(proxy.address) // Access to address is not allowed, undefined

proxy.name = 'Bob' // Setting name is not allowed
proxy.age = 20 // Setting age to 20
```

上面的例子中，我们定义了一个 `proxy` 对象，用于代理 `data` 对象。通过使用 `get` 和 `set` 拦截器，我们对 `name` 和 `address` 属性进行了限制，只有 `age` 属性可以被访问和修改。当访问被限制的属性时，会输出相应的提示信息并返回 `undefined`，当设置被限制的属性时，会输出相应的提示信息并返回 `false`，从而达到了访问控制和数据保护的目的。

## Proxy和Reflect配合使用监听对象的改变

一、如何做

在ES6中，可以使用Proxy对象来监听另一个对象的改变。Proxy对象可以代理另一个对象，拦截并处理对该对象的访问和操作，并可以通过Reflect方法进行对原对象的操作。

配合使用Reflect方法和Proxy对象，可以实现对对象的属性的监听和响应。这种方式可以使代码更加简洁、易于理解和维护。

二、案例

下面是一个简单的例子，用于监听一个对象的属性的改变：

```js
let person = {
  name: 'Alice',
  age: 18
}

let handler = {
  set(target, property, value, receiver) {
    console.log(`Set ${property} to ${value}`)
    return Reflect.set(target, property, value, receiver)
  }
}

let proxy = new Proxy(person, handler)

proxy.age = 20
console.log(proxy.age) // 输出20
```

> 在上面的代码中，我们创建了一个名为person的对象，该对象有两个属性：name和age。然后我们定义了一个名为handler的对象，用于拦截对person对象的set操作。在handler对象的set方法中，我们打印了对应的信息，并使用Reflect.set方法对原对象进行操作。最后，我们使用Proxy对象对person对象进行代理，将handler对象作为Proxy的handler参数传入。这样，我们就可以监听person对象的属性改变，并对其进行相应的操作。
>
> 在调用proxy.age = 20时，我们对person对象的age属性进行了赋值操作，这会触发handler对象的set方法。在set方法中，我们使用了Reflect.set方法对原对象进行操作，并返回操作结果。最后，我们输出proxy对象的age属性，可以发现该属性已经被更新为20。

## 说说Reflect的作用和为什么需要使用它

一、Reflect 的出现

在早期的 ECMAScript 规范中，为了提供对象自身操作的方法，将这些方法设计到了 Object 中，导致 Object 对象变得越来越繁琐。

二、设计初衷

后来引入了 Reflect 对象（注意：是一个对象），设计初衷是为了提供一个统一的接口来操作对象，可以将对象自身操作的方法放到 Reflect 对象中，使得 Object 对象更加简洁。

Reflect 对象还提供了一些便捷的操作方法，比如 Reflect.get()、Reflect.set()、Reflect.construct() 等，用于进行对象属性的获取、设置、构造等操作。

三、和Object的区别

Reflect提供的方法比Object更加严格，例如它的方法返回值通常是一个布尔值，表示操作是否成功；

而Object对象中的方法在返回值和使用方式上存在一些不足之处，例如方法的返回值通常是undefined而不是明确的布尔值，容易造成误解和使用错误。

四、Reflect的优势：

- 提供了一套完整的操作对象的方法，包括读取、设置、删除等，可以替代一些Object上的方法。
- 方法的命名更加统一和直观，更符合语义。
- Reflect的方法都是静态方法，可以方便地进行函数式编程。
- Reflect方法的返回值更加明确：所有的Reflect方法都返回一个Boolean值或一个操作结果，不会抛出错误，可以使代码更加简洁和易于理解，更容易判断操作是否成功。
- 支持Proxy对象：在Proxy对象中监听时，可以使用Reflect方法替换掉部分操作，避免了对原对象的直接操作。
  - 例如Reflect.get()、Reflect.set()、Reflect.apply()等方法可以替换掉Proxy中对应的handler方法。

五、Reflect的局限性：

- Reflect的方法虽然提供了更加灵活和统一的操作，但是由于它是一个新的对象，所以在一些老的浏览器中可能不被支持。
- Reflect的方法不能完全替代Object上的方法，有些方法还是需要在Object上调用。
- Reflect的方法虽然提供了更加明确的返回值，但是一些操作的返回值可能和Object上的方法有所不同。

总的来说，Reflect提供了更加灵活和统一的操作对象的方法，可以使得代码更加简洁和易于维护，但是也需要在使用时考虑到其局限性。

## Reflect的好处

好处一：代理对象的目的是通过对原对象进行包装来提供额外的行为或修改原始对象的行为，而不会直接操作原对象。这样做可以**减少对原对象的修改，同时使得代码更加模块化和可扩展。**可以在操作原对象时提供一个间接的方式，这样可以在操作前后进行一些额外的逻辑处理，如校验、日志记录等。

好处二：Reflect的方法通常会返回一个布尔类型的值，表示该操作是否成功。这个返回值可以用于**判断操作是否成功**，并且可以通过返回值的不同来区分不同的错误类型，以便进行更加精确的错误处理。

好处三：在使用Reflect.set/get时，我们可以通过**传递一个receiver参数来控制访问器的this指向**。这个参数称为receiver，并且可以是任何对象，但通常是外层的Proxy对象。这种方式可以提高代码的可读性和可维护性，同时可以确保访问器函数中的this指向是正确的。不过需要注意的是，receiver必须是原对象的代理对象，否则会抛出TypeError异常。

## Reflect的好处案例

一、好处一：

假设我们有一个原始对象person，包含了person的姓名和年龄属性。我们想要为这个对象添加一个计算属性，用于计算person的出生年份。我们可以通过使用代理来实现：

```js
const person = {
  name: "Alice",
  age: 30
};

const personProxy = new Proxy(person, {
  get(target, prop) {
    if (prop === "birthYear") {
      return new Date().getFullYear() - target.age;
    }
    return target[prop];
  }
});

console.log(personProxy.name); // "Alice"
console.log(personProxy.age); // 30
console.log(personProxy.birthYear); // 1991
```

二、好处二：

假设我们有一个对象user，包含了user的姓名和邮箱属性。我们想要在修改邮箱属性时，检查邮箱地址是否合法。我们可以通过使用Reflect来实现：

```js
const user = {
  name: "Bob",
  email: "bob@example.com"
};

const userProxy = new Proxy(user, {
  set(target, prop, value) {
    if (prop === "email") {
      if (isValidEmail(value)) {
        return Reflect.set(target, prop, value);
      } else {
        return false; // 返回false表示操作失败
      }
    }
    return Reflect.set(target, prop, value);
  }
});

console.log(userProxy.email); // "bob@example.com"
console.log(userProxy.email = "invalid email"); // false，操作失败
```

三、好处三：

假设我们有一个对象book，包含了book的标题和作者属性。我们想要在获取和设置作者属性时，将this指向外层的bookProxy对象。我们可以通过使用Reflect来实现：

```js
const book = {
  title: "JavaScript: The Good Parts",
  author: "Douglas Crockford"
};

const bookProxy = new Proxy(book, {
  get(target, prop, receiver) {
    if (prop === "author") {
      return Reflect.get(target, prop, receiver);
    }
    return target[prop];
  },
  set(target, prop, value, receiver) {
    if (prop === "author") {
      return Reflect.set(target, prop, value, receiver);
    }
    return Reflect.set(target, prop, value);
  }
});

console.log(bookProxy.title); // "JavaScript: The Good Parts"
console.log(bookProxy.author); // "Douglas Crockford"

const authorProxy = new Proxy(bookProxy.author, {
  get(target, prop, receiver) {
    console.log(receiver === bookProxy); // true
    return target[prop];
  },
  set(target, prop, value, receiver) {
    console.log(receiver === bookProxy); // true
    return Reflect.set(target, prop, value, receiver);
  }
});

console.log(authorProxy); // "Douglas Crockford"
authorProxy = "John Doe";
console.log(bookProxy.author); // "John Doe"
```

## Promise的基本使用

一、Promise是什么

在JavaScript中，Promise是一种用于处理异步操作的对象。它是一个代表了某个未来完成或失败的操作的占位符，而不是直接返回结果的函数调用。

- 异步编程的一种解决方案,比传统的解决方案--回调函数-更加合理和更强大
- 是一个对象
- 对象的状态不受外界影响
- 一旦状态改变,就不会再变

二、Promise有三种状态：

- Pending（进行中）：初始状态，既不是成功，也不是失败状态。
- Fulfilled（已成功）：表示操作成功完成，此时会指定Promise的返回值。
- Rejected（已失败）：表示操作失败，此时会指定Promise的失败原因。

Promise的状态只能从Pending转换到Fulfilled或Rejected，状态一旦转换就不会再变化。

- 当状态从Pending转换到Fulfilled时，会调用then()方法中的成功回调函数；
- 当状态从Pending转换到Rejected时，会调用catch()方法或then()方法的失败回调函数。

三、以下是Promise的基本使用方法：

```js
const promise = new Promise((resolve,reject) => {
  resolve(value) //该函数执行时会回调onFulfilled
  reject(reason) //该函数执行时会回调onRejected
  console.log("这个回调函数会被立即执行~")
})

// 监听promise对象的状态 方式一
promise.then(onFulfilled).catch(onRejected)
// 监听promise对象的状态 方式二
promise.then(onFulfilled,onRejected)
```

## Promise的实例方法和类方法

一、Promise的实例方法

1、then(onFulfilled,onRejected)

- onFulfilled ---->成功时的回调
- onRejected ----> 失败时的回调
- 返回值是一个新的promise对象，所以promise支持链式调用的原因

2、catch(onRejected)

- onRejected ---->失败时的回调

3、finally(onFinally)

- onFinally ---->无论Promise状态为fulfilled还是rejected，在执行完then或catch指定的回调函数后，都会执行的回调

二、Promise的类方法

1、Promise.all(iterable)

- 接受一个可迭代对象（如数组），并返回一个新的Promise对象；
- 当所有的Promise对象都成功时，该Promise对象的状态变为Fulfilled，将所有Promise对象的返回值以数组的形式返回；
- 如果其中有一个Promise对象失败，则该Promise对象的状态变为Rejected，并返回第一个失败的Promise对象的错误信息。

2、Promise.race(iterable)

- 接受一个可迭代对象，返回一个新的Promise对象。
- 当可迭代对象中的某个Promise对象改变状态时（不管是成功还是失败），该Promise对象的状态就跟着改变
- 将改变的Promise对象的返回值或错误信息作为该Promise对象的返回值或错误信息。

3、Promise.allSettled(iterable)

- 该方法接受一个可迭代对象（如数组），并返回一个新的Promise对象；
- 当所有的Promise对象都结束时（无论成功还是失败），该Promise对象的状态变为Fulfilled；
- 将所有Promise对象的状态和返回值或错误信息以数组的形式返回。

4、Promise.any(iterable)

- 接受一个可迭代对象，返回一个新的Promise对象；
- 当可迭代对象中的任何一个Promise对象成功时，该Promise对象的状态就跟着改变为Fulfilled；
- 将第一个成功的Promise对象的返回值作为该Promise对象的返回值；
- 如果所有的Promise对象都失败了，则该Promise对象的状态变为Rejected，并返回所有Promise对象的错误信息。

5、Promise.resolve(value)

- 该方法返回一个状态为Fulfilled的Promise对象，将指定的参数value作为返回值。

6、Promise.reject(reason)

- 该方法返回一个状态为Rejected的Promise对象，将指定的参数reason作为错误信息。

## 写出Promise基本使用的代码 

Promise 是一种用于处理异步操作的对象，下面是 Promise 基本使用的代码示例：

```js
// 定义一个 Promise 对象
const promise = new Promise((resolve, reject) => {
  // 异步操作，比如通过 Ajax 获取数据
  setTimeout(() => {
    const data = { name: "张三", age: 20 };
    // 将获取的数据传递给 resolve 函数，表示操作成功
    resolve(data);
    // 如果异步操作出错，可以传递错误信息给 reject 函数
    // reject("获取数据出错");
  }, 1000);
});

// 使用 then 方法处理成功的回调函数和错误的回调函数
promise
  .then((data) => {
    console.log("获取数据成功：", data);
  })
  .catch((error) => {
    console.log("获取数据失败：", error);
  });
```

上述代码中，首先定义了一个 Promise 对象，这个对象里面包含了一个异步操作（比如通过 Ajax 获取数据），然后通过 resolve 函数将获取的数据传递给成功的回调函数，通过 reject 函数传递错误信息给错误的回调函数。使用 then 方法可以处理成功的回调函数，使用 catch 方法可以处理错误的回调函数。

## 写（10遍）Promise的结构，手写~

```js
const promise = new Promise((resove, reject) => {
    resove(),
    reject()
}

promise.then(res => {
 console.log(res)
}),catch(err => {
 console.log(err)
}) 
```

## promise的方法有哪些和解决了什么问题？

Promise是一种异步编程的解决方案，它提供了一系列方法来处理异步操作的结果。Promise的方法有以下几种：

1. then()：用于指定异步操作成功时的回调函数，可以在then()方法中接收异步操作的结果，并对其进行处理。
2. catch()：用于指定异步操作失败时的回调函数，可以在catch()方法中接收异步操作的错误信息，并进行处理。
3. finally()：用于指定无论异步操作成功或失败时都要执行的回调函数，可以在finally()方法中执行一些清理操作。
4. all()：用于将多个异步操作合并成一个Promise对象，当所有异步操作都成功时，返回一个包含所有异步操作结果的数组；当其中一个异步操作失败时，返回该异步操作的错误信息。
5. race()：用于将多个异步操作合并成一个Promise对象，当其中任意一个异步操作成功或失败时，返回该异步操作的结果或错误信息。

解决了什么问题？

Promise的出现解决了回调函数嵌套过深、错误处理困难等异步编程的问题。它通过Promise对象来管理异步操作，将异步操作的状态分为“未完成”、“已完成”和“已失败”三种状态，可以避免回调地狱的问题，并且提供了更加可靠、可读性更高的异步编程方式。

## 解释一下JavaScript的同步和异步，以及如何使用Promise、async/await处理异步操作。

JavaScript 中的同步和异步是针对代码执行顺序的概念。同步代码会按照代码的书写顺序依次执行，而异步代码不会阻塞后续代码的执行，它们会被放入一个事件队列中，等待特定的事件触发后才会被执行。

JavaScript 中常用的异步操作包括定时器、事件监听、Ajax 请求、Promise 等。在处理异步操作时，我们可以使用 Promise 和 async/await。

Promise 是一种用于处理异步操作的对象，它可以用于处理延迟请求、文件读写、动画效果等异步操作。使用 Promise，我们可以将异步代码封装成一个 Promise 对象，并使用 then()、catch() 方法处理异步操作完成后的回调函数和错误处理，例如：

```js
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Data fetched successfully!');
    }, 2000);
  });
};

fetchData().then((result) => {
  console.log(result);
}).catch((error) => {
  console.error(error);
});
```

async/await 是 ECMAScript 2017 中引入的异步操作处理方式，它提供了一种更加简洁的方式来处理异步操作。我们可以使用 async 函数声明异步函数，并在其中使用 await 关键字等待异步操作完成，例如：

```js
const fetchData = async () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Data fetched successfully!');
    }, 2000);
  });
};

const displayData = async () => {
  try {
    const result = await fetchData();
    console.log(result);
  } catch (error) {
    console.error(error);
  }
};

displayData();
```

在使用 async/await 时，需要注意以下几点：

- await 关键字只能在 async 函数中使用；
- async 函数会返回一个 Promise 对象，我们可以使用 then()、catch() 方法处理异步操作完成后的回调函数和错误处理；
- 如果使用 try/catch 捕获异步操作的错误，需要在 async 函数中使用 try/catch，而不能在外部使用。

总的来说，Promise 和 async/await 都是处理异步操作的有效方式，具体使用取决于具体场景和团队的编码风格。

## 什么是迭代器？什么是可迭代对象？

### 一、迭代器

迭代器（Iterator）是一种用于遍历集合（Collection）的接口，它提供了一种统一的访问集合元素的方式，使得集合内部的实现方式对外部透明。

在JavaScript中，迭代器通常由一个next方法和一个done属性组成。next方法用于返回集合中的下一个元素，done属性表示是否已经遍历到集合的末尾。

- 迭代器是帮助我们对某个数据结构进行遍历的对象
- 迭代器也是一个具体的对象，这个对象需要符合迭代器**协议**
  - 迭代器协议定义了产生一系列值（无论是有限还是无限个）的标准方式
  - 在`JavaScript`中这个标准就是一个特定的`next`方法

- `next`方法的要求
  - 一个无参数或者一个参数的函数，返回一个应当拥有以下两个属性的对象：
  - `done`（`boolean`）
    - 如果迭代器可以产生序列中的下一个值，则为 `false`。（这等价于没有指定 `done `这个属性。）
    - 如果迭代器已将序列迭代完毕，则为 `true`。这种情况下，`value `是可选的，如果它依然存在，即为迭代结束之后的默认返回值。
  - `value`
    - 迭代器返回的任何 `JavaScript `值。`done `为 `true `时可省略


```js
// 封装一个为数组创建迭代器的函数
function createArrayIterator(arr) {
    let index = 0
    return {
        next: function() {
            if (index < arr.length) {
                return { done: false, value: arr[index++] }
            } else {
                return { done: true }
            }
        }
    }
}
```

### 二、可迭代对象

可迭代对象（Iterable）是实现了迭代器接口的对象，它可以被for...of循环遍历。在JavaScript中，Array、Map、Set、String等数据结构都是可迭代对象。

可迭代对象可以通过 [Symbol.iterator] 方法返回一个迭代器对象。该迭代器对象需要实现next方法，以便被for...of循环或者使用展开运算符(...)等方式遍历可迭代对象。

- 和迭代器不是一个概念

  - 当一个对象实现了`iterable protocol`协议时，它就是一个可迭代对象；
  - 这个对象的要求是必须实现 `@@iterator`方法，在代码中我们使用 `Symbol.iterator `访问该属性

- 转成这样的好处

  - 当一个对象变成一个可迭代对象的时候，就可以进行某些迭代操作
  - 比如 `for...of` 操作时，其实就会调用它的` @@iterator` 方法

- 实现可迭代协议的原生对象

  - `String`、`Array`、`Map`、`Set`、`arguments`对象、`NodeList`集合...

- 可迭代对象的应用

  - JavaScript中语法：`for ...of`、展开语法（`spread syntax`）、`yield*`、解构赋值（`Destructuring_assignment`）
  - 创建一些对象时：`new Map([Iterable])`、`new WeakMap([iterable])`、`newSet([iterable])`、`new WeakSet([iterable])`

  - 一些方法的调用：`Promise.all(iterable)`、`Promise.race(iterable)`、`Array.from(iterable)`

- 迭代器的中断

  - 比如遍历的过程中通过`break`、`return`、`throw`中断了循环操作
  - 比如在解构的时候，没有解构所有的值

- 自定义类的迭代实现

```js
class Person {
  constructor(name, age, height, friends) {
    this.name = name
  ...
  }
  // 实例方法
  running() {}
  [Symbol.iterator]() { 
    let index = 0
    const iterator = {
      next: () => {
        if (index < this.friends.length) {
          return { done: false, value: this.friends[index++] }
        } else {
          return { done: true }
        }
      }
    }
    return iterator
  }
}
```

==案例==

例如，`数组`、`字符串`、`Set`、`Map`等都是可迭代对象，它们都实现了`Symbol.iterator`接口，因此可以使用`for...of...`循环遍历它们的元素。

```js
const arr = [1, 2, 3]
for (const item of arr) {
  console.log(item)
}
// 输出：1 2 3

const str = 'hello'
for (const char of str) {
  console.log(char)
}
// 输出：h e l l o
```

需要注意的是，由于对象并没有实现`Symbol.iterator`接口，因此不能直接使用`for...of...`循环遍历对象的属性。不过，我们可以通过手动实现`Symbol.iterator`接口，来使对象也成为可迭代对象。

```js
const obj = {
  a: 1,
  b: 2,
  c: 3,
  [Symbol.iterator]: function* () {
    const keys = Object.keys(this)
    for (let i = 0; i < keys.length; i++) {
      yield this[keys[i]]
    }
  }
}

for (const value of obj) {
  console.log(value)
}
// 输出：1 2 3
```

在上面的代码中，我们手动实现了`Symbol.iterator`接口，将对象的属性值作为迭代器的返回值，使对象也成为可迭代对象，从而可以使用`for...of...`循环遍历对象的属性值。

下面是一个例子，展示了如何实现一个迭代器对象和一个可迭代对象：

```js
// 实现一个迭代器对象
const myIterator = {
  items: [1, 2, 3],
  index: 0,
  next() {
    if (this.index < this.items.length) {
      return { value: this.items[this.index++], done: false }
    } else {
      return { value: undefined, done: true }
    }
  }
}

// 实现一个可迭代对象
const myIterable = {
  [Symbol.iterator]: function() {
    return myIterator
  }
}

// 使用for...of循环遍历可迭代对象
for (const item of myIterable) {
  console.log(item)
}
```

在上面的代码中，我们首先定义了一个迭代器对象`myIterator`，该对象有一个`items`数组和一个`next()`方法。

next方法会返回数组中的下一个元素。然后，我们定义了一个可迭代对象`myIterable`，该对象通过`Symbol.iterator`方法返回迭代器对象`myIterator`。

最后，我们使用`for...of...`循环遍历可迭代对象`myIterable`，输出数组中的每一个元素。

## 可迭代对象的应用场景？

1、JavaScript中语法：`for..of...`、`展开语法(spread syntax)`、`yield＊`、`解构赋值(Destructuring＿assignment)`

2、创建一些对象时：`new Map([lterable])`、`new WeakMap([iterable])`、`new Set([iterable])`、`new WeakSet([iterable])`

3、一些方法的调用：`Promise.all(iterable)`、`Promise.race(iterable)`、`Array.from(iterable)`；

## 什么是生成器（函数）？生成器和迭代器有什么关系？

**生成器**

生成器（Generator）是一种特殊的函数，它可以在执行过程中暂停，并在需要时继续执行。

生成器使用函数关键字`function*`来定义，函数体中使用`yield`关键字来指定生成器的每个步骤。

调用生成器函数将返回一个生成器对象，该对象具有`next()`方法，每次调用`next()`方法都会执行生成器函数的下一个步骤，并返回一个包含当前执行状态的对象，该对象包含`value`和`done`两个属性，分别表示生成器返回的值和生成器是否已经执行完毕。

- Generator是ES6新增的一种特殊函数，可以通过`yield`关键字来控制函数的执行流程。
- 生成器函数需要在`function`的后面加一个符号` *`，执行时返回一个生成器对象。
- 生成器函数的执行流程可以被`yield`关键字中断，调用`next()`函数可以继续执行。
- `next()`函数可以传递参数，作为上一个`yield`语句的返回值。
- 生成器可以通过`return`传递值来提前结束函数执行。
- 使用`throw`函数可以抛出异常，但是在`catch`语句中不能继续`yield`新的值。
- 生成器函数可以用来替代迭代器，通过`yield`语法糖生成一个可迭代对象。
- 在自定义类中实现迭代器时，可以使用生成器实现，通过在类中定义`Symbol.iterator`方法并使用`yield*`语句来迭代可迭代对象。

**举例说明**

例如，以下代码定义了一个生成器函数，用于生成斐波那契数列。

```js
function* fibonacci() {
  let a = 0
  let b = 1
  while (true) {
    yield a；
    [a, b] = [b, a + b]
  }
}

const gen = fibonacci()
console.log(gen.next().value) // 输出：0
console.log(gen.next().value) // 输出：1
console.log(gen.next().value) // 输出：1
console.log(gen.next().value) // 输出：2
console.log(gen.next().value) // 输出：3
console.log(gen.next().value) // 输出：5
```

**生成器和迭代器有紧密的关系。**

每个生成器都是一个迭代器，而每个迭代器并不一定是一个生成器。

通过`yield`关键字，生成器函数将自身的执行状态暴露给了外界，从而可以通过生成器对象的`next()`方法来控制生成器函数的执行流程。

因此，生成器可以看作是一种方便控制的迭代器。

生成器还有一个重要的特性，就是可以使用`yield*`语法来嵌套调用其他生成器。这种嵌套调用可以让我们轻松地构建出复杂的迭代器，从而实现更加灵活和高效的迭代操作。

## 异步函数和普通函数的区别以及关系？

### 异步函数和普通函数的区别

1、执行顺序

- 普通函数的执行顺序是同步的，执行过程中会阻塞后续代码的执行，直到当前函数执行完成
- 异步函数的执行顺序是异步的，函数内部的异步操作不会阻塞后续代码的执行，异步操作完成后会调用回调函数来执行后续代码

2、返回值

- 普通函数的返回值直接由函数体内的代码计算得出并返回
- 异步函数的返回值是一个`Promise`对象，实际的返回值会被包裹在`Promise`的`resolve`中返回给调用者

3、异常处理

- 普通函数抛出异常会导致程序停止并抛出异常
- 异步函数抛出异常会被包裹在一个被`reject`的`Promise`对象中返回给调用者，调用者可以通过`catch`方法捕获异常并进行处理

4、await 关键字

- 异步函数中可以使用`await`关键字等待异步操作完成，同步等待操作的执行过程中会阻塞后续代码的执行

### 异步函数和普通函数的关系

- 异步函数和普通函数都是函数，只是异步函数内部可能包含异步操作，而普通函数不包含异步操作。
- 异步函数和普通函数之间的区别在于返回值和执行过程；
- 异步函数在语法上更加清晰，可以让开发者更加直观地知道一个函数是异步的，更加方便地进行异步编程；
- 异步函数可以让我们更加方便地使用Promise，使得异步编程更加简洁明了。
- 异步函数和普通函数，都可以使用`try...catch`语句捕获同步操作的异常。不同之处在于，对于异步函数中的异步操作，如果没有使用`try...catch`语句进行异常处理，那么异常会被抛到异步操作的回调函数中，而不是被当前函数捕获。

总的来说，异步函数是一种特殊的函数，用于处理异步操作的结果，并且可以通过`await`等待其他异步操作的完成。而普通函数则只能按顺序执行代码，没有异步操作的特性。

## 异步编程

异步编程是指编写不会阻塞（或卡住）主线程的程序，让程序在等待异步操作完成时能够继续执行其他任务。异步编程的主要目的是提高程序的响应速度和并发能力，避免程序因为阻塞主线程而变得不可响应或者变得缓慢。

在JavaScript中，异步编程可以通过`回调函数`、`Promise`、`async/await`等方式来实现。常见的异步操作包括网络请求、定时器、文件读写等等。

以下是几种常见的异步编程方法：

1、回调函数：将函数作为参数传递给另一个函数，在异步操作完成后执行回调函数。回调函数是异步编程最常见的方法之一，但它也容易导致回调地狱（callback hell）的问题。

```js
function fetchData(callback) {
  // 异步操作，比如发起网络请求
  setTimeout(() => {
    const data = { name: 'Tom', age: 18 };
    callback(data); // 异步操作完成后调用回调函数
  }, 1000);
}

fetchData((data) => {
  console.log(data); // 输出 { name: 'Tom', age: 18 }
});
```

2、Promise：Promise是异步编程的一种解决方案，它可以将异步操作封装成一个Promise对象，使得异步操作可以像同步操作一样进行处理。Promise对象可以通过`then()`方法注册回调函数，或通过`catch()`方法捕获异常。

```js
function fetchData() {
  return new Promise((resolve, reject) => {
    // 异步操作，比如发起网络请求
    setTimeout(() => {
      const data = { name: 'Tom', age: 18 };
      resolve(data); // 异步操作成功时调用resolve函数
    }, 1000);
  });
}

fetchData()
  .then((data) => {
    console.log(data); // 输出 { name: 'Tom', age: 18 }
  })
  .catch((error) => {
    console.error(error); // 输出错误信息
  });
```

3、async/await：async/await是ES2017引入的异步编程语法糖，它可以让异步操作看起来像同步操作。async关键字用于标识一个函数是异步函数，await关键字用于等待异步操作完成，并返回异步操作的结果。

```js
async function fetchData() {
  return new Promise((resolve, reject) => {
    // 异步操作，比如发起网络请求
    setTimeout(() => {
      const data = { name: 'Tom', age: 18 };
      resolve(data); // 异步操作成功时调用resolve函数
    }, 1000);
  });
}

async function getData() {
  try {
    const data = await fetchData();
    console.log(data); // 输出 { name: 'Tom', age: 18 }
  } catch (error) {
    console.error(error); // 输出错误信息
  }
}

getData();
```

异步编程是JavaScript开发中非常重要的一部分，需要仔细理解和掌握。在实际开发中，异步编程可以用于处理各种情况，例如：

1、处理网络请求：当我们向服务器发起请求时，由于网络速度较慢，需要等待服务器的响应。如果使用同步代码，则会在等待服务器响应时阻塞主线程，导致页面无响应。因此，我们可以使用异步编程来处理网络请求，使其在等待响应时不会阻塞主线程。

2、处理定时器：当我们需要在一段时间后执行某个操作时，可以使用定时器来实现。如果使用同步代码，则会在等待定时器结束时阻塞主线程，导致页面无响应。因此，我们可以使用异步编程来处理定时器，使其在等待结束时不会阻塞主线程。

3、处理事件：当我们需要响应用户操作时，可以使用事件来实现。由于用户的操作是不可预知的，因此我们需要使用异步编程来处理事件。

在JavaScript中，异步编程可以使用回调函数、Promise、async/await等方式来实现。其中，回调函数是异步编程的最基本形式，它可以通过将函数作为参数传递给其他函数来实现。Promise是ES6中新增的一种异步编程方式，它可以使异步代码更加易读和易维护。async/await是ES8中新增的一种异步编程方式，它可以使异步代码看起来更像同步代码，使代码更加清晰明了。

在实际开发中，我们需要根据具体情况选择合适的异步编程方式来处理各种场景。需要注意的是，如果不合理地使用异步编程，可能会导致代码可读性差、调试困难等问题，因此需要谨慎使用。

## 线程和进程的区别？以及关系？

一、基本概念：线程和进程都是操作系统中用来实现多任务的基本概念。

二、主要区别：

1、定义：

进程是操作系统资源分配的最小单位，一个进程可以包含多个线程；线程是进程中的执行单元，是 CPU 调度的最小单位。

2、资源占用：

进程是一个独立的内存空间，每启动一个进程都需要分配独立的地址空间，它独享系统资源；而线程是共享进程的资源，包括内存空间、文件描述符和信号处理等，因此线程之间的切换比进程更快。

3、调度：

操作系统通过进程进行资源分配和调度，每个进程都拥有自己的 PCB（进程控制块）来管理进程的执行情况；而线程的调度则是由进程进行调度，同一进程中的线程可以共享资源和数据，线程间的切换不需要操作系统的介入，所以调度更加简单高效。

4、同步：

由于线程共享进程的资源，因此线程之间的同步和通信更加方便快捷；而进程之间的同步则需要使用一些 IPC（进程间通信）机制，如管道、消息队列、共享内存等。

三、两者关系

在实际应用中，进程和线程通常都是相互关联、相互影响的。

进程可以通过创建多个线程来实现并发处理任务，线程之间可以通过共享内存来交换数据；而线程的切换和调度依赖于进程，进程之间的通信也需要通过线程间通信机制来实现。

因此，进程和线程是相互依存、相互支持的关系。

## 操作系统的工作方式

**一、操作系统：**

操作系统是计算机系统中最核心的软件之一，它提供了对计算机硬件的控制和管理，以便应用程序和用户可以使用它们。

**二、主要任务包括以下几个方面：**

1、进程管理：

操作系统可以创建、撤销进程，并调度它们的执行。它为每个进程分配系统资源（如CPU时间、内存和文件句柄）并管理它们的访问权限。操作系统还提供了进程间通信机制，允许进程之间交换数据和协调操作。

2、内存管理：

操作系统负责管理计算机的内存，包括分配、释放和保护内存区域。它还提供了虚拟内存机制，允许进程使用比实际可用内存更大的地址空间，这些地址空间被映射到物理内存或硬盘上的交换文件中。

3、文件系统管理：

操作系统提供了对文件和目录的管理。它负责分配磁盘空间、创建和删除文件、读写文件内容以及控制文件访问权限。

4、设备管理：

操作系统控制计算机的硬件设备，包括处理器、内存、磁盘、键盘、鼠标、显示器等。它提供了设备驱动程序，使得应用程序可以通过标准接口访问设备。

5、用户接口：

操作系统提供了用户与计算机交互的接口，包括命令行界面、图形用户界面、Web界面等。

**三、操作系统的工作方式可以分为两种：**

1、批处理方式：

在批处理方式下，操作系统将一批作业一起提交，并在它们完成时将结果返回给用户。在批处理方式下，用户需要编写一些脚本文件，告诉操作系统如何处理作业。这种方式适用于大规模的数据处理任务，例如银行的账单处理、工资计算等。

2、交互式方式：

在交互式方式下，操作系统允许用户通过命令行界面或图形用户界面与计算机交互。用户可以输入命令、启动应用程序、打开文件等。操作系统会立即响应用户的操作，使用户能够即时看到结果。这种方式适用于个人计算机和小型网络环境。

## JavaScript为什么不处理成多线程的

JavaScript 是一种单线程编程语言，这是因为它最初是为了在浏览器中执行脚本而设计的。当时，浏览器只有一个主线程用于处理用户界面的渲染、事件处理和 JavaScript 代码的执行等任务，所以 JavaScript 引擎也必须在该主线程上执行。

尽管现代浏览器已经变得更加复杂，但基本的单线程架构仍然存在。这是因为 JavaScript 的多线程处理可能会导致一些问题，比如竞态条件、死锁和资源共享等问题。这些问题在并发编程中很常见，需要非常小心地处理，否则会导致程序崩溃或不可预测的行为。

为了解决这些问题，现代浏览器提供了一些异步编程模型，比如 Promise 和 async/await 等，以帮助开发人员更好地处理并发和异步操作。这些模型使得 JavaScript 代码能够在单线程模型下模拟并发执行，而无需使用多线程。

虽然 JavaScript 本身不支持多线程，但浏览器中的 Web Worker API 提供了一种使用单独的线程运行 JavaScript 代码的方法，以避免对主线程的阻塞。但是，这些工作线程之间仍然需要进行通信和同步，以避免出现并发问题。

![image-20230508114239242](E:\coder\09_OneNote\image\image-20230508114239242.png)

## 说一下 web worker

Web Worker 是 HTML5 标准中定义的一个 API，它允许在浏览器的后台线程中运行 JavaScript 脚本，从而可以避免主线程被阻塞，提高页面的性能和响应速度。

Web Worker 是一个独立的 JavaScript 环境，它可以在主线程之外运行。它有自己的全局对象、内存空间和执行环境，与主线程相互独立。因此，Web Worker 可以执行一些耗时的计算任务，如数据处理、图片处理等，而不会对页面的用户交互产生影响。

Web Worker 的使用可以分为以下几个步骤：

- 创建 Worker 对象：使用 new 关键字创建 Worker 对象，并指定要在后台执行的 JavaScript 文件。
- 向 Worker 发送消息：使用 postMessage() 方法向 Worker 发送消息。
- 接收 Worker 返回的消息：在主线程中通过监听 Worker 对象的 message 事件来接收 Worker 返回的消息。
- 终止 Worker：使用 terminate() 方法终止 Worker 的执行。

需要注意的是，Web Worker 中无法访问 DOM，也不能与主线程共享同一个内存空间，因此需要通过消息传递来进行通信。此外，Web Worker 也无法访问主线程中的一些全局变量和函数，因此需要在 Worker 中重新定义。

Web Worker 的使用可以大大提高网页的性能和响应速度，但需要注意避免滥用，以免导致系统资源的过度消耗。

**简而言之**

在 HTML 页面中，如果在执行脚本时，页面的状态是不可响应的，直到脚本执行完成后，页面才变成可相应。web worker 是运行在后台的 js，独立于其他脚本，不会影响页面的性能。 并且通过 postMessage 将结果回传到主线程。这样在进行复杂操作的时候，就不会阻塞主线程了。

如何创建 web worker：

1. 检测浏览器对于 web worker 的支持性
2. 创建 web worker 文件（js，回传函数等）
3. 创建 web worker 对象

## 事件队列、微任务、宏任务的理解？

在 JavaScript 中，事件循环（event loop）是一种机制，用于处理异步代码的执行。

在 JavaScript 中，所有代码都是单线程执行的，也就是说，同一时间只能执行一个任务，而事件循环就是==负责管理任务执行的机制。==

事件循环的核心是处理任务队列（task queue），而任务队列可以被分为宏任务（macro-task）和微任务（micro-task）。

事件循环的基本原理是，当 JavaScript 引擎遇到一个异步任务（比如定时器、网络请求、DOM 事件等），它不会立即执行这个任务，而是把这个任务添加到任务队列中。然后 JavaScript 引擎继续执行同步代码，直到执行完毕，然后开始从任务队列中取出任务并执行。这个过程不断重复，被称为事件循环。

### 任务队列（task queue）

用于存储待执行的任务（包括同步任务和异步任务）的队列结构。在 JavaScript 中，任务队列通常被划分为宏任务队列（Macro Task Queue）和微任务队列（Micro Task Queue）两类。

**（1）宏任务（macro-task）**

是由浏览器或 Node.js 提供的任务，包括 setTimeout、setInterval、DOM 事件、Ajax 请求等，这些任务都会被放入宏任务队列中，等待执行。当执行一个宏任务时，会先执行当前宏任务所产生的所有微任务，再执行下一个宏任务。

**（2）微任务（micro-task）**

微任务队列由 JavaScript 引擎提供的任务，包括 Promise 的 then/catch/finally 方法、async/await 中的 await 、queueMicrotask()、Object.observe 方法、MutationObserver 方法等，这些任务会被放入微任务队列中，等待执行。当执行完一个宏任务时，会立即执行当前宏任务产生的所有微任务，直到微任务队列为空，才会执行下一个宏任务。

当事件循环从任务队列中取出任务时，它首先会执行所有微任务，然后再执行一个宏任务，然后再执行微任务，依次循环。

事件循环的设计使得 JavaScript 能够处理异步任务，同时保证了任务执行的顺序和可靠性。开发人员可以利用事件循环机制来实现异步编程，以避免阻塞代码执行。同时，对事件循环机制的深入理解也是解决 JavaScript 并发编程问题的关键。

## 掌握微任务、宏任务相关的面试题

面试题一

```js
console.log("script start")

function requestData(url) {
  console.log("requestData")
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("setTimeout")
      resolve(url)
    }, 2000);
  })
}

// 2.await/async
async function getData() {
  console.log("getData start")
  const res = await requestData("why")
  
  console.log("then1-res:", res)
  console.log("getData end")
}

getData()

console.log("script end")

// script start
// getData start
// requestData
// script end

// setTimeout

// then1-res: why
// getData end
```

 面试题二

```js
async function async1 () {
  console.log('async1 start')
  await async2();
  console.log('async1 end')
}

async function async2 () {
  console.log('async2')
}

console.log('script start')

setTimeout(function () {
  console.log('setTimeout')
}, 0)

async1();

new Promise (function (resolve) {
  console.log('promise1')
  resolve();
}).then (function () {
  console.log('promise2')
})

console.log('script end')
```

## Promise 面试题

```js
console.log("script start")

setTimeout(function () {
  console.log("setTimeout1");
  new Promise(function (resolve) {
    resolve();
  }).then(function () {
    new Promise(function (resolve) {
      resolve();
    }).then(function () {
      console.log("then4");
    });
    console.log("then2");
  });
});

new Promise(function (resolve) {
  console.log("promise1");
  resolve();
}).then(function () {
  console.log("then1");
});

setTimeout(function () {
  console.log("setTimeout2");
});

console.log(2);

queueMicrotask(() => {
  console.log("queueMicrotask1")
});

new Promise(function (resolve) {
  resolve();
}).then(function () {
  console.log("then3");
});

console.log("script end")
```

## 浏览器本地存储方式及使用场景

### Cookie

Cookie是最早被提出来的本地存储方式，在此之前，服务端是无法判断网络中的两个请求是否是同一用户发起的，为解决这个问题，Cookie就出现了。Cookie的大小只有4kb，它是一种纯文本文件，每次发起HTTP请求都会携带Cookie。

Cookie的特性：

- Cookie一旦创建成功，名称就无法修改
- Cookie是无法跨域名的，也就是说a域名和b域名下的cookie是无法共享的，这也是由Cookie的隐私安全性决定的，这样就能够阻止非法获取其他网站的Cookie
- 每个域名下Cookie的数量不能超过20个，每个Cookie的大小不能超过4kb
- 有安全问题，如果Cookie被拦截了，那就可获得session的所有信息，即使加密也于事无补，无需知道cookie的意义，只要转发cookie就能达到目的
- Cookie在请求一个新的页面的时候都会被发送过去

如果需要域名之间跨域共享Cookie，有两种方法：

1. 使用Nginx反向代理
2. 在一个站点登陆之后，往其他网站写Cookie。服务端的Session存储到一个节点，Cookie存储sessionId

Cookie的使用场景：

- 最常见的使用场景就是Cookie和session结合使用，我们将sessionId存储到Cookie中，每次发请求都会携带这个sessionId，这样服务端就知道是谁发起的请求，从而响应相应的信息。
- 可以用来统计页面的点击次数

### LocalStorage

LocalStorage是HTML5新引入的特性，由于有的时候我们存储的信息较大，Cookie就不能满足我们的需求，这时候LocalStorage就派上用场了。

LocalStorage的优点：

- 在大小方面，LocalStorage的大小一般为5MB，可以储存更多的信息
- LocalStorage是持久储存，并不会随着页面的关闭而消失，除非主动清理，不然会永久存在
- 仅储存在本地，不像Cookie那样每次HTTP请求都会被携带

LocalStorage的缺点：

- 存在浏览器兼容问题，IE8以下版本的浏览器不支持
- 如果浏览器设置为隐私模式，那我们将无法读取到LocalStorage
- LocalStorage受到同源策略的限制，即端口、协议、主机地址有任何一个不相同，都不会访问

LocalStorage的常用API

```javascript
// 保存数据到 localStorage
localStorage.setItem('key', 'value');

// 从 localStorage 获取数据
let data = localStorage.getItem('key');

// 从 localStorage 删除保存的数据
localStorage.removeItem('key');

// 从 localStorage 删除所有保存的数据
localStorage.clear();

// 获取某个索引的Key
localStorage.key(index)
```

LocalStorage的使用场景：

- 有些网站有换肤的功能，这时候就可以将换肤的信息存储在本地的LocalStorage中，当需要换肤的时候，直接操作LocalStorage即可
- 在网站中的用户浏览信息也会存储在LocalStorage中，还有网站的一些不常变动的个人信息等也可以存储在本地的LocalStorage中

### SessionStorage

SessionStorage和LocalStorage都是在HTML5才提出来的存储方案，SessionStorage 主要用于临时保存同一窗口(或标签页)的数据，刷新页面时不会删除，关闭窗口或标签页之后将会删除这些数据。

SessionStorage与LocalStorage对比

- SessionStorage和LocalStorage都在**本地进行数据存储**；
- SessionStorage也有同源策略的限制，但是SessionStorage有一条更加严格的限制，SessionStorage**只有在同一浏览器的同一窗口下才能够共享**；
- LocalStorage和SessionStorage**都不能被爬虫爬取**；

SessionStorage的常用API

```javascript
// 保存数据到 sessionStorage
sessionStorage.setItem('key', 'value');

// 从 sessionStorage 获取数据
let data = sessionStorage.getItem('key');

// 从 sessionStorage 删除保存的数据
sessionStorage.removeItem('key');

// 从 sessionStorage 删除所有保存的数据
sessionStorage.clear();

// 获取某个索引的Key
sessionStorage.key(index)
```

SessionStorage的使用场景

- 由于SessionStorage具有时效性，所以可以用来存储一些网站的游客登录的信息，还有临时的浏览记录的信息。当关闭网站之后，这些信息也就随之消除了。

## cookie、localStorage、sessionStorage的区别

cookie、localStorage、sessionStorage都是Web前端常用的存储数据的方式，它们之间的区别如下：

1、存储大小限制不同：

cookie的大小限制为4KB左右；localStorage的大小限制为5MB或更大（不同浏览器可能有所不同）；sessionStorage的大小限制也为5MB或更大（不同浏览器可能有所不同）。

2、数据生命周期不同：

cookie的生命周期由过期时间和路径控制，如果不设置过期时间，则cookie为会话级别（关闭浏览器时cookie即失效）；localStorage和sessionStorage的生命周期都为本地存储，localStorage的数据会永久保存，除非手动删除，而sessionStorage的数据在关闭浏览器时即被删除。

3、存储方式不同：

cookie的存储方式为字符串类型，可以在客户端和服务端之间传递；localStorage和sessionStorage的存储方式为键值对，只能在客户端使用。

4、作用范围不同：

cookie的作用范围为整个域名下的所有页面，包括子域名；localStorage和sessionStorage的作用范围为当前页面或当前窗口。

下面是一个简单的示例代码，用于演示cookie、localStorage和sessionStorage的使用：

```js
// 设置cookie
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2022 12:00:00 UTC; path=/";

// 获取cookie
let username = document.cookie;

// 设置localStorage
localStorage.setItem("username", "John Doe");

// 获取localStorage
let username = localStorage.getItem("username");

// 设置sessionStorage
sessionStorage.setItem("username", "John Doe");

// 获取sessionStorage
let username = sessionStorage.getItem("username");
```

> 在实际项目中，我们可以根据具体需求选择使用cookie、localStorage或sessionStorage来存储数据，以实现不同的功能。例如，可以使用cookie来记录用户的登录状态，使用localStorage来存储用户的个性化设置，使用sessionStorage来实现表单数据的临时存储等。

## localStorage、sessionStorage的区别

- 关闭网页后重新打开，localStorage会保留，而sessionStorage会被删除； 
- 在页面内实现跳转，localStorage会保留，sessionStorage也会保留； 
- 在页面外实现跳转（打开新的网页），localStorage会保留，sessionStorage不会被保留； 

localStorage和sessionStorage都是HTML5提供的客户端存储技术，可以在浏览器端保存数据。它们的区别在于：

1、数据的生命周期：localStorage中的数据可以长期存储，即使关闭浏览器也不会被清除，除非主动删除或清除缓存。而sessionStorage中的数据只能在当前会话中有效，一旦关闭浏览器窗口或标签页，数据就会被清除。

2、存储大小：localStorage和sessionStorage的存储大小是不同的，localStorage一般可以存储5MB的数据，而sessionStorage一般可以存储2.5MB的数据。

3、数据共享：localStorage中的数据可以在同一域名下的多个窗口、标签页、甚至不同的浏览器中共享。而sessionStorage中的数据只能在同一标签页或窗口中共享。

4、API使用：localStorage和sessionStorage使用的API基本相同，只是前缀不同，例如：localStorage.setItem()和sessionStorage.setItem()。

综上所述，localStorage适用于需要长期存储的数据，而sessionStorage适用于短期存储、不需要跨窗口或浏览器共享的数据。

## 正则表达式常见的规则练习

下表是关于 JavaScript 正则表达式的基本内容总结：

| 创建正则表达式               |                                        |
| ---------------------------- | -------------------------------------- |
| `new RegExp(pattern, flags)` | 使用构造函数创建正则表达式             |
| `/pattern/flags`             | 直接使用正则表达式字面量创建正则表达式 |

| 正则表达式方法 |                                                      |
| -------------- | ---------------------------------------------------- |
| `test(str)`    | 检测字符串是否匹配正则表达式，返回 `true` 或 `false` |
| `exec(str)`    | 检索字符串中指定的值，返回找到的值，并确定其位置     |

| 字符串方法                         |                                                              |
| ---------------------------------- | ------------------------------------------------------------ |
| `match(pattern)`                   | 在字符串中查找一个或多个与正则表达式匹配的文本。如果使用了 `g` 标志，则返回所有匹配的文本 |
| `matchAll(pattern)`                | 返回一个迭代器，该迭代器包含所有匹配的结果。如果没有匹配，则返回空迭代器 |
| `search(pattern)`                  | 在字符串中搜索指定正则表达式并返回第一个匹配项的位置         |
| `replace(pattern, replacement)`    | 替换与正则表达式匹配的子字符串。如果使用了 `g` 标志，则替换所有匹配的子字符串 |
| `replaceAll(pattern, replacement)` | 替换与正则表达式匹配的所有子字符串                           |
| `split(pattern)`                   | 使用正则表达式（或固定字符串）分割一个字符串并将分割后的字符串存储到数组中 |

| 修饰符 |                  |
| ------ | ---------------- |
| `g`    | 全局匹配         |
| `i`    | 不区分大小写匹配 |
| `m`    | 多行匹配         |

| 规则              | 描述                                   | 示例                                    |
| ----------------- | -------------------------------------- | --------------------------------------- |
| 字符类            |                                        |                                         |
| /d                | 匹配数字                               | /\d/匹配"123"中的1                      |
| /D                | 匹配非数字                             | /\D/匹配"abc"中的"a"                    |
| /s                | 匹配空白字符(空格、制表符、换行符等)   | /\s/匹配"hello  world"中的空格          |
| /S                | 匹配非空白字符                         | /\S/匹配"hello  world"中的"h"           |
| /w                | 匹配单词字符，包括下划线               | /\w/匹配"hello_world"中的"h"            |
| /W                | 匹配非单词字符                         | /\W/匹配"hello  world"中的" "           |
| .                 | 匹配除换行符以外的任意字符             | /h.llo/匹配"hello"中的"e"               |
| 锚点              |                                        |                                         |
| ^                 | 匹配字符串的开头                       | /^hello/匹配"hello world"中的"hello"    |
| $                 | 匹配字符串的结尾                       | /world$/匹配"hello world"中的"world"    |
| \b                | 匹配单词边界                           | /\bhello\b/匹配"hello world"中的"hello" |
| 转义字符          |                                        |                                         |
| \                 | 转义特殊字符                           | /\^hello/匹配"^hello"                   |
| 集合(Sets)        |                                        |                                         |
| []                | 匹配集合中的任意一个字符               | /[abc]/匹配"abc"中的"a"                 |
| [2,]              | 匹配大于等于2的数字                    | /[2-9]/匹配"123"中的"2"                 |
| [2,6]             | 匹配2到6之间的数字                     | /[2-6]/匹配"12345"中的"2"               |
| 量词(Quantifiers) |                                        |                                         |
| 数量{n}           | 匹配n个前面的字符                      | /hel{2}o/匹配"hello"中的"llo"           |
| 贪婪/惰性模式     |                                        |                                         |
| 贪婪模式          | 匹配规则会匹配到符合条件的最后一个内容 | /\d+/匹配"123456"中的"123456"           |
| 惰性模式          | 匹配到第一个符合规则的正则就返回       | /\d+?/匹配"123456"中的"1"               |
| 捕获组            |                                        |                                         |
| ()                | 将匹配到的内容作为一个分组             | /(\d+)/匹配"123abc"中的"123"            |
| (?:)              | 不希望括号中的内容出现在结果           |                                         |

# 📁 AJAX


## 服务端渲染和前后端分离的区别

服务端渲染和前后端分离是两种不同的Web应用程序架构方式。

一、SSR 服务端渲染

服务端渲染 (Server-Side Rendering，SSR) 是指在服务器端将应用程序的HTML、CSS、JavaScript等资源处理好后，将整个HTML页面返回给客户端浏览器。

这意味着服务器端会负责渲染页面的结构和内容，而客户端只需要负责渲染页面的交互部分，例如点击按钮等操作。因为服务器端已经处理好了页面内容，所以页面加载速度会比较快，而且对搜索引擎友好，可以提高SEO效果。

优点:

- 更快的响应时间，不用等待所有的js加载完成，也能显示比较完整的页面
- 更好的SEO，可以将SEO的关键信息直接在后台渲染成html，保证了搜索引擎能爬取到关键数据
- 无需占用客户端资源，解析模板交给后端工作，对于客户端的资源占用更少

缺点

- 占用服务器资源，一个小小的页面的改动，都需要请求一次完整的html页面，有悖于程序员的"DRY(Don\`t repeat yourself)"原则，如果短时间访问过多，对服务器造成一定的访问压力
- 一些常见的api需要先对运行环境判断再使用

二、前后端分离

前后端分离 (Front-end and Back-end Separation) 是指将应用程序的前端和后端分开开发，通过API接口进行通信。前端通常使用JavaScript框架（例如React、Vue、Angular等）来渲染页面，后端则负责处理业务逻辑和数据存储。前端和后端可以独立开发和部署，因此可以更好地实现团队协作和快速迭代。前后端分离的应用程序通常需要更多的网络请求和数据交互，因此可能会对性能和SEO产生一定的影响。

优点:

- 前端专注于ui界面的开发，后端专注于api的开发，职责单一
- 体验更好

缺点:

- 第一次响应内容较慢，不如服务端渲染快
- 不利于SEO优化，只是记录一个页面，对于SEO较差

## 前后端分离的优势

前后端分离是一种架构设计模式，将前端和后端的开发过程和技术栈分离开来。这种架构模式带来了许多优势，包括：

1. 独立开发：前后端分离使得前端和后端可以并行开发，各自专注于自己的领域。前端开发人员可以专注于用户界面和交互逻辑，后端开发人员可以专注于业务逻辑和数据处理。这提高了开发效率和团队合作。

2. 松耦合：前后端分离通过 API 接口进行通信，前后端之间的耦合度降低。前端和后端可以独立演化，可以使用不同的技术栈和框架。这样可以更灵活地进行技术选型和技术升级，而不会影响到整个系统。

3. 前端技术选型自由：前后端分离允许前端团队根据项目需求选择适合的前端技术栈和工具。前端开发人员可以使用流行的前端框架（如React、Angular、Vue.js等），并结合现代化的开发工具和工作流程，提高开发效率和用户体验。

4. 提升性能和扩展性：前后端分离允许将前端资源（如HTML、CSS、JavaScript文件）进行静态化和缓存，减少后端的负载和响应时间。前端资源可以通过 CDN 加速，提供更好的性能和用户体验。此外，通过增加多个前端实例和负载均衡，可以更好地应对高流量和扩展需求。

5. 多端适配：前后端分离使得后端提供的 API 可以被多个前端客户端使用，如网页、移动端应用、第三方应用等。这种多端适配能力为跨平台和跨设备的应用提供了更大的灵活性和可扩展性。

需要注意的是，前后端分离也存在一些挑战，如增加了系统复杂性、前后端接口设计和维护等方面的工作。此外，前后端分离并不适用于所有项目和场景，需要根据具体情况进行权衡和选择。


## 对HTTP协议的理解

### 一、HTTP

超文本传输协议（HyperText Transfer Protocol）：一种用于分布式协作式的应用层协议；

端口号：定义了客户端和服务器之间交换报文的格式和方式，默认为80端口；

传输层协议：使用tcp作为传输层协议，保证了数据的可靠性。

### 二、组成:

一个HTTP请求主要包括: 请求和响应

#### 1、请求（request）

主要包含: 包含响应行、响应头、响应体

（1）请求行:
- 请求方法字段
- URL字段
- HTTP协议版本字段
- `GET/index.html HTTP/1.1`

（2）请求头:
- 键值对组成
- User-Agent: 对应展示的浏览器的类型
- Content-type: 对应的请求内容的数据类型
  - application/x-www-form-urlencoded 数据以`&`分割的键值对，键值对用`=`分割
  - application/json json类型
  - application/xml xml类型
  - text/plain 文本类型
  - multipart/form-data 表示上传文件
- keep-alive

（3）请求体: get/post所带的内容

#### 2、响应（response）

（1）响应行：由协议版本、状态码、状态码的原因短语组成 `HTTP/1.1 200 OK`

（2）响应头：包含键值对组成，如Content-Type、Content-Length、Server等

（3）响应体：服务器返回的实体数据

### **三、请求方法：**

- `get` 向服务器获取数据
- `post` 将响应实体交给指定的资源
- `head` 请求一个与get请求响应相同的响应 没有实体
- `put` 上传文件，用于替换目标资源的所有
- `patch` 用于对资源的部分修改
- `delete` 删除指定的资源
- `connect` 建立一个到目标资源标识的服务器的隧道，通常用于代理服务器
- `track` 回显服务器收到的请求 主要用于测试和诊断

### 四、响应状态码

`200`表示请求被服务器端正常处理，

`201`表示POST请求创建新的资源，

`301`表示永久重定向，

`4xx`表示客户端发生错误，

- `400 Bad Request` 请求报文存在语法错误
- `401 Unauthorized` 未授权的错误，必须携带身份信息
- `403 Forbidden` 没有权限访问
- `404 Not Found` 服务器找不到请求资源

`5xx`表示服务器错误

- `500 Internal Server Error` 服务器内部错误
- `503 Service Unavailable` 服务器不可用，处于维护或重载状态


## DRY(Don`t repeat yourself) 原则

“DRY”（Don’t Repeat Yourself）是一种软件开发原则，也称为“不要重复自己”原则。这个原则的核心思想是避免重复的代码，减少代码的冗余和重复性，从而提高代码的可维护性、可读性、可复用性和可扩展性。

具体来说，“DRY”原则要求开发人员避免在代码中重复出现相同的逻辑或代码片段，而是将这些逻辑或代码片段抽象出来，封装成函数、类、模块或组件等可复用的代码块，这样可以减少代码量，提高代码的可读性和可维护性，同时也可以方便代码的复用和扩展。

遵循“DRY”原则可以提高代码的质量和效率，减少代码的错误和维护成本，使代码更加健壮和可靠。但是，有时候为了追求效率或特殊需求，可能需要牺牲一定的“DRY”原则，这需要在实际情况下进行权衡和取舍。


## AJAX最主要是用来干嘛的

AJAX是一种用于创建动态Web应用程序的技术。它允许Web页面在不刷新整个页面的情况下异步地向服务器请求数据，并更新页面的一部分。AJAX技术的出现大大提升了Web应用程序的用户体验，使得Web应用程序能够更像桌面应用程序一样快速、动态地响应用户操作。

具体来说，AJAX可以用来：

1、异步加载数据：通过AJAX，Web应用程序可以异步地加载数据，而不必刷新整个页面。

这使得Web应用程序更加快速和流畅，并且可以提供更好的用户体验。

2、动态更新页面：使用AJAX，Web应用程序可以在不刷新整个页面的情况下动态地更新页面内容。

例如，当用户提交表单时，可以使用AJAX将表单数据异步地发送到服务器进行处理，并更新页面的一部分，而不必刷新整个页面。

3、实现交互式用户界面：AJAX使得Web应用程序可以动态地更新页面内容，因此可以创建更加交互式的用户界面。

例如，可以使用AJAX实现自动完成搜索框、无限滚动、实时通讯等功能。

**总之，AJAX使得Web应用程序更加动态、交互式和流畅，提高了用户体验。**

## 客户端给服务器传递参数的四种方式

在客户端和服务器之间进行通信时，常用的传递参数的方式有以下四种：

方式一：GET请求的query参数

GET请求的query参数：这是通过URL的查询字符串将参数传递给服务器。查询字符串是位于URL末尾的问号后面的参数列表，每个参数用“&”符号分隔。例如，http://example.com/search?q=apple&category=fruit 中的查询字符串是“q=apple&category=fruit”。这种方式适合传递一些简单的参数，但是由于参数暴露在URL中，所以不适合传递敏感信息。

方式二：POST请求 x-www-form-urlencoded 格式 

POST请求 x-www-form-urlencoded 格式：这是通过表单数据的方式将参数传递给服务器，常见的场景是用户在网站上填写表单并提交。在POST请求中，表单数据通常被编码为x-www-form-urlencoded格式，即字段名和值之间用“=”符号分隔，不同字段之间用“&”符号分隔。服务器可以使用请求正文中的数据来获取这些参数。

方式三：POST请求 FormData 格式

POST请求 FormData 格式：这也是通过表单数据的方式将参数传递给服务器，不同的是它支持更多类型的数据，比如文件上传。FormData是一个包含键值对的对象，每个键值对表示一个表单字段和它的值。与x-www-form-urlencoded不同的是，使用FormData时不需要对数据进行编码，因为浏览器会自动进行处理。

方式四：POST请求 JSON 格式 

POST请求 JSON 格式：这种方式通常用于API接口，客户端会将请求参数封装成JSON格式的数据，并将其放入请求正文中发送给服务器。服务器在接收到请求后，需要从请求正文中解析JSON数据，然后读取其中的参数。这种方式适合传递比较复杂的数据结构，但是需要客户端和服务器都支持JSON数据的处理。

## AJAX网络请求封装

```js
// 练习hyajax -> axios
function hyajax({
  url,
  method = "get",
  data = {},
  timeout = 10000,
  headers = {}, // token
  success,
  failure
} = {}) {
  // 1.创建对象
  const xhr = new XMLHttpRequest()

  // 2.监听数据
  xhr.onload = function() {
    if (xhr.status >= 200 && xhr.status < 300) {
      success && success(xhr.response)
    } else {
      failure && failure({ status: xhr.status, message: xhr.statusText })
    }
  }

  // 3.设置类型
  xhr.responseType = "json"
  xhr.timeout = timeout

  // 4.open方法
  if (method.toUpperCase() === "GET") {
    const queryStrings = []
    for (const key in data) {
      queryStrings.push(`${key}=${data[key]}`)
    }
    url = url + "?" + queryStrings.join("&")
    xhr.open(method, url)
    xhr.send()
  } else {
    xhr.open(method, url)
    xhr.setRequestHeader("Content-type", "application/json")
    xhr.send(JSON.stringify(data))
  }

  return xhr
}
```

### Promise方式

```js
// 练习hyajax -> axios
function hyajax({
  url,
  method = "get",
  data = {},
  timeout = 10000,
  headers = {}, // token
} = {}) {
  // 1.创建对象
  const xhr = new XMLHttpRequest()

  // 2.创建Promise
  const promise = new Promise((resolve, reject) => {

    // 2.监听数据
    xhr.onload = function() {
      if (xhr.status >= 200 && xhr.status < 300) {
        resolve(xhr.response)
      } else {
        reject({ status: xhr.status, message: xhr.statusText })
      }
    }

    // 3.设置类型
    xhr.responseType = "json"
    xhr.timeout = timeout

    // 4.open方法
    if (method.toUpperCase() === "GET") {
      const queryStrings = []
      for (const key in data) {
        queryStrings.push(`${key}=${data[key]}`)
      }
      url = url + "?" + queryStrings.join("&")
      xhr.open(method, url)
      xhr.send()
    } else {
      xhr.open(method, url)
      xhr.setRequestHeader("Content-type", "application/json")
      xhr.send(JSON.stringify(data))
    }
  })

  promise.xhr = xhr

  return promise
}

// 使用
<script src="./utils/hyajax_promise.js"></script>
<script>
  const promise = hyajax({
    url: "http://123.207.32.32:1888/02_param/get",
    data: {
      username: "coderwhy",
      password: "123456"
    }
  })

  promise.then(res => {
    console.log("res:", res)
  }).catch(err => {
    console.log("err:", err)
  })
</script>
```


## XMLHttpRequest和Fetch请求的异同

XMLHttpRequest和Fetch都是在前端中用于发起HTTP请求的API，它们的主要区别在于使用方式和性能。

一、XMLHttpRequest

- XMLHttpRequest是早期用于前端发起HTTP请求的API，它可以通过JavaScript在后台发起HTTP请求，然后异步获取响应数据。
- 支持同步和异步请求，可以设置请求头、请求体、响应头等参数，具有一定的灵活性。
- 它的API设计相对较为复杂，需要写较多的代码，而且在处理跨域请求时需要特殊处理。

二、Fetch

- Fetch是ES6引入的新的API，它提供了一种更加现代、简洁的方式来处理HTTP请求。
- Fetch API使用Promise，返回一个值是`Promise` , 在请求成功时调用`resolve`回调
- 通过链式调用的方式来发起和处理请求，具有更加简单和易于理解的API设计，可以直接将响应数据转换为JSON对象或其他格式。
- 与XMLHttpRequest不同，不用把所有操作放在同一个对象上
- 语法简单，更加语义化
- 基于标准的promise实现，支持async/await
- Fetch API支持跨域请求，且不需要写额外的代码。
- Fetch API不支持同步请求，且在某些情况下需要手动处理HTTP错误。

三、Fetch缺点

- 不支持abort(超时取消请求)，不支持超时控制
- 没有办法检测请求进度，XHR可以
- 默认不会携带cookie

四、ajax缺点

- 使用起来比较繁琐

# 📁 Others




## JavaScript事件总线的作用

JavaScript事件总线是一种事件管理机制，它允许多个组件或模块之间通过触发和监听事件来通信。它提供了一种松散耦合的方式，让代码更加模块化和可重用。

事件总线的作用有以下几个方面：

1、解耦：事件总线能够将各个模块之间的通信解耦，使得模块之间的依赖关系更加简单和清晰。通过事件总线，模块之间可以独立开发和测试，而不必关心其他模块的实现细节。

2、简化：使用事件总线可以简化代码，减少重复性的代码。如果多个模块需要完成相同的任务，可以将这个任务封装成一个事件，并通过事件总线来触发和监听这个事件，避免多次编写相同的代码。

3、扩展：事件总线能够轻松地扩展功能，因为可以通过添加新的事件来增加功能，而不需要修改现有的代码。这样可以使得系统更加灵活和可扩展。

总之，JavaScript事件总线提供了一种灵活、松散耦合的方式来管理事件和组件之间的通信，从而使得代码更加模块化、可重用和可扩展。


## 工具函数封装成类的优点

将工具函数封装成类的主要优点如下：

1、可以更好地组织代码结构：将相关的功能封装到一个类中，可以更好地组织代码结构，使得代码更加清晰易懂，同时也方便维护和扩展。

2、提高代码的可重用性：将工具函数封装成类后，可以通过实例化对象来调用这些函数，从而提高了代码的可重用性，避免了代码的重复编写。

3、可以方便地共享数据：将工具函数封装成类后，可以通过类属性来共享数据，这样可以在不同的方法之间方便地传递数据。

4、支持面向对象编程的特性：将工具函数封装成类后，可以支持面向对象编程的特性，例如封装、继承、多态等，使得代码更加灵活和可扩展。

5、提高代码的可测试性：将工具函数封装成类后，可以更容易地进行单元测试和集成测试，因为可以针对类的每个方法进行测试，而不需要考虑函数之间的依赖关系。


## 说说你对防抖、节流的理解，他们的区别，应用场景(面试)

一、防抖 (Debounce)：

将多次执行函数变成最后一次执行，等待固定时间还没有事件触发时执行的函数

1、应用场景

- 按钮的点击
- 屏幕滚动时的复杂计算
- 输入框输入时进行搜索
- 用户缩放浏览器的resize事件

2、简单的防抖函数实现

```js
function myDebounce(execFn, delay) {
     let timer = 0
     
     function _debounce(...args) {
       if (timer) clearTimeout(timer)
       timer = setTimeout(() => {
         execFn.apply(this, args)
         timer = null
       }, delay)
     }
 
     return _debounce
}
```

二、节流 (Throttle) :

按照固定的时间频率(间隔)来执行对应的函数

1、应用场景:

- 监听页面的滚动事件，通过节流来降低事件调用的频率，减轻浏览器的负担。
- 鼠标移动
- 用户频繁点击按钮的操作，防止用户频繁点击按钮导致重复提交等问题。

2、简单实现

```js
function myThrottle(execFn, interval) {
    let initTime = 0

    function throttle(...args) {
      let nowTime = Date.now()
      const waitTime = interval - (nowTime - initTime)
      if (waitTime <= 0) {
        execFn.apply(this, args)
        initTime = nowTime
      }
    }
    return throttle
  }
```

三、它们的区别在于：

- 防抖是指在一定时间内只执行最后一次，而节流是指在一定时间内只执行一次。
- 防抖是在最后一次触发事件后等待一段时间再执行，而节流是在一段时间内等待执行。

四、应用场景：

- 防抖：比如在用户输入时，减少请求的次数，以减轻服务器压力。
- 节流：比如在监听滚动事件时，减少事件触发的次数，以减轻浏览器的负担。还可以应用在按钮的点击事件中，以防止用户频繁点击按钮导致重复提交等问题。


## 防抖和节流的原理

防抖和节流都是一种常用的前端优化技巧，它们的原理如下：

1、防抖：当一个函数被频繁触发时，只有在一定的时间间隔内最后一次触发才会执行。比如，在用户不断输入搜索关键字的时候，防抖可以确保只有用户停止输入后，才会发起搜索请求。

防抖的实现原理是，设置一个定时器，当函数被触发时，清除当前的定时器，并重新设置一个定时器。只有当定时器的时间到达后，才会执行函数。如果在这个时间内再次触发了函数，就会清除定时器，并重新设置。

2、节流：当一个函数被频繁触发时，每隔一定的时间间隔才会执行一次。比如，在滚动事件中，节流可以确保滚动事件不会被频繁触发，从而提高页面性能。

节流的实现原理是，设置一个时间戳变量，在函数执行时，判断当前时间与上次执行的时间是否超过了设定的时间间隔。如果超过了，就执行函数，并更新时间戳变量；否则，不执行函数。这样，就可以确保函数的执行间隔不会小于设定的时间间隔。


需要注意的是，防抖和节流都是通过延迟函数的执行来实现的，因此会造成一定的延迟。在具体应用时，需要根据实际情况选择合适的时间间隔。

## 说说对象的引用赋值、浅拷贝、深拷贝的区别

在 JavaScript 中，对象（包括数组和函数）的复制和传递是通过引用赋值来实现的。这意味着当你将一个对象复制给另一个变量或将其作为参数传递给一个函数时，实际上是将对原始对象的引用复制给了这个新的变量或函数参数。因此，在对这个新的变量或函数参数进行更改时，原始对象也会随之更改。

引用赋值、浅拷贝和深拷贝是处理 JavaScript 中对象赋值和复制时的三种不同方法。

### 一、引用赋值

引用赋值就是将一个对象的引用赋值给另一个变量，这两个变量将指向同一个对象。当其中任何一个变量修改对象时，另一个变量也会反映这个变化。

- 把源对象指向自身所在堆内存空间的指针给了新对象 两个对象所指向的内存空间是一样的 修改其中一个的值 另一个也会发生改变

示例如下：

```js
let obj1 = { name: 'Alice' };
let obj2 = obj1;

obj2.name = 'Bob';
console.log(obj1.name); // 输出 'Bob'
console.log(obj2.name); // 输出 'Bob'
```

### 二、浅拷贝

浅拷贝是指复制一个对象，创建一个新的对象，但是新对象中的属性和原始对象中的属性是相同的引用。这意味着，如果你更改了新对象中的某个属性，原始对象中相应的属性也会被更改。

- 可以通过`{...obj}`、`Object.assign({},obj)`的方式进行对象的浅拷贝；
- 对于obj中的值是原始数据类型的，将对应的值赋值给了newObj中对应的属性；
- 对于obj中是复杂数据类型的值，把对应在内存中的指针赋值给了newObj中对应的key，对于复杂数据类型的value修改其中一个另一个也发生改变。

示例如下：

```js
let obj1 = { name: 'Alice', age: 20 };
let obj2 = Object.assign({}, obj1);

obj2.name = 'Bob';
console.log(obj1.name); // 输出 'Alice'
console.log(obj2.name); // 输出 'Bob'

obj2.age = 30;
console.log(obj1.age); // 输出 20
console.log(obj2.age); // 输出 30

obj1.work = { company: 'ABC' };
let obj3 = Object.assign({}, obj1);

obj3.work.company = 'DEF';
console.log(obj1.work.company); // 输出 'DEF'
console.log(obj3.work.company); // 输出 'DEF'
```

从示例中可以看出，虽然 obj1 和 obj2 中的 name 和 age 属性互不影响，但是 obj1 和 obj3 中的 work 属性中的 company 属性值却是互相影响的。

### 三、深拷贝(真实开发中使用非常少)

深拷贝是指复制一个对象，创建一个新的对象，并且新对象中的属性与原始对象中的属性完全独立，修改新对象中的属性不会影响原始对象中的属性。

可以使用 JSON.parse(JSON.stringify(obj)) 或者使用递归实现深拷贝。

示例如下：

```js
let obj1 = { name: 'Alice', age: 20 };
let obj2 = JSON.parse(JSON.stringify(obj1));

obj2.name = 'Bob';
console.log(obj1.name); // 输出 'Alice'
console.log(obj2.name); // 输出 'Bob'

obj2.age = 30;
console.log(obj1.age); // 输出 20
console.log(obj2.age); // 输出 30

obj1.work = { company: 'ABC' };
let obj
```

缺点: 对于某些属性如 undefined,Symbol,function,Symbol 会自动忽略; 对于set map 会转成对象。

## JS作用域+this指向+原型考题

考题一：

```js
function Foo(){
    getName = function(){console.log(1)} //注意是全局的window.
    return this;
}

Foo.getName = function(){console.log(2)}
Foo.prototype.getName = function(){console.log(3)}
var getName = function(){console.log(4)}
function getName(){
    console.log(5)
}

Foo.getName();    //2
getName();      //4
Foo().getName();  //1
getName();      //1
new Foo().getName();//3
```

考题二：

```js
var o = {
a:10,
b:{
a:2,
fn:function(){
console.log( this.a ); // 2
console.log( this );   //代表b对象
}
}
}
o.b.fn();
```

考题三：

```js
window.name = 'ByteDance';
function A(){
this.name = 123;
}
A.prototype.getA = function(){
console.log( this );
return this.name + 1;
}
let a = new A();
let funcA = a.getA;
funcA();  //this代表window
```

考题四：

```js
var length = 10;
function fn(){
    return this.length + 1;
}
var obj = {
    length:5,
    test1:function(){
        return fn();
    }
}
obj.test2 = fn;
console.log( obj.test1() );//1
console.log( fn()===obj.test2() ); *//false*
console.log( obj.test1() == obj.test2() ); *//false*
```

## JS作用域考题

> 除了函数外，js是没有块级作用域。
> 作用域链：内部可以访问外部的变量，但是外部不能访问内部的变量。
> 注意：如果内部有，优先查找到内部，如果内部没有就查找外部的。
> 注意声明变量是用var还是没有写（window.）
> 注意：js有变量提升的机制【变量悬挂声明】
> 优先级：声明变量 > 声明普通函数 > 参数 > 变量提升
>
> **面试的时候怎么看：**
> 本层作用域有没有此变量【注意变量提升】
> 注意：js除了函数外没有块级作用域
> 普通声明函数是不看写函数的时候顺序

考题一：

```js
function c(){
 var b = 1;
 function a(){
     console.log( b );
     var b = 2;
     console.log( b );
 }
 a();
 console.log( b );
}
c();
```

考题二：

```js
var name = 'a';
(function(){
 if( typeof name == 'undefined' ){
     var name = 'b';
     console.log('111'+name);
 }else{
     console.log('222'+name);
 }
})()
```

考题三：

```js
function fun( a ){
 var a = 10;
 function a(){}
 console.log( a );
}
fun( 100 );
```

## 给字符串新增方法实现功能

问题？

给字符串对象定义一个addPrefix函数，当传入一个字符串str时，它会返回新的带有指定前缀的字符串，例如：

```js
console.log( 'world'.addPrefix('hello') ) // helloworld
```

解答

通过给字符串的原型对象String.prototype添加一个addPrefix()方法

```js
String.prototype.addPrefix("hello")
String.prototype.addPrefix = function(prefix) {
  return prefix + this;
}

// 示例用法
const str = 'world';
const newStr = str.addPrefix('hello ');
console.log(newStr); // 输出：hello world
```

注意！！！

注意，这种方式虽然可以实现要求，但是修改原型对象可能会带来一些潜在的问题，因为它会影响到所有的字符串对象。因此，在实际开发中，最好不要修改原型对象，而是将函数定义为一个独立的方法，通过传递参数来完成相应的操作。

## 找出字符串出现最多次数的字符以及次数

```js
function findMostFrequentChar(str) { // 定义函数，传入一个字符串参数
  const count = {}; // 创建一个空对象用于存储字符出现的次数
  let maxChar = ''; // 最大出现次数的字符
  let maxCount = 0; // 最大出现次数

  // 遍历字符串并统计字符出现次数
  for (let i = 0; i < str.length; i++) { // 遍历字符串中的每个字符
    const char = str.charAt(i); // 获取当前字符
    if (count[char]) { // 如果对象中已经存在该字符，表示出现过
      count[char]++; // 对该字符出现的次数进行累加
    } else { // 如果对象中不存在该字符，表示第一次出现
      count[char] = 1; // 初始化该字符出现的次数为1
    }
  }

  // 遍历统计结果并找出出现次数最多的字符以及次数
  for (const char in count) { // 遍历对象中的每个属性
    if (count[char] > maxCount) { // 如果该字符出现的次数大于最大出现次数
      maxChar = char; // 更新最大出现次数的字符
      maxCount = count[char]; // 更新最大出现次数
    }
  }

  return { // 返回结果对象
    char: maxChar, // 最大出现次数的字符
    count: maxCount // 最大出现次数
  };
}

// 示例用法
const str = 'abcaabbccaaaa'; // 声明一个字符串
const result = findMostFrequentChar(str); // 调用函数，传入字符串，获取结果对象
console.log(`出现最多的字符是 "${result.char}"，出现了 ${result.count} 次。`); // 输出结果字符串
```

## 面向函数、面向对象？

> 函数式编程（Functional Programming）和面向对象编程（Object-Oriented Programming）是两种不同的编程范式，它们各自具有不同的特点和优劣势。

一、函数式编程

一种以函数为核心的编程范式，它强调的是通过函数的组合和变换来完成程序的计算。函数式编程语言中的函数一般是无状态的，也就是说函数没有副作用，不会改变输入的参数，同时也不会改变程序的状态。这种编程方式可以帮助程序员更容易地编写出可靠、可复用、易于维护和并发执行的程序。

函数式编程强调的是将代码划分成一个个的函数，函数之间尽可能少的依赖和副作用，从而避免了代码中的许多常见问题，例如竞态条件和不确定性。函数式编程还支持高阶函数、闭包和柯里化等概念，这些概念可以让程序员以更简洁和优雅的方式表达他们的思想。

二、面向对象编程

与之相对的是面向对象编程，它的核心是对象，将数据和操作数据的函数封装在一起，形成一个完整的对象。面向对象编程语言的程序一般是有状态的，也就是说，它的状态是由对象的属性和方法决定的，而且对象的方法可以改变它的属性，从而改变程序的状态。面向对象编程可以帮助程序员更容易地建模复杂系统，并且可以将数据和相关的操作组织在一起，提高程序的可维护性和可重用性。

在某些情况下，面向对象编程则更适合表达现实世界中的事物和关系。面向对象编程强调的是将数据和相关操作封装在一起，通过对象之间的交互来完成任务。

三、两者关系

在实际开发中，函数式编程和面向对象编程并不是完全对立的，而是可以相互结合使用，形成一种更加灵活、高效的编程方式。比如，在函数式编程中，可以将一些常用的操作（如 map、reduce、filter 等）封装成高阶函数，然后在面向对象编程中使用这些函数来实现具体的业务逻辑。同时，在面向对象编程中，也可以使用函数式编程中的一些技术（如 Lambda 表达式、Stream API 等）来简化代码的编写和优化程序的性能。

在现代编程语言中，面向对象编程和函数式编程并不是相互排斥的，而是可以互相融合使用。例如在JavaScript中，ES6中的箭头函数和高阶函数就是函数式编程的典型应用，而ES6中的类则是面向对象编程的典型应用。在Vue 3和React中，虽然函数式编程得到了更多的支持，但面向对象编程的概念仍然存在，例如在React中，类组件和函数组件都可以用来定义组件。所以说，我们并不需要放弃面向对象编程，而是应该在不同的场景下，灵活地选择使用不同的编程范式。

四、发展趋势

最近几年，一些流行的编程框架似乎共同抵制面向对象编程，转向函数式编程，这种趋势让人有一种面向对象编程被抛弃的感觉。以React为例，最初声明组件时都是用类组件，但从React 16开始推出hooks后，可以直接用函数式声明组件，这种写法越来越受欢迎。另外，Vue 3的Composition API也几乎抛弃了Options API，推荐使用setup函数来声明组件。这种趋势似乎在整个编程社区都很流行，而面向对象编程的思维正在被慢慢抛弃，转向函数式编程。这种情况让人想到90年代JAVA面向对象编程盛行的时期，而如今函数式编程正在逐渐兴起。

## 延迟加载JS有哪些方式？

延迟加载 JavaScript 是一种优化网页加载速度的技术，可以在网页加载时推迟 JavaScript 文件的下载和执行时间。这可以减少网页的初始加载时间，因为 JavaScript 文件的下载和执行可能会阻塞 HTML 和 CSS 文件的渲染。

1、异步加载：

使用 `async` 属性可以异步加载 JavaScript 文件，这样文件可以在后台下载并执行，而不会阻塞网页的渲染。

```html
<script async src="main.js"></script>
```

2、延迟加载：

使用 `defer` 属性可以将 JavaScript 文件的下载推迟到网页的渲染完成后执行，这样可以确保文件不会阻塞网页的渲染。

```html
<script defer src="main.js"></script>
```

3、动态加载：

使用 JavaScript 代码动态创建   `<script>` 标签，并将其添加到网页中，这样可以在网页加载时动态加载 JavaScript 文件，而不需要在 HTML 中指定文件路径。

```js
var script = document.createElement('script');
script.src = 'main.js';
document.head.appendChild(script);
```

4、懒加载：

懒加载是一种技术，用于推迟加载某些元素（如图片或视频），直到用户滚动到它们的位置。这可以减少网页的初始加载时间，并改善用户体验。可以使用一些第三方库来实现懒加载功能。

> 需要注意的是，虽然延迟加载可以减少网页的初始加载时间，但过度使用可能会对网页性能产生负面影响。因此，建议仅在必要时使用延迟加载，并进行适当的测试和优化。

## 白屏加载时间过长优化

白屏加载时间指的是网页打开后到出现页面内容之前的时间，也就是所谓的“白屏时间”。优化白屏加载时间可以提高用户体验，降低用户的等待时间，增强网站的可用性。

以下是一些优化白屏加载时间的方法：

1. 减少 HTTP 请求：通过合并和压缩 CSS 和 JavaScript 文件、使用 CSS Sprites 和图像合并、删除不必要的资源等方式减少网页的 HTTP 请求次数。
2. 使用浏览器缓存：对于静态资源，比如 CSS 和 JavaScript 文件、图像等，可以设置缓存时间，让浏览器在下次请求相同的资源时从缓存中读取，从而减少 HTTP 请求次数，提高页面加载速度。
3. 延迟加载：对于非关键资源，可以将其延迟加载，等到页面主要内容加载完成后再加载。这可以减少页面的加载时间，并提高用户的体验。
4. 使用 CDN：使用内容分发网络（CDN）可以加速资源的下载，降低服务器负载，提高用户访问速度。
5. 压缩资源：可以使用 gzip 或其他压缩技术对资源进行压缩，从而减少资源的大小，加快下载速度。
6. 优化图像：使用适当的图像格式、尺寸和质量，可以减少图像的大小，加快下载速度。
7. 减少重定向：减少网站的重定向次数可以降低白屏时间。
8. 使用缓存技术：使用缓存技术，比如 Memcached 或 Redis，可以缓存一些常用的数据，从而提高网站的响应速度。

以上是一些常见的优化白屏加载时间的方法，可以根据具体情况选择适合自己网站的方法进行优化。

## 服务器获取到的数组，处理方式有哪些

服务器获取到的数组在前后端开发中非常常见，通常需要对其进行处理，以满足业务需求。以下是一些处理方式：

1. 遍历和过滤：遍历数组可以查找和处理其中的元素，过滤数组可以按照指定的条件筛选出符合要求的元素。
2. 排序：对数组进行排序可以按照指定的顺序重新排列数组中的元素。
3. 去重：通过去重操作可以从数组中删除重复的元素，得到一个去重后的新数组。
4. 分页：将大型数组按照页码和每页元素数量分成若干页，实现分页展示功能。
5. 连接和拆分：将多个数组连接成一个大数组，或者将一个数组拆分成多个小数组。
6. 聚合：对数组进行聚合操作，可以将数组中的元素按照一定的规则合并，得到一个新的聚合后的数组。
7. 映射和归约：通过映射和归约操作，可以将一个数组中的每个元素按照指定的规则转换成另一个值，或者将数组中的所有元素归约成一个值。
8. 统计和分析：通过统计和分析操作，可以对数组中的元素进行统计和分析，得到数组中元素的最大值、最小值、平均值、中位数等信息。

以上处理方式只是其中的一部分，具体处理方式还要根据具体的业务需求来选择。在实际开发中，常常会结合多种处理方式来对数组进行处理。

## 虚拟滚动原理

虚拟滚动是一种优化技术，用于处理大型列表或表格等UI组件中的性能问题。它的基本原理是只渲染可见部分的UI元素，而不是一次性渲染整个列表或表格。这可以显著提高应用程序的性能和响应速度，特别是当UI组件包含大量数据时。

虚拟滚动的原理可以分为以下几个步骤：

1. 计算可见区域

首先，需要计算出UI组件的可见部分。这通常涉及到计算组件的高度、宽度和滚动位置等参数。根据这些参数，可以确定可见的UI元素的数量和位置。

2. 渲染可见元素

接下来，需要将可见的UI元素渲染到屏幕上。这通常通过DOM操作来实现。在渲染过程中，只渲染可见区域内的元素，而不是一次性渲染整个列表或表格。

3. 动态调整渲染

一旦可见区域被渲染出来，需要动态地调整渲染以响应用户的滚动操作。当用户滚动列表或表格时，需要重新计算可见区域，并重新渲染可见元素。这可以通过监听滚动事件来实现。

4. 处理数据

在虚拟滚动中，只渲染可见的UI元素，并不是将整个数据集加载到内存中。因此，需要实现一种数据处理机制，以便在滚动时动态加载和卸载数据。通常，可以通过将数据划分为固定大小的块，然后动态加载和卸载块来实现这个机制。


总之，虚拟滚动是一种优化技术，通过只渲染可见的UI元素，从而提高了大型列表或表格等UI组件的性能和响应速度。它的基本原理包括计算可见区域、渲染可见元素、动态调整渲染和处理数据等步骤。

## 在你的项目中，你是如何处理跨域请求的？

因为浏览器的同源策略（ip，端口，协议需要一致），我们跨域请求的时候会出现跨域问题， 在开发环境中，我使用代理服务器（如vue.config.js中的proxy配置）解决跨域问题。在生产环境中，我是用nginx的代理解决跨域问题。当然也可以让后端在服务器端设置响应头，允许跨域请求。或者是用websocket，websocket没有跨域问题。

## 请谈谈你对前端性能优化的理解，以及在项目中采取了哪些措施来提升性能？

前端性能优化分为两类，一种是让文件加载更快，另一种是让文件渲染更快。

加载更快的方法

- 让传输的数据包更小（压缩文件/图片）：图片压缩和文件压缩
- 减少网络请求的次数：雪碧图/精灵图、节流防抖
- 减少渲染的次数：缓存（HTTP缓存、本地缓存、Vue的keep-alive缓存等）
- 使用CDN：利用内容分发网络（Content Delivery Network）加速静态资源的加载速度，将资源部署到离用户更近的服务器

文件渲染更快的方法

- 提前渲染：ssr服务器端渲染
- 避免渲染阻塞：CSS放在HTML的head中 JS放在HTML的body底部
- 避免无用渲染：懒加载
- 减少渲染次数：对dom查询进行缓存、将dom操作合并、减少重排重绘

## 前端性能优化有哪些

前端性能优化是指通过各种手段来提高网页的加载速度、交互速度和渲染速度，提升用户体验。以下是一些前端性能优化的技巧：

1. 减少 HTTP 请求：减少网页中的图片、样式表、脚本等文件的数量，可以减少网页的加载时间。
2. 压缩资源文件：使用压缩工具（如Gzip）压缩 CSS、JavaScript、HTML 等文件，可以减小文件大小，从而提高加载速度。
3. 启用浏览器缓存：通过设置HTTP缓存头，让浏览器缓存网页资源，可以避免重复下载相同的资源，从而提高加载速度。
4. 延迟加载：通过将一些非必要的资源，如图片、JavaScript 等延迟加载，可以提高页面的加载速度。
5. 使用 CDN：使用 CDN（内容分发网络），可以加快资源文件的下载速度，从而提高网页的加载速度。
6. 减小 DOM 操作：减小DOM操作的次数和复杂度，可以提高渲染速度。
7. 使用缓存技术：通过使用缓存技术（如 LocalStorage 和 SessionStorage）可以减少网络请求，提高页面渲染速度。
8. 减少重排和重绘：通过减少DOM操作和使用CSS动画代替JavaScript动画，可以减少页面的重排和重绘，提高页面渲染速度。
9. 使用雪碧图：将多个小图标合并成一个雪碧图，可以减少HTTP请求次数，从而提高页面加载速度。
10. 使用Web Workers：使用Web Workers可以将一些耗时的任务分配到不同的线程，避免阻塞主线程，提高页面渲染速度。

## 是否可以在JS中执行301重定向

答案：否

### 301和302是什么？

> **301，永久重定向**：在请求的URL已被移除时使用，响应的location首部中应包含资源现在所处的URL
> **302，临时重定向**：和永久重定向类似，客户端应用location给出URL临时定位资源，将来的请求仍为原来的URL。

### 为什么不行？

JS完全运行在客户端上。301是服务器作为响应发送的响应代码。因此，客户端的JS不可能执行301重定向.

但是客户端可以执行简单的跳转，只能不能设置301状态码，代码如下：

```js
// 假设旧域名为 www.a.com 新域名为 www.b.com 
if (document.domain =='www.a.com') 
this.location = "http://www.b.com" + 
this.location.pathname + this.location.search;

```

> 另一方面，服务端的Node.js是可以做301重定向的，如下

```js
const http = require('http'); 
const server = http.createServer((req, res) => {
// 设置响应状态码 
res.statusCode = 301; 
// 响应头设置新地址 
res.setHeader('Location', 'http://www.a.com'); res.end(); }); 

server.listen(3000, () => console.log('server running...')

```

## 惰性求值

惰性求值（Lazy Evaluation）是一种延迟计算的方式，只有在需要时才会进行计算。它的主要优点是可以节省计算资源，提高程序的性能和效率。

惰性求值通常用于函数式编程中，比如在 JavaScript 中使用的柯里化（Currying）和函数组合（Function Composition）技术。它们都可以通过惰性求值来避免不必要的计算，从而提高程序的效率和可读性。

举个例子，假设有一个函数 `add`，它接收两个数字参数并返回它们的和。现在有一个数组 `arr`，包含很多数字，我们需要将这些数字相加并返回它们的总和，可以这样实现：

```javascript
function add(a, b) {
  return a + b;
}

function sum(arr) {
  return arr.reduce(add, 0);
}

const result = sum([1, 2, 3, 4, 5]); // 15
```

这个实现方式使用了 `reduce` 函数来对数组中的数字进行求和，但是它会立即对数组中的每一个数字进行计算，即使有些数字在后续的计算中并不会被用到。如果数组很大，这样的计算量就会非常大，影响程序的性能。

使用惰性求值，我们可以将计算延迟到真正需要的时候再进行。这可以通过使用函数来实现，比如使用柯里化和函数组合技术：

```javascript
function add(a) {
  return function(b) {
    return a + b;
  };
}

function sum(arr) {
  return arr.map(add).reduce(function(a, b) {
    return a(b);
  }, 0);
}

const result = sum([1, 2, 3, 4, 5]); // 15
```

这个实现方式使用了柯里化和函数组合技术，将计算过程分为两步：第一步是将每个数字都转换为一个函数，这个函数接收一个数字参数并返回它和原来的数字相加的结果；第二步是使用 `reduce` 函数将这些函数组合起来并计算它们的总和。在第二步中，每个函数都只会在需要时才会被调用，避免了不必要的计算。

## preload 和 prefetch 的应用场景？

**1、webpack优化之preload和prefetch**

单页面应用由于页面过多，可能会导致代码体积过大，从而使得首页打开速度过慢。所以切分代码，优化首页打开速度尤为重要。

但是所有的技术手段都不是完美的。当我们切割代码后，首页的js文件体积减少了好多。但是也有一个突出的问题：

那就是当跳转其他页面的时候，需要下载相应页面的js文件，这就导致体验极其不好，每一次点击访问新页面都要等待js文件下载，然后再去请求接口获取数据。频繁出现loading动画的体验真的不好。

所以如果我们在进入首页后，在浏览器的空闲时间提前下好用户可能会点击页面的js文件，这样首页的js文件大小得到了控制，而且再点击新页面的时候，相关的js文件已经下载好了，就不再会出现loading动画。

**2、动态引入js文件，实现code-splitting，减少首页打开时间，**

按需引入，只需添加注释即可。

- 代码分割注释：`/* webpackChunkName: 'mp-supports' */`
- prefetch注释：`/* webpackPrefetch: true */`

更多的，可以查看[webpack注释黑魔法](https://webpack.js.org/api/module-methods/#magic-comments)

使用案例：

```js
const { default: lodash } = await import(/* webpackChunkName: "lodash" */ /* webpackPrefetch: true */ 'lodash');

// Multiple possible targets
import(
    /* webpackInclude: /\.json$/ */
    /* webpackExclude: /\.noimport\.json$/ */
    /* webpackChunkName: "my-chunk-name" */
    /* webpackMode: "lazy" */
    /* webpackPrefetch: true */
    /* webpackPreload: true */
    `./locale/${language}`
);
```


## prefetch 与 preload 的区别是什么?

`prefetch`和`preload`是两种预加载资源的方式，都可以提高网站性能，但它们有着不同的使用场景和行为。

一、preload

- preload 是一个声明式 fetch，可以强制浏览器在不阻塞 document 的 onload 事件的情况下请求资源。
- preload 顾名思义就是一种预加载的⽅式，它通过声明向浏览器声明一个需要提前加载的资源，当资源真正被使用的时候⽴即执⾏，就无需等待⽹络的消耗。

`preload`用于预加载当前页面所需的资源，例如CSS、JavaScript、字体等。它告诉浏览器在加载页面之前先加载指定的资源，以便在页面加载完成后能够立即使用。

使用`preload`可以加快页面加载速度和响应时间，但是需要注意，过多的`preload`请求可能会降低性能和资源利用率。

示例：

```js
<link rel="preload" href="style.css" as="style">
<script src="script.js" rel="preload"></script>
```

二、prefetch

- 告诉浏览器这个资源将来可能需要，但是什么时间加载这个资源是由浏览器来决定的。
- 若能预测到用户的⾏为，⽐如懒加载，点击到其它⻚⾯等则相当于提前预加载了需要的资源。

`prefetch`用于预加载将来可能需要的资源，例如下一页的HTML、图像、视频等。它告诉浏览器在当前页面加载完成后预加载指定的资源，以便在用户浏览到下一页时可以立即使用。

使用`prefetch`可以提高网站的整体性能和用户体验，但是需要注意，过多的`prefetch`请求可能会占用过多的网络带宽和系统资源。

示例：

```js
<link rel="prefetch" href="next-page.html">
<link rel="prefetch" href="image.jpg">
```

需要注意的是，`preload`和`prefetch`不是万能的解决方案，需要根据具体的使用场景和需求来选择合适的方式。同时，也需要注意不要滥用这两种方式，以免影响性能和用户体验。