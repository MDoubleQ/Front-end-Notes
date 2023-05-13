# 写在前头

最近看执行上下文，一直没有找到很好的文章或者书籍。大多数都是ES3的旧解释了。

**执行上下文在 ES3 中，包含三个部分。**

scope：作用域，也常常被叫做作用域链。

variable object：变量对象，用于存储变量的对象。

this value：this 值。

**在 ES5 中，我们改进了命名方式，把执行上下文最初的三个部分改为下面这个样子。**

lexical environment：词法环境，当获取变量时使用。

variable environment：变量环境，当声明变量时使用。

this value：this 值。

**在 ES2018 中，执行上下文又变成了这个样子，this 值被归入 lexical environment，但是增加了不少内容。**

lexical environment：词法环境，当获取变量或者 this 值时使用。

variable environment：变量环境，当声明变量时使用

code evaluation state：用于恢复代码执行位置。

Function：执行的任务是函数时使用，表示正在被执行的函数。

ScriptOrModule：执行的任务是脚本或者模块时使用，表示正在被执行的代码。

Realm：使用的基础库和内置对象实例。

Generator：仅生成器上下文有这个属性，表示当前生成器。

下面是我推荐的不同版本的执行上下文的文章

- ES3

冴羽老师的 [JavaScript深入之执行上下文](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fmqyqingfeng%2FBlog%2Fissues%2F8)

- ES5

掘金翻译计划 [[译\] 理解 JavaScript 中的执行上下文和执行栈](https://juejin.cn/post/6844903682283143181#heading-9)

- ES2018

原文地址：[Understanding Execution Context and Execution Stack in Javascript](https://link.juejin.cn?target=https%3A%2F%2Fblog.bitsrc.io%2Funderstanding-execution-context-and-execution-stack-in-javascript-1c9ea8642dd0) （要翻墙） 下面的内容就是我翻译的这篇文章（四级水平加机翻，yyds）

# 了解JavaScript程序是如何内部执行的

如果您是或想成为一名JavaScript开发人员，那么您必须知道JavaScript程序是如何在内部执行的。理解执行上下文和执行堆栈对于理解其他JavaScript概念(如提升、作用域和闭包)至关重要。

正确理解执行上下文和执行堆栈的概念将使您成为更好的JavaScript开发人员。

闲话少说，让我们开始吧:)

# 什么是执行上下文?

简单地说，执行上下文是评估和执行Javascript代码的环境的一个抽象概念。任何代码在JavaScript中运行时，都在执行上下文中运行。

## 执行上下文的类型（Types of Execution Context）

在JavaScript中有三种类型的执行上下文。

- 全局执行上下文——这是默认的或基本的执行上下文。任何不在函数内部的代码位于全局执行上下文中。它执行两件事:它创建一个全局对象，它是一个window对象(在浏览器的情况下)，并将this的值设置为等于全局对象。一个程序中只能有一个全局执行上下文。
- 函数执行上下文——每次调用函数时，都会为该函数创建一个全新的执行上下文。每个函数都有自己的执行上下文，但它是在调用或调用（原文是it’s created when the function is invoked or called）函数时创建的。可以有任意数量的函数执行上下文。每当创建一个新的执行上下文时，它都会按照已定义的顺序执行一系列步骤，我将在本文后面讨论这些步骤。
- Eval函数执行上下文——在`Eval`函数内部执行的代码也会获得它自己的执行上下文，但JavaScript开发人员通常不使用`Eval`，所以我在这里不讨论它。

## 执行栈（Execution Stack）

执行栈，在其他编程语言中也被称为“调用栈”，是一个具有后进先出结构的栈，它用于存储代码执行期间创建的所有执行上下文。

当JavaScript引擎第一次遇到脚本时，它会创建一个全局执行上下文，并将其推入当前执行栈。每当引擎发现一个函数调用时，它就会为该函数创建一个新的执行上下文，并将其推到栈的顶部。

引擎会执行那些执行上下文位于栈顶部的函数。当这个函数完成时，它的执行栈从栈中弹出，控件到达当前栈中被弹出的上下文的下面的上下文。

让我们通过下面的代码示例来理解这一点:

```js
let a = 'Hello World!';
function first() {
  console.log('Inside first function');
  second();
  console.log('Again inside first function');
}
function second() {
  console.log('Inside second function');
}
first();
console.log('Inside Global Execution Context');

```

![img](E:\coder\09_OneNote\image\3cfcee9ac06f4aeea9bb9423eadd7b53tplv-k3u1fbpfcp-zoom-in-crop-mark4536000.webp)

图片就是上面代码的执行上下文堆栈。

当浏览器加载上述代码时，Javascript引擎会创建一个全局执行上下文，并将其推入当前执行栈。当遇到对`first()`的调用时，Javascript引擎会为该函数创建一个新的执行上下文（函数执行上下文），并将其推到当前执行堆栈的顶部。

当在`first()`函数中调用`second()`函数时，Javascript引擎会为该函数创建一个新的执行上下文，并将其推到当前执行栈的顶部。当`second()`函数结束时，它的执行上下文从当前栈中弹出，控件到达它下面的执行上下文，也就是`first()`函数的执行上下文。

# 如何创建执行上下文?

到目前为止，我们已经看到了JavaScript引擎是如何管理执行上下文的，现在让我们来理解JavaScript引擎是如何创建执行上下文的。

执行上下文的创建分为两个阶段:1)创建阶段和2)执行阶段。

