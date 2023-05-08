# 📁JavaScript基础

## 简单聊聊JavaScript的历史

1. 1994 年，网景公司发布 Navigator 浏览器 0.9 版本
   - 发布时，Navigator 浏览器还不能有与用户的交互效果
   - 网景公司急需希望选定一门语言作为浏览器的脚本语言

2. 同年，网景公司招聘了 Brendan Eich，希望帮助选定一门脚本语言
   - 最开始是选定 Scheme 语言作为浏览器的脚本语言

3. 1995 年，Sun 公司将 Oak 语言改名为 Java 正式向市场推出
   - 轰动一时
   - Java 的口号非常吸引人"Write once Run anywhere"
   - 网景公司因此希望与 Sun 合作，希望将 Java 嵌入到网页中，作为浏览器的脚本语言
   - 这时，Brendan Eich 还是坚持选择 Scheme，而公司高层则希望简化 Java 作为脚本语言

4. Brendan Eich 用 10 天时间设计出 JavaScript，网景公司正式使用 JavaScript 作为 Navigator 的脚本语言
   - 最初命名为 Mocha
   - Navigator 2.0 beta 更名为 LIveScript
   - Navigator 2.0 beta3 正式命名为 JavaSript（一说为蹭 Java 的热度）

## 对JS引擎的理解(自己的话术总结)

JavaSript 是一门解释型语言

JS 引擎是 JavaScript 语言的运行解释器

- 浏览器内核中有两种引擎，其中一种就是 JS 引擎
  - **排版引擎**
    - 负责 HTML 和 CSS 解析和排版
  - **JS 引擎**
    - 负责解析和运行 JavaScript 语句


常见 JS 引擎有

- SpiderMonkey -> 第一款 JavaScript 引擎，Brendan Eich 开发
- Chakra -> 微软开发
- WebKit -> JavaScriptCore -> APPLE 开发
- Chrome -> V8 -> GOOGLE 开发
- 小程序 -> JSCore -> 腾讯开发

## JavaScript的交互方式有哪些？

共有四种交互方式：

1. 弹窗输出 alert("Hello World!")
2. 控制台输出 console.log("Hello World!")
3. 文档输出 document.write("Hello World!")
4. 弹出输入框输入 prompt("Please write some words!")

```js
// alert() 函数
alert("Hello World!")

// console.log() 函数
console.log("Hello World!")

// document.write() 函数
document.write("Hello World!")

// prompt() 函数
prompt()
prompt("Notification")
// 变量赋值时使用 prompt()函数
var variable = prompt("Notification")
```

## JS有哪些数据类型?它们的区别?

JavaScript有7（红宝书第四版中，无bigInt）基本数据类型和1种复杂数据类型，它们分别是：

1. number：表示数字，包括整数和浮点数。
2. string：表示文本字符串，可以包含任何字符，包括数字、字母、符号等；
3. boolean：表示布尔值，真（true）假（false）；
4. null：表示空值，表示一个空对象指针。或者不存在的值。用于未知的值，只有一个null值的独立类型；
5. undefined：表示一个未定义的值，通常是因为变量未被赋值，或者是对象没有这个属性；
6. symbol：表示唯一的标识符。
7. bigint：表示大整数，可以表示更大范围的整数。

除了基本数据类型外，JavaScript还有一种复杂数据类型：对象（Object），它是由一组无序的键值对组成的集合，包含引用类型和复杂类型；

**它们的区别在于：**

1. 基本数据类型是按值访问的，而复杂数据类型是按引用访问的。
2. 基本数据类型的值不可变，如果改变一个基本数据类型的值，实际上是创建了一个新的值。而复杂数据类型可以改变其属性和值。
3. 对于基本数据类型，可以使用typeof操作符来判断其类型，但对于对象类型，使用typeof操作符返回的是"object"。
4. 基本数据类型占用固定的内存大小，而对象类型的大小是动态的，由其属性和值的个数决定。
5. 在JavaScript中，所有数据类型都是一等公民，可以作为变量、函数的参数和返回值。

总的来说，基本数据类型是简单的、不可变的，而对象类型是复杂的、可变的，它们在不同的场景下具有不同的应用。

## 数据类型按照什么分类

在 JavaScript 中，数据类型可以分为原始类型和引用类型。

原始类型（Primitive data types）指的是存储简单数据值的数据类型，包括数字（Number）、字符串（String）、布尔值（Boolean）、null 和 undefined。这些数据类型都是按值访问的，即每个变量都包含它们自己的值，互不影响。

引用类型（Reference data types）指的是存储对象（Object）的数据类型，包括对象、数组（Array）、函数（Function）和日期（Date）等。这些数据类型都是按引用访问的，即每个变量存储的是对象在内存中的地址，多个变量可能引用同一个对象，修改一个变量的值也会影响到其他变量。

在 JavaScript 中，使用 typeof 操作符可以检测一个变量的数据类型。对于原始类型，typeof 返回对应的字符串（"number"、"string"、"boolean"、"null" 或 "undefined"）；对于引用类型，typeof 返回 "object"，无法具体区分出对象、数组、函数等不同的引用类型。

## JS数据类型考题

考题一：

```js
console.log( true + 1 );

console.log( 'name' + true );

console.log( undefined + 1 );

console.log( typeof undefined );
```

考题二：

```js
console.log( typeof(NaN) );

console.log( typeof(null) );
```

考题一：

1. `true + 1` 的结果是 `2`，因为 `true` 会被转换为数字 `1`，然后进行加法运算。
2. `'name' + true` 的结果是 `'nametrue'`，因为 `true` 会被转换为字符串 `'true'`，然后进行字符串拼接。
3. `undefined + 1` 的结果是 `NaN`，因为 `undefined` 会被转换为 `NaN`，然后进行加法运算得到 `NaN`。
4. `typeof undefined` 的结果是 `'undefined'`，因为 `undefined` 是一个原始值类型，其类型为 `'undefined'`。

考题二：

1. `typeof(NaN)` 的结果是 `'number'`，因为 `NaN` 是一个特殊的数字值，代表“非数值”（Not-A-Number）。
2. `typeof(null)` 的结果是 `'object'`，因为 `null` 是一个特殊的值，代表空对象指针/引用。历史原因造成了在 JavaScript 中使用 `typeof` 运算符检测 `null` 时会返回 `'object'`。

## 常见的运算符有哪些？

| 运算符 | 运算规则   | 范例      | 结果   |
| ------ | ---------- | --------- | ------ |
| +      | 加法       | 2 + 3     | 5      |
| +      | 连接字符串 | '中'+'国' | '中国' |
| \_     | 减法       | 2 - 3     | \-1    |
| \*     | 乘法       | 2 \* 3    | 6      |
| /      | 除法       | 5 / 2     | 2.5    |
| %      | 取余       | 5 % 2     | 1      |
| \*\*   | 幂         | 2 \*\* 3  | 8      |
| \==    | 相等       | 4 == 3    | false  |
| !=     | 不相等     | 4 != 3    | true   |
| \>     | 大于       | 4 > 3     | true   |
| <      | 小于       | 4 < 3     | false  |
| \>=    | 大于等于   | 4 <= 3    | false  |
| <=     | 小于等于   | 4 >= 3    | false  |

## parseInt和parseFloat的区别

`parseInt`和`parseFloat`都是JavaScript内置的函数，用于将字符串解析为数字类型。它们之间的主要区别在于，`parseInt`只能解析整数，而`parseFloat`可以解析整数和浮点数。

具体来说，`parseInt`函数将字符串解析为整数，如果字符串以非数字字符开头，则返回NaN（不是数字的特殊值）。例如：

```jsx
var num1 = parseInt("123"); // num1 等于 123
var num2 = parseInt("12.34"); // num2 等于 12
var num3 = parseInt("abc123"); // num3 等于 NaN
```

在第一个示例中，`parseInt`将字符串"123"解析为整数123，并将其赋值给`num1`变量。在第二个示例中，`parseInt`将字符串"12.34"解析为整数12，并将其赋值给`num2`变量。由于字符串以小数点开头，因此`parseInt`会停止解析并返回整数部分。在第三个示例中，由于字符串以非数字字符"a"开头，因此`parseInt`无法解析它并返回NaN。

另一方面，`parseFloat`函数将字符串解析为浮点数，如果字符串以非数字字符开头，则返回NaN。例如：

```js
var num1 = parseFloat("123.45"); // num1 等于 123.45
var num2 = parseFloat("12.34.56"); // num2 等于 12.34
var num3 = parseFloat("abc123"); // num3 等于 NaN
```

在第一个示例中，`parseFloat`将字符串"123.45"解析为浮点数123.45，并将其赋值给`num1`变量。在第二个示例中，由于字符串包含多个小数点，因此`parseFloat`只解析第一个小数点之前的部分，并返回浮点数12.34。在第三个示例中，由于字符串以非数字字符"a"开头，因此`parseFloat`无法解析它并返回NaN。

需要注意的是，`parseInt`和`parseFloat`都可以接受第二个参数，用于指定解析的进制（基数）。例如，可以使用`parseInt("1010", 2)`将二进制字符串"1010"解析为十进制数10。

## yield是什么

`yield`是一个关键字，用于定义生成器函数（Generator Function）中的暂停点。生成器函数是一种特殊类型的函数，可以通过调用它来创建一个生成器对象（Generator Object），该对象可以按需生成一系列值，而不需要一次性生成所有值。

在生成器函数中，可以使用`yield`语句来指定生成器在生成值时的暂停点。每次调用生成器的`next()`方法时，生成器都会执行到下一个`yield`语句处，并将`yield`语句后面的值作为`next()`方法的返回值返回。例如：

```js
function* generateSequence() {
  yield 1;
  yield 2;
  yield 3;
}

var generator = generateSequence();

console.log(generator.next()); // 输出 { value: 1, done: false }
console.log(generator.next()); // 输出 { value: 2, done: false }
console.log(generator.next()); // 输出 { value: 3, done: false }
console.log(generator.next()); // 输出 { value: undefined, done: true }
```

在这个例子中，`generateSequence`是一个生成器函数，它包含了三个`yield`语句，用于在生成器生成值时的暂停点。当生成器被创建后，可以通过调用其`next()`方法来逐个获取生成器生成的值。每次调用`next()`方法时，生成器都会执行到下一个`yield`语句处，并将其后面的值作为`next()`方法的返回值返回，直到生成器生成所有的值后返回`{ value: undefined, done: true }`。

需要注意的是，生成器函数和生成器对象只在ES6及以上的版本中被支持。另外，`yield`语句只能在生成器函数中使用，不能在普通函数中使用。

## JavaScript 操作符

[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators)

JavaScript中的操作符是用于执行各种操作的符号或单词。这些操作符可以用于算术、赋值、比较、逻辑、位运算、条件语句、函数调用、成员访问、删除、类型检查、实例检查、void 表达式、生成器和异步函数等方面。

**JavaScript中的操作符有很多种类，其中包括：**

1. 算术操作符：用于执行基本数学运算，例如加法(+), 减法(-), 乘法(\*), 除法(/), 取模(%)等。
2. 赋值操作符：用于将值赋给变量，例如等号(=), 加等于(+=), 减等于(-=), 乘等于(\*=), 除等于(/=), 取模等于(%=)等。
3. 比较操作符：用于比较两个值的大小，例如相等(==), 不相等(!=), 大于(>), 小于(<), 大于等于(>=), 小于等于(<=)等。
4. 逻辑操作符：用于组合和比较布尔值，例如逻辑与(&&), 逻辑或(||), 逻辑非(!)等。
5. 位操作符：用于对数字的二进制表示进行操作，例如按位与(&), 按位或(|), 按位异或(^), 按位非(~), 左移位(<<), 右移位(>>)等。
6. 条件操作符：也称为三元操作符，用于根据条件选择不同的值，例如表达式 ? 值1 : 值2。
7. 函数调用操作符：用于调用函数，例如函数名()。
8. 成员访问操作符：用于访问对象或数组的属性或方法，例如对象.属性或对象\["属性"\]。
9. delete 操作符：用于删除对象的属性或数组的元素，例如delete 对象.属性或delete 对象\["属性"\]。
10. typeof 操作符：用于检查值的类型，例如typeof 值。
11. instanceof 操作符：用于检查对象是否是某个类的实例，例如对象 instanceof 类名。
12. void 操作符：用于计算一个表达式并返回 undefined，例如void 表达式。
13. yield 操作符：用于生成器函数中，将一个值返回给生成器的调用方，并暂停生成器的执行。
14. await 操作符：用于异步函数中，暂停异步函数的执行，直到一个 Promise 对象的状态变为 resolved。

> 这些操作符的内部实现方式是通过编译器将它们转换为相应的 JavaScript 代码来实现的。不同的操作符会被编译器转换为不同的代码，以便在 JavaScript 引擎中执行。

## ‘2’ >‘12’值比较



```js
 "2" > "12" → true
```

在JavaScript中，字符串的比较是基于它们的Unicode码点进行的。在Unicode编码中，数字字符的编码是按照它们的值的大小进行排序的。

当我们比较字符串'2'和'12'时，JavaScript首先比较它们的第一个字符'2'和'1'，由于'2'的Unicode码点（50）大于'1'的Unicode码点（49），所以'2'被认为是“大于”'1'。这导致字符串'2'被认为是大于字符串'12'。

==JavaScript 高级程序设计（第4版）P\_70==

在使用关系操作符比较两个字符串时，会发生一个有趣的现象。很多人认为小于意味着“字母顺序靠前”，而大于意味着“字母顺序靠后”，实际上不是这么回事。对字符串而言，关系操作符会比较字符串中对应字符的编码，而这些编码是数值。比较完之后，会返回布尔值。问题的关键在于，大写字母的编码都小于小写字母的编码，因此以下这种情况就会发生：

```
let result = "Brick" < "alphabet"; // true
```

在这里，字符串"Brick"被认为小于字符串"alphabet"，因为字母 B 的编码是 66，字母 a 的编码是 97。要得到确实按字母顺序比较的结果，就必须把两者都转换为相同的大小写形式（全大写或全小写），然后再比较：

```
let result = "Brick".toLowerCase() < "alphabet".toLowerCase(); // false
```

## count++和++count的区别

他们都是JavaScript中的**自增运算符**，区别在于他们的**返回值**不同：

- counte++是后置自增运算符，他先返回原来的值，再将变量+1；
- ++counte是前置自增运算符，他先将变量+1，再返回新的值

如果要立刻使用自增之后的值，就用前置型，反之使用后置型。

```js
var currentIndex = 5;
var result = 100 + currentIndex++;
var result2 = 100 + ++currentIndex;
console.log("result:" + result); // 结果为105
console.log("result:" + result2); // 结果为107
```

## 说出 == 和 === 的区别

==（普通相等）

- 在比较两个值之前，如果类型不同，则会先将运算元转换成Number的值，再进行比较；（这个过程是隐式的类型转换）
- Null类型比较特殊：在进行比较时，会被当作一个对象和原生类型进行比较，而不会被转换为Number，当另一个对象是"null"或"undefined"时才会返回true。

===（严格相等运算符）

- 不会进行类型转换，只有在两个运算元类型相同的情况下才会返回true。

## 三种循环的区别：

while：每次迭代之前都要检查条件；

do..while：每次迭代后都要检查条件；

for (... ; ... ; ... ; )：每次迭代之前都要检查条件，可以使用其他设置。

## 逻辑与&&和逻辑或||的本质(了解)

逻辑与:也叫作短路==与==

- 从左往右,依次计算
- 当计算第一个运算元,先隐式转换为Boolean值进行比较
  - true ,继续下一个比较
  - false ,直接返回该运算元的初始值

- 如果找到最后也没有找到,就返回最后一个运算元

逻辑或:也叫做短路==或==

- 从左往右,依次计算
- 当计算第一个运算元,先隐式转换为Boolean值进行比较
  - true ,直接返回该运算元的初始值
  - false ,继续下一个比较

- 如果找到最后也没有找到,就返回最后一个运算元

## 举一个switch使用场景的案例

在JavaScript中，switch语句通常用于根据不同的情况执行不同的代码块。下面是一个使用switch语句的示例，该示例根据一周中的天数打印不同的消息：

```js
let day = new Date().getDay();
switch (day) {
  case 0:
    console.log("今天是星期天");
    break;
  case 1:
    console.log("今天是星期一");
    break;
  case 2:
    console.log("今天是星期二");
    break;
  case 3:
    console.log("今天是星期三");
    break;
  case 4:
    console.log("今天是星期四");
    break;
  case 5:
    console.log("今天是星期五");
    break;
  case 6:
    console.log("今天是星期六");
    break;
  default:
    console.log("无效的日期");
    break;
}
```

