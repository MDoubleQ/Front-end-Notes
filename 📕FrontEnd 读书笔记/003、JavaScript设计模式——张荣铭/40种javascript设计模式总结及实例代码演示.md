## 什么是设计模式？

一个模式就是一个可重用的方案，可应用于在软件设计中的常见问题。另一种解释就是一个我们如何解决问题的模板 - 那些可以在许多不同的情况里使用的模板。

- 设计模式是我们在 解决问题的时候针对特定问题给出的简洁而优化的处理方案
- 在 JS 设计模式中，**最核心的思想：封装变化。**
- 将变与不变分离，确保变化的部分灵活、不变的部分稳定。

没必要完全去套设计模式，而是去理解它们共同的思想，保持初心--**提升代码的可读性、可扩展性、可维护性**，最终达到「还记着没有，我现在全忘了，忘得干干净净的了」的境界。

## 23 种设计模式（曾探）

## 七项基本原则

设计一些设计模式时，一般遵循如下七项基本原则。

1. 单一职责原则 (Single Responsibility Principle)
2. 开放-关闭原则 (Open-Closed Principle)
3. 里氏替换原则 (Liskov Substitution Principle)
4. 依赖倒转原则 (Dependence Inversion Principle)
5. 接口隔离原则 (Interface Segregation Principle)
6. 最少知道原则（The Least Knowledge Principle）
7. 组合/聚合复用原则 (Composite/Aggregate Reuse Principle)

这些原则里，我认为比较实用而且很重要的是：

- 单一职责原则、
- 开放-关闭原则、
- 最少知道原则。

## 本书设计模式的分类：

创建型设计模式： 1、简单工厂模式 2、工厂方法模式 3、抽象工厂模式 4、建造者模式 5、原型模式 6、单例模式

结构型设计模式： 7、外观模式 8、适配器模式 9、代理模式 10、装饰者模式 11、桥接模式 12、组合模式 13、享元模式

行为型设计模式： 14、模板方法模式 15、观察者模式 16、状态模式 17、策略模式 18、职责链模式 19、命令模式 20、访问者模式 21、中介者模式 22、备忘录模式 23、迭代器模式 24、解释器模式

技巧型设计模式： 25、链模式 26、委托模式 27、数据访问对象模式 28、节流模式 29、简单模板模式 30、惰性模式 31、参与者模式 32、等待者模式

架构型设计模式： 33、同步模块模式 34、异步模块模式 35、Widget模式 36、MVC模式 37、MVP模式 38、MVVM模式

备注：该分类借鉴于《JavaScript设计模式-张容铭》

## 前言

讲设计模式的书很多，但是专讲js设计模式的书不多，比较著名的就是曾琛老师的《javascript设计模式与开发实践》，里面讲了14种javascript设计模式以及这些设计模式所遵循的几大编码原则。

无意中发现了百度张容铭的《javascript设计模式》一书，竟然讲了40种设计模式。

尽管也同意曾琛老师说的，由于js中本来一切都是对象，所以有些其他语言需要使用某种设计模式解决的问题，可能在js中并不需要使用这种模式就能解决问题。比如用来创建对象的工厂模式。但是如果我们能使用js去完成这些设计模式的编写，那也没坏处，它可以使我们建立起一种超越具体编程语言的编程思维。

另外，这本书中很多代码中都有值得学习的书写规范、编码技巧及编码思想，还是能够受益匪浅的。

张的这本书好的一点是，每一种设计模式都是结合具体的应用场景来编写的，并且但凡有代码实现的地方，几乎每一行代码都事无巨细地加了注释，这是我在其他技术类书籍中很罕见到的，简直佩服。

而缺点也很明显，这本书的校验工作不甚认真，有很多代码有错误之处，另外很多代码示例省略了html页面相关的实现。

所以——我抄书了！不过我不觉得抄书可耻，从学习编程的第一天，我就秉持着一个理念：学习过程中的所有代码，只有自己敲一遍，才算学过（甚至这样都只能达到基本理解而非学懂）。

本文下面对书中40种设计模式的总结，我还完成了书中所有代码示例的实现，对书中的错误进行了修正，补全了所有作者省略掉的代码，保证每一个示例都可以在node环境或者浏览器页面或者浏览器控制台可以看到演示效果。

具体请看这个github仓库： [javascript_Pattern](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fhjb2722404%2Fjavascript-Pattern)

希望可以帮助到需要的同学。
## 开篇 从函数到对象

> 从函数到对象

本节课围绕实现一个验证用户输入的用户名、邮箱、密码的功能，从函数逐渐到对象，使用了多种不同方式去实现，并总结了各种方式的特点。

### 01：函数式编程实现

```js
function checkForm() {
  checkName(), checkEmail(), checkPassword();
}

function checkName() {
  var nameEl = document.getElementById("name").value;
  if (!nameEl) {
    alert("Please input the corrent user name!");
    return false;
  }
}

function checkEmail() {
  var emailEl = document.getElementById("email").value;
  if (!emailEl) {
    alert("Please input the corrent email!");
    return false;
  }
}

function checkPassword() {
  var password = document.getElementById("password").value;
  if (!password) {
    alert("Please input the correct password!");
    return false;
  }
}

```

返回 `false` 可以用于阻止表单提交。当某个输入框的数据不合法时，调用对应的检查函数并在其中弹出警告框是一种常见的做法。在弹出警告框后，如果函数返回 `false`，那么表单就不会提交，这样就可以让用户有机会更正错误的输入。

缺点：

1、全局变量空间污染：在当前示例中，`checkName()`、`checkEmail()` 和 `checkPassword()` 函数中使用了局部变量 `nameEl`、`emailEl` 和 `password`，但它们都没有使用 `var`、`let` 或 `const` 关键字进行声明，因此它们都成为了全局变量，污染了全局变量空间。这可能导致变量命名冲突和意外的副作用。

2、缺乏代码组织性：当前示例中的函数定义是分散的，难以维护和管理。在 `checkForm()` 函数中直接调用 `checkName()`、`checkEmail()` 和 `checkPassword()` 函数，导致代码逻辑分散并且难以追踪。

### 02：用对象字面量给对象添加方法

对象式定义、点语法调用

```js
let check = {
  name() {
    let nameValue = document.getElementById("name").value;
    if (!nameValue) {
      alert("Please input the corrent user name");
      return false;
    }
  },
  email() {
    let emailValue = document.getElementById("email").value;
    if (!emailValue) {
      alert("Please input the corrent email");
      return false;
    }
  },
  password() {
    let passwordValue = document.getElementById("password").value;
    if (!passwordValue) {
      alert("Please input the corrent password");
      return false;
    }
  },
};

function checkForm() {
  check.name();
  check.email();
  check.password();
}
```

缺点：可扩展性和可维护性较差，无法复用和继承（即无法用new关键字复制出一个相同的对象）