## 组件创建阶段（The Creation Phase）

执行上下文在创建阶段创建。在创建阶段会发生以下事情:

1. 创建LexicalEnvironment组件。
2. 创建VariableEnvironment组件。

因此，执行上下文可以在概念上表示为:

```ini
ExecutionContext = {
  LexicalEnvironment = <ref. to LexicalEnvironment in memory>,
  VariableEnvironment = <ref. to VariableEnvironment in  memory>,
}

```

## 词法环境（Lexical Environment）

**[官方ES6文档](https://link.juejin.cn?target=https%3A%2F%2F262.ecma-international.org%2F6.0%2F)将词汇环境定义为**

（词法环境）Lexical Environment是一种规范类型，用于根据ECMAScript代码的词法嵌套结构定义标识符与特定变量和函数的关联。词法环境由一个环境记录和一个可能为空的外部词汇环境引用组成。

简单地说，词法环境是一个保存标识符-变量映射的结构。(这里标识符指的是变量/函数的名称，变量是对实际对象[包括函数对象和数组对象]或原始数据的引用)。

例如，考虑下面的代码片段:

```ini
var a = 20;
var b = 40;
function foo() {
  console.log('bar');
}

```

所以上面代码片段的词法环境是这样的:

```yaml
lexicalEnvironment = {
  a: 20,
  b: 40,
  foo: <ref. to foo function>
}

```

每个词法环境有三个组成部分:

1. Environment Record（环境记录器）
2. Reference to the outer environment（指向外部环境的引用）
3. This binding. （this绑定）

### Environment Record （环境记录器）

环境记录器是变量和函数声明存储在词法环境中的位置。

此外，环境记录器亦有两类:

- **声明性环境记录（Declarative environment record）**——顾名思义，它存储变量和函数声明。函数代码的词法环境包含一个声明性环境记录。
- **对象环境记录（Object environment record）**——全局代码（global code）的词法环境包含一个客观环境记录（objective environment record）。除了变量和函数声明，对象环境记录（the object environment record）还存储了一个全局绑定对象(浏览器中的window对象)。因此，对于每个绑定对象的属性(在浏览器中，它包含浏览器提供给window对象的属性和方法)，记录中会创建一个新条目（new entry）。

注意:对于函数代码（function code），环境记录还包含一个参数对象（argument对象），该对象包含传递给函数的索引和参数之间的映射，以及传递给函数的参数的长度(数量)。例如，下面函数的参数对象是这样的:

```js
function foo(a, b) {
  var c = a + b;
}
foo(2, 3);
// argument object
Arguments: {0: 2, 1: 3, length: 2},

```

### Reference to the Outer Environment（指向外部环境的引用）

**Reference to the Outer Environment**指的是它能够接触到外部的词法环境。这意味着，如果在当前词法环境中没有找到想要查找的变量，JavaScript引擎可以在外部环境中查找它们。

### This Binding （this绑定）

在此组件中，this的值被确定或设置（determined or set）。

在全局执行上下文中，this的值指向全局对象。(在浏览器中，它指的是Window对象)。

在函数执行上下文中，this的值取决于函数的调用方式。如果它是通过对象引用调用的，那么this的值被设置为该对象，否则，this的值被设置为全局对象或未定义(在严格模式下)。例如:

```js
const person = {
  name: 'peter',
  birthYear: 1994,
  calcAge: function() {
    console.log(2018 - this.birthYear);
  }
}
person.calcAge(); 
// 'this' refers to 'person', because 'calcAge' was called with 'person' object reference
// 'this'指的是'person'，因为'calcAge'是用'person'对象引用调用的
const calculateAge = person.calcAge;
calculateAge();
// 'this' refers to the global window object, because no object reference was given
// 'this'引用全局window对象，因为没有给出对象引用

```

抽象地说，伪代码中的词法环境是这样的:

```js
GlobalExectionContext = {
  LexicalEnvironment: {
    EnvironmentRecord: {
      Type: "Object",
      // Identifier bindings go here
      // 标识符绑定到这里
    }
    outer: <null>,
    this: <global object>
  }
}
FunctionExectionContext = {
  LexicalEnvironment: {
    EnvironmentRecord: {
      Type: "Declarative",
      // Identifier bindings go here
      // 标识符绑定到这里
    }
    outer: <Global or outer function environment reference>,
    this: <depends on how function is called>
  }
}

```

## 变量环境 （Variable Environment）

它也是一个词法环境，它的环境记录器（EnvironmentRecord）保存由VariableStatements 在执行上下文中创建的绑定。

如上所述，变量环境也是一个词法环境，因此它具有上述定义的词法环境的所有属性和组件。

在ES6中，词法环境（LexicalEnvironment）组件和变量环境（VariableEnvironment）组件之间的一个区别是，前者用于存储函数声明和变量(let和const)绑定，而后者仅用于存储变量(var)绑定。

## 执行程序阶段（Execution Phase）

在这个阶段，所有这些变量的赋值都完成了，代码也最终执行了。

## Example （例子）

让我们看一些例子来理解上述概念:

```js
let a = 20;
const b = 30;
var c;
function multiply(e, f) {
  var g = 20;
  return e * f * g;
}
c = multiply(20, 30);

```

当执行上述代码时（the above code is executed），JavaScript引擎创建一个全局执行上下文来执行全局代码。所以在创建阶段，全局执行上下文看起来像这样:

```js
GlobalExectionContext = {
  LexicalEnvironment: {
    EnvironmentRecord: {
      Type: "Object",
      // Identifier bindings go here
      a: < uninitialized > ,
      b: < uninitialized > ,
      multiply: < func >
    }
    outer: < null > ,
    ThisBinding: < Global Object >
  },
  VariableEnvironment: {
    EnvironmentRecord: {
      Type: "Object",
      // Identifier bindings go here
      c: undefined,
    }
    outer: < null > ,
    ThisBinding: < Global Object >
  }
}

```

在执行阶段（During the execution phase），完成变量赋值。因此，在执行阶段，全局执行上下文将类似于以下内容。

```js
GlobalExectionContext = {
  LexicalEnvironment: {
      EnvironmentRecord: {
        Type: "Object",
        // Identifier bindings go here
        a: 20,
        b: 30,
        multiply: < func >
      }
      outer: <null>,
      ThisBinding: <Global Object>
    },
  VariableEnvironment: {
      EnvironmentRecord: {
        Type: "Object",
        // Identifier bindings go here
        c: undefined,
      }
      outer: <null>,
      ThisBinding: <Global Object>
    }
  }

```

当遇到对`function multiply(20,30)`的调用时，将创建一个新的函数执行上下文来执行函数代码。所以在创建阶段，函数执行上下文看起来像这样:

```js
FunctionExectionContext = {
LexicalEnvironment: {
    EnvironmentRecord: {
      Type: "Declarative",
      // Identifier bindings go here
      Arguments: {0: 20, 1: 30, length: 2},
    },
    outer: <GlobalLexicalEnvironment>,
    ThisBinding: <Global Object or undefined>,
  },
VariableEnvironment: {
    EnvironmentRecord: {
      Type: "Declarative",
      // Identifier bindings go here
      g: undefined
    },
    outer: <GlobalLexicalEnvironment>,
    ThisBinding: <Global Object or undefined>
  }
}

```

在此之后，执行上下文将经历执行阶段（the execution phase），这意味着完成对函数内变量的赋值。所以在执行阶段，函数的执行上下文看起来像这样:

```js
FunctionExectionContext = {
LexicalEnvironment: {
    EnvironmentRecord: {
      Type: "Declarative",
      // Identifier bindings go here
      Arguments: {0: 20, 1: 30, length: 2},
    },
    outer: <GlobalLexicalEnvironment>,
    ThisBinding: <Global Object or undefined>,
  },
VariableEnvironment: {
    EnvironmentRecord: {
      Type: "Declarative",
      // Identifier bindings go here
      g: 20
    },
    outer: <GlobalLexicalEnvironment>,
    ThisBinding: <Global Object or undefined>
  }
}

```

函数完成后，返回值被存储在`c`中。因此全局词法环境被更新。之后，全局代码完成，程序结束。

注意——你可能已经注意到`let`和`const`定义的变量在创建阶段没有任何关联的值，但是`var`定义的变量被设置为`undefined`。

这是因为，在创建阶段，代码被扫描以查找变量和函数声明，而函数声明被完整地存储在环境中，变量最初被设置为未定义(对于`var`)或保持未初始化(对于`let`和`const`)。

这就是为什么你可以在声明之前访问`var`定义的变量(虽然未定义)，但在声明之前访问`let`和`const`变量时会得到引用错误的原因。

这就是我们所说的变量提升（hoisting）。

注意:在执行阶段，如果JavaScript引擎无法在源代码中声明`let`变量的实际位置找到它的值，那么它将给它赋值为`undefined`。

## 总结(Conclusion)

我们已经讨论了JavaScript程序是如何在内部执行的。虽然要成为出色的JavaScript开发人员并不需要学习所有这些概念，但充分理解上述概念将有助于您更容易、更深入地理解其他概念，如变量声明提升(hoisting)、作用域（Scope）和闭包（Closures）。

就是这样，如果你觉得这篇文章有帮助，请点击👏按钮，并随时在下面发表评论!我很乐意和😃交流



作者：默海笑
链接：https://juejin.cn/post/7129510217863299102
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。