在此示例中，我们首先获取当前日期的星期几，并将其存储在变量day中。然后，我们使用switch语句根据day的值执行不同的代码块。如果day的值为0，表示星期天，我们将打印一条消息"今天是星期天"。如果day的值为1，表示星期一，我们将打印一条消息"今天是星期一"，依此类推。如果day的值不在0到6之间，则执行默认代码块，打印一条消息"无效的日期"。

## null和undefined的区别

阮一峰的网络日志

[https://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html](https://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)

目前，null和undefined基本是同义的，只有一些细微的差别。

**null表示"没有对象"，即该处不应该有值。**典型用法是：

（1） 作为函数的参数，表示该函数的参数不是对象。

（2） 作为对象原型链的终点。

```javascript
Object.getPrototypeOf(Object.prototype)
// null
```

**undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。**典型用法是：

（1）变量被声明了，但没有赋值时，就等于undefined。

（2）调用函数时，应该提供的参数没有提供，该参数等于undefined。

（3）对象没有赋值的属性，该属性的值为undefined。

（4）函数没有返回值时，默认返回undefined。

```javascript
var i;
i // undefined

function f(x){console.log(x)}
f() // undefined

var  o = new Object();
o.p // undefined

var x = f();
x // undefined
```

## JavaScript中的指针和引用

在 JavaScript 中，不存在指针的概念，而是存在引用的概念。

引用是一个变量指向一个对象在内存中的地址，而不是指向一个对象本身。当我们对一个引用进行操作时，实际上是对对象在内存中的位置进行操作。因此，如果多个变量引用同一个对象，它们实际上是引用同一个内存位置中的对象，对其中一个变量所做的修改会影响到其他变量。

例如：

```js
let obj1 = {name: 'John'};
let obj2 = obj1;

console.log(obj1.name); // 输出 'John'
console.log(obj2.name); // 输出 'John'

obj2.name = 'Doe';

console.log(obj1.name); // 输出 'Doe'
console.log(obj2.name); // 输出 'Doe'
```

在上面的例子中，`obj2` 引用了 `obj1` 所指向的对象，因此当我们修改 `obj2.name` 的值时，`obj1.name` 的值也被修改了。

需要注意的是，JavaScript 中有一些基本类型（如字符串、数字、布尔值等）是按值传递的，而不是按引用传递的。这意味着当我们将一个基本类型的值赋给一个变量时，该变量存储的是该值的一个副本，而不是该值在内存中的位置。因此，当我们修改该变量的值时，不会影响其他变量。

# 📁 javaScript_函数

## JavaScript中的函数是什么？

在JavaScript中，函数是一种可重用的代码块，可以接受输入参数并执行一系列操作，最后返回一个值。

函数通常用于封装可重复使用的代码块，从而使代码更加模块化和可维护。

在JavaScript中，函数可以定义为具名函数表达式或匿名函数表达式。具名函数表达式是指将函数定义分配给变量，而匿名函数表达式则是直接将函数定义写在代码中。

以下是一个定义具名函数表达式的示例：

```js
function add(x, y) {
  return x + y;
}
```

在这个例子中，`add`是函数的名称，它接受两个参数`x`和`y`，并返回它们的和。

以下是定义匿名函数表达式的示例：

```js
var add = function(x, y) {
  return x + y;
};
```

在这个例子中，`add`是一个变量，它被分配一个函数定义，该函数接受两个参数`x`和`y`，并返回它们的和。这种函数定义方式通常用于在代码中动态创建函数，并将其分配给变量。

无论使用哪种方式定义函数，都可以通过调用函数名称并传递所需的参数来调用函数。例如，要调用`add`函数并将两个数字相加，可以使用以下代码：

```js
var sum = add(2, 3); // sum 等于 5
```

这将调用`add`函数，并将数字2和3作为参数传递。函数将执行并返回它们的和，该和将被分配给变量`sum`。

## 总结局部变量和全局变量的使用

**局部变量**

在函数内部定义的变量，只能在函数内部访问。当函数被调用时，局部变量被创建，并在函数结束时被销毁。局部变量通常用于存储在函数中使用的临时值。局部变量的作用域仅限于函数内部，它们对于函数外部是不可见的。

**全局变量**

在程序的任何地方定义的变量，其作用域跨越整个程序。全局变量可以在程序的任何地方使用，包括函数内部和外部。全局变量通常用于存储在整个程序中需要访问的值，例如配置设置和计数器。

**变量的访问顺序**

在访问变量时，程序会首先搜索当前作用域中的变量。如果变量未在当前作用域中找到，则程序将继续向上搜索，直到找到变量或搜索到程序的最顶层作用域。因此，当函数中存在与全局变量同名的局部变量时，函数将使用局部变量，而不是全局变量。

> 总之，局部变量的作用域仅限于函数内部，全局变量的作用域跨越整个程序。在访问变量时，程序会按照作用域链的顺序搜索变量。

## 头等公民、函数回调、匿名函数的概念理解？

**头等公民**

在 JavaScript 中，函数被视为头等公民（First-Class Citizen）。这意味着函数可以像任何其他数据类型一样被使用，例如可以将函数存储在变量中、将函数作为参数传递给其他函数或从函数中返回函数等。这使得 JavaScript 的函数具有非常强大的灵活性，可以用于实现许多高级编程技术，如函数式编程。

**函数回调**

函数回调是一种常见的 JavaScript 编程模式，它涉及到将一个函数作为参数传递给另一个函数，然后在后者中调用该函数。

这样的函数通常称为回调函数（Callback Function）。函数回调的主要优点是可以实现异步编程，即在异步操作完成时，使用回调函数来处理返回的数据或执行某些操作。

```js
function ask(isLove, yes, no ) {
  if(confirm(isLove)) {
    yes()
  } else {
    no()
  }
}

function showOk() {
  alert("you agreed")
}
function showNo() {
  alert("you reject")
}

ask ("Do you love me ", showOk, showNo)
```

**匿名函数**

匿名函数是一种没有名称的函数，可以直接将其作为值分配给变量或将其作为参数传递给其他函数。匿名函数通常用于需要临时创建函数的场景，例如在事件处理程序中创建函数，或在执行某些操作之前定义函数。由于匿名函数没有名称，因此它们通常只能通过变量来访问。

总之，JavaScript 中的函数头等公民，可以像任何其他数据类型一样使用。函数回调是一种常见的编程模式，可以实现异步编程。匿名函数是没有名称的函数，通常用于需要临时创建函数的场景。这些概念的深入理解有助于编写更高效、更灵活的 JavaScript 代码。

```js
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
```

## parameter和argument的区别

在JavaScript中，parameter（参数）和argument（实参）是两个相关但不同的概念。

**Parameter（参数）：**

在JavaScript中，参数是函数定义（function definition）时在函数括号内声明的变量，用于接收函数调用时传入的值。在函数内部，这些参数的值可以被访问和使用。函数定义时声明的参数也被称为形参（formal parameters）。

例如，下面的函数add有两个参数num1和num2：

```
function add(num1, num2) {
  return num1 + num2;
}
```

**Argument（实参）：**

在JavaScript中，实参是函数调用（function call）时传递给函数的值，可以是字面量、变量、表达式等。实参的值将会被赋给函数定义中对应的参数。函数调用时传入的实参也被称为实际参数（actual parameters）或者简称实参（arguments）。

例如，当我们调用add(2, 3)时，2和3就是函数调用时传入的实参：

```
add(2, 3); // 实参为 2 和 3
```

在这个例子中，2和3将分别赋给函数add定义中的num1和num2参数。函数执行后会返回5。

**总结：**

在JavaScript中，参数和实参都是在函数调用过程中起作用的。参数是函数定义时声明的变量，用于接收函数调用时传入的实参值。实参是在函数调用时传递给函数的值。理解参数和实参的区别很重要，因为它们对于编写可重用的函数非常重要。

JavaScript中的参数和实参也可以分别称为形参（formal parameters）和实际参数（actual parameters），这两个术语也被广泛使用。形参表示函数定义时声明的参数，而实际参数则表示函数调用时传递给函数的值。因此，参数和实参的概念是非常相似的，只是在语义上略有不同。

## 整理图中常见的代码规范

![image-20230430210920866](E:\coder\09_OneNote\image\image-20230430210920866.png)

- 函数名跟()之间不需要空格
- 函数多个参数之间用逗号加空格分隔, 且第一个参数和最后一个参数跟()之间没有空格
- 函数参数的 () 跟 后面的 { 保持在同一行, 且之间有一个空格
- 换行的缩进为两个空格
- for/if/while等关键字跟()之间有一个空格
- 运算符的前后加一个空格,自增自减运算不加
- 调用函数时,多个参数之间用逗号加空格分隔, 且第一个参数和最后一个参数跟()之间没有空格
- 流程控制语句之前加一行空行, } else { 保持在同一行

## 总结Chrome的debug调试技巧

Chrome开发者工具Console区域: 可以查看代码中使用console.log() 输出的信息

给代码添加断点(breakpoint): 代码运行时遇到断点便会停止执行

- VSCode中,点击对应的代码行号左侧的红点即可添加断点,或者在代码上方加上 debugger
- Chrome中Source区域:找到要调试的文件,在代码左侧的行号处点击即可添加断点

Watch区域: 输入对应的变量,可以观察代码运行过程中变量的值的变化情况

Breakpoints区域:可以查看js代码中所有添加的断点

Scope区域:查看代码生成的作用域

上方工具栏按钮作用(从左到由):

- 控制调试程序的暂停和恢复
- 跳过下一个函数调用,执行下一行代码
- 进入下一个函数调用,可查看函数内部执行顺序
- 跳出当前函数
- 进入下一个函数调用,不会进入setTimeout内部的函数

## 函数的不同名称

当在JavaScript中使用同一个概念时，在不同的情况下，可能会有不同的术语来描述它们。例如，函数在不同的上下文中可能被称为不同的名称，但它们仍然是函数。

操作函数时，通常是通过引用或作用域来实现的。这些概念是JavaScript中最基础的概念之一。

以下是一些例子，以帮助您更好地理解这些概念：

1、普通函数：

这是JavaScript中最基本的函数类型，它只是一段可执行的代码块。

```javascript
function add(x, y) {
return x + y;
}
```

2、构造函数：

这是一种特殊类型的函数，它用于创建新的对象实例。

- 它们的命名以大写字母开头。
- 它们只能由 "new" 操作符来执行。

构造函数，或简称构造器，就是常规函数，但大家对于构造器有个共同的约定，就是其命名首字母要大写。

构造函数只能使用 new 来调用。这样的调用意味着在开始时创建了空的 this，并在最后返回填充了值的 this。

```javascript
function Person(name, age) {
this.name = name;
this.age = age;
}
let john = new Person('John', 30);
```

3、静态方法：

这是一个附加到构造函数本身而不是实例的方法。

```javascript
function Circle(radius) {
this.radius = radius;
}
Circle.calculateArea = function(radius) {
return Math.PI * radius * radius;
};
```

4、动态方法：

这是通过在构造函数的原型上定义方法来创建的方法，这些方法将在每个实例上共享。

```javascript
function Animal(name) {
this.name = name;
}
Animal.prototype.speak = function() {
console.log('The animal makes a noise.');
};
```

5、闭包：

这是一个由函数和其相关的引用组成的包，可以访问其创建时的作用域。

```javascript
function makeCounter() {
let count = 0;
return function() {
count += 1;
return count;
};
}
let counter = makeCounter();
```

6、公共方法：

这是一个可从实例中访问的方法。

```javascript
function Car(model, year) {
this.model = model;
this.year = year;
this.start = function() {
console.log('Engine started');
};
}
let myCar = new Car('Tesla', 2020);
myCar.start();
```

7、私有方法：

这是仅从构造函数内部访问的方法。

```javascript
function Counter() {
let count = 0;
function increment() {
count += 1;
}
this.getCount = function() {
return count;
};
this.incrementCount = function() {
increment();
};
}
let counter = new Counter();
```

8、特权方法：

这是一种可以访问构造函数中私有方法和公共方法的方法。

```javascript
function Person(name) {
let age = 0;
function incrementAge() {
age += 1;
}
this.getName = function() {
return name;
};
this.getAge = function() {
return age;
};
this.hasBirthday = function() {
incrementAge();
};
}
let person = new Person('John');
person.hasBirthday();
```

# 📁 javaScript_面向对象

## 检查空对象的方式有哪些？

在 JavaScript 中，可以使用以下几种方式来检查一个对象是否为空：

1、Object.keys()

方法检查对象是否有任何属性：

```js
const obj = {};
if (Object.keys(obj).length === 0) {
  console.log("Object is empty");
}
```

2、for...in

循环遍历对象的属性，如果对象有任何属性，则对象不为空：

```js
function isEmpty(obj) {
  for (let key in obj) {
    // 如果进到循环里面，说明有属性。
    return false;
  }
  return true;
}
```

3、JSON.stringify()

方法将对象转换为 JSON 字符串，如果字符串为 "{}"，则对象为空：

```js
const obj = {};
if (JSON.stringify(obj) === '{}') {
  console.log("Object is empty");
}
```

注意，以上方法都假定对象是纯粹的 JavaScript 对象，而不是从原型链继承属性的对象。如果对象有继承的属性，需要考虑使用其他方法进行检查。

4、Object.entries()

该方法返回一个由对象的可枚举属性键值对组成的数组。如果该数组长度为0，则对象为空。

```js
const obj = {};
if (Object.entries(obj).length === 0) {
  console.log("Object is empty");
}
```

5、Object.getOwnPropertyNames()

该方法返回一个由对象自身的属性键组成的数组。如果该数组长度为0，则对象为空。

```js
const obj = {};
if (Object.getOwnPropertyNames(obj).length === 0) {
  console.log("Object is empty");
}
```

6、lodash库的 isEmpty() 方法

使用 lodash库 等 JavaScript 库提供的 isEmpty() 方法。

```js
const _ = require('lodash');
const obj = {};
if (_.isEmpty(obj)) {
  console.log("Object is empty");
}
```

这些方法的效率和可读性各有不同，可以根据实际需要和代码风格选择使用哪种方法。

## 值传递和引用传递的区别

在JavaScript中，有两种变量传递方式：值传递和引用传递。

**值传递**

值传递指的是将一个变量的值复制到另一个变量中。这样，在接受变量的函数中，该变量的值就是其原始值的一个副本。在这种情况下，如果改变接受变量的函数的参数值，不会对原始变量的值产生任何影响。

例如，以下代码：

```
let a = 10;
let b = a;
b = 20;

console.log(a); // 输出10
console.log(b); // 输出20
```

在这个例子中，变量a的值为10。我们将a的值复制到变量b中。然后，我们将变量b的值更改为20。但是，变量a的值仍然是10，因为它是通过值传递而不是引用传递来传递的。

**引用传递**

引用传递指的是将一个对象的**引用**复制到另一个变量中，是该对象“在内存中的地址”。在接受变量的函数中，该变量包含原始对象的引用，而不是副本。如果更改接受变量的函数中对象的属性，则会影响原始对象。

例如，以下代码：

```
let obj1 = { value: 10 };
let obj2 = obj1;
obj2.value = 20;

console.log(obj1.value); // 输出20
console.log(obj2.value); // 输出20
```

在这个例子中，我们创建了一个对象obj1，该对象具有一个名为value的属性，其值为10。我们将obj1的引用复制到变量obj2中。然后，我们更改obj2的value属性的值为20。这也更改了obj1的value属性的值，因为它们引用同一个对象。这就是引用传递的作用。

**值类型和引用类型**

- 值类型(原始类型):在变量中保存的是值本身,占据的空间是在栈内存中分配的
- 引用类型(对象类型):在变量中保存的是对象的“引用”,占据的空间是在堆内存中分配的

1)将值类型传递给函数参数,函数内部对参数的改变不会影响函数外部的变量

```js
function foo(a) {
  a = 200
}
var num = 100
foo(num) 
console.log(num) // 100
```

2)将引用类型传递给函数参数,函数参数保存的是对象的"引用",在函数内部修改对象的属性会影响函数外部的变量

```js
function foo(a) {
  a.name = "HTML"
}

var obj = {
  name: "JavaScript"
}
foo(obj)
console.log(obj.name) // HTML
```

## new操作背后的原理

**前言**

我们知道，在 ES6 之前（ES5），JavaScript 中类的表现形式就是构造函数。

JavaScript 中的构造函数是怎么样的？

- 构造函数也是一个**普通的函数**，从表现形式上看，和普通的函数没有任何区别（除了按照惯例，构造函数名称的首字母通常会大写）；
- 但如果一个**普通函数被 **new** 操作符调用**了，那么这个函数就叫做**构造函数**；

**原理**

如果一个函数被 new 操作符调用了，那么它会执行如下操作：