1. 缺乏封装性：上述代码中，验证逻辑直接以对象字面量的形式暴露在外部，没有封装在一个独立的对象或类中。这导致代码缺乏封装性，难以进行模块化和重用。
2. 代码耦合度高：所有的验证逻辑都耦合在同一个对象 `check` 中，导致它们之间紧密关联。一旦需要修改其中一个验证方法，可能会影响其他验证方法的功能。这增加了代码的脆弱性和难以维护性。
3. 难以扩展和定制：如果需要添加更多的验证规则或修改现有的规则，需要直接修改 `check` 对象中的方法。这种直接修改的方式可能会导致代码的不稳定和破坏现有功能。

### 03：使用点语法来给对象添加方法

同上，只不过定义时使用函数，添加方法时使用对象语法；

```js
function checkForm() {
  check.name(), check.email(), check.password();
}

let check = {};
check.name = function () {
  let nameValue = document.getElementById("name").value;
  if (!nameValue) {
    alert("Please input the corrent user name");
    return false;
  }
};
check.email = function () {
  let emailValue = document.getElementById("email").value;
  if (!emailValue) {
    alert("Please input the corrent email");
    return false;
  }
};
check.password = function () {
  let passwordValue = document.getElementById("password").value;
  if (!passwordValue) {
    alert("Please input the corrent password");
    return false;
  }
};
```

### 04：用函数方法返回包装对象

调用方法：先利用函数返回一个对象，再调用该对象的方法

```js
let checkObject = () => {
  return {
    checkName() {
      let nameValue = document.getElementById("name").value;
      if (!nameValue) {
        alert("Please input the corrent user name");
        return false;
      }
    },
    checkEmail() {
      let emailValue = document.getElementById("email").value;
      if (!emailValue) {
        alert("Please input the corrent user email");
        return false;
      }
    },
    checkPassword() {
      let passwordValue = document.getElementById("password").value;
      if (!passwordValue) {
        alert("Please input the corrent user password");
        return false;
      }
    },
  };
};

function checkForm() {
  let a = checkObject();
  a.checkName();
  a.checkEmail();
  a.checkPassword();
}
```

缺点**：**返回的对象与定义的对象没有关联【无法同步】，这些方法是在每次调用 `CheckObject` 函数时动态创建的，因此每个新对象都具有不同的标识符。虽然这些方法具有相同的名称，但它们是==通过不同的对象引用来访问的==。

如果在多个地方调用`CheckObject()`函数并使用其返回的对象进行检查，不同地方的返回对象是不一样的，而且也无法共享数据或状态。

此外，如果`CheckObject`需要维护一些私有数据或状态，这种模式也无法实现。

### 05：使用类的方式：构造函数（使用this赋值）

使用 this 定义实例方法，使用 new 创建新对象

```js
let CheckObject = function() {
  this.checkName = function() {
    let name = document.getElementById('name').value
    if(!name){
      alert("Please input the corrent name")
      return false
    }
  },
  this.checkEmail = function() {
    let email = document.getElementById("email").value
    if(!email){
     alert("Please input the corrent email")
      return false
    }
  },
  this.checkPassword = function() {
    let password = document.getElementById("password").value
    if(!password){
      alert("Please input the corrent password")
      return false
    }
  }
}

function checkForm() {
  let a = new CheckObject()
  a.checkName()
  a.checkEmail()
  a.checkPassword()
}
```

缺点：

1. 内存浪费：每次调用 `checkForm()` 函数时都会创建一个新的 `CheckObject` 对象，而这个对象内部的 `checkName()`, `checkEmail()`, `checkPassword()` 方法是相同的。这意味着每次验证都会创建新的方法对象，浪费了内存资源。
2. 代码冗余：`CheckObject` 对象的每个方法都是在实例化对象时创建的。如果在多个地方需要进行表单验证，每次都需要实例化 `CheckObject` 对象，这会导致代码冗余。
3. 对象方法不可复用：这种方式下，`CheckObject` 对象的方法仅在 `checkForm()` 函数中被调用，无法在其他地方复用。如果其他部分需要使用相同的验证逻辑，就需要重新实例化 `CheckObject` 对象或复制方法代码，增加了重复编写代码的风险。
4. 不符合面向对象的设计原则：`CheckObject` 对象的每个方法都是通过 `this` 关键字定义的，这意味着每个实例对象都拥有独立的方法副本。然而，这些方法的功能是相同的，没有必要为每个对象实例都创建一份相同的方法。

### 06：使用类的方式：构造函数（使用原型赋值）

- 使用原型赋值，避免类的共用属性和方法被重复实例化赋值，减少性能开销

```js
// 这里定义一个函数
let CheckObject = function () {};
CheckObject.prototype.checkName = function () {
  let name = document.getElementById("name").value;
  if (!name) {
    alert("Please input the corrent name");
    return false;
  }
};
CheckObject.prototype.checkEmail = function () {
  let email = document.getElementById("email").value;
  if (!email) {
    alert("Please input the corrent email");
    return false;
  }
};
CheckObject.prototype.checkPassword = function () {
  let password = document.getElementById("password").value;
  if (!password) {
    alert("Please input the corrent password");
    return false;
  }
};

// 用分号分隔
function checkForm() {
  let a = new CheckObject();
  a.checkName();
  a.checkEmail();
  a.checkPassword();
}
```

缺点：每一个方法都要写一次prototype，太多重复

### 07：使用类的方式：构造函数（使用原型对象赋值）

- 不用每个方法都写prototype,只需要写一次，以原型对象的方式一次性赋值；

```js
let CheckObject = function () {};

CheckObject.prototype = {
  checkName() {
    let name = document.getElementById("name").value;
    if (!name) {
      alert("Please input the corrent name");
      return false;
    }
  },
  checkEmail() {
    let email = document.getElementById("email").value;
    if (!email) {
      alert("Please input the corrent email");
      return false;
    }
  },
  checkPassword() {
    let password = document.getElementById("password").value;
    if (!password) {
      alert("Please input the corrent password");
      return false;
    }
  },
};

function checkForm() {
  let a = new CheckObject();
  a.checkName();
  a.checkEmail();
  a.checkPassword();
}
```

缺点：会重写类的prototype属性，导致 constructor 属性丢失

### 08：使用类的方式：构造函数（使用原型对象赋值）--实现链式调用

- 每个方法都返回 this （即实例对象自身）来实现链式调用

```js
let CheckObject = function () {};

CheckObject.prototype = {
  checkName: function () {
    let name = document.getElementById("name").value;
    if (!name) {
      alert("Please input the correct name");
      // change
      return this;
    }
+   return this;
  },
  checkEmail: function () {
    let email = document.getElementById("email").value;
    if (!email) {
      alert("Please input the correct email");
      // change
      return this;
    }
+   return this;
  },
  checkPassword: function () {
    let password = document.getElementById("password").value;
    if (!password) {
      alert("Please input the correct password");
      // change
      return this;
    }
+   return this;
  },
};

function checkForm() {
  let a = new CheckObject();
  // change
  a.checkName().checkEmail().checkPassword();
  // 执行其他操作，因为所有验证都通过了
  alert("All validations passed. Submitting the form...");
}
```

