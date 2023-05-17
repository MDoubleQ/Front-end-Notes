## 什么是设计模式？

一个模式就是一个可重用的方案，可应用于在软件设计中的常见问题。另一种解释就是一个我们如何解决问题的模板 - 那些可以在许多不同的情况里使用的模板。

- 设计模式是我们在 解决问题的时候针对特定问题给出的简洁而优化的处理方案
- 在 JS 设计模式中，**最核心的思想：封装变化。**
- 将变与不变分离，确保变化的部分灵活、不变的部分稳定。

没必要完全去套设计模式，而是去理解它们共同的思想，保持初心--**提升代码的可读性、可扩展性、可维护性**，最终达到「还记着没有，我现在全忘了，忘得干干净净的了」的境界。

## 23 种设计模式（曾探）

## 七项基本原则

https://pattern.windliang.wang/posts/%E5%89%8D%E7%AB%AF%E7%9A%84%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%E7%B3%BB%E5%88%97-%E5%9F%BA%E6%9C%AC%E5%8E%9F%E5%88%99.html

设计一些设计模式时，一般遵循如下七项基本原则。

二十三个经典的 [设计模式 (opens new window)](https://pattern.windliang.wang/)已经过完了 ，这里再把一些基本原则过一下，以便平时开发中可以更好的体会。

### 单一职责原则 SRP(Single Responsibility Principle)

> There should never be more than one reason for a class to change." In other words, every class should have only one responsibility.

定义：一个类或者模块应该有且只有一个改变的原因，在 `js` 中的话更多的会应用在对象、函数中。

最难的地方就在于结合具体场景对单一职责的判定了，为了应用这个原则把一个模块拆的太细其实也不太好，所以需要我们在方便性和稳定性之间做一个权衡。

之前讲的 [代理模式 (opens new window)](https://pattern.windliang.wang/posts/前端的设计模式系列-代理模式.html)、[装饰器模式 (opens new window)](https://pattern.windliang.wang/posts/前端的设计模式系列-装饰器模式.html)都有体现。

### 开闭原则 OCP(open–closed principle)

> Software entities should be open for extension, but closed for modification.

定义：一个软件实体如类、模块和函数应该对扩展开放，对修改关闭。模块应尽量在不修改原代码的情况下进行扩展。

平常开发中，要把变的部分和不变的部分分离出来，设计一个结构的时候尽可能的考虑一下未来可能变化的部分。

可以通过放置 `hook` 、使用回调函数的方式达到扩展的目的。

之前讲的 [发布订阅模式 (opens new window)](https://pattern.windliang.wang/posts/前端的设计模式系列-发布订阅模式.html)、[模版方法模式 (opens new window)](https://pattern.windliang.wang/posts/前端的设计模式系列-模版模式.html)、[策略模式 (opens new window)](https://pattern.windliang.wang/posts/前端的设计模式系列-策略模式.html)、[职责链模式 (opens new window)](https://pattern.windliang.wang/posts/前端的设计模式系列-责任链模式.html)都有体现。

### 里氏替换原则 LSP(Liskov substitution principle)

> Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.

定义：所有引用基类的地方必须能透明地使用其子类的对象，也可以简单理解为任何基类可以出现的地方，子类一定可以出现。

举个例子就是如果某个地方可以用 `A` 类， `B` 类继承于 `A` 类，那么这个地方一定可以使用 `B` 类。

这个原则告诉我们在继承类的时候，如果要实现一个新功能，不要去覆盖父类已经实现的方法，而应该去写一个新方法。

平常前端开发中很少去写类和继承，这个原则用的比较少。

### 接口隔离原则 ISP(Interface Segregation Principle)

> Many client-specific interfaces are better than one general-purpose interface.

定义：客户端不应该依赖它不需要的接口，类间的依赖关系应该建立在最小的接口上。简单来说就是建立单一的接口，不要建立臃肿庞大的接口。也就是接口尽量细化，同时接口中的方法尽量少。

举个例子就是 `A` 接口有 `5` 个方法，`B` 类实现 `A` 接口，但 `B` 类只用到其中的 `3` 个方法，此时可以考虑对 `A` 接口进行拆分。

`js` 中没有接口，忽略。

### 依赖倒转原则 DIP(Dependency Inversion Principle)

> Depend upon abstractions, not concretions

定义： 程序要依赖于抽象接口，不要依赖于具体实现。简单的说就是要对抽象进行编程，不要对实现进行编程，这样就降低了客户与实现模块间的耦合。

其实就是经常说的面向接口（或者基类）编程。

但 `js` 中没有接口和抽象类，这种原则也就用不到了。

上边五个原则就是经常看到的 `SOLID` 原则，除了这些还有几个其他的原则。

### 最小知道原则 LOD(principle of least knowledge)

定义：一个软件实体应当尽可能少的与其他实体发生相互作用。每一个软件单位对其他的单位都只有最少的知识，而且局限于那些与本单位密切相关的软件单位。

实体的话在前端中更多的对应对象、函数，[门面模式 (opens new window)](https://pattern.windliang.wang/posts/前端的设计模式系列-外观模式.html)可以看作该原则的应用。

最小知道原则又叫做迪米特法则 LOD(Law of Demeter)，迪米特其实是宙斯(Zeus) 的姐姐，名字来源的话这里截取下[维基百科 (opens new window)](https://en.wikipedia.org/wiki/Law_of_Demeter)。

> *The Greek goddess of Agriculture.*
>
> The Demeter project was named after Demeter because we were working on a hardware description language Zeus and we were looking for a tool to simplify the implementation of Zeus. We were looking for a tool name related to Zeus and we chose a sister of Zeus: Demeter.
>
> Later we promoted the idea that Demeter-style software development is about growing software as opposed to building software. We introduced the concept of a growth plan which is basically a sequence of more and more complex UML class diagrams.
>
> Growth plans are useful for building systems incrementally.

大意就是当时是用一个叫做 `Zeus` 的硬件语言，然后找到了一个优化 `Zens` 的工具，为了让它们产生联系，就起了 `Demeter` 这个名字。

另外截取一下 「JavaScript 设计开发与实现」书里提到的关于两个名字之间的建议：

> 许多人更倾向于使用迪米特法则这个名字，也许是因为显得更酷一点。但本书参考 *Head First*
>
> *Design Patterns* 的建议，称之为最少知识原则。一是因为这个名字更能体现其含义，另一个原因
>
> 是“法则”给人的感觉是必须强制遵守，而原则只是一种指导，没有哪条原则是在实际开发中必
>
> 须遵守的。比如，虽然遵守最小知识原则减少了对象之间的依赖，但也有可能增加一些庞大到难
>
> 以维护的第三者对象。跟单一职责原则一样，在实际开发中，是否选择让代码符合最少知识原则，
>
> 要根据具体的环境来定。

#### 合成/聚合复用原则 CARP(Composite/Aggregate Reuse Principle)

定义：尽量使用合成/聚合，而不是通过继承达到复用的目的。

### 其他原则

#### KISS 原则

定义： Keep It Simple, Stupid，在设计中应当注重简约的原则。

#### YAGNI 原则

定义：You aren't gonna need it，表示暂时不需要的就不要做。

#### DRY 原则

定义：Don't Repeat Yourself，不要写重复的代码。

#### 总

所有的原则只是协助于我们写成易维护、易扩展的代码，不能为了去实现而实现、进行过度设计。

一些代码如果未来完全不用改变，那就用最简单的方式实现即可，当第二次、第三次修改的时候再来重构也不迟。

设计模式和基本原则的应用一定是结合具体场景的，空谈的话也没有任何意义。

我们只需要先了解这些原则，然后在日常开发中慢慢进行体会。

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

所以——我抄书了！不过我不觉得抄书可耻，从学习编程的第一天，我就秉持着一个理念：==学习过程中的所有代码，只有自己敲一遍，才算学过（甚至这样都只能达到基本理解而非学懂）。==

本文下面对书中40种设计模式的总结，我还完成了书中所有代码示例的实现，对书中的错误进行了修正，补全了所有作者省略掉的代码，保证每一个示例都可以在node环境或者浏览器页面或者浏览器控制台可以看到演示效果。

具体请看这个github仓库： [javascript_Pattern](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fhjb2722404%2Fjavascript-Pattern)

希望可以帮助到需要的同学。
## 开篇 从函数到对象

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

**1、建造者模式的例子：**

> 假设我们要创建一个游戏角色对象，该角色有以下属性：姓名、职业、等级、武器、护甲。我们将使用建造者模式和工厂模式来创建该游戏角色对象。

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

### ⭐01 外观模式

外观模式是一种结构型设计模式，它提供了一个简化的接口，用于访问复杂子系统的一组接口。

外观模式的目标：通过创建一个高层接口，将子系统的复杂性隐藏起来，使得客户端可以更轻松地使用子系统。

外观模式的主要思想：将一组复杂的子系统接口封装在一个外观对象中，客户端只需要与外观对象进行交互，而无需直接与子系统的各个接口进行交互。外观对象充当了客户端与子系统之间的中介，通过简化的接口提供了对子系统功能的访问。

常见的应用场景：多个浏览器之间实现相同功能的兼容性。由于不同浏览器对于某些功能的实现方式不同，为了确保应用程序在各种浏览器中都能正常工作，可以使用外观模式来封装各个浏览器的差异性，提供一个统一的接口给应用程序使用。

外观模式还可以在小型代码库中用来封装多个功能，简化底层操作方法。通过创建一个外观对象，将复杂的底层操作封装起来，对外部提供一个简单的接口，使得使用者可以更方便地使用这些功能。

> 场景一：假设我们正在开发一个音频播放器应用程序。该应用程序需要与音频引擎、音频控制器和音频可视化组件等多个子系统进行交互。每个子系统都有自己的接口和复杂的实现逻辑。为了简化客户端与这些子系统的交互，我们可以使用外观模式。

```js
// 音频引擎子系统
var AudioEngine = {
  init: function() {
    console.log('Initializing audio engine...');
  },
  play: function() {
    console.log('Playing audio...');
  },
  pause: function() {
    console.log('Pausing audio...');
  },
  stop: function() {
    console.log('Stopping audio...');
  }
};

// 音频控制器子系统
var AudioController = {
  volumeUp: function() {
    console.log('Increasing volume...');
  },
  volumeDown: function() {
    console.log('Decreasing volume...');
  },
  mute: function() {
    console.log('Muting audio...');
  }
};

// 音频可视化子系统
var AudioVisualizer = {
  visualize: function() {
    console.log('Visualizing audio...');
  }
};

// 外观对象
var AudioPlayer = {
  play: function() {
    AudioEngine.init();
    AudioEngine.play();
    AudioVisualizer.visualize();
  },
  pause: function() {
    AudioEngine.pause();
  },
  stop: function() {
    AudioEngine.stop();
  },
  volumeUp: function() {
    AudioController.volumeUp();
  },
  volumeDown: function() {
    AudioController.volumeDown();
  },
  mute: function() {
    AudioController.mute();
  }
};

// 在应用程序中使用外观对象
AudioPlayer.play(); // 输出:
// Initializing audio engine...
// Playing audio...
// Visualizing audio...

AudioPlayer.pause(); // 输出: Pausing audio...

AudioPlayer.stop(); // 输出: Stopping audio...

AudioPlayer.volumeUp(); // 输出: Increasing volume...

AudioPlayer.mute(); // 输出: Muting audio...
```

在这个示例中，我们创建了一个外观对象`AudioPlayer`，它封装了音频引擎、音频控制器和音频可视化组件等多个子系统的复杂接口。客户端只需与`AudioPlayer`对象进行交互，无需了解每个子系统的具体实现细节。

> 场景二：假设我们正在开发一个网络请求库，该库需要处理不同类型的请求（GET、POST、PUT、DELETE等）并与服务器进行通信。每种请求类型都有自己的配置和实现逻辑，包括设置请求头、处理请求参数、处理响应等。为了简化客户端与网络请求库的交互，我们可以使用外观模式。

```js
// GET请求子系统
var GetRequest = {
  send: function(url, options) {
    // 发送GET请求的具体实现逻辑
    console.log('Sending GET request to:', url);
    console.log('Options:', options);
  }
};

// POST请求子系统
var PostRequest = {
  send: function(url, options) {
    // 发送POST请求的具体实现逻辑
    console.log('Sending POST request to:', url);
    console.log('Options:', options);
  }
};

// PUT请求子系统
var PutRequest = {
  send: function(url, options) {
    // 发送PUT请求的具体实现逻辑
    console.log('Sending PUT request to:', url);
    console.log('Options:', options);
  }
};

// DELETE请求子系统
var DeleteRequest = {
  send: function(url, options) {
    // 发送DELETE请求的具体实现逻辑
    console.log('Sending DELETE request to:', url);
    console.log('Options:', options);
  }
};

// 外观对象
var RequestFacade = {
  get: function(url, options) {
    GetRequest.send(url, options);
  },
  post: function(url, options) {
    PostRequest.send(url, options);
  },
  put: function(url, options) {
    PutRequest.send(url, options);
  },
  delete: function(url, options) {
    DeleteRequest.send(url, options);
  }
};

// 在应用程序中使用外观对象
RequestFacade.get('https://api.example.com/data', { headers: { 'Authorization': 'Bearer token' } });

RequestFacade.post('https://api.example.com/data', { body: { name: 'John', age: 25 } });

RequestFacade.put('https://api.example.com/data/1', { body: { name: 'Jane', age: 30 } });

RequestFacade.delete('https://api.example.com/data/1');
```

在这个示例中，我们创建了一个外观对象`RequestFacade`，它封装了不同类型的请求（GET、POST、PUT、DELETE）的复杂接口，将复杂的请求接口进行了封装和简化。

客户端只需与`RequestFacade`对象进行交互来发送不同类型的请求，无需了解每个请求类型的具体实现细节。

### ⭐02 适配器模式

适配器模式是一种结构型设计模式，它允许将一个类的接口转换成另一个接口，以满足不同类之间的接口兼容性需求。

适配器模式的主要目的是解决两个已有接口之间不兼容的问题，让它们能够协同工作。适配器通过封装一个已有类的接口，提供一个新的接口供其他类使用。

#### 适配器模式涉及以下几个角色：

1. 目标接口（Target Interface）：定义客户端期望的接口，适配器将目标接口转换为适配者接口。
2. 适配器（Adapter）：实现目标接口，并在内部持有适配者对象的引用。适配器将目标接口的方法调用转发给适配者对象。
3. 适配者（Adaptee）：已有的类或对象，其接口与目标接口不兼容。
4. 客户端（Client）：使用目标接口进行操作的类或对象。

#### 适配器模式的工作原理如下：

1. 客户端通过调用目标接口的方法来实现所需功能。
2. 适配器实现了目标接口，并在内部持有一个适配者对象的引用。
3. 当客户端调用适配器的方法时，适配器将请求转发给适配者对象的相应方法。
4. 适配者对象执行实际的操作，并将结果返回给适配器。
5. 适配器将结果返回给客户端，使其能够正常工作。

#### 适配器模式的优点包括：

- 解决接口不兼容问题，使得不同接口的类能够协同工作。
- 可以在不修改现有代码的情况下引入新功能。
- 增加代码的灵活性和复用性。

#### 适配器模式的适用场景包括：

1、组件库接口适配：当我们使用第三方组件库时，组件库提供的接口可能与我们的代码需求不匹配。此时，可以创建一个适配器类，将组件库的接口转换为我们需要的接口。适配器类实现目标接口，并在内部调用组件库的接口进行适配转换，使得组件库能够与我们的代码无缝协同工作。

> 假设我们正在使用一个图表库，它提供了一个`drawChart`方法来绘制图表。但是，我们的应用程序中已经存在一个绘图类`Plotter`，它具有`plot`方法来绘制图表。为了与图表库无缝协同工作，我们可以创建一个适配器类`ChartAdapter`，它实现了`plot`方法，内部调用图表库的`drawChart`方法进行适配转换。

```js
// 已有的绘图类
function Plotter() {
  this.plot = function() {
    // 绘制图表的具体实现
    console.log('Plotting chart...');
  };
}

// 图表库
function ChartLibrary() {
  this.drawChart = function() {
    // 绘制图表的具体实现
    console.log('Drawing chart...');
  };
}

// 适配器类
function ChartAdapter() {
  var chartLibrary = new ChartLibrary();

  this.plot = function() {
    chartLibrary.drawChart();
  };
}

// 在应用程序中使用适配器
var plotter = new Plotter();
plotter.plot(); // 输出: Plotting chart...

var chartAdapter = new ChartAdapter();
chartAdapter.plot(); // 输出: Drawing chart...
```

在这个示例中，通过创建`ChartAdapter`适配器类，我们成功地将图表库的接口转换为了`Plotter`类已有的接口。现在，无论是使用`Plotter`类还是`ChartAdapter`类，都可以绘制图表。

2、参数适配：有时候我们需要使用一个方法，但是该方法的参数与我们当前的数据结构不匹配。通过创建适配器类，我们可以将当前数据结构的参数适配为符合目标方法要求的参数。适配器类接收当前数据结构的参数，在内部进行适配处理后，调用目标方法并传递适配后的参数，以实现对方法的适配。

> 假设我们有一个发送邮件的函数`sendEmail`，它接受一个包含收件人、主题和内容的对象作为参数。但是，我们现在需要从不同的数据源中获取邮件信息，例如一个包含`to`、`subject`和`body`属性的简单对象或一个具有不同属性名称的复杂对象。我们可以使用适配器模式来适配不同的数据源，使其符合`sendEmail`函数的参数要求。

```js
function sendEmail(email) {
  console.log(`Sending email to: ${email.to}`);
  console.log(`Subject: ${email.subject}`);
  console.log(`Content: ${email.body}`);
}

// 简单对象数据源
var simpleEmail = {
  to: 'john@example.com',
  subject: 'Hello',
  body: 'This is a simple email.'
};

// 复杂对象数据源
var complexEmail = {
  recipient: 'jane@example.com',
  title: 'Greetings',
  message: 'This is a complex email.'
};

// 适配器类
function EmailAdapter(email) {
  this.to = email.recipient || email.to;
  this.subject = email.title || email.subject;
  this.body = email.message || email.body;
}

// 在应用程序中使用适配器
sendEmail(simpleEmail); // 输出:
// Sending email to: john@example.com
```

3、数据适配：在某些情况下，我们需要将数据转换成另一种数据结构以满足特定的需求。适配器模式可以用于数据适配，将原始数据进行转换和重组，以适应目标数据结构的要求。适配器类负责将原始数据适配为目标数据结构，并提供符合目标接口的方法供客户端使用。

> 假设我们从外部API获取了一组学生数据，每个学生对象包含`name`和`score`属性。但是我们的应用程序需要将学生数据转换为包含`studentName`和`studentScore`属性的对象。我们可以创建一个适配器类`StudentAdapter`来适配学生数据。

```js
// 外部数据源的学生对象
var externalStudent = {
  name: 'John',
  score: 90
};

// 适配器类
function StudentAdapter(student) {
  this.studentName = student.name;
  this.studentScore = student.score;
}

// 在应用程序中使用适配器
var adaptedStudent = new StudentAdapter(externalStudent);
console.log(adaptedStudent); // 输出: { studentName: 'John', studentScore: 90 }
```

### ⭐03 代理模式

代理模式是一种结构型设计模式，它允许通过代理对象来控制对另一个对象的访问（原因：一个对象不能直接引用另一个对象）。代理对象充当了被代理对象的中介，它可以拦截并处理对被代理对象的请求，同时还可以在必要时将请求传递给被代理对象。

在 JavaScript 中，代理模式通常用于在访问对象之前或之后执行一些额外的逻辑，或者对对象的访问进行控制和限制。

代理模式的优点是可以在不修改原始对象的情况下，通过引入代理对象来控制和扩展对原始对象的访问。代理对象可以拦截请求、执行额外的逻辑、提供缓存、限制访问等功能。这种方式使得代码更灵活、可扩展，并能提供更好的控制和保护。

**举个例子来说明代理模式的应用。**

> 假设我们有一个图片加载器，用于从服务器加载图片并显示在网页上。由于图片文件可能比较大，加载和显示图片可能会耗费一定的时间。我们希望在图片加载完成之前显示一个加载中的提示，并在图片加载完成后将其显示出来。
>
> 这时候，我们可以使用代理模式来实现这个需求。我们创建一个图片代理对象，作为图片加载器和实际图片对象之间的中介。代理对象在图片加载之前显示加载中的提示，然后将加载请求转发给实际的图片对象进行加载。当图片加载完成后，代理对象将其显示在网页上。

```js
function Image(url) {
  this.url = url;
}

Image.prototype.load = function () {
  console.log(`Loading image from ${this.url}`);
  // 模拟图片加载延迟
  setTimeout(() => {
    console.log(`Image loaded: ${this.url}`);
  }, 1000);
};

// 图片代理对象
function ImageProxy(url) {
  this.url = url;
  this.image = null; // 实际的图片地址
}

ImageProxy.prototype.load = function() {
  if (!this.image) {
    this.image = new Image(this.url); // 创建实际的图片对象
  }
  console.log("Displaying loading indicator")

  // 在图片加载完成后将其显示出来
  setTimeout(() => {
    this.image.load()
  }, 1000)
}

// 使用代理对象加载和显示图片
const imageProxy1 = new ImageProxy("example.com/image.JPG")
imageProxy1.load();
// 输出：
// Displaying loading indicator
// (1秒后)
// Loading image from example.com/image.jpg
// (1秒后)
// Image loaded: example.com/image.jpg
```

在上述示例中，`ImageProxy` 充当了图片加载器和实际图片对象之间的代理对象。当调用 `load` 方法时，代理对象首先显示加载中的提示，然后创建实际的图片对象并调用其 `load` 方法进行图片加载。这样就可以在加载图片时显示加载中的提示，并在加载完成后将其显示出来。

> 代理模式其实说简单了就是对原有对象/函数再包装一层，并且保持和原对象一致的行为。那么为什么不直接改原对象呢？
>
> 第一，可能不方便直接改原对象，所以只能采取代理模式包一层了。
>
> 第二，「单一职责原则」，如果直接修改原对象，会增加原有对象的复杂度，原对象如果负责的职责过多，引起对象改动的原因就会增多。
>
> 第三，未来如果新功能要去掉，修改起来也不方便。如果使用了代理模式，只需要把原来引用的地方还原即可。

### ⭐04 装饰器模式

装饰器模式是一种结构型设计模式，遵循开放封闭原则，它允许在**不改变原有对象的情况下，通过对其进行包装拓展，以满足用户更复杂的需求。**

装饰器模式通过将对象包装在一个装饰器对象中，来动态地添加新的行为或功能。装饰器对象通过缓存原有对象的方法和属性，并在自己的方法中调用原有对象的方法和新增的方法，从而实现功能的拓展。

在装饰器模式中，有三个主要角色：

1. 组件（Component）：它是被装饰的原始对象，它定义了基本的接口和行为。
2. 装饰器（Decorator）：它是包含了与组件相同接口的对象，它实际上是对组件的包装。装饰器与组件实现了相同的接口，这样可以将装饰器链式地组合在一起，以透明地为组件添加功能。
3. 装饰器客户端（Client）：它使用装饰器对象来处理请求。它通过与装饰器交互来实现对组件的功能扩展。

以下是装饰器模式的基本工作原理：

1. 定义组件接口：创建一个基本组件接口或抽象类，定义了组件的基本方法。
2. 实现组件：实现具体的组件类，它们实现了组件接口并提供了基本功能。
3. 创建装饰器类：创建装饰器类，它与组件实现相同的接口，以便可以透明地包装组件对象。
4. 在装饰器中添加功能：在装饰器中添加额外的功能，可以在调用原始组件方法前后执行一些操作，或者在原始功能的基础上添加新的行为。
5. 使用装饰器：在客户端代码中使用装饰器对象来处理请求。客户端可以使用一个或多个装饰器对象来组合功能，形成一个装饰器链。

**装饰器模式与适配器模式的区别**

装饰器模式与适配器模式的区别在于关注点不同。

- 适配器模式旨在使不兼容的接口变得兼容，需要了解原有方法的细节，并进行适配。
- 而装饰器模式则不关心原有方法的实现细节，只关注对对象的功能拓展。

简单的装饰器：

```js
// 原有对象
class Component {
  operation() {
    console.log("Component operation");
  }
}

// 装饰器对象
class Decorator {
  constructor(component) {
    this.component = component;
  }

  operation() {
    this.component.operation();
    this.additionalOperation();
  }

  additionalOperation() {
    console.log("Additional operation");
  }
}

// 使用装饰器包装原有对象
const component = new Component();
const decoratedComponent = new Decorator(component);

// 调用装饰器对象的方法，实现功能拓展
decoratedComponent.operation();

// 输出：
// Component operation
// Additional operation
```

假设我们有一个电子商务网站，我们希望对用户进行身份验证、日志记录和缓存处理。我们可以使用装饰器模式来实现这些功能的透明拓展。

```js
// 基本的用户服务类，提供了一些基本的用户操作方法：
function UserService() {}

UserService.prototype.getUser = function(userId) {
  console.log("Getting user with ID: " + userId);
  // 模拟从数据库获取用户信息
  return { id: userId, name: "John Doe" };
};

// 身份验证装饰器
function AuthenticationDecorator(userService) {
  this.userService = userService;
}

AuthenticationDecorator.prototype.getUser = function(userId) {
  this.authenticateUser();
  return this.userService.getUser(userId);
};

AuthenticationDecorator.prototype.authenticateUser = function() {
  console.log("Authenticating user...");
  // 进行身份验证逻辑
};

// 日志记录装饰器
function LoggingDecorator(userService) {
  this.userService = userService;
}

LoggingDecorator.prototype.getUser = function(userId) {
  this.logRequest(userId);
  return this.userService.getUser(userId);
};

LoggingDecorator.prototype.logRequest = function(userId) {
  console.log("Logging request for user with ID: " + userId);
  // 记录请求日志
};

// 缓存装饰器
function CachingDecorator(userService) {
  this.userService = userService;
  this.cache = {};
}

CachingDecorator.prototype.getUser = function(userId) {
  if (this.cache[userId]) {
    console.log("Fetching user from cache with ID: " + userId);
    return this.cache[userId];
  }

  var user = this.userService.getUser(userId);
  this.cache[userId] = user;
  return user;
};

// 创建原始的 UserService 对象
var userService = new UserService();

// 使用装饰器进行功能拓展
var decoratedUserService = new CachingDecorator(
  new LoggingDecorator(new AuthenticationDecorator(userService))
);

// 调用拓展后的方法
var user1 = decoratedUserService.getUser(123);
var user2 = decoratedUserService.getUser(456);
var user3 = decoratedUserService.getUser(123);

console.log(user1);
console.log(user2);
console.log(user3);
```

ES5实现

```js
// 定义一个基本的用户服务类 UserService，它提供了一些基本的用户操作方法：
class UserService {
  getUser(userId) {
    console.log(`Getting user with ID: ${userId}`);
    // 模拟从数据库获取用户信息
    return { id: userId, name: "John Doe" };
  }
}

// 定义装饰器类，用于拓展 UserService 的功能：
// 身份验证装饰器
class AuthenticationDecorator {
  constructor(userService) {
    this.userService = userService;
  }

  getUser(userId) {
    this.authenticateUser();
    return this.userService.getUser(userId);
  }

  authenticateUser() {
    console.log("Authenticating user...");
    // 进行身份验证逻辑
  }
}

// 日志记录装饰器
class LoggingDecorator {
  constructor(userService) {
    this.userService = userService;
  }

  getUser(userId) {
    this.logRequest(userId);
    return this.userService.getUser(userId);
  }

  logRequest(userId) {
    console.log(`Logging request for user with ID: ${userId}`);
    // 记录请求日志
  }
}

// 缓存装饰器
class CachingDecorator {
  constructor(userService) {
    this.userService = userService;
    this.cache = new Map();
  }

  getUser(userId) {
    if (this.cache.has(userId)) {
      console.log(`Fetching user from cache with ID: ${userId}`);
      return this.cache.get(userId);
    }

    const user = this.userService.getUser(userId);
    this.cache.set(userId, user);
    return user;
  }
}

// 使用装饰器来包装 UserService 对象，以实现功能的拓展
// 创建原始的 UserService 对象
const userService = new UserService();

// 使用装饰器进行功能拓展
const decoratedUserService = new CachingDecorator(
  new LoggingDecorator(new AuthenticationDecorator(userService))
);

// 调用拓展后的方法
const user1 = decoratedUserService.getUser(123);
const user2 = decoratedUserService.getUser(456);
const user3 = decoratedUserService.getUser(123);

console.log(user1);
console.log(user2);
console.log(user3);
```

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

### 01 模板方法模式

- 父类中定义一组操作算法骨架，而降一些实现步骤延迟到子类中，使得子类可以不改变父类的算法机构的同时可重新定义算法中某些实现步骤
- 将多个模型抽象化归一，从中抽象提出出一个最基本的模板，其他模块只需要继承这个模板方法，也可以拓展某些方法
- 继承类也可以作为模板类

### ⭐02 观察者模式

观察者模式（Observer Pattern）是一种行为型设计模式，也被称为发布-订阅者模式或消息机制。它定义了一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都会得到通知并自动更新。

观察者模式包含以下几个核心角色：

1. 主体（Subject）：也称为被观察者或发布者，它维护一系列观察者对象，并在状态变化时通知观察者。
2. 观察者（Observer）：也称为订阅者或监听者，它定义了接收和处理主体通知的方法。
3. 消息（Message）：作为观察者和主体之间进行通信的数据，包含消息类型和相关的参数。
4. 消息容器（Message Container）：用于存储和管理订阅者注册的消息。

观察者模式的基本方法包括：

- 接收消息（Register）：将订阅者注册的消息推入消息容器中，包括消息类型和处理动作。
- 发布消息（Publish）：当主体对象发布一个消息时，将所有订阅了该消息类型的观察者依次执行相应的处理动作，包括消息类型和行为参数。

观察者模式的优点在于它实现了主体和观察者之间的解耦，使得它们可以独立地进行扩展和变化。主体对象不需要关心具体的观察者，而观察者也不需要知道主体对象的细节，从而实现了松耦合的设计。

观察者模式在实际应用中非常常见，例如事件处理、GUI编程、消息队列等场景中都可以使用观察者模式来实现事件的订阅和通知机制。

总之，观察者模式通过定义一种依赖关系，使主体对象与观察者对象解耦，并实现了一对多的通知机制。它提供了一种灵活的方式来实现发布-订阅的场景，并支持动态的添加和移除观察者。

> 假设我们有一个简单的新闻发布系统，其中包含一个新闻主题（Subject）和多个订阅者（Observers）。每当有新闻发布时，订阅者都会收到相应的通知并进行相应的处理。

```js
// 主题（Subject）- 新闻发布者
function NewsPublisher() {
  this.observers = []; // 订阅者列表
}

// 注册订阅者
NewsPublisher.prototype.registerObserver = function(observer) {
  this.observers.push(observer);
};

// 取消注册订阅者
NewsPublisher.prototype.unregisterObserver = function(observer) {
  var index = this.observers.indexOf(observer);
  if (index !== -1) {
    this.observers.splice(index, 1);
  }
};

// 发布新闻
NewsPublisher.prototype.publishNews = function(news) {
  console.log("Publishing news: " + news);
  this.notifyObservers(news);
};

// 通知所有订阅者
NewsPublisher.prototype.notifyObservers = function(news) {
  var self = this;
  this.observers.forEach(function(observer) {
    observer.update(news);
  });
};

// 订阅者（Observer）- 新闻订阅者
function NewsSubscriber(name) {
  this.name = name;
}

// 更新方法
NewsSubscriber.prototype.update = function(news) {
  console.log(this.name + " received news: " + news);
};

// 创建新闻发布者和订阅者
var publisher = new NewsPublisher();

var subscriber1 = new NewsSubscriber("Subscriber 1");
var subscriber2 = new NewsSubscriber("Subscriber 2");
var subscriber3 = new NewsSubscriber("Subscriber 3");

// 订阅者注册到发布者
publisher.registerObserver(subscriber1);
publisher.registerObserver(subscriber2);
publisher.registerObserver(subscriber3);

// 发布新闻
publisher.publishNews("Breaking News: COVID-19 Vaccine Approved!");

// 输出：
// Publishing news: Breaking News: COVID-19 Vaccine Approved!
// Subscriber 1 received news: Breaking News: COVID-19 Vaccine Approved!
// Subscriber 2 received news: Breaking News: COVID-19 Vaccine Approved!
// Subscriber 3 received news: Breaking News: COVID-19 Vaccine Approved!
```

ES6实现

```js
// 主题（Subject）- 新闻发布者
class NewsPublisher {
  constructor() {
    this.observers = []; // 订阅者列表
  }

  // 注册订阅者
  registerObserver(observer) {
    this.observers.push(observer);
  }

  // 取消注册订阅者
  unregisterObserver(observer) {
    const index = this.observers.indexOf(observer);
    if (index !== -1) {
      this.observers.splice(index, 1);
    }
  }

  // 发布新闻
  publishNews(news) {
    console.log(`Publishing news: ${news}`);
    this.notifyObservers(news);
  }

  // 通知所有订阅者
  notifyObservers(news) {
    this.observers.forEach(observer => {
      observer.update(news);
    });
  }
}

// 订阅者（Observer）- 新闻订阅者
class NewsSubscriber {
  constructor(name) {
    this.name = name;
  }

  // 更新方法
  update(news) {
    console.log(`${this.name} received news: ${news}`);
  }
}

// 创建新闻发布者和订阅者
const publisher = new NewsPublisher();

const subscriber1 = new NewsSubscriber('Subscriber 1');
const subscriber2 = new NewsSubscriber('Subscriber 2');
const subscriber3 = new NewsSubscriber('Subscriber 3');

// 订阅者注册到发布者
publisher.registerObserver(subscriber1);
publisher.registerObserver(subscriber2);
publisher.registerObserver(subscriber3);

// 发布新闻
publisher.publishNews('Breaking News: COVID-19 Vaccine Approved!');

// 输出：
// Publishing news: Breaking News: COVID-19 Vaccine Approved!
// Subscriber 1 received news: Breaking News: COVID-19 Vaccine Approved!
// Subscriber 2 received news: Breaking News: COVID-19 Vaccine Approved!
// Subscriber 3 received news: Breaking News: COVID-19 Vaccine Approved!
```



### 03 状态模式

- 当一个对象的内部状态发生改变时，会导致其行为的改变。
- 对于分支条件内部独立结果的管理，可以使用状态模式
- 每一种条件作为对象内部的一种状态，面对不同判断结果，它其实就是选择对象内的一种状态
- 对于状态模式，主要目的就是将条件判断的不同结果转化为对象内部的状态，既然是状态对象的内部状态，所以一般作为状态对象内部的私有变量，然后提供一个能够调用状态对象内部状态的接口方法对象。这样方便管理状态。

### ⭐04 策略模式

策略模式是一种行为型设计模式，它允许在运行时选择算法的行为。该模式将一组算法封装成独立的对象，使它们可以相互替换，而不会影响客户端代码。

策略模式的主要思想是将算法的定义和使用相互分离，使得算法可以独立于客户端变化而变化。它将每个算法封装在一个独立的策略类中，并通过一个公共接口让客户端可以动态地选择和使用不同的算法。

在策略模式中，客户端通过使用一个上下文对象来执行特定的算法。上下文对象持有一个策略对象的引用，并将具体的任务委托给策略对象来处理。客户端可以根据需要在运行时切换不同的策略对象，而不需要修改客户端的代码。

策略模式的优点在于可以提供灵活性和可扩展性。通过将算法封装在策略类中，可以轻松地增加、修改或替换算法，而无需修改客户端的代码。这使得系统更具可维护性和可测试性。

总之，策略模式通过封装一组算法，使其可以相互替换，并与客户端解耦。它提供了一种灵活的方式来选择和执行不同的算法，以满足不同的需求。

1、一个典型的应用场景是表单验证。在表单中，可能会有多个不同的验证规则，例如必填字段、长度限制、格式验证等。每个验证规则都可以封装成一个具体的策略类，而表单对象充当上下文对象。客户端可以根据实际需求选择不同的验证策略，并将表单对象委托给相应的策略对象进行验证。

首先，我们定义一个表单对象作为上下文对象：

```javascript
function Form() {
  this.fields = [];
}

Form.prototype.addField = function(field) {
  this.fields.push(field);
};

Form.prototype.validate = function() {
  var isValid = true;

  for (var i = 0; i < this.fields.length; i++) {
    var field = this.fields[i];

    if (!field.validate()) {
      isValid = false;
    }
  }

  return isValid;
};
```

然后，我们定义不同的验证规则作为具体的策略类：

```javascript
// 必填字段验证策略
function RequiredFieldStrategy() {}

RequiredFieldStrategy.prototype.validate = function(value) {
  return value !== '';
};

// 长度限制验证策略
function LengthLimitStrategy(maxLength) {
  this.maxLength = maxLength;
}

LengthLimitStrategy.prototype.validate = function(value) {
  return value.length <= this.maxLength;
};

// 格式验证策略
function FormatValidationStrategy(pattern) {
  this.pattern = pattern;
}

FormatValidationStrategy.prototype.validate = function(value) {
  return this.pattern.test(value);
};
```

最后，我们可以在客户端代码中使用表单对象和验证策略：

```javascript
// 创建表单对象
var form = new Form();

// 添加字段到表单
var usernameField = { name: 'username', value: '', strategy: new RequiredFieldStrategy() };
var passwordField = { name: 'password', value: 'password123', strategy: new LengthLimitStrategy(8) };
var emailField = { name: 'email', value: 'example.com', strategy: new FormatValidationStrategy(/\S+@\S+\.\S+/) };

form.addField(usernameField);
form.addField(passwordField);
form.addField(emailField);

// 验证表单字段
var isValid = form.validate();
console.log('Form is valid:', isValid); // 输出：Form is valid: false
```

在上面的例子中，我们使用策略模式来实现表单验证。表单对象充当上下文对象，而每个验证规则（必填字段、长度限制、格式验证）充当具体的策略类。

客户端可以根据需要选择不同的验证策略，并将相应的验证策略对象设置给表单字段对象的`strategy`属性。调用表单对象的`validate`方法时，会委托给各个字段的验证策略对象进行验证，并返回最终的验证结果。

2、假设我们正在开发一个电商网站，其中有一个购物车功能，我们希望能够根据不同的促销策略计算购物车中商品的总价格。

首先，我们定义一个购物车对象（上下文对象）：

```javascript
function ShoppingCart() {
  this.items = [];
}

ShoppingCart.prototype.addItem = function(item) {
  this.items.push(item);
};

ShoppingCart.prototype.calculateTotalPrice = function() {
  // 假设这里有一些其他的逻辑处理

  // 根据当前的促销策略计算商品的总价格
  if (this.pricingStrategy) {
    return this.pricingStrategy.calculateTotalPrice(this.items);
  } else {
    // 默认情况下，没有设置促销策略时，直接计算商品的原始总价格
    return this.items.reduce(function(total, item) {
      return total + item.price;
    }, 0);
  }
};
```

然后，我们定义促销策略对象（具体的策略类）：

```javascript
// 普通促销策略：不打折，直接计算商品原始总价格
function RegularPricingStrategy() {}

RegularPricingStrategy.prototype.calculateTotalPrice = function(items) {
  return items.reduce(function(total, item) {
    return total + item.price;
  }, 0);
};

// 折扣促销策略：对商品总价格进行折扣
function DiscountPricingStrategy(discount) {
  this.discount = discount;
}

DiscountPricingStrategy.prototype.calculateTotalPrice = function(items) {
  var totalPrice = items.reduce(function(total, item) {
    return total + item.price;
  }, 0);

  return totalPrice * (1 - this.discount);
};
```

最后，我们可以在客户端代码中使用购物车对象和促销策略对象：

```javascript
// 创建购物车对象
var cart = new ShoppingCart();

// 添加商品到购物车
cart.addItem({ name: 'Product 1', price: 10 });
cart.addItem({ name: 'Product 2', price: 20 });
cart.addItem({ name: 'Product 3', price: 30 });

// 设置促销策略为折扣促销策略（打8折）
cart.pricingStrategy = new DiscountPricingStrategy(0.2);

// 计算购物车商品的总价格
var totalPrice = cart.calculateTotalPrice();
console.log('Total Price:', totalPrice); // 输出：48

// 切换促销策略为普通促销策略
cart.pricingStrategy = new RegularPricingStrategy();

// 重新计算购物车商品的总价格
totalPrice = cart.calculateTotalPrice();
console.log('Total Price:', totalPrice); // 输出：60
```

在上面的例子中，我们使用策略模式来计算购物车中商品的总价格。购物车对象充当上下文对象，而普通促销策略和折扣促销策略充当具体的策略类。

客户端可以根据需求选择不同的促销策略，将其设置给购物车对象的`pricingStrategy`

### ⭐05 职责链模式

职责链模式（Chain of Responsibility Pattern）是一种行为型设计模式，它通过将请求的发送者和接收者解耦，使多个对象都有机会处理这个请求。请求在一条职责链上依次传递，直到有一个对象能够处理它为止。

职责链模式的核心思想是将请求和处理分离，每个处理者都只关注自己能处理的请求，并将不能处理的请求传递给下一个处理者。这样可以实现请求的传递和处理的解耦，提高系统的灵活性和可维护性。

职责链模式包含以下几个角色：

1. 抽象处理者（Handler）：定义了处理请求的接口，并持有下一个处理者的引用。
2. 具体处理者（ConcreteHandler）：实现抽象处理者的接口，负责处理特定类型的请求，如果自己不能处理，则将请求传递给下一个处理者。

职责链模式的工作流程如下：

1. 客户端创建一个职责链，并将处理请求的对象按照一定的顺序连接起来形成一条链。
2. 当一个请求发生时，从链的头部开始，每个处理者判断自己是否能够处理该请求，如果能够处理，则处理请求并结束；如果不能处理，则将请求传递给下一个处理者。
3. 请求在链上依次传递，直到有一个处理者能够处理它为止，或者到达链的末尾仍然没有处理者能够处理该请求。

职责链模式的优点在于它能够动态地组织和管理对象之间的关系，使系统更灵活和可扩展。它使得请求的发送者和接收者解耦，增强了代码的可维护性和可测试性。同时，职责链模式也有助于避免请求的发送者与接收者之间的耦合，提高了系统的灵活性。

> 假设我们有一个家庭智能设备控制系统，其中包含了多个设备，例如电灯、空调和电视。我们希望能够通过命令的方式控制这些设备的开关状态。
>

首先，我们定义一个抽象命令类 `Command`，它包含了执行命令和撤销命令的方法。

```javascript
// 抽象命令类
class Command {
  execute() {}
  undo() {}
}
```

然后，我们实现具体的命令类，例如开灯命令、关灯命令、开空调命令、关空调命令等。

```javascript
// 开灯命令
class LightOnCommand extends Command {
  constructor(light) {
    super();
    this.light = light;
  }

  execute() {
    this.light.turnOn();
  }

  undo() {
    this.light.turnOff();
  }
}

// 关灯命令
class LightOffCommand extends Command {
  constructor(light) {
    super();
    this.light = light;
  }

  execute() {
    this.light.turnOff();
  }

  undo() {
    this.light.turnOn();
  }
}

// 开空调命令
class ACOnCommand extends Command {
  constructor(ac) {
    super();
    this.ac = ac;
  }

  execute() {
    this.ac.turnOn();
  }

  undo() {
    this.ac.turnOff();
  }
}

// 关空调命令
class ACOffCommand extends Command {
  constructor(ac) {
    super();
    this.ac = ac;
  }

  execute() {
    this.ac.turnOff();
  }

  undo() {
    this.ac.turnOn();
  }
}
```

接下来，我们定义设备类，例如电灯类和空调类。

```javascript
// 电灯类
class Light {
  turnOn() {
    console.log('Light is turned on');
  }

  turnOff() {
    console.log('Light is turned off');
  }
}

// 空调类
class AC {
  turnOn() {
    console.log('AC is turned on');
  }

  turnOff() {
    console.log('AC is turned off');
  }
}
```

最后，我们可以创建控制器类，它包含了执行命令和撤销命令的方法，并通过命令对象来操作设备。

```javascript
class Controller {
  constructor() {
    this.commands = [];
  }

  addCommand(command) {
    this.commands.push(command);
  }

  executeCommand() {
    for (const command of this.commands) {
      command.execute();
    }
  }

  undoCommand() {
    for (const command of this.commands.reverse()) {
      command.undo();
    }
  }
}
```

现在，我们可以测试这个家庭智能设备控制系统。

```javascript
// 创建设备对象
const light = new Light();
const ac = new AC();

// 创建命令对象
const lightOnCommand = new LightOnCommand(light);
const lightOffCommand = new LightOffCommand(light);
const acOnCommand = new ACOnCommand(ac);
const acOffCommand = new ACOffCommand(ac);

// 创建控制器对象
const controller = new Controller();

// 添加命令到控制器
controller.addCommand(lightOnCommand);
controller.addCommand(acOnCommand);
controller.add
```

### 06 命令模式

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

迭代器模式（Iterator Pattern）是一种行为型设计模式，它提供一种顺序访问聚合对象中各个元素的方法，而又不需要暴露该对象的内部结构。

迭代器模式将遍历和迭代的责任封装到迭代器对象中，而不是由聚合对象来进行遍历。这样做的好处是可以让聚合对象和迭代算法相互独立，彼此不受影响。聚合对象只需要提供一个创建迭代器的方法，而迭代器负责管理遍历过程。

迭代器模式通常包含以下几个角色：

1. 迭代器接口（Iterator）：定义了遍历聚合对象的方法，包括获取当前元素、移动到下一个元素等操作。
2. 具体迭代器（ConcreteIterator）：实现迭代器接口，负责实现具体的遍历算法。
3. 聚合对象接口（Aggregate）：定义了创建迭代器的方法。
4. 具体聚合对象（ConcreteAggregate）：实现聚合对象接口，负责创建具体迭代器。

迭代器模式的核心思想是将遍历和迭代的责任分离，使得聚合对象和迭代器对象可以独立变化，互不影响。聚合对象只需要提供迭代器的接口，而不需要暴露内部结构，从而提高了封装性和灵活性。

在 ES5 中实现迭代器模式需要借助于闭包和函数对象的特性。下面是一个使用 ES5 实现迭代器模式的简单案例：

```javascript
// 迭代器函数
function createIterator(array) {
  var index = 0;

  // 返回迭代器对象
  return {
    hasNext: function() {
      return index < array.length;
    },

    next: function() {
      return array[index++];
    }
  };
}

// 聚合对象
var aggregate = {
  data: [1, 2, 3, 4, 5],

  // 创建迭代器
  createIterator: function() {
    return createIterator(this.data);
  }
};

// 使用迭代器遍历聚合对象
var iterator = aggregate.createIterator();
while (iterator.hasNext()) {
  console.log(iterator.next());
}
```

在这个案例中，我们定义了一个 `createIterator` 函数，它接受一个数组作为参数，并返回一个迭代器对象。迭代器对象包含了 `hasNext` 和 `next` 方法，用于判断是否还有下一个元素并获取下一个元素。

聚合对象 `aggregate` 中包含了一个数据数组和 `createIterator` 方法，用于创建对应的迭代器对象。

最后，我们使用迭代器遍历聚合对象的数据数组。首先调用 `aggregate.createIterator()` 方法创建迭代器对象，然后使用 `while` 循环和迭代器的 `hasNext` 和 `next` 方法遍历数据并输出结果。

这个案例展示了如何使用 ES5 实现简单的迭代器模式，通过迭代器对象和聚合对象的配合使用，实现了对聚合对象内部元素的顺序访问，同时又不需要暴露内部结构。

### 11 解释器模式

- 对于一种语言，给出其文法形式，并定义一种解释器，通过使用这种解释器来解释语言中定义的句子

## 第五篇 技巧型设计模式

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

JavaScript 中的 MVVM（Model-View-ViewModel）设计模式是一种用于构建用户界面的架构模式。它将应用程序分为三个主要部分：模型（Model）、视图（View）和视图模型（ViewModel）。

1. 模型（Model）：
   模型表示应用程序的数据和业务逻辑。它可以是一个简单的 JavaScript 对象或一个复杂的数据结构。模型通常包含用于获取、保存和更新数据的方法。

2. 视图（View）：
   视图是用户界面的可见部分，它负责展示数据和与用户进行交互。在 JavaScript 中，视图通常由 HTML 和 CSS 组成，但也可以使用 JavaScript 框架（如 React 或 Angular）创建动态视图。

3. 视图模型（ViewModel）：
   视图模型是连接模型和视图的桥梁。它将模型中的数据转换为视图可以使用的格式，并将视图中的用户交互操作转换为对模型的操作。视图模型通常包含与用户交互相关的命令、属性和事件处理程序。

MVVM 的核心思想是数据绑定。视图和视图模型之间建立了双向的数据绑定关系，当模型的数据改变时，视图会自动更新，当用户在视图中进行操作时，视图模型会自动更新模型的数据。

在 JavaScript 中，有一些流行的框架和库可以帮助实现 MVVM 设计模式，例如 Vue.js 和 Knockout.js。这些框架提供了方便的工具和机制来处理数据绑定、视图更新和用户交互等方面的任务，简化了 MVVM 的实现过程。

MVVM的优点包括：

1. 分离关注点：MVVM将数据逻辑与用户界面分开，使代码更易于维护和测试。

2. 可重用性：视图模型可以独立于具体的视图进行测试和重用，从而提高开发效率。

3. 可扩展性：由于模型、视图和视图模型之间的明确分离，可以轻松添加新的视图和视图模型，而无需修改现有代码。

4. 支持团队协作：MVVM通过明确定义各组件之间的接口和通信方式，促进了团队合作和并行开发。

需要注意的是，MVVM并非适用于所有类型的应用程序，而是特别适用于具有复杂用户界面和大量数据交互的应用程序。它通常与现代的前端框架和库（如WPF、Angular、Vue.js等）结合使用。

在 JavaScript 中实现 MVVM 设计模式，可以按照以下步骤进行：

1. 定义模型（Model）： 创建一个 JavaScript 对象或类来表示应用程序的数据和业务逻辑。模型应该包含用于获取、保存和更新数据的方法。
2. 创建视图（View）： 使用 HTML、CSS 和 JavaScript 框架（如 React、Angular 或 Vue.js）创建用户界面的可见部分。视图应该能够展示数据和响应用户的交互操作。
3. 创建视图模型（ViewModel）： 创建一个 JavaScript 对象或类来充当视图和模型之间的桥梁。视图模型应该包含与用户交互相关的命令、属性和事件处理程序。
4. 实现数据绑定： 在视图模型中创建属性，并将其与视图中的元素进行绑定。这可以通过使用框架提供的数据绑定语法或手动实现观察者模式来完成。当模型的数据发生变化时，视图模型会自动更新绑定的属性，进而更新视图。
5. 处理用户交互： 在视图模型中定义命令和事件处理程序，用于响应用户在视图中的交互操作。这些命令和事件处理程序可以修改模型的数据，从而触发数据绑定机制，使视图自动更新。
6. 连接模型、视图和视图模型： 在应用程序的入口点，创建模型、视图和视图模型的实例，并将它们连接起来。这可以通过手动实例化对象并建立关联，或使用框架提供的机制（如组件或指令）来完成。

```js
// 模型（Model）
function Model() {
  this.data = {
    message: 'Hello, MVVM!',
  };
}

// 视图模型（ViewModel）
function ViewModel(model) {
  this.model = model;
  this.message = '';

  // 数据绑定
  Object.defineProperty(this, 'message', {
    get: function() {
      return this.model.data.message;
    },
    set: function(value) {
      this.model.data.message = value;
    },
  });
}

// 视图（View）
function View(viewModel) {
  this.viewModel = viewModel;

  // 初始化视图
  this.init = function() {
    var messageInput = document.getElementById('messageInput');
    var messageDisplay = document.getElementById('messageDisplay');

    // 绑定输入框与视图模型属性
    messageInput.value = this.viewModel.message;
    messageInput.addEventListener('input', function(event) {
      this.viewModel.message = event.target.value;
    }.bind(this));

    // 绑定视图模型属性与显示元素
    Object.defineProperty(this.viewModel, 'message', {
      get: function() {
        return messageDisplay.innerText;
      },
      set: function(value) {
        messageDisplay.innerText = value;
      },
    });
  };
}

// 实例化模型、视图模型和视图
var model = new Model();
var viewModel = new ViewModel(model);
var view = new View(viewModel);

// 初始化视图
view.init();
```

> 作者：何建博本尊
> 链接：https://juejin.cn/post/6844903954036293640
> 来源：稀土掘金
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。