1. 在内存中创建一个新对象；
2. 将这个新对象内部的 \[\[Prototype\]\] 属性赋值为构造函数的 prototype 属性；
3. 将构造函数内部的 this 赋值为这个新对象（即 this 指向新对象）；
4. 执行构造函数内部的代码（给新对象添加属性）；
5. 如果构造函数返回了非空对象，则返回该对象；否则，返回刚创建的新对象；

**手写函数模拟 new**

下面，我们就根据上面的原理，尝试自己手写一个函数，模拟实现 new 操作符的功能。

1、基本实现

我们先用 ES5 的语法来进行实现：

```js
function useNewOperator() {
  var constructor = arguments[0]
  var args = [].slice.call(arguments, 1)

  // 1. 在内存中创建一个新对象
  var obj = {}

  // 2. 这个新对象内部的 [[Prototype]] 指针被赋值为构造函数（constructor）的 prototype 属性
  obj.__proto__ = constructor.prototype

  // 3. 构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）
  // 4. 执行构造函数内部的代码（给新对象添加属性）
  var res = constructor.apply(obj, args)

  // 5. 如果构造函数返回非空对象，则返回该对象；否则，返回刚才创建的新对象
  if (res != null && (typeof res === 'object' || typeof res === 'function')) {
    return res
  }
  return obj
}

// 测试
function Person(name, age) {
  this.name = name
  this.age = age

  // return undefined
  // return null
  // return {}
  // return 123
  // return ''
  // return String(123)
  // return new String(123)
  // return { name: 'wy' }
}

Person.prototype.sayName = function() {
  console.log(this.name);
}

const p1 = new Person('zhj', 20)
console.log(p1); // Person {name: 'zhj', age: 20}
p1.sayName() // zhj

const p2 = useNewOperator(Person, 'zhj', 20)
console.log(p2); // Person {name: 'zhj', age: 20}
p2.sayName() // zhj
```

2、考虑参数类型

上面的基本实现能跑但还存在问题，即没有考虑传入第一个参数是否为函数类型，如果第一个参数传入的不是函数，那么在执行 constructor.apply(obj, args) 这行代码调用 constructor() 时就会报错了。所以我们需要加上判断，如果第一个参数传入的不是一个函数，就直接抛出异常：

```js
function useNewOperator() {
  var constructor = arguments[0]
+
+  if (typeof constructor !== 'function') {
+    throw new TypeError('the first argument to useNewOperator function must be a function')
+  }
+
  var args = [].slice.call(arguments, 1)

  // 1. 在内存中创建一个新对象
  var obj = {}

  // 2. 这个新对象内部的 [[Prototype]] 指针被赋值为构造函数（constructor）的 prototype 属性
  obj.__proto__ = constructor.prototype

  // 3. 构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）
  // 4. 执行构造函数内部的代码（给新对象添加属性）
  var res = constructor.apply(obj, args)

  // 5. 如果构造函数返回非空对象，则返回该对象；否则，返回刚才创建的新对象
  if (res != null && (typeof res === 'object' || typeof res === 'function')) {
    return res
  }
  return obj
}

// 测试
function Person(name, age) {
  this.name = name
  this.age = age
}

Person.prototype.sayName = function() {
  console.log(this.name);
}

const obj = {}
const p2 = useNewOperator(obj, 'zhj', 20) // Uncaught TypeError: the first argument to useNewOperator function must be a function
console.log(p2);
p2.sayName()
```

3、Object.prototype.\_\_proto\_\_ 的替代方案

前面我们在将新对象内部的 \[\[Prototype\]\] 属性赋值为构造函数的 prototype 属性时，是通过给 obj 上的 \_\_proto\_\_ 属性赋值实现的（相当于使用了 Object.prototype.\_\_proto\_\_），虽然可以，但不推荐使用 Object.prototype.\_\_proto\_\_，更推荐使用 Object.getPrototypeOf/Reflect.getPrototypeOf 和 Object.setPrototypeOf/Reflect.setPrototypeOf（参考链接：[developer.mozilla.org/zh-CN/docs/…](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2Fproto) ）。所以我们做如下修改：

```js
function useNewOperator() {
  var constructor = arguments[0]

  if (typeof constructor !== 'function') {
    throw new TypeError('the first argument to useNewOperator function must be a function')
  }

  var args = [].slice.call(arguments, 1)

  // 1. 在内存中创建一个新对象
  var obj = {}

  // 2. 这个新对象内部的 [[Prototype]] 指针被赋值为构造函数（constructor）的 prototype 属性
+ Object.setPrototypeOf(obj, constructor.prototype)

  // 3. 构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）
  // 4. 执行构造函数内部的代码（给新对象添加属性）
  var res = constructor.apply(obj, args)

  // 5. 如果构造函数返回非空对象，则返回该对象；否则，返回刚才创建的新对象
  if (res != null && (typeof res === 'object' || typeof res === 'function')) {
    return res
  }
  return obj
}

// 测试
function Person(name, age) {
  this.name = name
  this.age = age
}

Person.prototype.sayName = function() {
  console.log(this.name);
}

const p1 = new Person('zhj', 20)
console.log(p1); // Person {name: 'zhj', age: 20}
p1.sayName() // zhj

const p2 = useNewOperator(Person, 'zhj', 20)
console.log(p2); // Person {name: 'zhj', age: 20}
p2.sayName() // zhj
```

或者我们还可以使用 Object.create() 直接指定原型来创建新对象：

```js
function useNewOperator() {
  var constructor = arguments[0]

  if (typeof constructor !== 'function') {
    throw new TypeError('the first argument to useNewOperator function must be a function')
  }

  var args = [].slice.call(arguments, 1)

  // 1. 在内存中创建一个新对象
- var obj = {}
-
  // 2. 这个新对象内部的 [[Prototype]] 指针被赋值为构造函数（constructor）的 prototype 属性
+ var obj = Object.create(constructor.prototype)

  // 3. 构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）
  // 4. 执行构造函数内部的代码（给新对象添加属性）
  var res = constructor.apply(obj, args)

  // 5. 如果构造函数返回非空对象，则返回该对象；否则，返回刚才创建的新对象
  if (res != null && (typeof res === 'object' || typeof res === 'function')) {
    return res
  }
  return obj
}

// 测试
function Person(name, age) {
  this.name = name
  this.age = age
}

Person.prototype.sayName = function() {
  console.log(this.name);
}

const p1 = new Person('zhj', 20)
console.log(p1); // Person {name: 'zhj', age: 20}
p1.sayName() // zhj

const p2 = useNewOperator(Person, 'zhj', 20)
console.log(p2); // Person {name: 'zhj', age: 20}
p2.sayName() // zhj
```

4、使用 ES6 语法实现

下面，我们再来使用 ES6 语法（剩余参数（rest parameters）、const）进行实现：

```js
function useNewOperator(constructor, ...args) {
  if (typeof constructor !== 'function') {
    throw new TypeError('the first argument to useNewOperator function must be a function')
  }

  // 1. 在内存中创建一个新对象
  const obj = {}

  // 2. 这个新对象内部的 [[Prototype]] 指针被赋值为构造函数（constructor）的 prototype 属性
  Object.setPrototypeOf(obj, constructor.prototype)
  // 或者使用 Object.create() 直接指定原型创建新对象
  // const obj = Object.create(constructor.prototype)

  // 3. 构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）
  // 4. 执行构造函数内部的代码（给新对象添加属性）
  const res = constructor.apply(obj, args)

  // 5. 如果构造函数返回非空对象，则返回该对象；否则，返回刚才创建的新对象
  if (res != null && (typeof res === 'object' || typeof res === 'function')) {
    return res
  }
  return obj
}

// 测试
function Person(name, age) {
  this.name = name
  this.age = age
}

Person.prototype.sayName = function() {
  console.log(this.name);
}

const p1 = new Person('zhj', 20)
console.log(p1); // Person {name: 'zhj', age: 20}
p1.sayName() // zhj

const p2 = useNewOperator(Person, 'zhj', 20)
console.log(p2); // Person {name: 'zhj', age: 20}
p2.sayName() // zhj
```

5、考虑 ES6 的 new.target 检测

最后，还有一个点需要考虑，就是 ES6 新增的 new.target 属性，在通过使用 new 操作符被调用的构造方法或函数中，new.target 会返回一个指向构造方法或函数的引用（参考链接：[developer.mozilla.org/en-US/docs/…](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FJavaScript%2FReference%2FOperators%2Fnew.target) ）。所以我们可以使用 new.target 来检测函数或构造方法是否是通过 new 操作符被调用的。那么我们还需要在自己实现的 useNewOperator 函数中添加相应的代码：

```js
function useNewOperator(constructor, ...args) {
  if (typeof constructor !== 'function') {
    throw new TypeError('the first argument to useNewOperator function must be a function')
  }

+ // 在通过使用 new 操作符被调用的构造方法或函数中，new.target 返回一个指向构造方法或函数的引用。
+ useNewOperator.target = constructor

  // 1. 在内存中创建一个新对象
  const obj = {}

  // 2. 这个新对象内部的 [[Prototype]] 指针被赋值为构造函数（constructor）的 prototype 属性
  Object.setPrototypeOf(obj, constructor.prototype)
  // 或者使用 Object.create() 直接指定原型创建新对象
  // const obj = Object.create(constructor.prototype)

  // 3. 构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）
  // 4. 执行构造函数内部的代码（给新对象添加属性）
  const res = constructor.apply(obj, args)

  // 5. 如果构造函数返回非空对象，则返回该对象；否则，返回刚才创建的新对象
  if (res != null && (typeof res === 'object' || typeof res === 'function')) {
    return res
  }
  return obj
}

// 测试
function Person(name, age) {
  console.log('this:', this);
  console.log('new.target:', new.target);
  console.log('useNewOperator.target:', useNewOperator.target);
  this.name = name
  this.age = age
}

Person.prototype.sayName = function() {
  console.log(this.name);
}

const p1 = new Person('zhj', 20)
// const p1 = Person('zhj', 20)
console.log(p1);
p1.sayName()

const p2 = useNewOperator(Person, 'zhj', 20)
console.log(p2);
p2.sayName()
```

无注释版本

```js
function useNewOperator(constructor, ...args) {
  if (typeof constructor !== 'function') {
    throw new TypeError('the first argument to useNewOperator function must be a function')
  }
  useNewOperator.target = constructor

  const obj = {}
  Object.setPrototypeOf(obj, constructor.prototype)
  // const obj = Object.create(constructor.prototype)
  const res = constructor.apply(obj, args)
  if (res != null && (typeof res === 'object' || typeof res === 'function')) {
    return res
  }
  return obj
}
```

以上，就是关于 new 操作背后的原理，以及手写函数模拟实现 new 操作过程的所有内容啦~如果你还有什么疑问欢迎在评论区与我互动。

## `for of`与`for in`的区别

for...of 和 for...in 是 JavaScript 中用于循环遍历对象和数组的两种不同的语法。它们的用法和功能虽然有些相似，但是它们之间还是有一些区别的。

**for...of 循环**

for...of 循环用于遍历一个可迭代对象（如数组、字符串、Set、Map 等），并将每个元素的值赋给指定的变量。具体语法如下：

```js
for (variable of iterable) {
  // code block to be executed
}
```

其中，variable 是一个变量名，用于存储每个元素的值；iterable 是一个可迭代对象，用于遍历每个元素。下面是一个使用 for...of 循环遍历数组的例子：

```js
let arr = [1, 2, 3];
for (let num of arr) {
  console.log(num);
}
```

在这个例子中，我们使用 for...of 循环遍历数组 arr，并将每个元素的值赋给变量 num，然后将其输出到控制台上。

需要注意的是，for...of 循环只能遍历可迭代对象中的值，而不能遍历对象的属性。

**for...in 循环**

for...in 循环用于遍历一个对象的可枚举属性，并将每个属性的名称赋给指定的变量。具体语法如下：

```js
for (variable in object) {
  // code block to be executed
}
```

其中，variable 是一个变量名，用于存储每个属性的名称；object 是一个对象，用于遍历每个属性。下面是一个使用 for...in 循环遍历对象的例子：

```js
let obj = { a: 1, b: 2, c: 3 };
for (let key in obj) {
  console.log(key + ": " + obj[key]);
}
```

在这个例子中，我们使用 for...in 循环遍历对象 obj 的所有可枚举属性，将属性的名称赋给变量 key，并将属性的值输出到控制台上。

需要注意的是，for...in 循环遍历对象的属性时，可能会包括一些不是自身属性的属性，比如继承属性、原型链上的属性等。因此，使用 for...in 循环遍历对象时，需要使用 hasOwnProperty() 方法来判断属性是否为对象自身的属性。

总的来说，for...of 循环用于遍历可迭代对象中的值，而 for...in 循环用于遍历对象中的属性。

**遍历数组的元素：**

```js
for (let i=0; i<arr.length; i++)
// 运行得最快，可兼容旧版本浏览器。
for (let item of arr)
// 现代语法，只能访问 items。
for (let i in arr) 
// 永远不要用这个。
```

**总结**

- for...in可以遍历对象和数组，for...of不能遍历对象
- for...in 循环不仅遍历对象的键名，还会遍历⼿动添加的其它键，甚⾄包括原型链上的键
- for...in遍历的索引为字符串类型
- for..of适⽤遍历数/数组对象/字符串/map/set等拥有迭代器对象的集合，但是不能遍历对象
- for...of与forEach()不同的是，它可以正确响应break、continue和return语句
- 具有迭代器对象才可以使⽤for...of

## 可迭代对象和可枚举对象的区别

可迭代对象和可枚举对象是 JavaScript 中两个不同的概念。

**可迭代对象**

可迭代对象是指实现了 Symbol.iterator 方法的对象，该方法返回一个迭代器对象。迭代器对象包含一个 next 方法，用于返回序列中的下一个值和一个布尔值，指示序列是否已经到达结尾。迭代器对象可以通过 for...of 循环来遍历序列中的值。

常见的可迭代对象包括数组、字符串、Set、Map 等。例如，下面的代码使用 for...of 循环遍历一个数组：

```
let arr = [1, 2, 3];
for (let num of arr) {
  console.log(num);
}
```

**可枚举对象**

可枚举对象是指可以通过 for...in 循环遍历其属性的对象。在 JavaScript 中，所有对象都有原型链，因此它们可能会继承其他对象的属性。默认情况下，继承的属性是不可枚举的，而对象自身的属性通常是可枚举的。

可以通过 Object.defineProperty() 方法来设置属性的可枚举性，如下所示：

```
let obj = {};
Object.defineProperty(obj, "a", { value: 1, enumerable: true });
Object.defineProperty(obj, "b", { value: 2, enumerable: false });

for (let key in obj) {
  console.log(key + ": " + obj[key]);
}
// 输出：a: 1
```

在这个例子中，我们创建了一个对象 obj，并定义了两个属性 a 和 b。其中，属性 a 的可枚举性设置为 true，属性 b 的可枚举性设置为 false。然后，我们使用 for...in 循环遍历对象 obj 的属性，只有属性 a 被输出到控制台上。

需要注意的是，Object.keys() 方法可以返回对象自身的所有可枚举属性的名称组成的数组，而 Object.getOwnPropertyNames() 方法可以返回对象自身的所有属性的名称组成的数组。

## 对象方法简写的区别

**方法简写**

ES6中的方法简写语法。它使得定义对象的方法更加简洁明了。除了省略了 "function" 关键字外，方法简写语法还可以使用箭头函数和常规函数的方式来定义方法。

```js
// 这些对象作用一样

user = {
  sayHi: function() {
    alert("Hello");
  }
};

// 方法简写看起来更好，对吧？
let user = {
  sayHi() { // 与 "sayHi: function(){...}" 一样
    alert("Hello");
  }
};
```

如上所示，我们可以省略 "function"，只写 sayHi()。

**和普通函数的区别**

在原型上，使用方法简写语法和传统的对象方法定义是有区别的。当您使用方法简写语法定义对象方法时，该方法将成为对象的实例方法，而不是原型方法。也就是说，每个对象实例都会拥有自己的方法实现，而不是共享一个方法实现。

考虑以下示例：

```js
function Person(name) {
  this.name = name;
}

Person.prototype = {
  // 对象方法使用方法简写语法
  sayHi() {
    console.log(`Hi, my name is ${this.name}`);
  }
};

let john = new Person("John");
let jane = new Person("Jane");

john.sayHi(); // "Hi, my name is John"
jane.sayHi(); // "Hi, my name is Jane"
```

> 在上面的示例中，我们使用方法简写语法定义了 Person.prototype 上的 sayHi 方法。然后，我们创建了两个 Person 对象实例，每个实例都具有自己的 sayHi 方法实现。这是因为每个对象实例都有自己的属性和方法，而不是共享原型上的属性和方法。

相比之下，如果使用传统的对象方法定义方式，方法将成为原型方法，每个对象实例都将共享该方法实现。例如：