### 9、使用了 ES6 的类 (`class`) 来创建 `FormValidator` 类

```js
class CheckObject {
  checkName() {
    let name = document.getElementById("name").value;
    if (!name) {
      alert("Please input the correct name");
      return false;
    }
  }

  checkEmail() {
    let email = document.getElementById("email").value;
    if (!email) {
      alert("Please input the correct email");
      return false;
    }
  }

  checkPassword() {
    let password = document.getElementById("password").value;
    if (!password) {
      alert("Please input the correct password");
      return false;
    }
  }
}

function checkForm() {
  let a = new CheckObject();
  a.checkName();
  a.checkEmail();
  a.checkPassword();
}
```

这种优化后的代码具有以下优点：

1. 采用了现代的类语法，代码更加简洁和易读。
2. 使用类的实例方法，使得方法共享同一个实现，节省了内存空间。
3. 代码结构清晰，类的职责明确。
4. 可以方便地添加新的检查方法，扩展性强。
5. 遵循了面向对象的设计原则，代码更加可维护和可扩展。

## 第一篇 面向对象基础

> 面向对象编程基础

### 01：类的属性与方法封装

私有属性（Private Properties）：在类内部使用 `var`、`let` 或 `const` 关键字定义的属性，无法通过类的实例对象或外部访问，仅在类的内部可见。

私有方法（Private Methods）：在类内部定义的函数，无法通过类的实例对象或外部直接调用，仅在类的内部可调用。

实例属性（Instance Properties）：通过在构造函数内部使用 `this` 关键字定义的属性，每个类的实例对象都拥有自己的副本，并且可以通过实例对象的点语法访问。

实例方法（Instance Methods）：通过在构造函数内部使用 `this` 关键字定义的方法，每个类的实例对象都拥有自己的副本，并且可以通过实例对象的点语法调用。

特权方法（Privileged Methods）：通过在构造函数内部使用 `this` 关键字定义的方法，特权方法可以访问私有属性，并且可以通过实例对象的点语法调用。特权方法常用于提供对私有属性的安全访问和修改。

构造函数（Constructor）：用于创建类的实例对象的函数，通过 `new` 关键字调用。构造函数中定义了实例属性和实例方法。

静态属性（Static Properties）：在类内部使用 `static` 关键字或类/构造函数的名称直接定义的属性，不属于实例对象，而是属于类本身，可以通过类的名称访问。

- 使用类的名称直接定义静态属性：

```javascript
class MyClass {
  static staticProperty = "Static Property";
}

console.log(MyClass.staticProperty); // 输出："Static Property"
```

- 使用 `static` 关键字定义静态属性：

```javascript
class MyClass {
  static staticProperty;
}

MyClass.staticProperty = "Static Property";

console.log(MyClass.staticProperty); // 输出："Static Property"
```

- 使用构造函数函数对象直接定义静态属性：

```javascript
function MyClass() {
  // 构造函数内部直接定义静态属性
}

MyClass.staticProperty = "Static Property";

console.log(MyClass.staticProperty); // 输出："Static Property"

// 这些方法都可以用来定义类的静态属性，它们将属性直接关联到类本身，而不是类的实例对象。通过类的名称或类本身，你可以访问和使用这些静态属性。
```

静态方法（Static Methods）：在类内部使用 `static` 关键字或类/构造函数的名称直接定义的方法，不属于实例对象，而是属于类本身，可以通过类的名称调用。

- 使用类的名称直接定义静态方法：

```js
class MyClass {
  static staticMethod() {
    console.log("Static Method");
  }
}

MyClass.staticMethod(); // 输出："Static Method"
```

- 使用 `static` 关键字定义静态方法：

```js
class MyClass {
  static staticMethod() {
    console.log("Static Method");
  }
}

MyClass.staticMethod(); // 输出："Static Method"
```

公有属性（Public Properties）：通过在类的原型对象上添加的属性，所有实例对象通过原型链访问时可以获取到相同的值。

公有方法（Public Methods）：通过在类的原型对象上添加的方法，所有实例对象通过原型链访问时共享同一个方法实现，不会重复创建。

```js
function Person(name, age) {
  // 私有属性
  let privateName = name;
  
  // 私有方法
  function privateMethod() {
    console.log("This is a private method");
  }
  
  // 特权方法
  this.getPrivateName = function() {
    return privateName;
  };
  
  // 实例方法
  this.greet = function() {
    console.log("Hello, my name is " + privateName + " and I am " + age + " years old.");
  };
}

// 静态属性
Person.staticProperty = "Static Property";

// 静态方法
Person.staticMethod = function() {
  console.log("This is a static method");
};

// 公有属性
Person.prototype.publicProperty = "Public Property";

// 公有方法
Person.prototype.publicMethod = function() {
  console.log("This is a public method");
};
```

### 02：利用闭包实现类的静态属性

- 利用闭包添加类的静态私有属性和静态私有方法
- 缺点：在闭包外部利用原型添加静态公有属性和方法，从形式上看似脱离了闭包这个类

```js

```

### 03：在闭包内部实现一个完整的类

- 这样实现，类的定义和与原型添加静态公有属性和方法都在同一个闭包内，更像一个整体

```js

```

### 04：创建对象的安全模式

- 利用 instanceof 方法类判断是否使用 new 关键字
- 可以保证忘记写 new 的时候也能正常实例化对象

```js
const Book = function (name, time, type) {
  if (this instanceof Book) {
    this.name = name;
    this.time = time;
    this.type = type;
  } else {
    return new Book(name, time, type);
  }
};

const book3 = Book("You don't know JavaScript", "2005", "JavaScript");
console.log(book3);
/*
Book {
  name: "You don't know JavaScript",
  time: '2005',
  type: 'JavaScript'
} 
*/
```

### 05：类式继承

- 将父类的实例赋值给子类的原型
- 如果父类中的共有属性是引用类型，则子类的一个实例更改该继承过来的共有属性，就会直接影响到其他子类实例
- 实例化父类时无法对父类构造函数进行初始化

```js

```



### 06：构造函数继承

- 利用call来更改子类执行环境为父类，利用绑定的this，子类继承了父类的共有属性。
- 使用此种方法，继承没有涉及子类的原型，所以父类的原型方法自然不会被子类继承。
- 如果想被子类继承就必须要放在构造函数中
- 每个实例都会单独拥有一份，不能共有，违背了代码复用原则。

```js

```



### 07：组合继承

- 综合两种继承方式的优点，过滤掉缺点
- 缺点：父类构造函数执行了两遍

```js

```



### 08：原型继承

- 利用过渡对象的原型继承其他对象来生成新的对象
- 缺点：由于是类式继承的封装，父类对象中的值类型属性被复制，引用类型的属性被共用

```js

```



### 09：寄生式继承

- 利用原型继承方法，new 一个新对象
- 对新对象进行拓展，可以为新对象添加自己私有的方法和属性
- 返回新对象
- 由于是对原型继承的二次封装，所以具有一样的缺点

```js

```



### 10：寄生组合式继承