```js
function Person(name) {
  this.name = name;
}

Person.prototype.sayHi = function() {
  console.log(`Hi, my name is ${this.name}`);
};

let john = new Person("John");
let jane = new Person("Jane");

john.sayHi(); // "Hi, my name is John"
jane.sayHi(); // "Hi, my name is Jane"
```

> 在上面的示例中，我们使用传统的对象方法定义方式将 sayHi 方法添加到了 Person.prototype 上。这意味着每个 Person 对象实例都共享同一个 sayHi 方法实现。因此，john.sayHi() 和 jane.sayHi() 都输出相同的结果，因为它们共享相同的方法实现。

综上所述，在原型上，方法简写语法和传统的对象方法定义方式之间有区别。使用方法简写语法定义对象方法会将方法定义为对象的实例方法，而不是原型方法。

## 可选连`?.`的使用

可选链 ?. 语法有三种形式：

1. obj?.prop —— 如果 obj 存在则返回 obj.prop，否则返回 undefined。
2. obj?.\[prop\] —— 如果 obj 存在则返回 obj\[prop\]，否则返回 undefined。
3. obj.method?.() —— 如果 obj.method 存在则调用 obj.method()，否则返回 undefined。

正如我们所看到的，这些语法形式用起来都很简单直接。?. 检查左边部分是否为 null/undefined，如果不是则继续运算。

?.链使我们能够安全地访问嵌套属性。

> 但是，我们应该谨慎地使用 ?.，根据我们的代码逻辑，仅在当左侧部分不存在也可接受的情况下使用为宜。以保证在代码中有编程上的错误出现时，也不会对我们隐藏。

## toString 和 valueOf方法

在 JavaScript 中，所有对象都继承了两个内置方法：toString 和 valueOf。这两个方法都可以被重写以改变对象的默认行为。

1、toString 方法

toString 方法将对象转换为字符串。当我们使用 console.log() 或者 alert() 等方法输出一个对象时，实际上是调用了该对象的 toString 方法。如果我们没有重写 toString 方法，那么默认返回 `"[object Object]"` 字符串。

例如，下面的代码重写了一个对象的 toString 方法，将其转换为 JSON 字符串：

```js
const myObject = {
  name: 'John',
  age: 30,
  toString() {
    return JSON.stringify(this);
  }
};

console.log(myObject); // {name: "John", age: 30}
```

在这个例子中，myObject 对象重写了 toString 方法，将对象转换为 JSON 字符串。因此，当我们输出 myObject 对象时，它会自动调用 toString 方法，并将对象转换为字符串。

2、valueOf 方法

valueOf 方法返回对象的原始值。在大多数情况下，这个值与对象本身相同，但是我们可以重写 valueOf 方法，以改变对象的原始值。

例如，下面的代码重写了一个对象的 valueOf 方法，将其转换为数字：

```js
const myObject = {
  value: 42,
  valueOf() {
    return this.value;
  }
};

console.log(myObject + 8); // 50
```

在这个例子中，myObject 对象重写了 valueOf 方法，将其转换为数字。因此，当我们将 myObject 对象与数字相加时，它会自动调用 valueOf 方法，并将对象转换为数字。

需要注意的是，toString 和 valueOf 方法是 JavaScript 中非常有用的内置方法，它们可以被用来自定义对象的行为。但是，在重写这些方法时，需要注意其返回值的类型和格式，以确保代码的可读性和可维护性。

**两者区别**

虽然 toString 和 valueOf 方法都是内置方法，都可以被重写，但它们有着不同的作用和返回值。

toString 方法

将对象转换为字符串，返回一个字符串类型的值。如果我们没有重写 toString 方法，它会返回一个 "\[object Object\]" 的字符串，表示该对象的类型。但是，我们可以重写 toString 方法，以自定义对象的字符串表示形式。

valueOf 方法

返回对象的原始值，通常是一个数值、字符串或布尔值。如果我们没有重写 valueOf 方法，它会返回对象本身。但是，我们可以重写 valueOf 方法，以改变对象的原始值。

> 需要注意的是，虽然 toString 和 valueOf 方法都可以被重写，但它们在对象转换和计算中的应用场景是不同的。toString 方法通常用于输出对象的字符串表示形式，而 valueOf 方法则通常用于将对象转换为原始值，以进行算术运算或其他类型的操作。

## JS对象考题

JS对象注意点：

1. 对象是通过new操作符构建出来的，所以对象之间不相等(除了引用外)；
2. 对象注意：引用类型**（共同一个地址）**；
3. 对象的key都是字符串类型；
4. 对象如何找属性|方法；

查找规则：

先在对象本身找 ===> 构造函数中找 ===> 对象原型中找 ===> 构造函数原型中找 ===> 对象上一层原型查找

考题一：

```js
[1,2,3] === [1,2,3]   //false
```

考题二：

```js
var obj1 = {
    a:'hellow'
}
var obj2 = obj1;
obj2.a = 'world';

console.log(obj1); *//{a:world}*

(function(){
console.log(a); *//undefined*
    var a = 1;
})();
```

考题三：

```js
var a = {}
var b = {
    key:'a'
}

var c = {
    key:'c'
}

a[b] = '123';
a[c] = '456';

console.log( a[b] ); // 456
```

# 📁 javaScript_内置类

## 原始值和对象的区别

JavaScript 中的原始值和对象有以下几个区别：

1、存储方式不同

原始值是简单的数据类型，它们的值直接存储在变量或常量中。JavaScript 中有 6 种原始值：undefined、null、布尔值、数字、字符串和 Symbol。例如：

```js
let x = 42; // 数字类型的原始值
let y = "hello world"; // 字符串类型的原始值
let z = true; // 布尔类型的原始值
```

而对象是引用类型，它们的值是存储在内存中的对象，变量或常量中只是存储了该对象的引用。例如：

```js
let obj = {x: 42, y: "hello world"}; // 对象类型的值
```

2、可变性不同

原始值是不可变的，即它们的值不能被修改。如果我们对一个原始值进行修改，实际上是创建了一个新的值。例如：

```js
let x = 42;
x++; // x 的值变成了 43，但是原始值 42 并没有被修改
```

而对象是可变的，即对象的属性值可以被修改。例如：

```js
let obj = {x: 42, y: "hello world"};
obj.x++; // 修改了 obj 对象的 x 属性值，使其变成了 43
```

3、传递方式不同

原始值是按值传递的，即当我们将一个原始值赋值给一个变量或常量时，实际上是将该原始值复制一份，然后将复制后的值赋给变量或常量。例如：

```js
let x = 42;
let y = x; // 将 x 的值复制一份，然后赋给 y
```

而对象是按引用传递的，即当我们将一个对象赋值给一个变量或常量时，实际上是将该对象的引用复制一份，然后将复制后的引用赋给变量或常量。例如：

```js
let obj1 = {x: 42, y: "hello world"};
let obj2 = obj1; // 将 obj1 的引用复制一份，然后赋给 obj2
```

> 原始类型不是对象。它们不能存储额外的数据。
>
> 需要注意的是，原始值和对象虽然有所不同，但是它们都是 JavaScript 中的数据类型，都可以用来完成各种任务。在编写代码时，需要根据具体情况选择适当的数据类型。

## Number的常见操作

```js
// /number---Number 数字包装类
// window.Number
// Number 构造函数--Number包装类对象
// Number 类属性
console.log(Number.MAX_VALUE);
console.log(Number.MIN_VALUE);

// 最大安全整数和最小安全整数
console.log(Number.MAX_SAFE_INTEGER);
console.log(Number.MIN_SAFE_INTEGER);

// 实例方法
var num = new Number(1000);
console.log(num.toString(), num);
console.log((123).toString());
var num1 = 90;

// 转换进制
console.log(num1.toString(8));
console.log(num1.toString(16));

// 保留几位小数,会四舍五入,返回的是字符串
var num3 = 1.24902;
console.log(num3.toFixed(2)); //1.25
console.log(typeof num3.toFixed(2));

// 类方法 ,字符串--数字
var str = "178.2991";
console.log(Number.parseInt(str));
console.log(Number.parseFloat(str));

// window.parseInt===Number.parseInt,所以可以省略Number
console.log(window.parseInt === Number.parseInt); //true
console.log(parseInt(str));

isFinite (value)
// 将其参数转换为数字，如果是常规数字而不是 NaN/Infinity/-Infinity，则返回 true
// 常常被用于验证字符串值是否为常规数字

isNaN(value) // 将其参数转换为数字，然后测试它是否为 NaN
```

## Number类的操作

**类属性**

- Number.MAX_SAFE_INTEGER      最大安全整数
- Number.MIN_SAFE_INTEGER       最小安全整数

**实例方法**

- toString(base)，将数字转成字符串，并且按照base进制进行转化
- toFixed(digits)，格式化一个数字，保留digits位的小数,会四舍五入

**类方法**

- Number.parseInt(string[, radix])，将字符串解析成整数，也有对应的全局方法parseInt；
- Number. parseFloat(string)，将字符串解析成浮点数，也有对应的全局方法parseFloat；

## Math的常见操作

```js
// object,是对象,不是构造函数
console.log(typeof Math);

// 属性
console.log(Math.PI);

// 方法
var num = 12.5082;
console.log(Math.floor(num)); //12
console.log(Math.ceil(num)); //13
console.log(Math.round(num)); //13
console.log(Math.pow(2, 3)); //2的3次方=8

Math.max(a, b, c...) 和 Math.min(a, b, c...)
// 从任意数量的参数中返回最大值和最小值。

Math.pow(n, power)
// 返回 n 的给定（power）次幂。

Math.random()
// 返回 0 到 1 的随机数

// 需求: [15~50)的随机数
for (var i = 0; i < 100; i++) {
  let random = Math.floor(Math.random() * 35) + 15;
  console.log(random);
}

// 需求: [15~50]的随机数
for (var i = 0; i < 100; i++) {
  // [0,35]---[15,50]
  let random = Math.floor(Math.random() * 36) + 15;
  console.log(random);
}
```

**属性**

- Math.PI：圆周率

**常见的方法**

- Math.floor：向下舍入取整
- Math.ceil：向上舍入取整
- Math.round：四舍五入取整
- Math.random：生成0~1的随机数（包含0，不包含1）
- Math.pow(x, y)：返回x的y次幂

**公式: \[a,b)的随机数**

- y=a,x=b-a, Math.floor(Math.random() \* x) + y

## 整理String的常见操作

1、字符串长度：

可以使用字符串的length属性来获取字符串的长度。

```js
const str = "Hello, World!";
console.log(str.length); // 13
```

2、字符串索引：

可以使用方括号或charAt()方法获取字符串中指定位置的字符。

```js
const str = "Hello, World!";
console.log(str[0]); // "H"
console.log(str.charAt(1)); // "e"
```

3、字符串切片：

可以使用slice()方法或字符串的substring()、substr()方法获取字符串的子串。

```js
const str = "Hello, World!";
console.log(str.slice(0, 5)); // "Hello"
console.log(str.substring(7)); // "World!"
```

4、字符串拼接：

可以使用+操作符或concat()方法将多个字符串拼接成一个字符串。

```js
const str1 = "Hello";
const str2 = "World";
console.log(str1 + ", " + str2 + "!"); // "Hello, World!"
console.log(str1.concat(", ", str2, "!")); // "Hello, World!"
```

5、字符串替换：

可以使用replace()方法替换字符串中的指定字符或字符串。

```js
const str = "Hello, World!";
console.log(str.replace("World", "JavaScript")); // "Hello, JavaScript!"
```

6、字符串查找：

可以使用indexOf()方法或includes()方法查找字符串中是否包含指定字符或字符串。

```js
const str = "Hello, World!";
console.log(str.indexOf("o")); // 4
console.log(str.includes("World")); // true
```

7、字符串大小写转换：

可以使用toUpperCase()方法或toLowerCase()方法将字符串转换为大写或小写。

```js
const str = "Hello, World!";
console.log(str.toUpperCase()); // "HELLO, WORLD!"
console.log(str.toLowerCase()); // "hello, world!"
```

8、去除空格：

可以使用trim()方法去除字符串两端的空格。

```js
const str = "   Hello, World!   ";
console.log(str.trim()); // "Hello, World!"
```

9、字符串分割：

可以使用split()方法将字符串按指定分隔符分割成数组。

```js
const str = "Hello, World!";
console.log(str.split(",")); // ["Hello", " World!"]
```

10、字符串替换

replace()：该方法用于替换字符串中的指定字符或字符串，返回一个新的字符串。

```js
const str = "Hello, World!";
console.log(str.replace("World", "JavaScript")); // "Hello, JavaScript!"
```

11、判断字符串开头结尾

```js
// startsWith()：该方法用于判断一个字符串是否以指定的字符或字符串开头，返回一个布尔值。
const str = "Hello, World!";
console.log(str.startsWith("Hello")); // true
console.log(str.startsWith("World")); // false

// endsWith()：该方法用于判断一个字符串是否以指定的字符或字符串结尾，返回一个布尔值。
const str = "Hello, World!";
console.log(str.endsWith("World!")); // true
console.log(str.endsWith("Hello")); // false
```

12、去除首尾空格

trim()：该方法用于去除一个字符串的首尾空格，返回一个新的字符串。

```js
const str = "   Hello, World!   ";
console.log(str.trim()); // "Hello, World!"
```

13、数组 ===> 字符串

join() 是 JavaScript 中数组对象的方法，它将数组的所有元素以指定的分隔符连接成一个字符串，并返回该字符串。

```js
const fruits = ["apple", "banana", "orange"];
const joinedFruits = fruits.join(", "); // 使用", "作为分隔符
console.log(joinedFruits); // "apple, banana, orange"
```

14、普通for循环遍历

最常见的遍历数组和字符串的方式之一，也是最基础的方式。可以使用 length 属性获取数组或字符串的长度，然后使用 for 循环遍历每个元素。

```js
const arr = [1, 2, 3];
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
// 输出：1 2 3

const str = "Hello, World!";
for (let i = 0; i < str.length; i++) {
  console.log(str[i]);
}
// 输出：H e l l o ,   W o r l d !
```

15、for...of...循环

新的遍历方式，它可以遍历可迭代对象中的元素，例如数组和字符串。在 for..of 循环中，不需要使用下标或索引，而是直接使用每个元素的值。

```js
const arr = [1, 2, 3];
for (const item of arr) {
  console.log(item);
}
// 输出：1 2 3

const str = "Hello, World!";
for (const char of str) {
  console.log(char);
}
// 输出：H e l l o ,   W o r l d !
```

16、字符串不可变性

在 JavaScript 中字符串是不可变的，即一旦创建就不能修改。因此，任何修改字符串的操作都会返回一个新的字符串。例如，使用 replace() 方法替换字符串中的某个字符时，实际上是返回了一个新的字符串，而原始字符串并没有发生变化。

```js
const str = "Hello, World!";
const newStr = str.replace("World", "JavaScript");
console.log(str); // "Hello, World!"
console.log(newStr); // "Hello, JavaScript!"
```

17、创建方式 new String()

在 JavaScript 中，可以使用 new String() 构造函数来创建一个字符串对象。这种方式创建的字符串是一个对象，而不是基本数据类型的字符串。

一般来说，在 JavaScript 中创建字符串时，推荐使用基本字符串类型，而不是字符串对象。

```js
const strObj = new String("hello");
console.log(strObj); // 输出：[String: 'hello']
console.log(typeof strObj); // 输出：object
```

## JS判断变量是不是数组，你能写出哪些方法？

1、使用Array.isArray()方法：

ES6中新增了Array.isArray()方法，可以更加方便地判断一个变量是否为数组。

```js
const arr = [1, 2, 3];
if (Array.isArray(arr)) {
  console.log("arr is an array");
} else {
  console.log("arr is not an array");
}
```

2、使用 instanceof 操作符：

```js
javascriptCopy codeconst arr = [1, 2, 3];
if (arr instanceof Array) {
  console.log("arr is an array");
} else {
  console.log("arr is not an array");
}
```

3、使用 Object.prototype.toString.call() 方法：

```js
const arr = [1, 2, 3];
if (Object.prototype.toString.call(arr) === '[object Array]') {
  console.log("arr is an array");
} else {
  console.log("arr is not an array");
}
```

Object.prototype.toString.call() 方法第三种方式是最常用的，因为它可以用来检测所有类型的对象，而不仅仅是数组。

4、isPrototypeOf() 方法

使用Array.prototype作为原型对象，然后调用isPrototypeOf()方法来检测变量是否是这个原型对象的实例。如果变量是数组，则返回true，否则返回false。

注意，这种方式虽然可行，但是不如前面提到的方式简洁易读。

```js
const arr = [1, 2, 3];
if (Array.prototype.isPrototypeOf(arr)) {
  console.log("arr is an array");
} else {
  console.log("arr is not an array");
}
```



## 整理Array的常见操作

1、创建数组:

- 通过 \[\]
- 通过 Array()构造函数