- 是寄生继承与构造函数继承的组合方式
- 在构造函数继承中调用父类的构造函数
- 在寄生方法中将父类原型的一个副本赋值给子类的原型，并且修正因为重写子类原型而导致子类的constractor属性被修改的问题
- 缺点：子类再想添加原型方法必须通过 prototype 对象的点语法形式添加

```js

```



### 11：单继承

- 利用 for...in 将源对象属性复制到目标对象上
- 这种方法只能进行浅复制

```js

```



### 12：多继承

- 利用函数的 arguments 对象 和 for循环，进行多个对象的继承（属性复制）
- 将该方法绑定到对象原型上,这样所有对象就可以直接拥有此方法

```js

```



### 13：多态

- 多态，就是同一个方法多种调用方式
- 也是通过判断 arguments对象的长度，不同长度执行不同方法来实现

```js

```



## 第二篇 创建型设计模式

> 创建型设计模式

### 01-01：无工厂模式

通过类实例化对象，实现登陆注册时的各类警告信息弹出框

```js
/**
 * @param {string} text - 警告框显示的文本
 * @returns {void} - 没有返回值，使用 alert 弹出警告框
 */
const LoginAlert = function (text) {
  // 这里可以创建对象的安全模式
  this.text = text;
};

LoginAlert.prototype.show = function () {
  // 显示警告框
  alert(this.text);
};

// 用户名错误提示框
const userNameAlert = new LoginAlert("用户名不能多于16个字母或数字");
userNameAlert.show();
// 密码错误提示框
const passwordAlert = new LoginAlert("输入的密码不正确");
passwordAlert.show();

/**
 * 新需求：用户名不存在提示，并且添加注册按钮
 * 由于多了注册按钮，所以上面的类无法再用，需要新建类
 */

/**
 * @param {string} text - 警告框显示的文本
 * @returns {void} - 没有返回值，使用 alert 弹出警告框
 */

const LoginConfirm = function (text) {
  this.text = text;
};

LoginConfirm.prototype.show = function () {
  alert(this.text, "This is a registration button");
};

const loginFailConfirm = new LoginConfirm(
  "您的用户名不存在,请重新输入或注册账号"
);
loginFailConfirm.show();

/**
 * 新需求：登录成功提示框，除了有确认取消按钮，还要有输入框接收用户输入
 * 由于新增了输入框，上面两个类都无法使用，需要新建类
 */

/**
 * @param {string} text - 警告框显示的文本
 * @returns {void} - 没有返回值，使用 alert 弹出警告框
 */
const LoginPrompt = function (text) {
    this.text = text;
};

LoginPrompt.prototype.show = function () {
  alert(this.text, "Here is the buttons,Here is the input box");
};

const loginPrompt = new LoginPrompt("欢迎回来，请输入心情：");
loginPrompt.show(); 
```

缺点：类的数量过多。每个不同的提示框类型都需要创建一个新的类，这样会导致类的数量增多，代码变得冗长和难以维护。

1. 类数量过多：每个不同的提示框类型都需要创建一个新的类，例如 `LoginAlert`、`LoginConfirm` 和 `LoginPrompt`。随着需求的增加，类的数量会不断增加，导致代码冗长。
2. 代码重复：在每个类中，都需要定义相同的构造函数和 `show` 方法。这种重复代码会增加维护成本，并且当需要进行修改时，需要在多个类中进行同样的更改。
3. 不利于扩展和灵活性：每个类都有自己独立的实现，无法灵活地添加新的功能或调整现有功能。如果需要新增一种提示框类型，就必须创建一个新的类，增加了开发的复杂性。
4. 不符合单一职责原则：每个类承担了过多的责任，既包括创建实例对象的功能，又包括展示提示框的功能。这种设计不符合单一职责原则，使得类的职责不够清晰。
5. 难以管理和维护：随着类的数量增多，代码会变得冗长，不易管理和维护。类之间的关系和依赖也变得复杂，给代码理解和调试带来困难。

### 01-02：基类工厂（Base Factory）

在工厂方法模式中，我们引入了一个基类工厂（Base Factory），它是一个抽象的工厂类，负责创建具体的对象实例。

基类工厂模式的核心思想是将对象的创建过程封装在一个工厂类中，通过该工厂类来创建对象实例。这样，调用者只需要知道工厂类的存在，而不需要直接实例化具体的对象类。

具体的对象类通常是基于一个共同的基类（Base Class）或接口（Interface）进行定义。基类工厂根据传入的参数来判断应该创建哪个具体的对象类，并返回相应的实例。

```js
/**
 * Created by jianbohe on 16/3/8.
 */

//简单工厂模式 实现 运动工厂

// 篮球基类
var Basketball = function(){
    this.intro = '篮球盛行于美国';
}
Basketball.prototype = {
    getMember:function(){
        console.log("每个队伍有需要5名球员");
    },
    getBallSize:function(){
        console.log('篮球很大');
    }
};

// 足球基类
var Football = function(){
    this.intro = '足球在全世界范围内流行';
}
Football.prototype = {
    getMember:function(){
        console.log("每个队伍有需要11名球员");
    },
    getBallSize:function(){
        console.log('足球较大');
    }
};

// 网球基类
var Tennis = function(){
    this.intro = '每年有很多网球比赛';
}
Tennis.prototype = {
    getMember:function(){
        console.log("每个队伍有需要1名球员");
    },
    getBallSize:function(){
        console.log('网球很小');
    }
};

// 运动工厂
var SprotsFactory = function(name){
    switch(name){
        case 'NBA':
            return new Basketball();
        case 'wordCup':
            return new Football();
        case 'FrenchOpen':
            return new  Tennis();
    }
}

// 为世界杯创建一个足球，只需要记住运动工厂 SportsFactory, 调用并创建
var football = SprotsFactory("wordCup");
console.log(football); //{ intro: '足球在全世界范围内流行' },添加到原型上的方法不会再实例中显示
console.log(football.intro); //足球在全世界范围内流行
football.getMember(); //每个队伍有需要11名球员
```

这种简单工厂模式的实现有以下缺点：

1. 违反了开放-封闭原则：当需要新增一种运动类型时，需要修改工厂函数的代码，添加相应的逻辑判断，违反了代码的可扩展性和可维护性。
2. 工厂函数职责过重：工厂函数负责根据不同的名称创建不同的对象，同时还需要掌握各种运动类型的创建逻辑，使得工厂函数职责过重，难以维护和扩展。
3. 无法满足复杂对象的创建需求：简单工厂模式适用于创建简单的对象，当需要创建的对象变得复杂且具有多层次的继承关系时，简单工厂模式的可扩展性变差，不易于管理和维护。
4. 违反了单一职责原则：基类中定义了一些与特定运动类型无关的方法，例如`getBallSize()`，这使得基类承担了多个职责，不符合单一职责原则。

综上所述，尽管简单工厂模式具有一定的灵活性和简洁性，但在复杂场景下可能导致代码不易扩展、维护和管理。更好的做法是使用其他创建型设计模式，如工厂方法模式或抽象工厂模式，以更好地满足复杂对象创建的需求，并提高代码的可扩展性和可维护性。

#### ES6基类工厂模式

```js
// 篮球基类
class Basketball {
  constructor() {
    this.intro = '篮球盛行于美国';
  }
  
  getMember() {
    console.log('每个队伍有需要5名球员');
  }
  
  getBallSize() {
    console.log('篮球很大');
  }
}

// 足球基类
class Football {
  constructor() {
    this.intro = '足球在全世界范围内流行';
  }
  
  getMember() {
    console.log('每个队伍有需要11名球员');
  }
  
  getBallSize() {
    console.log('足球较大');
  }
}

// 网球基类
class Tennis {
  constructor() {
    this.intro = '每年有很多网球比赛';
  }
  
  getMember() {
    console.log('每个队伍有需要1名球员');
  }
  
  getBallSize() {
    console.log('网球很小');
  }
}

// 运动工厂
const SportsFactory = function(name) {
  switch (name) {
    case 'NBA':
      return new Basketball();
    case 'wordCup':
      return new Football();
    case 'FrenchOpen':
      return new Tennis();
  }
};

// 为世界杯创建一个足球，只需要记住运动工厂 SportsFactory，调用并创建
const football = SportsFactory('wordCup');
console.log(football); // Football { intro: '足球在全世界范围内流行' }
console.log(football.intro); // 足球在全世界范围内流行
football.getMember(); // 每个队伍有需要11名球员
```

### 01-03：简单工厂

对于只有一个工厂类、创建单一对象的场景，简单工厂模式可以是一种合适的选择。它的主要优点是简单易用，适用于对象创建逻辑相对简单且固定的情况。在这种模式下，可以将相似的属性和行为抽象为工厂类的属性和方法，通过分支判断来处理不同的属性和行为。

简单工厂模式的优点包括：

1. 简化对象创建过程：通过工厂类，可以统一管理对象的创建过程，使得使用者无需关心具体的创建细节，简化了对象的实例化过程。
2. 隐藏对象的创建逻辑：使用者只需要关注工厂类提供的方法和参数，而无需了解对象的具体创建方式，提高了代码的封装性和抽象性。
3. 集中管理对象的创建和配置：工厂类可以集中管理对象的创建和配置，使得系统的代码更加集中和可维护。

然而，需要注意简单工厂模式的局限性。它适用于对象的创建逻辑相对简单且固定的情况，但随着需求的变化和复杂性的增加，可能需要引入其他创建型设计模式来提供更高的灵活性和可扩展性。

```js
/**
 * Created by jianbohe on 16/3/8.
 */

//简单工厂模式 实现 登陆注册时的各类警告信息弹出框

function createPop(type, text){

    //创建一个对象,并对对象拓展属性何方法
    var o = new Object();  // 过渡对象,借用寄生模式
    o.content = text;
    o.show = function(){
        console.log(o.content);
        o.showDiffrent();
    };

    if(type == 'alert'){
        o.showDiffrent=function(){
            //donothing
        }
    }else if(type == 'prompt'){
        o.showDiffrent=function(){
            console.log("there is buttons,","there is input");
        }
    }else if(type== 'confirm'){
        o.showDiffrent=function(){
            console.log("there is a register button");
        }
    }

    return o;
}

var passwordAlert = new createPop('alert','输入的密码不正确');
passwordAlert.show(); //输入的密码不正确

var loginFailConfirm = new createPop('confirm','您的用户名不存在，请重新输入或者注册账号');
loginFailConfirm.show(); //您的用户名不存在，请重新输入或者注册账号,there is a register button

var loginPrompt = new createPop('prompt','欢迎回来，请输入心情：');
loginPrompt.show(); //欢迎回来，请输入心情：there is buttons, there is input
```

这种简单工厂模式的实现有以下缺点：

1. 违反了开放-封闭原则：当需要新增一种弹出框类型时，需要修改工厂函数的代码，添加相应的逻辑判断，违反了代码的可扩展性和可维护性。
2. 工厂函数职责过重：工厂函数负责根据不同的类型创建不同的对象，并且需要了解各种弹出框类型的创建逻辑，使得工厂函数职责过重，难以维护和扩展。
3. 对象的创建和逻辑判断耦合在一起：工厂函数根据类型进行逻辑判断，并创建相应的对象，这种耦合导致代码可读性和可维护性降低。
4. 违反了单一职责原则：创建的对象既包含弹出框的内容属性，又包含显示方法和不同类型弹出框的差异化逻辑，使得对象承担了多个职责，不符合单一职责原则。

综上所述，尽管简单工厂模式具有一定的灵活性和简洁性，但在复杂场景下可能导致代码不易扩展、维护和管理。更好的做法是使用其他创建型设计模式，如工厂方法模式或抽象工厂模式，以更好地满足对象创建和逻辑判断的需求，并提高代码的可扩展性和可维护性。

### 02-01： 工厂方法模式前传1———— 类实例化方式



### 02-02： 工厂方法模式前传2———— 基类工厂模式



### 02-03： 工厂方法模式

- 将实际创建对象的工作推迟到子类当中
- 核心类是抽象类
- 采用安全模式类
- 将创建对象的基类放在工厂方法类的原型中

### 03-01： 抽象类

- 可以声明但不能使用的类
- 用来定义一个产品簇，声明一些必备方法，如果子类中没有重写就会抛出错误

### 03-02 抽象工厂模式

- 通过对类的工厂抽象使其业务用于对产品类簇的创建，而不负责创建某一类产品的实例
- 使用抽象工厂来为抽象的父类创建子类
- 在抽象工厂中让子类继承父类的一个实例（缓存类的实例），以此获得父类的对象属性
- 由于抽象工厂中的父类是抽象类，而抽象工厂方法不需要实例化，所以抽象工厂添加抽象类直接采用点语法来添加

### ⭐04-01 建造者模式（Builder Pattern）

建造者模式（Builder Pattern），它是一种创建型设计模式。建造者模式的主要目的是将一个复杂对象的构建过程与其表示分离，从而可以使用相同的构建过程创建不同的表示。

在建造者模式中，有两个核心角色：

1. Director（指导者）：负责使用构造器（Builder）来构建对象。它定义了构建对象的顺序和流程，但并不直接创建最终的对象。
2. Builder（构造器）：定义了构建复杂对象的接口和步骤。它抽象出了对象的各个部分的构建过程，并提供了一系列方法来设置对象的属性和组装它们。

**建造者模式和工厂模式的区别：**

- 建造者模式关注的是创建的过程，将复杂对象的构建过程与其表示分离，通过指导者和构造器来控制构建过程的顺序和细节。
- 工厂模式关注的是创建的最终结果，提供一种通用的接口来创建对象实例或者类簇，隐藏了实例化的具体逻辑。

假设我们要创建一个游戏角色对象，该角色有以下属性：姓名、职业、等级、武器、护甲。我们将使用建造者模式和工厂模式来创建该游戏角色对象。

**1、建造者模式的例子：**