```js
//数组的创建
var arr1 = ["HTML", "CSS", "JavaScript", "vue", "react"]
console.log(typeof arr1) //object

var arr2 = new Array()
var arr3 = new Array("HTML", "CSS", "JavaScript", "vue", "react")
```

2、访问数组中的元素 和 修改数组中的元素

- 通过\[index\]
- arr.at(i)
- i >= 0，arr.at(i)与arr\[i\] 完全相同对于 i为负数的情况，arr.at(i)则从数组的尾部向前数

```js
var arr =  new Array("HTML", "CSS", "JavaScript", "vue", "react")

// 访问数组中的元素
console.log(arr[2]) //JavaScript
console.log(arr[-1]) //undefined

//arr.at(i)
console.log(arr.at(3))//vue
console.log(arr.at(-4))//CSS

//修改数组中的元素
arr[3] = "Angular"
console.log(arr)//['HTML', 'CSS', 'JavaScript', 'Angular', 'react']
```

3、增加数组中的元素 和 删除数组中的元素

- 在数组的尾端添加或删除元素: push 在末端添加元素;pop 从末端取出一个元素
- 在数组的首端添加或删除元素: shift 取出队列首端的一个元素，整个数组元素向前前移动; unshift 在首端添加元素，整个其他数组元素向后移动
- 添加,删除和替换元素:arr.splice((start, deleteCount, item1, item2, itemN))
  - 从start位置开始，处理数组中的元素
  - deleteCount:要删除元素的个数，如果为0或者负数表示不删除
  - item1, item2, ...:在添加元素时，需要添加的元素;


```js
var arr =  new Array("HTML", "CSS", "JavaScript")

// 在数组的尾端添加或删除元素: push 和 pop
var num = arr.push("vue", "react")
console.log(arr, num) //['HTML', 'CSS', 'JavaScript', 'vue', 'react'] 5

var arr2 =  new Array("HTML", "CSS", "JavaScript")
var str = arr2.pop()
console.log(arr2, str)// ['HTML', 'CSS']  'JavaScript'

// 在数组的首端添加或删除元素 shift 和 unshift 
var arr3 =  new Array("HTML", "CSS", "JavaScript")
var str = arr3.shift()
console.log(arr3, str)//['CSS', 'JavaScript'] 'HTML'

var arr4 =  new Array("HTML", "CSS", "JavaScript")
var num = arr4.unshift("vue", "react")
console.log(arr4, num)//['vue', 'react', 'HTML', 'CSS', 'JavaScript'] 5

// arr.splice():返回被删除的元素组成的数组 没有被删除的元素 返回空数组

var arr5 =  new Array("HTML", "CSS", "JavaScript")
// 删除元素
var deleteaArr = arr5.splice(1, 2)
console.log(arr5) //['HTML']  
console.log(deleteaArr)//['CSS', 'JavaScript']

// 添加元素
var arr6 = new Array("HTML", "CSS", "JavaScript")
var deleteaArr = arr6.splice(0, 0, "vue", "react")
console.log(arr6)// ['vue', 'react', 'HTML', 'CSS', 'JavaScript']
console.log(deleteaArr)//[]

//替换元素
var arr7 = new Array("HTML", "CSS", "JavaScript")
var deleteArr = arr7.splice(1, 1, "vue", "react", "angular")
console.log(arr7)//['HTML', 'vue', 'react', 'angular', 'JavaScript']
console.log(deleteArr)//['CSS']
```

- 数组的长度:arr.length
- 数组的遍历:for; for..in; for..of

```js
var arr =  new Array("HTML", "CSS", "JavaScript")
//数组的长度
console.log(arr.length) // 3

//数组的遍历
for (var i = 0; i < arr.length; i++) {
  console.log(arr[i])
}

for (var index in arr) {
  console.log(index, arr[index])
}

for (var item of arr) {
  console.log(item)
}
```

- arr.slice(begin, end) 方法:用于对数组进行截取
  - 包含begin元素，但是不包含end元素
  - slice不会修改原数组 splice 修改原数组

- arr.concat方法:创建一个新数组，其中包含来自于其他数组和其他项的值
- arr.join:将一个数组的所有元素连接成一个字符串并返回这个字符串

```js
//arr.slice
var arr = new Array("HTML", "CSS", "JavaScript", "vue", "react")
var subArr = arr.slice(1, 3)
console.log(subArr) //['CSS', 'JavaScript']
console.log(arr) // ['HTML', 'CSS', 'JavaScript', 'vue', 'react']

//arr.conca
var arr2 = new Array("angular", "nodejs")
var arr3 = new Array("less", "sass")
var newArr = arr.concat(arr2, arr3)

// arr.join
var str = arr.join("--")
console.log(str)//HTML--CSS--JavaScript--vue--react
```

4、查找数组中的元素

- arr.indexOf(item, from) —— 从索引 from 开始搜索 item，如果找到则返回索引，否则返回 -1。
- arr.includes(item, from) —— 从索引 from 开始搜索 item，如果找到则返回 true（译注：如果没找到，则返回 false）。
- arr.find()——返回提供的数组中满足提供的函数的第一个元素
- arr.findIndex()——返回提供的数组中满足提供的函数的第一个元素的索引

```js
//arr.indexOf() 和 arr.includes()
var arr = new Array("HTML", "CSS", "JavaScript", "vue", "react")
var index = arr.indexOf("JavaScript")
console.log(index)// 2
console.log(arr.indexOf("less")) // -1

console.log(arr.includes("JavaScript")) // true
console.log(arr.includes("less")) // false

// arr.find() arr.findIndex()
var students = [
  { id: 100, name: "aa", age: 18 },
  { id: 101, name: "bb", age: 30 },
  { id: 102, name: "cc", age: 25 },
  { id: 103, name: "dd", age: 22 }
]
var stu1 = students.find(function(item) {
  return item.id === 101
})

console.log(stu1) //{id: 101, name: 'bb', age: 30}

var arr = new Array("HTML", "CSS", "JavaScript", "vue", "react")
var findIndex = arr.findIndex(function(item, index, arr) {
return item === "JavaScript"
})
// var findIndex = arr.findIndex(item => item === "JavaScript")
console.log(findIndex) // 2
```

5、数组的排序和反转

- arr.sort()方法:用于对数组进行排序, 直接改变原数组
- arr.reverse():方法将数组中元素的位置颠倒，并返回该数组

```js
var arr = new Array("HTML", "CSS", "JavaScript", "vue", "react")
arr.sort() 
console.log(arr)//['CSS', 'HTML', 'JavaScript', 'react', 'vue']

var arr2 = new Array(18, 3, 15, 56, 80, 66)
arr2.sort(function(item1, item2){
  return item1 - item2
})
console.log(arr2)// [3, 15, 18, 56, 66, 80]

arr2.reverse()
console.log(arr2)//[80, 66, 56, 18, 15, 3]
```

6、数组中的其他高阶函数

- arr.forEach():遍历数组，并且让数组中每一个元素都执行一次对应的方法
  - forEach(func) —— 对每个元素都调用 func，不返回任何内容。

- arr.filter():过滤出满足函数条件的元素创建一个新数组
- arr.map():返回由原数组中的每个元素都调用一次提供的函数后的返回值组成的新数组
- arr.reduce():用于计算数组中所有元素的总和

```js
//arr.forEach()
var arr = new Array("HTML", "CSS", "JavaScript", "vue", "react")
arr.forEach(function(item, index, arr) {
  console.log(index, item, arr)
})

//arr.filter()
var arr1 = new Array(1, 2, 3, 4, 5, 6, 7, 8)
var newarr = arr1.filter(function(item, index, arr){
  return item % 2 === 0
})
console.log(newarr)//[2, 4, 6, 8]

//arr.map()
var arr2 = new Array(3, 10, 15, 8, 6, 5)
var newarr2 = arr2.map(function(item, index, arr) {
  return item * 2
})
console.log(newarr2) //[6, 20, 30, 16, 12, 10]

//arr.reduce()
var nums = [11, 20, 55, 100, 88, 32]
var sum = nums.reduce(function(preValue, currentValue){
    return preValue + currentValue
}, 0)
console.log(sum) //306
```

7、Array.from()

Array.from() 方法是 ES6 中新增的方法，用于将类数组对象或可迭代对象转换成一个真正的数组。该方法接受两个参数：第一个参数是需要转换的对象，第二个参数是一个可选的 map 函数，用于对转换后的数组中的每个元素进行操作。

示例代码：

```js
// 将类数组对象转换为数组
let arrayLikeObj = { 0: 'a', 1: 'b', 2: 'c', length: 3 };
let arr1 = Array.from(arrayLikeObj);
console.log(arr1); // ['a', 'b', 'c']

// 将可迭代对象转换为数组
let set = new Set(['a', 'b', 'c']);
let arr2 = Array.from(set);
console.log(arr2); // ['a', 'b', 'c']

// 使用 map 函数对数组中的元素进行操作
let arr3 = Array.from([1, 2, 3], x => x * 2);
console.log(arr3); // [2, 4, 6]
```

可以看到，Array.from() 方法非常方便地将各种类型的对象转换成了数组，这在处理数据时非常有用。

转换数组，映射 Array 中的元素：

map(func) —— 根据对每个元素调用 func 的结果创建一个新数组。

```js
const arr = [1, 2, 3, 4];
const mappedArr = arr.map((element) => {
  return element * 2;
});
console.log(mappedArr); // [2, 4, 6, 8]
```

## sort背后原理是什么？

在 JavaScript 中，sort() 方法用于对数组进行排序。sort() 方法会修改原数组，并返回排序后的数组。sort() 方法使用的排序算法是快速排序（Quick Sort）。

快速排序是一种分治的排序算法，它的基本思想是选择一个基准元素，将数组分成两部分，一部分小于基准元素，一部分大于基准元素，然后对这两部分递归地进行排序。在实际应用中，快速排序通常是最快的排序算法之一。

sort() 方法的排序流程如下：

1. 首先选择一个基准元素（pivot），通常是数组的第一个元素或最后一个元素。
2. 然后将数组中小于基准元素的元素放在基准元素的左边，大于基准元素的元素放在基准元素的右边。这个过程称为分区（Partition）。
3. 接着递归地对左边的子数组和右边的子数组进行排序，直到整个数组都被排序。

在实际应用中，快速排序还需要考虑以下几点：

1. 对于小数组，快速排序的性能可能不如插入排序（Insertion Sort）。
2. 在分区时，为了避免最坏情况的出现（即分区后左边或右边的子数组长度为 0），可以采用随机选择基准元素或三数取中的方法来选择基准元素。
3. 对于具有相同元素的数组，为了避免快速排序出现退化情况（即分区不平衡），可以采用三路快速排序（Quick Sort 3-Way）。

> 总之，sort() 方法背后的原理是快速排序，它是一种高效的排序算法，并且在实际应用中有多种优化方式。

## find和filter的区别

在JavaScript中，find()和filter()都是用来筛选数组的方法

**主要区别如下：**

find()会返回第一个符合条件的元素，而filter()会返回所有符合条件的元素组成的新数组。

find()方法只会遍历数组中符合条件的元素，找到之后就会停止遍历，而filter()则会遍历整个数组，不管是否符合条件，都会进行处理。

**下面是两个方法的用法示例：**

```js
const arr = [1, 2, 3, 4, 5];

// 使用 find() 方法
const result1 = arr.find(item => item > 2);
console.log(result1); // 3

// 使用 filter() 方法
const result2 = arr.filter(item => item > 2);
console.log(result2); // [3, 4, 5]
```

从上面的示例中可以看出，find()方法返回的是第一个符合条件的元素，而filter()方法返回的是所有符合条件的元素组成的新数组。此外，find()方法在找到符合条件的元素后就会停止遍历，而filter()方法则会对整个数组进行遍历处理。

## some和every的区别

some 和 every 都是 JavaScript 数组的迭代方法，用于判断数组元素是否满足某个条件。

**它们的区别在于**：

1、some

some 方法会对数组中的每一个元素应用提供的测试函数，直到找到一个使测试函数返回 true 的元素，然后立即停止遍历并返回 true。如果所有元素都不满足条件，则返回 false。示例：

```js
const arr = [1, 2, 3, 4];

const hasEvenNumber = arr.some((num) => num % 2 === 0);

console.log(hasEvenNumber); // true
```

2、every

every 方法会对数组中的每一个元素应用提供的测试函数，直到找到一个使测试函数返回 false 的元素，然后立即停止遍历并返回 false。如果所有元素都满足条件，则返回 true。示例：

```js
const arr = [1, 2, 3, 4];

const allEvenNumbers = arr.every((num) => num % 2 === 0);

console.log(allEvenNumbers); // false
```

因此，some 和 every 的主要区别在于它们在数组中查找元素的方式，以及在何时停止遍历。

## slice是干嘛的、splice是否会改变原数组

slice和splice都是JavaScript数组的方法，但它们的功能是不同的。

**slice**

slice方法返回一个新的数组，该数组包含从原始数组中提取的元素。

slice方法接收两个参数，第一个参数是开始提取的位置，第二个参数是提取的结束位置（不包括该位置的元素）。

> 如果省略第二个参数，则提取从开始位置到数组的末尾的所有元素。slice方法不会修改原始数组，而是返回一个新的数组。

例如，以下代码将从原始数组arr中提取第二个到第四个元素，并将它们存储到新数组中newArr中：

```js
const arr = [1, 2, 3, 4, 5];
const newArr = arr.slice(1, 4);
console.log(newArr); // [2, 3, 4]
```

**splice**

splice方法用于添加或删除数组中的元素，并且会改变原始数组。

splice方法接收三个或更多参数。第一个参数是开始更改的位置，第二个参数是要删除的元素数量，第三个参数是要添加到数组中的新元素（如果有的话）。

> 如果省略第二个参数，则会删除开始位置到数组末尾的所有元素。splice方法返回被删除元素组成的数组。

例如，以下代码将删除原始数组arr中的第二个元素，并将其替换为6：

```js
const arr = [1, 2, 3, 4, 5];
const removedElements = arr.splice(1, 1, 6);
console.log(arr); // [1, 6, 3, 4, 5]
console.log(removedElements); // [2]
```

> 请注意，splice方法改变了原始数组arr，并且返回被删除元素组成的数组\[2\]。
>
> 因此，slice和splice方法都是对数组进行操作的重要工具，但它们的功能和效果是不同的。

## JS中的Array.splice()和Array.slice()方法有什么区别

`Array.splice()`和`Array.slice()`是 JavaScript 中常用的数组操作方法，它们的作用不同，具体区别如下：

1. `Array.splice()`
   `Array.splice()`方法用于向数组中插入或删除元素。它可以对原数组进行修改，返回被删除的元素组成的数组。`Array.splice()`方法接受 2 个或 3 个参数：

- 第一个参数：指定插入或删除的起始位置。
- 第二个参数：指定要删除的元素个数，如果为 0，则表示不删除任何元素。
- 第三个参数（可选）：指定要插入到数组中的元素。

示例：

```js
const arr = [1, 2, 3, 4, 5];

// 删除从位置 2 开始的 2 个元素，并插入新的元素
const removed = arr.splice(2, 2, 'a', 'b');
console.log(arr); // [1, 2, 'a', 'b', 5]
console.log(removed); // [3, 4]
```

在上面的示例中，`Array.splice()`方法从位置 2 开始删除 2 个元素，并将新的元素 `'a'` 和 `'b'` 插入到数组中。

2. `Array.slice()`
   `Array.slice()`方法返回一个新的数组，其中包含原数组的一部分。它不会修改原数组，而是返回一个新的数组。`Array.slice()`方法接受 2 个参数：

- 第一个参数（可选）：指定要返回的起始位置，如果不指定，则默认为 0。
- 第二个参数（可选）：指定要返回的结束位置（不包括该位置），如果不指定，则默认为原数组的长度。

示例：

```js
const arr = [1, 2, 3, 4, 5];

// 返回从位置 2 开始到位置 4（不包括）的子数组
const sliced = arr.slice(2, 4);
console.log(sliced); // [3, 4]
console.log(arr); // [1, 2, 3, 4, 5]
```

在上面的示例中，`Array.slice()`方法返回从位置 2 开始到位置 4（不包括）的子数组，不修改原数组。

总的来说，`Array.splice()`和`Array.slice()`方法的区别在于：

- `Array.splice()`会修改原数组，`Array.slice()`不会修改原数组。
- `Array.splice()`可以删除或插入元素，`Array.slice()`只能返回原数组的一部分。

## 数组中的forEach和map的区别？

forEach() 和 map() 两个⽅法都是ECMA5中Array引进的新⽅法，都是⽤来遍历数组中的每⼀项。

它们的主要区别是forEach是用来迭代数组中的每个元素，而map是用来对数组中的每个元素进行处理并返回新的数组。

**主要区别**

1、返回值不同

- forEach方法没有返回值或者说返回值为undefined，它的主要作用是迭代数组元素，而不是创建新的数组。
- map方法返回一个新的数组，数组的每个元素是对原数组的每个元素调用回调函数后的返回值。

2、使用方式不同

- forEach方法的回调函数有三个参数：当前元素、当前元素的索引和当前数组。这个回调函数可以改变当前元素的值，但是无法创建新的数组。
- map方法的回调函数有三个参数：当前元素、当前元素的索引和当前数组。这个回调函数可以创建新的数组，而且map方法会将每个回调函数的返回值组成一个新的数组。

3、用途不同

- forEach方法通常用于遍历数组并对每个元素执行一些操作，例如更新DOM元素等。
- map方法通常用于将一个数组转换为另一个数组，例如将一个数字数组的每个元素都乘以2，并返回一个新的数组。

总之，如果你需要遍历一个数组并对每个元素执行一些操作，使用forEach；如果你需要将一个数组转换为另一个数组并且每个元素都经过一些处理，使用map。

**其他区别：**

- map速度⽐forEach快
- map会返回⼀个新数组，不对原数组产⽣影响；foreach不会产⽣新数组，forEach返回undefined
- map因为返回数组所以可以链式操作，forEach不能
- map⾥可以⽤return（return的是什么，相当于把数组中的这⼀项变为什么（并不影响原来的数组，只是相当于把原数组克隆⼀份，把克隆的这⼀份的数组中的对应项改变了） 。
- forEach⾥⽤return不起作⽤，forEach不能⽤break，会直接报错。

## 整理Date的常见操作

创建date对象

```js
// 1.没有传入任何的参数, 获取到当前时间
var date = new Date()
console.log(date)  //Mon May 16 2022 09:00:32 GMT+0800 (中国标准时间)

// 2.传入参数: 时间字符串
var date2 = new Date("2022-01-01")
console.log(date2)//Sat Jan 01 2022 08:00:00 GMT+0800 (中国标准时间)

// 3.传入具体的年月日时分秒毫秒
var date3 = new Date(2033, 10, 10, 09, 08, 07, 333)
console.log(date3)//Thu Nov 10 2033 09:08:07 GMT+0800 (中国标准时间)

// 4.传入时间戳 1s -> 1000ms
var date4 = new Date(1111325412312)
console.log(date4)//Sun Mar 20 2005 21:30:12 GMT+0800 (中国标准时间)
```

dateString时间的表示方式

```js
//默认打印的时间格式是RFC 2822标准的:
var date = new Date()
console.log(date) // Mon May 16 2022 09:11:22 GMT+0800 (中国标准时间)
// 其他表示方式
console.log(date.toISOString()) //2022-05-16T01:13:06.968Z
console.log(date.toDateString()) //Mon May 16 2022
  
console.log(date.toLocaleDateString()) //2022/5/16
console.log(date.toLocaleTimeString()) //09:16:09
```

Date对象方法

```js
var date = new Date()
console.log(date) // Mon May 16 2022 09:24:32 GMT+0800

console.log(date.getFullYear()) //2022
console.log(date.getMonth()) // 4 (表示5月份)
console.log(date.getDate()) // 16
console.log(date.getHours()) // 9
console.log(date.getMinutes()) // 24
console.log(date.getSeconds()) // 32
console.log(date.getMilliseconds()) // 465
console.log(date.getTime()) //1652664272465
console.log(date.getDay()) // 1 星期一
```

获取date对象的时间戳

```js
// 获取时间戳的方式
var date1 = new Date()
var date2 = new Date("2033-03-03")

// 方法一: 当前时间的时间戳
var timestamp = Date.now() //1652665290035
console.log(timestamp)

// 方法二/三将一个date对象转成时间戳
var timestamp2 = date1.valueOf()
console.log(timestamp2) //1652665290035
var timestamp3 = date2.getTime()
console.log(timestamp3) //1993420800000

// 方法四:
console.log(+date) //1132324234242
```

字符串转时间戳:Date.parse(str)

```js
var str = "2022-08-31" // -> Wed Aug 31 2022 08:00:00 GMT+0800 (中国标准时间)
console.log(Date.parse(str))//1661904000000
var str2 = "2021/05/31 10:30"
console.log(Date.parse(str2))//1622428200000

var str3 = "2022.08.31"// -> Wed Aug 31 2022 00:00:00 GMT+0800 (中国标准时间)
console.log(Date.parse(str3))//1661875200000

var srt4 = "123abc"
console.log(Date.parse(srt4)) //NaN
```

## 数组如何进行降维（扁平化）

数组降维是指将多维数组转换为一维数组，也叫数组扁平化。在JavaScript中，可以使用多种方法实现数组降维。

1、使用flat()方法

ES6提供了数组的flat()方法，可以将多维数组扁平化为一维数组。flat()方法可以传入一个参数，用于指定扁平化的深度，默认为1。如果想要完全扁平化数组，可以传入Infinity作为参数。

示例代码：

```js
let arr = [1, [2, [3, 4]]];
let flattened = arr.flat(2);
console.log(flattened); // [1, 2, 3, 4]
```

2、使用reduce()方法

可以使用数组的reduce()方法实现数组扁平化。在reduce()方法中，可以通过递归调用reduce()方法，将多维数组转换为一维数组。

示例代码：

```js
let arr = [1, [2, [3, 4]]];
function flatten(arr) {
  return arr.reduce((acc, cur) => {
    return Array.isArray(cur) ? acc.concat(flatten(cur)) : acc.concat(cur);
  }, []);
}
let flattened = flatten(arr);
console.log(flattened); // [1, 2, 3, 4]
```

3、使用递归

使用递归也可以实现数组的扁平化。在递归中，可以判断数组的元素是否为数组，如果是数组就递归调用扁平化函数，否则将元素添加到结果数组中。

示例代码：

```js
let arr = [1, [2, [3, 4]]];
function flatten(arr) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    if (Array.isArray(arr[i])) {
      result = result.concat(flatten(arr[i]));
    } else {
      result.push(arr[i]);
    }
  }
  return result;
}
let flattened = flatten(arr);
console.log(flattened); // [1, 2, 3, 4]
```

4、使⽤数组的concat⽅法

```js
let arr = [1,2,[3,4]]
let result = []
result = Array.prototype.concat.apply([], arr)
```

5、使用数组的concat方法和扩展运算符

```js
var arr = [1,2,[3,4]]
var result = []
result = [].concat(...arr)
```

6、Array.some

利⽤Array.some⽅法判断数组中是否还存在数组，es6展开运算符连接数组

```js
let arr = [1,2,[3,4]]
while (arr.some(item => Array.isArray(item))) {
arr = [].concat(...arr);
}
```

## 数组去重，能用几种方法实现？

数组去重是指将数组中重复的元素去掉，只保留其中的一个。在 JavaScript 中，可以使用多种方法实现数组去重。

1、使用 Set 数据结构

Set 是 ES6 中引入的一种新的数据结构，它的特点是不允许出现重复元素。可以利用这个特性，将数组转换为 Set，再将 Set 转换回数组，这样就能去除数组中的重复元素了。

示例代码：

```js
let arr = [1, 2, 2, 3, 3, 4];
let deduplicated = Array.from(new Set(arr));
console.log(deduplicated); // [1, 2, 3, 4]
```

```js
function unique (arr) {
return Array.from(new Set(arr))
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,
null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
//[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {}, {}]
```

2、使用 filter() 方法

可以使用数组的 filter() 方法，利用 indexOf() 方法判断元素是否重复来实现数组去重。

示例代码：

```js
let arr = [1, 2, 2, 3, 3, 4];
let deduplicated = arr.filter((element, index) => {
  return arr.indexOf(element) === index;
});
console.log(deduplicated); // [1, 2, 3, 4]
```

```js
function unique(arr) {
return arr.filter(function(item, index, arr) {
//当前元素，在原始数组中的第⼀个索引==当前索引值，否则返回当前元素
return arr.indexOf(item, 0) === index;
});
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,
null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
//[1, "true", true, 15, false, undefined, null, "NaN", 0, "a", {…}, {…}]
```

3、使用 reduce() 方法

可以使用数组的 reduce() 方法，利用 includes() 方法判断元素是否重复来实现数组去重。

示例代码：

```js
let arr = [1, 2, 2, 3, 3, 4];
let deduplicated = arr.reduce((prev, cur) => {
  if (!prev.includes(cur)) {
    prev.push(cur);
  }
  return prev;
}, []);
console.log(deduplicated); // [1, 2, 3, 4]
```

4、使用 ES6 中的 Map 数据结构

Map 是一种 key-value 对应的数据结构，可以用来存储数组中的元素及其出现的次数，从而实现数组去重。

示例代码：

```js
let arr = [1, 2, 2, 3, 3, 4];
let map = new Map();
let deduplicated = [];
for (let i = 0; i < arr.length; i++) {
  if (!map.has(arr[i])) {
    map.set(arr[i], true);
    deduplicated.push(arr[i]);
  }
}
console.log(deduplicated); // [1, 2, 3, 4]
```

5、利⽤for嵌套for，然后splice去重（ES5中最常⽤）

```js
function unique(arr){
for(var i=0; i<arr.length; i++){
for(var j=i+1; j<arr.length; j++){
if(arr[i]==arr[j]){ //第⼀个等同于第⼆个，splice⽅法删除第⼆
个
arr.splice(j,1);
j--;
}
}
}
return arr;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,
null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
//[1, "true", 15, false, undefined, NaN, NaN, "NaN", "a", {…}, {…}] //NaN和{}没
有去重，两个null直接消失了
```

6、利⽤indexOf去重

```js
function unique(arr) {
if (!Array.isArray(arr)) {
console.log('type error!')
return
}
var array = [];
for (var i = 0; i < arr.length; i++) {
if (array .indexOf(arr[i]) === -1) {
array .push(arr[i])
}
}
return array;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,
null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
// [1, "true", true, 15, false, undefined, null, NaN, NaN, "NaN", 0, "a", {…},
{…}] //NaN、{}没有去重
```

7、利⽤ sort 去重

```js
function unique(arr) {
if (!Array.isArray(arr)) {
console.log('type error!')
return;
}
arr = arr.sort()
var arrry= [arr[0]];
for (var i = 1; i < arr.length; i++) {
if (arr[i] !== arr[i-1]) {
arrry.push(arr[i]);
}
}
return arrry;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,
null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
// [0, 1, 15, "NaN", NaN, NaN, {…}, {…}, "a", false, null, true, "true",
undefined] // NaN、{}没有去重
```

8、includes

```js
function unique(arr) {
if (!Array.isArray(arr)) {
console.log('type error!')
return
}
var array =[];
for(var i = 0; i < arr.length; i++) {
if( !array.includes( arr[i]) ) {//includes 检测数组是否有某个值
array.push(arr[i]);
}
}
return array
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,
null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
//[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {…}, {…}]
// {} 没有去重
```

9、利用递归去重

```js
function unique(arr){
return arr.reduce((prev,cur) => prev.includes(cur) ? prev : [...prev,cur],
[]);
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,
null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr));
// [1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {…}, {…}]
```

## 找出多维数组最大值

1、方案一（递归）

要找出多维数组的最大值，我们可以使用递归的方式来遍历整个数组，并找出最大值。具体的做法是：

1. 首先判断当前元素是否为数组，如果是，则递归调用该方法，并将子数组作为参数传递进去。
2. 如果当前元素不是数组，则与已经找到的最大值进行比较，如果比最大值还大，则更新最大值。

下面是一个示例代码，用于找出多维数组的最大值：

```js
function findMax(arr) {
  let max = -Infinity;
  for (let i = 0; i < arr.length; i++) {
    if (Array.isArray(arr[i])) {
      let subMax = findMax(arr[i]);
      if (subMax > max) {
        max = subMax;
      }
    } else {
      if (arr[i] > max) {
        max = arr[i];
      }
    }
  }
  return max;
}

// 示例用法
const arr = [1, 2, [3, 4, [5, 6]]];
const max = findMax(arr);
console.log(max); // 输出：6
```

> 在这个示例代码中，我们定义了一个名为`findMax()`的函数，用于找出多维数组的最大值。该函数接受一个参数`arr`，表示要查找的多维数组。
>
> 在函数中，我们首先定义一个变量`max`，用于保存已经找到的最大值。然后使用`for`循环遍历数组中的每一个元素。如果当前元素是数组，则递归调用`findMax()`方法，并将子数组作为参数传递进去，得到子数组的最大值，并将其与`max`比较，如果比`max`还大，则更新`max`。如果当前元素不是数组，则将其与`max`比较，如果比`max`还大，则更新`max`。最后返回`max`，即为多维数组的最大值。
>
> 注意，这个方法假设数组中所有元素都是数字类型。如果数组中包含其他类型的元素，则需要进行额外的判断和处理。
>

2、方案二（forEach）

```js
function fnArr(arr){
    var newArr = [];
    arr.forEach((item,index)=>{
        newArr.push( Math.max(...item)  )
    })
    return newArr;
}
console.log(fnArr([
    [4,5,1,3],
    [13,27,18,26],
    [32,35,37,39],
    [1000,1001,857,1]
]));
```

> 代码中的fnArr()函数使用了forEach()方法遍历二维数组中的每一个子数组，然后调用Math.max()方法找出子数组中的最大值，并将其放入一个新数组中。最后返回这个新数组。
>
> 需要注意的是，这种方式只适用于二维数组，如果数组的维度更高，那么需要使用递归的方式来实现。同时，这种方式假设所有子数组中的元素都是数字类型。如果数组中包含其他类型的元素，则需要进行额外的判断和处理。

# 📁 javaScript_DOM

## DOM和document对象的理解

1、DOM：文档对象模型(Document Object Model)，将页面所有的内容表示为可以修改的对象

- 浏览器将我们编写在HTML中的每一个元素(Element)都抽象成了一个个对象
- 所有这些对象都可以通过JavaScript来对其进行访问，那么我们就可以通过JavaScript来操作页面;
- 所以，我们将这个抽象过程称之为 文档对象模型(Document Object Model)

2、Document节点：表示的整个载入的网页，它的实例是全局的document对象

- 代表整个HTML或XML文档，是DOM层次结构中的根节点。
- 对DOM的所有操作都是从 document 对象开始的
- 它是DOM的入口点，Document对象提供了访问文档元素的方法和属性，可以使用它来访问文档中的元素，创建新元素，删除元素和修改元素属性等。

通常，使用JavaScript来操作DOM。通过Document对象，可以使用各种方法和属性来获取和修改文档中的元素，例如getElementById，getElementsByClassName，getElementsByTagName等。

总之，DOM是一种处理XML和HTML文档的标准方法，而Document对象是DOM中最重要的对象之一，它代表整个文档。

## DOM 中 Element 与 Node 有何区别

在DOM中，Element和Node都是对象，但它们代表不同的东西。

Element 继承于 Node，具有 Node 的⽅法，同时⼜拓展了很多⾃⼰的特有⽅法。

Node是DOM中所有节点类型的基类，包括元素节点、文本节点、注释节点等。Node对象具有许多常用属性和方法，例如nodeValue，nodeName，parentNode等。但是，Node对象不具有访问元素节点特定属性和方法的能力。

Element对象是表示文档中元素的节点类型，是Node的子类。Element对象继承了Node的所有属性和方法，并添加了许多专门用于元素节点的属性和方法，例如getAttribute，setAttribute，tagName等。因此，Element对象可以访问和修改元素节点的属性和内容。

在DOM中，元素节点是文档的主要组成部分，它包含了HTML或XML文档中的所有标记内容。因此，Element对象通常是DOM中最常用的对象之一。

综上所述，Node是DOM中所有节点类型的基类，而Element是表示文档中元素节点的节点类型，它们都具有许多属性和方法，但Element对象还可以访问和修改元素节点的特定属性和内容。

## 整理节点、元素的导航有哪些？

1、节点之间的导航:

- 父节点:parentNode
- 前兄弟节点:previousSibling
- 后兄弟节点:nextSibling
- 子节点:childNodes
- 第一个子节点:firstChild
- 第二个子节点:lastChild

2、元素之间的导航:

- 父元素:parentElement
- 前兄弟节点:previousElementSibling
- 后兄弟节点:nextElementSibling
- 子节点:children
- 第一个子节点:firstElementChild
- 第二个子节点:lastElementChild

## 节点（Node）常见的属性

1、nodeType

- 获取节点的类型
- 比如 注释节点8 文本节点3 元素节点1

2、tagName

- 获取元素的标签名词 仅适用于Element节点

3、nodeName

- 获取元素的标签名词 适用于任何Node节点

4、innerHTML,textContent

- 前者将元素中的HTML获取为字符串属性 后者仅仅获取文本内容

5、outerHTML

- 包含了完整的HTML
- 相当于innerHTML加上元素本身