```js
// 角色类
function Character(name, profession, level, weapon, armor) {
  this.name = name;
  this.profession = profession;
  this.level = level;
  this.weapon = weapon;
  this.armor = armor;
}

// 角色构造器
function CharacterBuilder(name, profession) {
  this.name = name;
  this.profession = profession;
}

CharacterBuilder.prototype.setLevel = function (level) {
  this.level = level;
  // 返回当前实例，以支持链式调用
  return this; 
};

CharacterBuilder.prototype.setWeapon = function (weapon) {
  this.weapon = weapon;
  // 返回当前实例，以支持链式调用
  return this;
};


CharacterBuilder.prototype.setArmor = function(armor) {
  this.armor = armor;
  // 返回当前实例，以支持链式调用
  return this;
};

CharacterBuilder.prototype.build = function() {
  return new Character(this.name, this.profession, this.level, this.weapon, this.armor);
};

//使用建造者创建角色
const characterBuilder1 = new CharacterBuilder("Qiqing", "ADC");
const character1 = characterBuilder1.setLevel(30).setWeapon("破败").setArmor("守望者铠甲").build();
console.log(character1);
```

在上述示例中，我们使用 `CharacterBuilder` 类来创建游戏角色对象。通过设置各个属性的方法，我们可以按照需要逐步构建角色对象。最后，使用 `build` 方法返回构建好的角色对象。

ES6语法：

```js
// 角色类
class Character {
  constructor(name, profession, level, weapon, armor) {
    this.name = name;
    this.profession = profession;
    this.level = level;
    this.weapon = weapon;
    this.armor = armor;
  }
}
// 角色构造器
class CharacterBuilder  {
  constructor(name, profession) {
    this.name = name;
    this.profession = profession;
  }

  setLevel(level) {
    this.level = level
    return this
  }

  setWeapon(weapon) {
    this.weapon = weapon;
    return this
  }
  setArmor(armor) {
    this.armor = armor;
    return this
  }

  build() {
    return new character(this.name,this.profession, this.level,this.weapon, this.armor)
  }
}

// 使用建造者创建角色
const chacterBuilder1 = new CharacterBuilder("qiqing", "ADC")
const chacter1 = characterBuilder1.setLevel(30).setWeapon("破败").setArmor("守望者铠甲").build()
console.log(chacter1)
```

**2、工厂模式：**

```js
// 角色类
function Character(name, profession, level, weapon, armor) {
  this.name = name;
  this.profession = profession;
  this.level = level;
  this.weapon = weapon;
  this.armor = armor;
}

// 角色工厂
function CharacterFactory() {}

CharacterFactory.prototype.createCharacter = function(name, profession, level, weapon, armor) {
  return new Character(name, profession, level, weapon, armor);
};

// 使用工厂创建角色
var characterFactory = new CharacterFactory();
var character = characterFactory.createCharacter('John', 'Warrior', 10, 'Sword', 'Shield');

```

ES6语法：

```js
// 角色类
class Character {
  constructor(name, profession, level, weapon, armor) {
    this.name = name;
    this.profession = profession;
    this.level = level;
    this.weapon = weapon;
    this.armor = armor;
  }
}

// 角色工厂
class CharacterFactory {
  createCharacter(name, profession, level, weapon, armor) {
    return new Character(name, profession, level, weapon, armor);
  }
}

// 使用工厂创建角色
const characterFactory = new CharacterFactory();
const character = characterFactory.createCharacter('John', 'Warrior', 10, 'Sword', 'Shield');

```

### ⭐05-01 构造函数继承基类

构造函数继承是一种实现多种子类继承同一父类并创建不同类型对象的方式。它通过在子类构造函数中调用父类构造函数来实现继承，并可以重写父类的方法。

```

```

缺点：每次子类继承都会执行一遍父类构造函数。如果父类的构造函数非常耗费资源，那么这种方式可能会造成性能问题。这主要是因为每个子类实例化时都要执行父类的构造函数，包括一些可能不需要的操作。

解决方案：使用原型链继承，而不是构造函数继承。原型链继承可以使所有子类实例共享父类的方法，而不需要在每个子类构造函数中执行父类的构造函数。

### ⭐05-02 原型继承

- 通过将耗资源的方法放入基类的原型来避免重复执行；
- 通过让子类的原型继承基类的实例，然后重写子类原型上继承自基类的方法来实现继承和子类的差异化实现
- 无论何时都能对基类活子类的原型进行拓展，所有实例都将自动获得这些新拓展的方法。

### ⭐06 单例模式

单例模式是一种只允许实例化一次的对象类，保证全局实例对象唯一。它的特点是在整个应用程序中只有一个实例存在，并提供了对该实例的全局访问点。

现在开发使用 `ES6` 模块，每个模块也同样是一个单例对象，平常业务开发中也很少去应用单例模式。

#### 一、单例模式的作用：

1、定义命名空间，通过将变量和方法放在单例对象中，可以避免全局命名空间的污染，实现模块化的代码组织。

```js
let Ming= {
  g: function (id) {
    return document.getElementById(id);
  },
  css: function (id, key, value) {
    this.g(id).style[key] = value;
  },
  attr: function (id, key, value) {
    this.g(id)[key] = value;
  },
  html: function (id, value) {
    this.g(id).innerHTML = value;
  },
  on: function (id, type, fn) {
    this.g(id)["on" + type] = fn;
  },
};
```

2、代码库的模块管理。通过将模块作为单例对象来管理，可以确保每个模块只被实例化一次，并提供了对模块的统一访问方式。

```js
let A = {
  Util: {
    util_method1(a) {
      console.log("util_method1:", a);
    },
    util_method2() {
      this.util_method1("util_method2")
    },
  },
  Tool: {
    tool_method1: function () {
      console.log("tm_1");
    },
    tool_method2: function () {
      console.log("tm_2");
    },
  },
  Ajax: {
    get: function () {
      console.log("get from remote");
    },
    post: function () {
      console.log("post to remote");
    },
  },
  others: {},
};
A.Util.util_method2() // util_method1: util_method2
A.Tool.tool_method1() // tm_1
A.Ajax.get() // get from remote
```

3、管理静态变量。通过将静态变量放在单例对象中，可以确保在整个应用程序中只有一个共享的静态变量实例。

```js
let Conf = (function () {
  let conf = {
    MAX_NUM: 1000,
    MIN_NUM: 1,
    COUNT: 1000,
  };

  return {
    get: function (name) {
      return conf[name] ? conf[name] : null
    }
  }
})();

let count = Conf.get('COUNT')
console.log(count) // 1000
```

#### 二、单例模式的实现方式

单例模式的实现方式有多种，其中一种常见的方式是使用闭包来创建私有作用域，并在该作用域中实例化对象：