6、nodeValue/data

- 获取非元素节点的文本内容

7、hidden

- 用于设置元素隐藏(全局属性)

## 说说attribute和Property的区别和关系

属性（Attributes）和属性（Properties）是Web开发中经常用到的概念，它们分别表示HTML元素上的特性和DOM中元素对象的属性。本文将分别讨论它们的定义、区别和使用建议。

1、Attributes

Attributes是HTML元素上的特性，可以通过HTML代码中的属性定义来设置。

例如，`<a href="https://www.example.com">Example</a>` 中的 `href` 属性。在浏览器解析HTML时，它会将属性值存储在元素的Attribute中。通过JavaScript可以通过元素的getAttribute()方法来获取属性的值。

Attributes可以分为标准的属性和非标准的属性。

- 标准属性包括`id`、`class`、`href`、`type`、`value`等等，
- 非标准属性则是用户自定义的，例如`abc`、`age`、`height`等。

2、Properties

Properties是DOM中元素对象的属性。这些属性是通过JavaScript代码创建的，并且代表了当前文档中元素的状态。

例如，HTML元素的属性可以通过元素的对应属性来访问例如`<input>`元素的`value`属性。在JavaScript中，可以通过直接设置或获取元素的属性来访问这些属性。例如，通过元素的`value`属性来获取或设置元素的值。

- 对于标准的attribute，会在DOM对象上创建对应的property属性。
- 大多数情况下，它们是相互作用的，改变其中一个，另一个也会随之改变。
- 大多数情况下，推荐获取attribute，使用property方式，因为它默认是有类型的。

虽然Attributes和Properties的值可能会相互依赖，但它们具有不同的目的和用途。通常情况下，应该优先使用Properties来访问元素的状态，因为它们更加直观且类型更明确。但在某些情况下，访问Attribute可能更为适合，例如在读取自定义属性时。

综上所述，Attributes和Properties在Web开发中扮演着不同的角色。对于HTML元素的状态，应该优先使用Properties来访问。但是，当需要读取或设置HTML元素的特性时，应该使用Attributes。

## 修改class和修改style的区别

在HTML和JavaScript中，我们可以使用class和style来修改元素的样式。虽然它们都可以实现修改元素样式的效果，但是它们之间有一些区别。

- 如果动态修改class完成某个功能 推荐动态的添加class
- 如果精准修改某个CSS属性的值 则修改style属性

**class**

class用于为元素定义CSS样式类，它可以在CSS样式表中定义一组样式，然后将这个样式类应用到一个或多个元素中。通过修改元素的class属性值，可以切换元素的样式类，从而改变元素的样式。

```javascript
<!-- CSS样式表中定义 -->
.red {
  color: red;
}

<!-- 应用到元素中 -->
<div class="red">Red text</div>

<!-- JavaScript中修改class属性值 -->
const elem = document.querySelector('.red');
elem.classList.add('blue'); // 添加blue样式类
elem.classList.remove('red'); // 移除red样式类
```

**style**

style用于为元素直接设置CSS样式，可以直接在元素上设置样式属性值，也可以使用JavaScript来修改样式属性值。通过修改元素的style属性值，可以实现直接修改元素的CSS样式的效果。

```javascript
<div style="color: red;">Red text</div>

<!-- JavaScript中修改style属性值 -->
const elem = document.querySelector('div');
elem.style.color = 'blue'; // 修改color属性值为blue
elem.style.backgroundColor = 'yellow'; // 添加backgroundColor属性值
```

**区别**

class和style的主要区别在于它们的作用范围和修改方式。

class可以定义一组CSS样式，并将这个样式类应用到多个元素中，从而实现样式的复用，可以通过修改元素的class属性值来切换元素的样式，比较适合用于修改多个元素的样式。

而style是直接为单个元素设置CSS样式属性值，可以通过修改元素的style属性值来修改元素的样式，比较适合用于修改单个元素的样式。

此外，class可以通过CSS样式表中的选择器来实现更加复杂的样式匹配和样式继承，而style则比较适合用于动态生成或修改单个元素的样式。

综上所述，class和style都是修改元素样式的常用方式，需要根据具体情况选择使用哪种方式来实现需要的样式效果。

## DOM常见的操作方法

DOM（Document Object Model）提供了许多方法和属性，可以用来访问和操作HTML和XML文档的内容。以下是常见的DOM操作方法：

**1、获取元素**

- document.getElementById('id')：根据id获取元素
- document.getElementsByClassName('class')：根据类名获取元素
- document.getElementsByTagName('tag')：根据标签名获取元素
- document.querySelector('selector')：根据选择器获取元素
- document.querySelectorAll('selector')：根据选择器获取所有符合条件的元素

**2、创建元素**

- document.createElement('tag')：创建一个新的元素节点

**3、插入和删除元素**

- parentElement.appendChild(childElement)：将子元素添加到父元素的末尾
- parentElement.insertBefore(newElement, referenceElement)：将新元素插入到参考元素之前
- parentElement.removeChild(childElement)：从父元素中删除子元素

**4、修改元素**

- element.innerHTML：设置或获取元素的HTML内容
- element.innerText：设置或获取元素的纯文本内容
- element.setAttribute(name, value)：设置元素的属性值
- element.getAttribute(name)：获取元素的属性值
- element.style.property = value：设置元素的样式属性值

**5、查询元素信息**

- element.tagName：获取元素的标签名
- element.id：获取或设置元素的id属性值
- element.className：获取或设置元素的类名
- element.parentElement：获取元素的父元素
- element.children：获取元素的子元素列表
- element.getAttribute(name)：获取元素的指定属性值

**6、事件操作**

- element.addEventListener('event', function)：为元素添加事件监听器
- element.removeEventListener('event', function)：为元素移除事件监听器

## 常见对DOM的增删改查

常见对DOM的增删改查操作如下：

增加元素：通过createElement()创建新元素，通过appendChild()将新元素添加到现有元素中。

```js
// 创建新的div元素
const newDiv = document.createElement('div');
// 添加新的div元素到现有的body元素中
document.body.appendChild(newDiv);
```

删除元素：通过removeChild()方法删除一个现有的元素。

```js
// 获取要删除的元素
const el = document.getElementById('my-element');
// 从父元素中移除该元素
el.parentNode.removeChild(el);
```

修改元素：通过innerHTML属性设置元素的HTML内容。

```js
// 获取要修改的元素
const el = document.getElementById('my-element');
// 设置元素的HTML内容
el.innerHTML = '<h1>New heading</h1>';
```

查询元素：通过querySelector()、getElementById()、getElementsByClassName()等方法获取现有的元素。

```js
// 获取单个元素
const el = document.querySelector('#my-element');
// 获取多个元素
const els = document.getElementsByClassName('my-class');
```

这些常见的DOM操作可以帮助我们实现动态的页面交互和内容更新。需要注意的是，频繁的DOM操作可能会导致性能问题，应尽量减少DOM操作的次数，可以考虑使用文档片段（DocumentFragment）等技术来优化。

## 动态创建html元素，并插入到body

可以使用JavaScript中的createElement()和appendChild()方法来动态创建HTML元素，并将其插入到body中。

以下是一个例子，创建一个div元素，并设置其class和文本内容，然后将其插入到body中：

```js
// 创建div元素
const div = document.createElement('div');

// 设置class属性
div.className = 'my-div';

// 设置文本内容
div.textContent = 'This is my div.';

// 将div插入到body中
document.body.appendChild(div);
```

在这个例子中，首先使用createElement()方法创建一个div元素。然后使用className属性设置其class，使用textContent属性设置文本内容。最后，使用appendChild()方法将其插入到body元素中。

为什么不用 innerText 设置文本内容?

```js
div.innerText = 'This is my div.';
```

虽然innerText可以用于设置元素的文本内容，但是它的行为可能不同于预期，因为它会忽略隐藏元素，同时也会将HTML解析为纯文本，因此在某些情况下可能会引起安全问题。比如，如果将用户输入的HTML代码设置为元素的innerText，那么该HTML代码将会被解析为纯文本并显示在页面上，而不是被浏览器解析为HTML标记。这可能会导致一些安全问题，比如XSS攻击。

相比之下，使用textContent可以更安全地设置元素的文本内容，因为它只会将文本解析为纯文本，而不会将其解析为HTML标记。同时，textContent也不会忽略隐藏元素，因此可以确保元素的文本内容是准确的。

## 显示当前时间

在界面中动态显示当前时间，可以使用 JavaScript 中的 Date 对象获取当前时间，然后将其显示在页面上。

首先，在 HTML 中创建一个用于显示时间的标签：

```html
<span id="current-time"></span>
```

然后，使用 JavaScript 获取该标签，并在 setInterval() 方法中每秒更新一次时间：

```js
function updateTime() {
  let now = new Date();
  let hours = now.getHours();
  let minutes = now.getMinutes();
  let seconds = now.getSeconds();
  let timeString = `${hours}:${minutes}:${seconds}`;
  document.getElementById('current-time').innerHTML = timeString;
}

setInterval(updateTime, 1000);
```

在上面的代码中，首先定义了一个 `updateTime()` 函数，该函数使用 `Date` 对象获取当前时间，并将其格式化为一个字符串。然后，将该字符串设置为 `id` 为 `current-time` 的标签的内容。最后，使用 `setInterval()` 方法每秒调用一次 `updateTime()` 函数，以更新显示的时间。

这样，每秒钟就会动态地显示当前时间了。

## 说说事件冒泡和事件捕获的理解

事件冒泡（event bubbling）和事件捕获（event capturing）是指在 DOM 树中处理事件的两种不同方式。

**事件冒泡**

事件冒泡是指当一个元素触发了某个事件时，该事件会首先在该元素上进行处理，然后沿着 DOM 树向上依次传递，直到到达根节点。这意味着如果一个子元素触发了事件，该事件将传递给它的父元素，然后再传递给更高层次的祖先元素。这种传递事件的方式就像气泡一样从下往上冒。

**事件捕获**

事件捕获则是相反的过程。事件从根节点开始进行处理，然后依次向下传递到最深层次的元素。当到达目标元素时，事件会在目标元素上进行处理。这种传递事件的方式就像捕捉一样从上往下抓。

默认情况下，浏览器采用的是事件冒泡模式。但是可以通过 addEventListener() 方法的第三个参数来设置事件模式，例如：

```js
element.addEventListener('click', handleClick, true); // 使用事件捕获模式
element.addEventListener('click', handleClick, false); // 使用事件冒泡模式
```

在这里，第三个参数为 true 时表示使用事件捕获模式，为 false 时表示使用事件冒泡模式。

## target 和 EvenTarget 的区别

在JavaScript中，事件触发过程中有两个重要的对象：target和currentTarget。target 和 EventTarget 是两个不同的概念。

**target**

target是事件对象的一个属性，它表示触发事件的目标元素，即事件最初发生的位置。在事件监听器中，可以通过访问事件对象的 target属性来获取触发事件的元素。

**EvenTarget**

EventTarget 是一个接口，它表示可以接收事件的对象。在 DOM 中，几乎所有的对象都实现了 EventTarget 接口，比如 document、window、HTML 元素等。实现了 EventTarget 接口的对象可以通过调用 addEventListener 方法来添加事件监听器，或者调用 dispatchEvent 方法来触发事件。

**两者联系**

可以看到，target 和 EventTarget 的作用不同，但它们之间有一定的联系。在事件监听器中，我们可以通过访问事件对象的 target 属性来获取触发事件的元素，而这个元素实际上就是一个实现了 EventTarget 接口的对象。我们可以在这个元素上添加事件监听器，也可以通过调用这个元素的 dispatchEvent 方法来触发事件。

在事件捕获和冒泡阶段，事件会在DOM树中进行传播，会涉及到多个元素，但是只有目标元素和当前元素是常常需要用到的。

需要注意的是，currentTarget和target有时会是同一个元素，比如在事件冒泡阶段，事件最终到达document对象时，target和currentTarget就是同一个对象。而在事件捕获阶段，由于事件是从顶层元素往下传递的，所以currentTarget和target的值就不一定相同了。

**案例**

在事件处理过程中，事件会从最外层的元素开始向内层传递，到达目标元素后再从目标元素向外层传递。在这个过程中，target始终表示最初触发事件的元素，而currentTarget则表示当前正在处理事件的元素。在捕获阶段，currentTarget表示的是最外层的元素，而在冒泡阶段，currentTarget则表示的是目标元素。

下面是一个例子，可以帮助更好地理解target和currentTarget之间的区别：

```js
<div id="outer">
  <div id="inner">
    Click me
  </div>
</div>

const outer = document.querySelector('#outer');
const inner = document.querySelector('#inner');

outer.addEventListener('click', function(event) {
  console.log('target:', event.target);
  console.log('currentTarget:', event.currentTarget);
});

inner.addEventListener('click', function(event) {
  console.log('target:', event.target);
  console.log('currentTarget:', event.currentTarget);
});
```

在上面的代码中，当点击“Click me”时，会依次触发内层元素和外层元素的事件监听函数。在内层元素的事件监听函数中，target和currentTarget都指向内层元素；在外层元素的事件监听函数中，target指向内层元素，而currentTarget则指向外层元素。

## EventTarget的使用

**前言**

- addEventListener:注册某个事件类型以及事件处理函数
- removeEventListener : 移除某个事件类型以及事件处理函数
- dispatchEvent : 派发某个事件类型到EventTarget上

**EventTarget**

EventTarget 接口是一个非常重要的接口，因为在 Web 应用程序中，几乎所有的事件都是由它来处理的。一个实现了 EventTarget 接口的对象可以被用作事件的目标对象，也就是说，可以向这个对象注册事件监听器，当事件发生时，目标对象会自动触发相应的事件监听器，并调用相应的处理函数。

在 JavaScript 中，常见的实现了 EventTarget接口的对象包括 window对象、document对象以及 DOM 元素。这些对象都具有相应的事件处理能力，可以用来处理用户的交互、实现动画效果、异步数据请求等等。

**常用方法**

EventTarget 接口定义了以下常用的方法：

- addEventListener(type, listener, options)：向目标对象注册事件监听器。type 表示事件类型，listener 表示事件处理函数，options 是一个可选的参数对象，用于配置事件监听器的一些属性，例如 capture、once、passive 等。默认情况下，事件监听器是在事件冒泡阶段处理的，如果需要在事件捕获阶段处理事件，可以将 capture 属性设置为 true。
- removeEventListener(type, listener, options)：从目标对象中移除事件监听器。和 addEventListener() 方法类似，需要指定要移除的事件类型和处理函数，同时也可以指定一些可选参数。
- dispatchEvent(event)：手动触发事件。event 表示要触发的事件对象，通常是一个 Event 子类的实例。触发事件时，事件会沿着 DOM 树进行传递，直到到达目标元素。

**其他属性和方法**

除了上面这些方法之外，EventTarget 还有一些其他的属性和方法，包括：

- on\[event\]：这是一个简便的方式来为目标对象注册事件监听器，例如 onclick、onload 等。实际上，这些属性就是 addEventListener() 方法的语法糖，例如 element.onclick = function() { ... } 就相当于 element.addEventListener('click', function() { ... })。
- eventPhase：表示当前事件所处的阶段，可能的值有 0（未初始化）、1（事件捕获阶段）、2（事件目标阶段）和 3（事件冒泡阶段）。
- dispatchEvent(event)：手动触发事件。event 表示要触发的事件对象，通常是一个 Event 子类的实例。触发事件时，事件会沿着 DOM 树进行传递，直到到达目标元素。

**案例演示**

下面是一个简单的示例，展示了如何使用 EventTarget 接口来注册和移除事件监听器，并手动触发事件：

```html
<button id="myButton">Click me</button>
```

```js
const button = document.getElementById('myButton');

function handleClick() {
  console.log('Button clicked!');
}

button.addEventListener('click', handleClick);

setTimeout(() => {
  button.removeEventListener('click', handleClick);
}, 5000);

const customEvent = new CustomEvent('myEvent', {
  detail: {
    message: 'Hello, world!'
  }
});

button.dispatchEvent(customEvent);
```

> 在这个示例中，我们首先获取了一个 button 元素，并为它注册了一个 click 事件监听器。该监听器会在按钮被点击时被触发，并在控制台输出一条信息。
> 接着，我们使用 setTimeout() 函数，5 秒钟之后，移除了之前注册的事件监听器。这意味着，在按钮被点击之后的 5 秒钟内，再次点击按钮时，并不会触发 handleClick() 函数。
> 最后，我们创建了一个自定义事件 myEvent，并将其分派到按钮元素上。在这个例子中，我们使用 CustomEvent 构造函数来创建一个自定义事件对象，并指定了一个 detail 属性，它是一个任意的 JavaScript 对象，用于存储事件的附加信息。然后，我们使用 button.dispatchEvent() 方法触发了这个自定义事件。当事件被触发时，会在控制台输出一个包含 message 属性的信息。