```js
var Singleton = (function() {
  // 私有变量和私有方法
  var instance;

  function init() {
    // 私有成员
    var privateVariable = "I am private";

    // 私有方法
    function privateMethod() {
      console.log("I am a private method");
    }

    return {
      // 公有方法
      publicMethod: function() {
        console.log("I am a public method");
      },
      // 公有变量
      publicVariable: "I am public",
      // 获取单例实例的方法
      getInstance: function() {
        if (!instance) {
          instance = init();
        }
        return instance;
      }
    };
  }

  return {
    // 获取单例实例的方法
    getInstance: function() {
      if (!instance) {
        instance = init();
      }
      return instance;
    }
  };
})();

// 使用单例对象
var singletonInstance1 = Singleton.getInstance();
var singletonInstance2 = Singleton.getInstance();

console.log(singletonInstance1 === singletonInstance2); // true，两个实例相同
```

#### 四、单例的延迟创建（惰性创建）

单例的延迟创建是指在需要使用单例对象时才进行实例化，而不是在程序启动或加载时就立即创建单例对象。这种延迟创建单例的方式可以避免在初始化阶段就创建单例对象，而是在需要使用时再进行实例化，提高了资源利用和性能。

常见的实现方式是使用惰性加载（Lazy Load）的技术，通过判断单例对象是否已经存在，如果存在则直接返回，如果不存在则进行实例化。这样可以在第一次访问单例对象时进行实例化，后续再次访问时直接使用已经创建的实例。

```js
// 定义立即执行函数，创建一个闭包，用于封装单例对象的创建过程
var Singleton = (function () {
  // 定义 instance 变量并初始化为 null。该变量用于保存单例实例的引用。
  var instance = null; 
	// 定义私有的 init 方法，用于创建单例对象的实例
  function init() {
    // 返回一个包含公有方法和属性的对象，这些方法和属性可以被外部调用。
    return {
      publicMethod: function () {
        console.log("This is a public method~");
      },
      publicProperty: "This is a public property~"
    };
  }
  // 返回一个包含获取单例实例方法的对象
  return {
    getInstance: function () {
      // 如果实例不存在，则进行实例化
      if (!instance) {
        instance = init();
      }
      // 返回单例实例
      return instance;
    }
  };
})();

// 获取单例实例
var singletonInstance = Singleton.getInstance();

// 调用单例实例的方法和属性
singletonInstance.publicMethod(); // 输出: This is a public method.
console.log(singletonInstance.publicProperty); // 输出: This is a public property.
```

创建闭包的目的是为了将单例对象的创建过程封装在一个私有的作用域内，并且在该作用域内保存单例实例的引用。这样可以实现以下效果：

1. 封装：通过使用立即执行函数创建闭包，将单例对象的创建过程和内部变量 `instance` 封装在一个私有作用域内，避免了全局命名空间的污染和外部对 `instance` 的直接访问。
2. 私有变量：闭包内部的变量 `instance` 是私有的，外部无法直接访问或修改该变量，只能通过提供的 `getInstance` 方法来获取单例实例。
3. 延迟创建：在第一次调用 `getInstance` 方法时，才会进行单例对象的实例化，而不是在脚本加载时立即创建。这样可以避免不必要的资源消耗，只有在需要使用单例实例时才进行创建。
4. 单例访问控制：通过在闭包内部维护一个单例实例的引用 `instance`，确保只有一个实例存在，并通过 `getInstance` 方法提供对该实例的统一访问方式。在后续调用 `getInstance` 方法时，直接返回已经存在的单例实例。

闭包的使用有助于实现单例模式的封装、访问控制和延迟创建等特性，提供了一种有效的方式来管理单例对象，并确保在整个应用程序中只有一个共享的实例存在。

## 第三篇 结构型设计模式

> 结构型设计模式

### 01 外观模式

- 为一组复杂的子系统接口提供一个更高级的统一接口，通过这个接口使得对子系统接口的访问更容易。
- 常见的应用为封装一个统一接口来实现不同浏览器的相同功能的兼容。
- 外观模式的另一个作用：小型代码库中用来封装多个功能，简化底层操作方法

### ⭐02 适配器模式

- 适配器模式是将一个类（对象）的接口（方法或属性）转换成另外一个接口，以满足用户需求，解决接口不兼容问题
- 用法一： 组件库接口适配
- 用法二： 参数适配
- 用法三： 数据适配

### ⭐03 代理模式

代理模式是一种结构型设计模式，它允许通过代理对象来控制对另一个对象的访问（原因：一个对象不能直接引用另一个对象）。代理对象充当了被代理对象的中介，它可以拦截并处理对被代理对象的请求，同时还可以在必要时将请求传递给被代理对象。

在 JavaScript 中，代理模式通常用于在访问对象之前或之后执行一些额外的逻辑，或者对对象的访问进行控制和限制。

代理模式的优点是可以在不修改原始对象的情况下，通过引入代理对象来控制和扩展对原始对象的访问。代理对象可以拦截请求、执行额外的逻辑、提供缓存、限制访问等功能。这种方式使得代码更灵活、可扩展，并能提供更好的控制和保护。



### ⭐04 装饰者模式

- 在不改变原对象的基础上，通过对其进行包装拓展（添加属性或者方法）使原有对象可以满足用户更复杂的需求、
- 通过缓存对象原有的方法和属性，然后在装饰者方法中调用原有属性和方法和新增的方法和属性来实现功能拓展
- 与适配器模式的不同：适配器需要了解原有方法的细节，而装饰器则不关心原有方法的实现细节。

### 05 桥接模式

- 在系统沿着多个维度变化的同时，又不增加其复杂度并已达到解耦。
- 主要特点是将实现层与抽象层解耦分离，使两部分可以独立变化
- 有时会增加开发成本和性能开销

### 06 组合模式

- 又称部分-整体模式，将对象组合成树形结构以表示“部分-整体”的层次结构。
- 组合模式使得用户对单个对象和组合对象的使用具有一致性。
- 接口要统一，可以通过继承同一个虚拟类来实现。

### 07 享元模式

- 运用共享技术有效地支持大量的细粒度的对象，避免对象间拥有相同内容造成多余开销
- 享元模式将数据和方法分成内部数据、内部方法和外部数据、外部方法。
- 内部方法与内部数据指相似或共有的数据和方法，将这一部分提取出来可以减少开销，提高性能

## 第四篇 行为型设计模式

> 行为型设计模式

### 01 模板方法模式

- 父类中定义一组操作算法骨架，而降一些实现步骤延迟到子类中，使得子类可以不改变父类的算法机构的同时可重新定义算法中某些实现步骤
- 将多个模型抽象化归一，从中抽象提出出一个最基本的模板，其他模块只需要继承这个模板方法，也可以拓展某些方法
- 继承类也可以作为模板类

### ⭐02 观察者模式

- 又称发布-订阅者模式或消息机制
- 它定义了一种依赖关系，解决了主体对象与观察者
- 包含两个基本方法：接收消息、向订阅者发布消息
- 还需要取消注册方法、消息容器。
- 接收消息（即消息注册）作用是将订阅者注册的消息推入消息容器，接收两个参数:消息类型和处理动作
- 发布消息作用是当观察者发布一个消息时将所有订阅者订阅的消息一次执行，接收两个参数：消息类型及行为参数

### 03 状态模式