## 对事件委托的理解

**是什么**

事件委托（Event Delegation）是一种常用的==前端开发技巧==，它可以帮助我们更高效地处理事件，并减少内存消耗。

**基本思想**

事件委托的基本思想是利用事件的冒泡机制，在父元素上统一处理多个子元素的事件。我们只需要将事件处理程序添加到父元素上，然后判断事件源是否是我们需要处理的子元素，如果是，就执行相应的操作。

**优势**

使用事件委托的好处在于，我们无需为每个子元素都添加事件处理程序，这样可以避免因为创建大量的事件处理程序而导致内存消耗过大的问题。此外，事件委托还可以解决动态添加和删除子元素时，需要重新绑定事件的问题。

**案例**

以下是一个使用事件委托的示例，假设我们有一个列表元素和多个列表项元素，我们想要为每个列表项添加点击事件处理程序：

```html
<ul id="list">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

我们可以在列表元素上添加一个 `click` 事件监听器，然后判断事件源是否是列表项元素，如果是，就执行相应的操作：

```javascript
const list = document.getElementById('list');

list.addEventListener('click', event => {
  const target = event.target;
  
  // 判断事件源是否是列表项元素
  if (target.nodeName === 'LI') {
    console.log(`Clicked ${target.innerText}`);
  }
});
```

在上面的代码中，我们首先获取了列表元素，并为其添加了一个 `click` 事件监听器。然后，在监听器函数中，我们使用 `event.target` 属性获取事件源，判断其是否是列表项元素，如果是，就在控制台输出相应的信息。

> 使用事件委托的方式，我们只需要在父元素上添加一个事件监听器，就可以处理多个子元素的事件。这样不仅可以减少内存消耗，而且还可以提高代码的可维护性。

# 📁 javaScript_事件

## 整理常见的事件

1. 点击事件（click）：当用户在元素上单击时触发。
2. 双击事件（dblclick）：当用户在元素上双击时触发。
3. 鼠标移动事件（mousemove）：当用户在元素上移动鼠标时触发。
4. 鼠标悬停事件（mouseover）：当鼠标移动到元素上时触发，如果鼠标移到元素的子元素上，则不会触发。
5. 鼠标移出事件（mouseout）：当鼠标从元素上移开时触发，如果鼠标移到元素的子元素上，则不会触发。
6. 按键事件（keydown、keyup）：当用户按下或释放键盘上的键时触发。
7. 表单事件（submit、reset、change、focus、blur）：当用户提交表单、重置表单、改变表单元素的值、聚焦或失焦时触发。
8. 页面生命周期事件（load、unload、beforeunload）：当页面加载、卸载或即将卸载时触发。
9. 视窗事件（resize、scroll）：当窗口大小调整或滚动时触发。
10. 触摸事件（touchstart、touchmove、touchend、touchcancel）：当用户在触摸屏上触摸元素时触发。
11. 动画事件（animationstart、animationend、animationiteration）：当CSS动画开始、结束或重复时触发。
12. 过渡事件（transitionstart、transitionend）：当CSS过渡开始或结束时触发。

以上是一些常见的事件，JavaScript还提供了更多的事件类型，具体根据实际需求来选择。

## mouseenter和mouseover的区别

1、mouseenter

- 不会冒泡
- 进入子元素的时候不会有任何行为

mouseenter事件只有在鼠标指针进入事件的目标元素时才被触发。它不会冒泡，也就是说，当鼠标指针进入一个元素时，如果该元素有子元素，那么这个事件只会在目标元素上触发一次，不会在子元素上触发。同时，当鼠标指针从目标元素内部移动到其子元素上时，不会触发该事件。

2、mouseover

- 会进行冒泡行为
- 进入子元素 会先out父元素 在over子元素 在over父元素

而mouseover事件在鼠标指针进入事件目标元素或其子元素时都会被触发。它会进行冒泡，也就是说，当鼠标指针进入一个元素时，该事件会在目标元素和其所有祖先元素上触发，而当鼠标指针从目标元素内部移动到其子元素上时，会先触发一次mouseout事件在目标元素上，然后再在子元素上触发一次mouseover事件，最后再在目标元素及其祖先元素上触发一次mouseover事件。

> 因此，mouseenter事件和mouseover事件在处理鼠标指针进入和离开元素时有所不同，mouseenter事件更加严格，而mouseover事件更加灵活。

## 说说load和DOMContentLoaded的区别

`load` 和 `DOMContentLoaded` 都是针对页面加载事件的。

**load**

- 浏览器加载完所有的HTML 还加载完所有的外部资源 样式 图片等

`load` 事件在页面及其所有相关资源（如图片、脚本、样式等）都加载完成后触发。如果在 `load` 事件触发之前添加了新的资源，那么这些新的资源也需要加载完成后才能触发 `load` 事件。

**DOMContentLoaded**

- HTML文档所有资源都加载完成 并构建了DOM树 但是一些外部资源还没有加载完成 如图片的src

`DOMContentLoaded` 事件则是在页面的 HTML 和 DOM 树构建完成后触发，不需要等待其他资源的加载。也就是说，当 `DOMContentLoaded` 触发时，仅仅是页面的 HTML 和 DOM 树构建完成，但并不代表所有资源都已加载完毕，比如图片可能还在加载中。

**总结**

因此，如果你需要在页面加载完成后执行一些操作，比如对 DOM 进行操作，那么建议使用 `DOMContentLoaded` 事件，因为它触发的时机比 `load` 事件更早，而且不需要等待所有资源的加载完成。如果你需要等待所有资源都加载完成后再执行某些操作，那么使用 `load` 事件是更为合适的选择。

# 📁 Others

包括自己平时遇到的问题，和学习整理的知识点~

## 如何实现页面文本不可复制

实现页面文本不可复制的方法有多种，以下是几种常见的方法：

**使用CSS属性**

user-select:none; 可以通过在CSS中将user-select属性设置为none来禁止文本被选中和复制。例如：

```css
body {
  -webkit-user-select: none; /* Safari */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* IE10+/Edge */
  user-select: none; /* Standard */
}
```

**使用JavaScript禁止复制**

可以使用JavaScript来防止文本复制，当用户尝试复制文本时，可以触发事件并阻止默认行为。例如：

```js
document.addEventListener("copy", function(event) {
  event.preventDefault();
});
```

**使用图片代替文本**

将文本转换为图片可以有效地防止复制。但是这种方法可能会导致一些SEO问题，因为搜索引擎无法读取图片中的文本。

> 需要注意的是，这些方法都不是100%可靠的，因为用户仍然可以通过一些特殊的技巧来复制文本。因此，如果您需要保护敏感信息，最好采用其他更加可靠的方法，如使用加密技术或限制访问权限等。

## 整理JSON的相关用法和应用场景

JSON（JavaScript Object Notation）是一种轻量级的数据交换格式，常用于前后端数据传输、配置文件、API等。

**三种用法**

- 简单值：可以是数字、字符串、布尔类型，也可以是 null 和 undefined。
- 对象值：由 key-value 组成，key 必须添加双引号，value 可以是简单值、对象值或数组值。
- 数组值：由多个值组成，内容可以是对象值、简单值或其他数组值。

**应用场景**

1、网络传输的JSON数据：

- 在前后端数据交互中，通常使用JSON作为数据格式进行传输，因为JSON具有轻量、易解析的特点，能够大大减小传输数据的大小，提高传输效率。

```js
 // 将JSON格式的字符串解析为JavaScript对象，可以使用JSON.parse()方法，例如：
const personJSON = '{"name":"Tom","age":20}';
const person = JSON.parse(personJSON);
console.log(person); // {name: "Tom", age: 20}
```

2、项目的某些配置文件：

- 如前端项目中的 package.json 文件，里面存储了项目的各种配置信息，包括项目名称、版本号、依赖等。可以通过读取JSON文件的方式读取配置信息

```js
{
  "database": {
    "host": "localhost",
    "port": 3306,
    "user": "root",
    "password": "123456",
    "database": "test"
  }
}
```

3、非关系型数据库将JSON作为存储文件：

- 像 MongoDB 这种非关系型数据库，常常使用JSON作为存储文件，通过解析JSON来操作数据。JSON的结构化和灵活性，使得它在这种场景下表现出色。

4、Web API 接口返回的数据格式：

- 很多 Web API 接口返回的数据格式都是JSON，比如 GitHub API、Twitter API 等等。前端通过解析这些JSON数据，可以快速构建出展示数据的页面。

```js
{
  "status": "success",
  "data": {
    "name": "Tom",
    "age": 20,
    "email": "tom@example.com"
  }
}
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
复制代码
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
复制代码
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

## cookie和session的区别


Cookie 和 Session 都是 Web 应用程序中常用的用户状态管理机制，两者的作用和实现方式有所不同，具体区别如下：

1. 存储位置不同

Cookie 保存在客户端浏览器上，而 Session 保存在服务器端。当客户端发送请求时，服务器会根据请求头中的 Cookie 信息获取客户端的状态。

2. 存储方式不同

Cookie 的数据以键值对的方式保存在客户端浏览器的文件中，可以通过 JavaScript 访问和修改。Session 的数据保存在服务器的内存中，客户端浏览器只保存一个 Session ID，用于在服务器端查找对应的 Session 数据。

3. 安全性不同

由于 Cookie 存储在客户端浏览器中，因此容易被恶意代码或攻击者窃取，从而导致用户的信息泄露。而 Session 存储在服务器端，相对来说更加安全。

4. 有效期不同

Cookie 可以设置一个过期时间，一旦到期，浏览器会自动删除该 Cookie。而 Session 的有效期通常由服务器端设置，用户关闭浏览器或长时间未操作时，Session 数据会自动销毁。

5. 存储容量不同

由于 Cookie 存储在客户端浏览器中，因此存储容量有限，一般只能保存几 KB 的数据。而 Session 存储在服务器端，存储容量相对较大，可以保存几 MB 的数据。

总的来说，Cookie 和 Session 都可以用于存储用户的状态信息，但是它们的实现方式和应用场景有所不同。一般来说，Cookie 适用于保存较小的数据，并需要在客户端使用，例如用户的偏好设置等；而 Session 适用于保存较大的数据，并需要在服务器端使用，例如用户的登录状态等。

## 代码报错

### 影响

JavaScript代码报错非常危险，因为它可能`导致后续代码无法执行，或者在执行时出现异常行为。`

当JavaScript代码遇到错误时，它会停止执行，并抛出一个异常。这个异常会中断当前的代码流程，导致后续代码无法执行。这可能会导致一系列问题，包括：

- 用户体验受损：如果JavaScript代码出错导致网站无法正常运行，用户可能会遇到错误信息或者空白页面，这会让用户感到沮丧并降低用户满意度。
- 安全漏洞：JavaScript代码出错可能导致安全漏洞，例如未被正确处理的用户输入，可以导致跨站脚本攻击（XSS）或SQL注入等攻击。
- 生产环境崩溃：JavaScript代码出错可能导致整个生产环境崩溃，这会影响到所有用户和业务，对公司带来重大影响。

因此，对于JavaScript代码，我们需要尽可能避免错误，并进行有效的错误处理。可以使用try-catch语句捕获和处理异常，以确保代码可以继续执行，并在出现错误时提供用户友好的错误信息。同时，通过使用代码审查和测试等技术，可以帮助我们发现和修复潜在的问题，提高代码质量和稳定性。

### 案例一

假设我们有一个简单的JavaScript函数，它的作用是计算两个数的和：

```
function sum(a, b) {
  return a + b;
}
```

如果我们在调用这个函数时传递的参数不是数字类型，那么JavaScript会抛出一个TypeError异常。例如：

```
sum(2, '3'); // 抛出异常
```

如果我们不进行有效的异常处理，这个异常会中断代码流程，并导致后续代码无法执行。

在这个例子中，我们的代码在调用`sum`函数时抛出了一个异常，导致后续代码无法执行。这对于网站的用户体验和安全性都是不利的。

如果我们使用try-catch语句来捕获和处理这个异常，我们就可以避免这个问题，如下图所示：

```
try {
  sum(2, '3'); // 抛出异常
} catch (e) {
  console.error('发生了一个错误：', e);
}
console.log('这里的代码仍然可以执行');
```

在这个例子中，我们使用了try-catch语句来捕获和处理异常。当异常发生时，控制流会跳转到catch语句块，并执行其中的代码。在这个例子中，我们使用console.error输出错误信息，但是我们也可以执行其他的异常处理逻辑，例如给用户友好的错误提示。在catch语句块结束后，控制流会继续执行后续的代码，不会中断整个程序的执行。

### 案例二

> 证明有效的异常处理可以提高程序的稳定性和可维护性：

假设我们正在编写一个在线购物网站的JavaScript代码，其中有一个函数用于向购物车中添加商品：

```
function addToCart(product) {
  if (!product.name || !product.price || !product.quantity) {
    throw new Error('商品信息不完整');
  }
  // 将商品添加到购物车中
  // ...
  console.log('商品已添加到购物车');
}
```

在这个函数中，我们首先进行了参数校验，如果参数不完整则抛出一个异常。这样可以确保我们只向购物车中添加合法的商品，并避免程序出现未知的错误。

接下来，我们使用try-catch语句来捕获和处理异常，并向用户显示友好的错误提示：

```
try {
  addToCart({ name: '苹果', price: 5 });
} catch (e) {
  console.error('添加商品到购物车失败：', e.message);
  alert('添加商品到购物车失败，请检查商品信息是否完整。');
}
```

在这个例子中，我们使用try-catch语句来捕获和处理异常。如果向购物车中添加商品时出现了异常，控制流会跳转到catch语句块，并输出错误信息。同时，我们还向用户显示了友好的错误提示，以提高用户体验。

通过这种方式，我们可以确保我们的JavaScript代码可以正确地处理异常，并提高程序的稳定性和可维护性。如果我们没有进行有效的异常处理，可能会导致程序出现未知的错误，并给用户带来不好的体验。

### 两种方式来检查代码报错

1、控制台输出：

在浏览器中打开开发者工具，选择控制台(Console)面板，可以查看JavaScript代码的控制台输出。如果代码中有错误，控制台会输出错误信息，并标明错误发生的位置和类型。通常，错误信息包含错误类型、错误描述和错误发生的代码位置等信息，可以帮助我们快速定位和修复错误。

2、调试工具：

调试工具是一种用于调试JavaScript代码的工具，可以帮助我们更方便地查看和调试代码。在浏览器中打开开发者工具，选择调试器(Debugger)面板，可以查看JavaScript代码的调试信息，并可以在代码中设置断点、单步调试和查看变量值等。通过调试工具，我们可以更直观地查看代码的执行流程和变量状态，快速定位和解决问题。

> 在实际开发中，我们通常会结合使用控制台输出和调试工具来检查代码报错。通过这些工具，我们可以快速定位和解决问题，并提高代码的质量和稳定性。

## javascript语言的缺陷与败笔有哪些

JavaScript是一种广泛使用的编程语言，具有许多优点，但也存在一些缺陷和败笔。以下是一些可能的缺陷和败笔：

1. 弱类型和动态类型：JavaScript是一种弱类型和动态类型语言，这意味着在编译时不会检查类型错误，而是在运行时检测错误。这可能导致难以调试和错误的行为。

2. 难以调试：由于JavaScript是一种动态类型语言，常常需要在运行时进行调试。这使得在开发大型项目时难以调试，并增加了编写质量高的代码的难度。

3. 全局变量：JavaScript的全局变量机制使得代码难以维护和重用。任何函数都可以访问和更改全局变量，这可能导致不可预测的行为和命名冲突。

4. 缺乏模块系统：JavaScript缺乏官方模块系统，这意味着在管理依赖关系时需要手动实现模块。这可能导致名称冲突和难以理解的代码。

5. 非标准化：JavaScript由不同的浏览器实现，这可能导致不同的浏览器之间存在不兼容性问题。此外，JavaScript也存在不同版本和实现之间的不兼容性。

6. 垃圾回收：JavaScript的垃圾回收机制不够完善，可能导致内存泄漏和性能问题。

7. 单线程：JavaScript是一种单线程语言，这意味着一次只能执行一个任务。这可能导致长时间运行的任务阻塞UI线程，并影响用户体验。

8. 非阻塞I/O：JavaScript的非阻塞I/O机制可能导致回调嵌套和复杂的控制流程，增加了代码的难度和错误的可能性。

9. 安全性问题：JavaScript可能受到跨站脚本攻击和其他安全漏洞的影响。这可能导致数据泄漏和恶意代码的执行。

总的来说，JavaScript作为一种动态语言，在开发中可以提高开发效率和灵活性，但也存在一些缺陷和败笔。在编写高质量的JavaScript代码时，需要考虑这些问题并采取相应的措施来避免问题。