- 当一个对象的内部状态发生改变时，会导致其行为的改变。
- 对于分支条件内部独立结果的管理，可以使用状态模式
- 每一种条件作为对象内部的一种状态，面对不同判断结果，它其实就是选择对象内的一种状态
- 对于状态模式，主要目的就是将条件判断的不同结果转化为对象内部的状态，既然是状态对象的内部状态，所以一般作为状态对象内部的私有变量，然后提供一个能够调用状态对象内部状态的接口方法对象。这样方便管理状态。

### ⭐04 策略模式

- 将定义的一组算法封装起来，使其相互之间可以替换
- 封装的算法具有一定的独立性，不会随客户端变化而变化
- 结构上与状态模式很像，在内部封装一个对象，通过返回的接口对象实现对内部对象的调用，但不需要管理状态
- 典型应用场景：表单验证

### ⭐05 职责链模式

- 解决请求的发送者与请求的接受者之间的耦合，通过职责链上的多个对象分解请求流程，实现请求在多个对象之间的传递，直到最后一个对象完成请求的处理。
- 把每件事独立出一个模块对象去处理，完整的需求被分解成相互独立的模块需求
- 方便进行单元测试，保证每个组件对象的处理逻辑的安全性

### ⭐06 命令模式

- 将请求与实现解耦并封装成独立对象，从而使不同的请求对客户端的实现参数化
- 将创建模块的逻辑封装在一个对象里，这个对象提供一个参数化的请求接口，通过调用这个接口并传递一些参数实现调用命令对象内部的一些方法

### 07 访问者模式

- 针对于对象结构中的元素，定义在不改变该对象的前提下访问结构中元素的新方法
- 我么知道call和apply的作用就是更改函数执行时的作用域，这正是访问者模式的精髓，通过这两种方法我们就可以让某个对象在其他作用域中运行
- 访问者模式解决数据与数据的操作方法之间的耦合，将数据的操作方法独立于数据，使其可以自由化演变。

### 08 中介者模式

- 通过中介者对象封装一系列对象之间的交互，使对象之间不再相互引用，降低他们之间的耦合
- 主要是通过模块间或对象间的复杂通信，来解决模块间或对象间的耦合
- 中介者对象的本质是封装多个对象的交互，并且这些对象的交互一般都是在中介者内部实现的。
- 与观察者模式相比，观察者模式中的订阅者是双向的，而中介者模式中订阅是单向的。

### 09 备忘录模式

- 在不破坏对象封装性的前提下，在对象之外捕获并保存该对象内部的状态以便日后对象使用或者对象恢复到以前的某个状态
- 主要任务是对现有数据或状态做缓存，这些数据或缓存将在可预期的将来再次用到
- 备忘录对象是对数据缓存器的一次保护性封装，防止外界访问
- 当数据量过大时会严重占用系统资源

### ⭐10 迭代器模式

- 在不暴露对象内部结构的同时，可以顺序地访问聚合对象内部的元素

### 11 解释器模式

- 对于一种语言，给出其文法形式，并定义一种解释器，通过使用这种解释器来解释语言中定义的句子

## 第五篇 技巧型设计模式

> 技巧型设计模式

### 01 链模式

- 通过在对象方法中将当前对象返回，实现对同一个对象方法的链式调用

### 02 委托模式

- 多个对象接收并处理同一请求，他们将请求委托给另一个对象同一处理请求
- 利用元素冒泡原理可以将所有子元素上的相同事件绑定到父元素上

### 03 数据访问对象模式

- 抽象和封装对数据源的访问与存储。
- 关键在于定义私有前缀和增删改查接口

### 04 节流模式

- 对重复的业务逻辑进行节流控制，执行最后一次操作并取消其他操作，以提高性能
- 节流器的关键点在于计数器和事件执行间隔时间的控制，在某个间隔内只允许触发一次。
- 节流模式可应用于优化滚动事件性能、优化浮层显隐性能、图片懒加载、统计回报次数优化等

### 05 简单模板模式

- 通过格式化字符串拼凑出视图，以避免创建视图时大量的节点操作。优化内存开销。
- 从定义可看出其主要针对的是有大量创建视图的高消耗DOM操作场景。

### 06 惰性模式

- 减少每次代码执行的重复性的分支判断，通过对对象重定义来屏蔽原对象中的分支判断
- 第一种是在文件加载进来时通过闭包执行该方法对其重新定义（会使页面加载时占用一定资源）
- 第二种是在第一种方式基础上做一次延迟执行，在函数第一次调用时对其重定义；

### 07 参与者模式

- 在特定的作用域中执行给定的函数，并将参数原封不动地传递。
- 主要是利用bind方法，它应用了函数柯里化思想来进行传参和作用域绑定

### 08 等待者模式

- 通过对多个异步进程监听，来触发未来发生的动作
- 其实就是简单地实现Promise规范，通过when/then/done/fail来处理请求和回调，通过resolve和reject状态来监听异步的结果。

## 第六篇 架构型设计模式

> 架构型设计模式

### 01 同步模块模式

- 请求发出后，无论模块是否存在，立即执行后续逻辑，实现模块开发中对模块的立即引用
- 可以解决多人协作开发时代码互相冲突导致开发进程阻塞的问题
- 实质是将所有模块按照层级关系绑定到一个单体对象上，使用时调用该单体对象来完成操作；
- 主要有两个方法，定义模块的define方法和引用模块的module方法
- 缺点：无法引用尚未加载完成的模块。

### 02 异步模块模式

- 请求发出后，继续其他业务逻辑，知道模块加载完成后执行后续的逻辑，实现模块开发中对模块加载完成后的引用。
- 核心思路利用闭包返回模块，对未加载模块进行计数，直到未加载模块为0，然后执行回调
- 在异步加载脚本文件时，要设置 asycn = true;

### 03 Widget模式

- 是指借用Web Widget思想将页面分解成部件，针对部件开发，最终组合成完整的页面
- 此模式多针对与页面视图的构造，它将页面分解为很多个组件（即模块），一个完整的组件包含该模块完整的视图和一套完整的功能；其实就是组件化技术。
- 模板引擎一般分四步：处理数据=>获取模板=>处理模板=>编译执行；
- 对于模板内的js语法解析，主要是eval()与new Function()技术来实现

### 04 MVC模式

- 即模型（model）-视图（view）-控制器（controller）
- 用一种将业务逻辑、数据、视图分离的方式组织架构代码，主要解决层次混乱问题

### 05 MVP模式

- 即模型(Model)-视图(View)-管理器(Presenter)
- View 层不直接引用Model层内的数据，而是通过Presenter层实现对Model层内的数据访问
- 所有层次的交互都发生在Presenter层中

### ⭐06 MVVM模式

- 即模型（Model）-视图（View）-视图模型（ViewModel）
- 为视图层量身定做一套视图模型，并在视图模型中创建属性和方法，为视图层绑定数据并实现交互
- 这样做以后 View层可以直接使用HTML来完成。

作者：何建博本尊
链接：https://juejin.cn/post/6844903954036293640
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。