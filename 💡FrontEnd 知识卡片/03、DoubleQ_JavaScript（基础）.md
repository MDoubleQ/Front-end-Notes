# 📁 JavaScript基础

## 简单聊聊JavaScript的历史

1、1994 年，网景公司发布 Navigator 浏览器 0.9 版本

- 发布时，Navigator 浏览器还不能有与用户的交互效果
- 网景公司急需希望选定一门语言作为浏览器的脚本语言

2、同年，网景公司招聘了 Brendan Eich，希望帮助选定一门脚本语言

- 最开始是选定 Scheme 语言作为浏览器的脚本语言

3、1995 年，Sun 公司将 Oak 语言改名为 Java 正式向市场推出

- 轰动一时
- Java 的口号非常吸引人"Write once Run anywhere"
- 网景公司因此希望与 Sun 合作，希望将 Java 嵌入到网页中，作为浏览器的脚本语言
- 这时，Brendan Eich 还是坚持选择 Scheme，而公司高层则希望简化 Java 作为脚本语言

4、Brendan Eich 用 10 天时间设计出 JavaScript，网景公司正式使用 JavaScript 作为 Navigator 的脚本语言

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

**共有四种交互方式**

```js
// 1、弹窗输出 alert("Hello World!")
alert("Hello World!")

// 2、控制台输出 console.log("Hello World!")
console.log("Hello World!")

// 3、文档输出 document.write("Hello World!")
document.write("Hello World!")

// 4、弹出输入框输入 prompt("Please write some words!")
prompt()
prompt("Notification")
// 变量赋值时使用 prompt()函数
var variable = prompt("Notification")
```

## 使用 `@param` 注释：

在代码中的注释 `@param` 是用来描述函数的参数的说明文档标记，通常用于生成文档或注释工具。它用于指定函数的参数名称、类型和描述信息。

你可以按照以下方式使用 `@param` 注释：

```javascript
/**
 * 函数的描述信息
 * @param {类型} 参数名 参数描述信息
 */
function functionName(parameter) {
  // 函数体
}
```

具体示例：

```javascript
/**
 * 计算两个数的和
 * @param {number} a 第一个数
 * @param {number} b 第二个数
 * @returns {number} 两个数的和
 */
function sum(a, b) {
  return a + b;
}
```

在上面的示例中，通过 `@param` 注释标记指定了函数 `sum` 的两个参数 `a` 和 `b` 的类型为 `number`，以及相应的描述信息。这些注释可以帮助其他开发人员理解函数的使用方式和参数的含义。

请注意，`@param` 注释只是用于提供文档或注释工具的参考，JavaScript 本身并不会解析这些注释。因此，你需要使用相应的文档生成工具或阅读器来处理这些注释并生成文档。

在大多数情况下，`@param` 注释是可选的，但它们对于代码文档化和可读性是非常有帮助的。

## JS有哪些数据类型?它们的区别?

**最新的 ECMAScript 标准定义了 8 种数据类型（7 种基本数据类型、1 种引用数据类型）**

| 分类             | 数据类型                                                     |
| :--------------- | :----------------------------------------------------------- |
| 7 种基本数据类型 | string（字符串）、number（数字）、boolean（布尔）、undefined（未定义）、null（空）、Symbol（符号）、BigInt（数值类型，表示任意精度的整数） |
| 1 种引用数据类型 | Object 对象：Array（数组）、Function（函数）、Date（时间）等 |

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

1. 基本数据类型是按值访问的，而复杂数据类型（对象、数组和函数）是按引用访问的。
2. 储存位置不同，基本数据类型储存在栈内存中，复杂数据类型储存在堆内存中。
3. 基本数据类型的值不可变，如果改变一个基本数据类型的值，实际上是创建了一个新的值。而复杂数据类型是可以改变其属性和值。
4. 对于基本数据类型，可以使用typeof操作符来判断其类型，但对于对象类型，使用typeof操作符返回的是"object"。
5. 基本数据类型占用固定的内存大小，而对象类型的大小是动态的，由其属性和值的个数决定。
6. 在JavaScript中，所有数据类型都是一等公民，可以作为变量、函数的参数和返回值。

总的来说，基本数据类型是简单的、不可变的，而对象类型是复杂的、可变的，它们在不同的场景下具有不同的应用。

## 栈内存和堆内存

在 JavaScript 中，内存分为栈内存和堆内存两种。

栈内存是一种存储方式，它用来存储程序执行过程中创建的变量和临时数据。栈内存的特点是后进先出（LIFO，Last-In-First-Out），即最后存入栈中的数据最先被取出。栈内存中存储的数据大小固定，而且它的内存空间是连续的，因此存取速度比较快。

堆内存是一种动态分配的内存池，它用来存储复杂的数据类型，比如对象、数组、函数等。堆内存的特点是数据大小不固定，存储空间不连续，因此存取速度比较慢。堆内存中的数据需要通过引用（指针）来访问，即变量中存储的是一个地址，这个地址指向堆内存中的实际数据。

## 基本数据类型和引用数据类型的储存

在 JavaScript 中，基本数据类型的值存储在栈内存中，而引用数据类型的值（如对象、数组、函数等）存储在堆内存中，变量中存储的是对堆内存中实际数据的引用。

当我们创建一个基本数据类型的变量时，会为其分配足够的内存来存储该类型的值，并将该值直接存储在变量的存储空间中，这个存储空间在栈内存中。

当我们创建一个引用数据类型的变量时，会为其分配一个存储引用数据类型的地址的空间，在堆内存中分配实际的数据存储空间，并将实际的数据存储在这个空间中，然后将这个空间的地址（对象的引用（reference）存储在变量的存储空间中。因此，变量中存储的是指向堆内存中实际数据的引用，而不是实际数据本身。

需要注意的是，JavaScript 的垃圾回收机制会自动回收不再使用的内存空间，包括堆内存和栈内存。当一个变量不再被引用时，它占用的内存空间就可以被垃圾回收机制回收。

## 数据类型按照什么分类

在 JavaScript 中，数据类型可以分为原始类型和引用类型。

原始类型（Primitive data types）指的是存储简单数据值的数据类型，包括数字（Number）、字符串（String）、布尔值（Boolean）、null 和 undefined、Symbol（ES2015）、BigInt（ES2020）。这些数据类型都是按值访问的，即每个变量都包含它们自己的值，互不影响。

引用类型（Reference data types）指的是存储对象（Object）的数据类型，包括对象、数组（Array）、函数（Function）和日期（Date）等。这些数据类型都是按引用访问的，即每个变量存储的是对象在内存中的地址，多个变量可能引用同一个对象，修改一个变量的值也会影响到其他变量。

在 JavaScript 中，使用 typeof 操作符可以检测一个变量的数据类型。对于原始类型，typeof 返回对应的字符串（"number"、"string"、"boolean"、"null" 或 "undefined"）；对于引用类型，typeof 返回 "object"，无法具体区分出对象、数组、函数等不同的引用类型。

## JS 检测数据类型的 4 种方式

在 JavaScript 中，有多种方法可以检测数据类型，以下是四种最常用的方法：

1、typeof 操作符：检测基本数据类型，包括 number、string、boolean、undefined、symbol 和 function。但是，它无法检测复杂数据类型，如对象、数组、null、日期等。它可以这样使用：

```js
typeof 'hello'; // 返回 "string"
typeof 123; // 返回 "number"
typeof true; // 返回 "boolean"
typeof undefined; // 返回 "undefined"
typeof null; // 返回 "object"
typeof []; // 返回 "object"
typeof {}; // 返回 "object"
typeof function(){}; // 返回 "function"
```

2、instanceof 操作符：检测一个对象是否是某个构造函数的实例，它适用于复杂数据类型，如对象、数组等。它可以这样使用：

```js
const arr = [1, 2, 3];
arr instanceof Array; // 返回 true
arr instanceof Object; // 返回 true
```

3、Array.isArray() 方法：检测一个值是否为数组。它可以这样使用：

```js
Array.isArray([]); // 返回 true
Array.isArray({}); // 返回 false
```

4、Object.prototype.toString.call() 方法：检测所有数据类型，包括基本数据类型和复杂数据类型。它返回一个以 "[object 数据类型]" 的格式表示数据类型的字符串。它可以这样使用：

```js
Object.prototype.toString.call('hello'); // 返回 "[object String]"
Object.prototype.toString.call(123); // 返回 "[object Number]"
Object.prototype.toString.call(true); // 返回 "[object Boolean]"
Object.prototype.toString.call(undefined); // 返回 "[object Undefined]"
Object.prototype.toString.call(null); // 返回 "[object Null]"
Object.prototype.toString.call([]); // 返回 "[object Array]"
Object.prototype.toString.call({}); // 返回 "[object Object]"
Object.prototype.toString.call(function(){}); // 返回 "[object Function]"
```

这四种方法可以根据具体的使用场景选择使用，以检测不同类型的数据。

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
 "2" > "12"  // true
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

- `while`：每次迭代之前都要检查条件；
- `do..while`：每次迭代后都要检查条件；
- `for (... ; ... ; ... ; )`：每次迭代之前都要检查条件，可以使用其他设置。

在JavaScript中，有三种常见的循环结构：for循环、while循环和do-while循环。它们的主要区别在于它们的语法和执行方式。

1、for循环： for循环是最常用的循环结构之一，它有以下语法结构：

```js
for (初始化; 条件; 增量) {
  // 循环体代码
}
```

其中，初始化部分在循环开始前执行一次，条件部分在每次循环开始前被计算并判断，如果条件为true，则执行循环体代码，然后执行增量部分，然后再次计算条件，直到条件为false为止。

2、while循环： while循环的语法结构如下：

```js
while (条件) {
  // 循环体代码
}
```

while循环与for循环类似，不同之处在于，它没有初始化和增量部分。只有一个条件，如果条件为true，则执行循环体代码，然后再次计算条件，直到条件为false为止。

3、do-while循环： do-while循环的语法结构如下：

```j's
do {
  // 循环体代码
} while (条件);
```

do-while循环与while循环相似，但它的执行方式略有不同。do-while循环会首先执行一次循环体代码，然后再计算条件。如果条件为true，则继续执行循环，否则循环结束。

总的来说，for循环通常用于遍历数组和对象等数据结构，while循环通常用于在满足特定条件时执行一段代码，而do-while循环通常用于需要至少执行一次循环体代码的情况。

## 逻辑与&&和逻辑或||的本质(了解)

1、逻辑与：也叫作短路==与==

- 从左往右，依次计算
- 当计算第一个运算元,先隐式转换为Boolean值进行比较
  - true，继续下一个比较
  - false，直接返回该运算元的初始值

- 如果找到最后也没有找到,就返回最后一个运算元

2、逻辑或：也叫做短路==或==

- 从左往右,依次计算
- 当计算第一个运算元,先隐式转换为Boolean值进行比较
  - true，直接返回该运算元的初始值
  - false，继续下一个比较

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

引用是一个变量指向一个对象在内存中的地址，而不是指向一个对象本身。因此，如果多个变量引用同一个对象，它们实际上是引用同一个内存位置中的对象，对其中一个变量所做的修改会影响到其他变量。

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

在JavaScript中，引用是一种数据类型，用于存储指向内存中对象或函数的地址。它们通常用于传递或操作复杂数据类型，如对象和数组。JavaScript中的变量有两种类型：基本类型和引用类型。

## 基本类型和引用类型

基本类型包括数字、字符串、布尔值、null和undefined，它们是按值传递的。也就是说，当你将一个基本类型的值分配给变量时，实际上是将该值存储在变量所在的内存位置中。当你将一个基本类型的变量作为参数传递给函数时，实际上是将该值的副本传递给函数，因此在函数中对该值的修改不会影响原始值。

引用类型包括对象、数组、函数等复杂数据类型，它们是按引用传递的。也就是说，当你将一个引用类型的值分配给变量时，实际上是将一个指向对象或数组的引用存储在变量所在的内存位置中。当你将一个引用类型的变量作为参数传递给函数时，实际上是将该引用的副本传递给函数，因此在函数中对该引用所指向的对象或数组的修改会影响原始对象或数组。

# 📁 javaScript_函数

## JavaScript中的函数是什么？

在JavaScript中，函数是一种可调用的对象，它通常用于执行特定的任务或计算并返回值。函数可以接受任意数量的参数，这些参数可以是任何JavaScript数据类型，包括基本类型和引用类型。函数还可以访问其外部作用域中的变量和函数，并且可以返回任何类型的值，包括基本类型、引用类型和其他函数。

函数的定义可以通过函数声明或函数表达式来完成。函数声明是将函数定义作为一个语句来声明，而函数表达式是将函数定义作为一个表达式来声明。以下是两种方式定义一个函数的示例：

```javascript
// 函数声明
function sum(a, b) {
  return a + b;
}

// 函数表达式
let sum = function(a, b) {
  return a + b;
};
```

在JavaScript中，函数也是一种对象，因此可以像其他对象一样进行操作。函数可以作为参数传递给其他函数，也可以从其他函数中返回，因此函数在JavaScript中也被称为“一等公民”。

除了常规函数之外，JavaScript还支持匿名函数、箭头函数、生成器函数、异步函数等不同类型的函数。这些函数有着不同的语法和用途，可以根据需要选择不同类型的函数来解决问题。

## 函数有什么作用

1、封装可重复使用的代码块

函数可以将一段可重复使用的代码封装到一个函数中，这样可以在程序中多次调用该函数来执行该代码块。这样可以大大减少代码的冗余，并提高代码的可维护性和可重用性。

2、实现程序逻辑和算法

函数可以用于实现程序的逻辑和算法。通过将程序逻辑和算法封装到函数中，可以提高程序的可读性和可维护性，使程序更易于理解和修改。

3、处理事件

在Web开发中，函数通常用于处理用户界面的事件，例如点击按钮、提交表单等。当事件发生时，JavaScript将调用相应的函数来执行特定的任务，从而实现交互式Web应用程序。

4、实现模块化开发

函数可以作为模块来使用，将程序分解成小的、可组合的模块，从而实现模块化开发。模块化开发可以提高代码的可读性和可维护性，并减少程序中的依赖关系和耦合度。

5、处理异步任务

函数可以用于处理异步任务，例如通过回调函数来处理异步操作的结果。异步任务是一种常见的编程模式，例如通过AJAX从服务器加载数据、处理定时器等操作。通过将异步任务封装到函数中，可以将其作为单独的模块来处理，并避免代码混乱和出错。

## 总结局部变量和全局变量的使用

**局部变量**

在函数内部定义的变量，只能在函数内部访问。当函数被调用时，局部变量被创建，并在函数结束时被销毁。局部变量通常用于存储在函数中使用的临时值。局部变量的作用域仅限于函数内部，它们对于函数外部是不可见的。

**全局变量**

在程序的任何地方定义的变量，其作用域跨越整个程序。全局变量可以在程序的任何地方使用，包括函数内部和外部。全局变量通常用于存储在整个程序中需要访问的值，例如配置设置和计数器。

**变量的访问顺序**

在访问变量时，程序会首先搜索当前作用域中的变量。如果变量未在当前作用域中找到，则程序将继续向上搜索，直到找到变量或搜索到程序的最顶层作用域（通常是全局作用域）。因此，当函数中存在与全局变量同名的局部变量时，函数将使用局部变量，而不是全局变量。

这种搜索变量的方式称为变量作用域查找或作用域链。当函数中存在与全局变量同名的局部变量时，函数将使用局部变量，而不是全局变量。这是因为函数中的局部变量具有更高的作用域优先级，优先级比同名的全局变量更高。

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

**1、普通函数：**

即可以直接调用，执行其中的代码块，并返回结果。可以通过函数名直接调用，也可以作为参数传递给其他函数。

```js
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // 5

function printMessage(message) {
  console.log(message);
}

printMessage("Hello World!"); // Hello World!
```

**2、构造函数：**

用于创建新的对象实例，通常为大写字母开头，具有一些特殊的语法规则。必须使用 new 操作符来执行，同时需要用 this 关键字来指代新创建的实例。

构造函数一般会包含一些属性和方法，用来初始化实例对象和操作实例对象。

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.greet = function() {
    console.log("Hello, my name is " + this.name + " and I am " + this.age + " years old.");
  };
}

var person1 = new Person("Alice", 28);
var person2 = new Person("Bob", 32);

person1.greet(); // Hello, my name is Alice and I am 28 years old.
person2.greet(); // Hello, my name is Bob and I am 32 years old.
```

**3、静态方法（Static Methods）：**

（1）在类本身上定义的方法，可以直接通过类名来调用静态方法，而无需创建类的实例对象。与构造函数相关联。静态方法常常用于实现工具函数和工厂函数等场景。

```js
// 传统的构造函数方式
function MyClass(name) {
  this.name = name;
}

MyClass.staticMethod = function() {
  console.log("This is a static method");
};

MyClass.staticMethod(); // 输出："This is a static method"
```

（2）ES6：静态关键字`static`来定义静态方法。静态方法在类的定义中直接添加，而不是在原型对象上定义。

```js
// ES6 类的语法方式
class MyClass {
  constructor(name) {
    this.name = name;
  }

  static staticMethod() {
    console.log("This is a static method");
  }
}

MyClass.staticMethod(); // 输出："This is a static method"
```

**4、实例方法（Instance Methods）：**

类的实例对象相关联的方法。它们可以通过在构造函数内部使用 `this` 关键字定义的方法，使得每个实例对象都可以独立访问和调用这些方法。每个实例对象都有自己的实例方法副本。

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  
  this.greet = function() {
    console.log("Hello, my name is " + this.name + " and I am " + this.age + " years old.");
  };
}

var person1 = new Person("Alice", 28);
person1.greet(); // Hello, my name is Alice and I am 28 years old.
```

**5、公有方法（Public Methods）**

通过在构造函数的**原型对象**上定义的方法，可以避免为每个实例对象创建独立的方法副本，并且只有一份，不会重复创建。

从而节省内存和提高代码的效率。通过**原型链继承**的方式，被所有通过构造函数创建的实例对象所共享。

```js
function MyClass(name) {
  // 实例属性
  this.name = name;
}

MyClass.prototype.sayHello = function() {
  console.log("Hello, my name is " + this.name);
};

var obj1 = new MyClass("Alice");
var obj2 = new MyClass("Bob");

obj1.sayHello(); // 输出："Hello, my name is Alice"
obj2.sayHello(); // 输出："Hello, my name is Bob"
```

**6、私有方法（Private Methods）：**

私有方法：一种在类或构造函数内部定义的方法。

特点：对外部是不可见的，只能从构造函数内部访问的方法，外部无法直接访问并且无法从实例对象中直接访问。

作用：私有方法可以用来实现一些内部的逻辑或数据结构，以及隐藏一些敏感信息。

> 可以通过特权方法、原型方法或闭包等方式间接地访问和调用私有方法。

```js
function MyClass() {
  // 私有属性
  let name = "qiqing";
  // 私有方法
  var privateMethod = function() {
    console.log("This is a private method");
  };
	
  // 特权方法
  this.publicMethod = function() {
    console.log("This is a public method");
    privateMethod();
  };
}

var obj = new MyClass();
obj.publicMethod(); // 输出："This is a public method"
                    //       "This is a private method"
```

**7、特权方法（Privileged Methods）：**

> 在JavaScript中，由于函数级作用域的特性，我们可以在构造函数内部定义变量和方法，并且这些变量和方法在外部无法直接访问。
>
> 这些在**构造函数内部**定义的变量和方法被称为**私有变量**和**私有方法**。

特权方法：在构造函数内部定义的一种**特殊类型的实例方法，可以访问和操作私有变量和私有方法**。

如何实现**：**通过在构造函数内部返回一个具有访问私有成员权限的对象或函数来实现。

特点**：**可以在外部调用，但是只能通过构造函数创建的实例对象来访问，而无法直接访问私有成员。这样可以在保持私有成员的封装性的同时，通过特权方法提供一些公共接口来操作私有成员。

```js
function MyClass() {
  var privateVariable = "private";

  function privateMethod() {
    console.log("This is a private method");
  }

  this.publicMethod = function() {
    console.log("This is a privileged method");
    console.log("Accessing private variable:", privateVariable);
    privateMethod();
  };
}

var obj = new MyClass();
obj.publicMethod(); // 输出："This is a privileged method"
                    //       "Accessing private variable: private"
                    //       "This is a private method"
```

**8、闭包：**

指的是一个函数与其相关的引用环境组成的整体。闭包可以访问其创建时的作用域，并将其保存在内存中。通常用于实现私有变量、缓存等场景。

```js
function createCounter() {
  var count = 0;
  return function() {
    count++;
    console.log("Count: " + count);
  };
}

var counter1 = createCounter();
counter1(); // Count: 1
counter1(); // Count: 2

var counter2 = createCounter();
counter2(); // Count: 1
counter1(); // Count: 3
```

## 静态属性和私有属性

静态属性和私有属性是两种不同类型的属性，它们在作用范围、访问方式和用途上有所区别。

1、作用范围：

- 静态属性：静态属性属于类本身，不属于类的实例对象。它在类级别上存在，并且所有实例对象共享同一个静态属性的值。
- 私有属性：私有属性属于类的实例对象，每个实例对象都有自己独立的私有属性。

2、访问方式：

- 静态属性：静态属性可以通过类名直接访问，也可以通过类的实例对象访问。使用类名访问时，语法为 `类名.静态属性名`；使用实例对象访问时，语法为 `实例对象.静态属性名`。
- 私有属性：私有属性只能在类的内部访问，外部无法直接访问。通常使用闭包或命名约定等方式来模拟私有属性的特性。

3、用途：

- 静态属性：静态属性常用于存储类级别的数据或共享的状态。例如，记录实例对象的个数、保存全局配置信息等。
- 私有属性：私有属性用于存储实例对象的私有数据，只有类内部的方法可以访问和操作私有属性。私有属性有助于实现类的封装和数据隐藏，确保数据的安全性和内部实现的隐私性。

总结：静态属性属于类本身，在类级别上存在；私有属性属于实例对象，在每个实例对象上独立存在。静态属性可以通过类名或实例对象访问，而私有属性只能在类的内部访问。静态属性用于类级别的数据存储和共享状态，私有属性用于实例对象的私有数据存储和封装。

```js
var Car = (function() {
  // 静态属性 - 跟踪汽车数量
  var carCount = 0;

  // 构造函数
  function Car(make, model) {
    // 私有属性 - 汽车详细信息
    var carMake = make;
    var carModel = model;

    // 增加汽车数量
    carCount++;
  }

  // 静态方法 - 获取汽车数量
  Car.getCarCount = function() {
    return carCount;
  };

  // 公有方法 - 获取汽车详细信息
  Car.prototype.getCarDetails = function() {
    return carMake + " " + carModel;
  };

  return Car;
})();

// 创建两个汽车实例
var car1 = new Car("Toyota", "Camry");
var car2 = new Car("Honda", "Accord");

// 调用静态方法，获取汽车数量
console.log(Car.getCarCount()); // 输出: 2

// 尝试访问私有属性
console.log(car1.carMake); // 输出: undefined
console.log(car2.carModel); // 输出: undefined

// 调用公有方法，访问静态属性和私有属性，获取汽车详细信息
console.log(car1.getCarDetails()); // 输出: "Toyota Camry"
console.log(car2.getCarDetails()); // 输出: "Honda Accord"
```

## 面向对象

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



# 📁 javaScript_面向对象

## 检查空对象的方式有哪些？

在 JavaScript 中，可以使用以下几种方式来检查一个对象是否为空：

1、Object.keys()

使用 `Object.keys(obj)` 获取对象所有可枚举的属性名，然后检查属性名数量是否为 0：

```js
const obj = {};
if (Object.keys(obj).length === 0) {
  console.log("Object is empty");
}
```

2、for...in

使用 `for...in` 循环遍历对象的所有属性，如果找到任何一个属性则表明对象不为空：

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

使用 `JSON.stringify(obj)` 将对象序列化为字符串，然后检查字符串是否为 `{}`

```js
const obj = {};
if (JSON.stringify(obj) === '{}') {
  console.log("Object is empty");
}
```

注意，以上方法都假定对象是纯粹的 JavaScript 对象，而不是从原型链继承属性的对象。如果对象有继承的属性，需要考虑使用其他方法进行检查。

如果对象有继承属性，则这些方法也会返回 `false`，因为继承属性会被视为对象的属性。

4、Object.entries()

该方法返回一个由对象的可枚举属性键值对组成的数组。如果该数组长度为0，则对象为空。

```js
const obj = {};
if (Object.entries(obj).length === 0) {
  console.log("Object is empty");
}
```

5、Object.getOwnPropertyNames()

该方法返回一个由对象自身的属性键组成的数组。如果该数组长度为0，则对象为空，这个方法会检查对象自身的所有属性，包括可枚举属性、不可枚举属性和 Symbol 类型的属性，但不包括继承属性。。

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

## 如何检查一个对象是否存在继承属性？

要检查一个对象是否存在继承属性，可以使用 `Object.getPrototypeOf(obj)` 方法获取该对象的原型对象，然后判断原型对象是否为空。如果原型对象为空，说明该对象没有继承属性；如果原型对象不为空，则说明该对象存在继承属性。

下面是一个检查对象是否存在继承属性的示例代码：

```
function hasInheritedProperties(obj) {
  const proto = Object.getPrototypeOf(obj);
  if (proto === null) {
    return false; // 没有继承属性
  } else {
    const inheritedProps = Object.getOwnPropertyNames(proto);
    return inheritedProps.length > 0; // 存在继承属性
  }
}
```

这个函数会返回一个布尔值，表示对象是否存在继承属性。如果对象不存在继承属性，则返回 `false`；否则返回 `true`。

需要注意的是，这个方法只检查对象的原型链上的第一个原型对象是否为空，如果对象的原型链有多个原型对象，且其中某个原型对象不为空，则该对象仍然存在继承属性。如果需要检查对象的整个原型链上是否存在继承属性，可以使用递归的方式遍历整个原型链。

```js
function isEmptyObject(obj) {
  // 检查对象自身的属性
  if (Object.getOwnPropertyNames(obj).length > 0) {
    return false;
  }
  // 获取对象的原型
  let proto = Object.getPrototypeOf(obj);
  // 如果原型为 null，表明已经到达原型链的末端，返回 true
  if (proto === null) {
    return true;
  }
  // 递归检查原型链上的属性
  return isEmptyObject(proto);
}
```

这个方法会递归地检查对象的原型链上的所有对象的属性是否为空，包括可枚举属性、不可枚举属性和 Symbol 类型的属性。如果所有属性都为空，则返回 `true`，否则返回 `false`。需要注意的是，这个方法的时间复杂度为 $O(n)$，其中 $n$ 表示对象的原型链长度。如果对象的原型链非常长，这个方法可能会导致栈溢出或性能问题。

## Object.getOwnpropertyNames() 和 Object.keys() 的区别？

`Object.getOwnPropertyNames()` 方法返回一个数组，包含指定对象自身属性（不包括继承属性）的名称。这个方法返回的数组包括对象的所有属性，包括不可枚举属性和 Symbol 类型的属性。

`Object.keys()` 方法返回一个数组，包含指定对象自身可枚举属性的名称。这个方法只返回对象自身的可枚举属性名称，不包括不可枚举属性和 Symbol 类型的属性。

因此，两者的区别在于返回的属性集合不同。如果对象只有可枚举属性，那么两者返回的结果是相同的。但如果对象有不可枚举属性或 Symbol 类型的属性，那么 `Object.getOwnPropertyNames()` 返回的结果会更多，而 `Object.keys()` 返回的结果会更少。下面是一个示例：

```js
const user = {
  name: 'Alice',
  age: 25
};

Object.defineProperty(user, 'password', {
  value: '123456',
  enumerable: false
});

console.log(Object.getOwnPropertyNames(user)); // 输出 ["name", "age", "password"]
console.log(Object.keys(user)); // 输出 ["name", "age"]
```

在这个例子中，我们使用 `Object.defineProperty()` 方法为 `user` 对象添加了一个不可枚举属性 `password`。在调用 `Object.getOwnPropertyNames()` 和 `Object.keys()` 方法时，`password` 属性会对它们的返回结果产生影响，使得两者的结果不同。

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
- 但如果一个普通函数被 **new** 操作符调用了，那么这个函数就叫做**构造函数**；

**原理**

如果一个函数被 new 操作符调用了，那么它会执行如下操作：

1. 在内存中创建一个新对象；
2. 将这个新对象内部的 \[\[Prototype\]\] 属性赋值为构造函数的 prototype 属性；
3. 将构造函数内部的 this 赋值为这个新对象（即 this 指向新对象）；
4. 执行构造函数内部的代码（给新对象添加属性）；
5. 如果构造函数返回了非空对象，则返回该对象；否则，返回刚创建的新对象；

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

- for...in可以遍历对象和数组，for...of不能遍历普通对象，适用遍历数/数组对象/字符串/map/set等**拥有迭代器**对象的集合
- for...in 循环不仅遍历对象的键名，还会遍历手动添加的其它键，甚至包括原型链上的键
- for...in遍历的索引为字符串类型
- for...of与forEach()不同的是，它可以正确响应break、continue和return语句

## for...of与forEach()

`for...of` 和 `forEach()` 都是用来迭代数组的方法，但是它们之间有一些重要的区别。

1. 语法：`for...of` 是 ES6 新增的语法，而 `forEach()` 是数组原型对象的方法。

2. 可迭代对象：`for...of` 可以迭代任何可迭代对象，包括数组、字符串、Set、Map、生成器等；而 `forEach()` 只能迭代数组。

3. 中断迭代：`for...of` 可以使用 `break` 和 `continue` 语句中断迭代；而 `forEach()` 不支持中断迭代。

4. 返回值：`for...of` 没有返回值；而 `forEach()` 返回值为 `undefined`。

5. 遍历顺序：`for...of` 会按照元素插入的顺序遍历数组；而 `forEach()` 则是按照元素的索引顺序遍历数组。

6. 对原数组的影响：`for...of` 不会修改原数组；而 `forEach()` 可以修改原数组。

## 可迭代对象和可枚举对象的区别

可迭代对象和可枚举对象是 JavaScript 中两个不同的概念。

**可迭代对象**

可迭代对象是指实现了 `Symbol.iterator` 方法的对象，该方法返回一个迭代器对象。迭代器对象包含一个 `next()` 方法，用于返回序列中的下一个值和一个布尔值，指示序列是否已经到达结尾。迭代器对象可以通过 `for...of` 循环来遍历序列中的值。

常见的可迭代对象包括`数组`、`字符串`、`Set`、`Map` 等。例如，下面的代码使用 `for...of` 循环遍历一个数组：

```js
let arr = [1, 2, 3];
for (let num of arr) {
  console.log(num);
}
```

**可枚举对象**

可枚举对象是指可以通过 `for...in` 循环遍历其属性的对象。在 JavaScript 中，所有对象都有原型链，因此它们可能会继承其他对象的属性。默认情况下，继承的属性是不可枚举的，而对象自身的属性通常是可枚举的。

可以通过 `Object.defineProperty()` 方法来设置属性的可枚举性，如下所示：

```js
let obj = {};
Object.defineProperty(
  obj, 
  "a",
  { 
    value: 1, enumerable: true
  });
Object.defineProperty(obj, "b", { value: 2, enumerable: false });

for (let key in obj) {
  console.log(key + ": " + obj[key]);
}
// 输出：a: 1
```

在这个例子中，我们创建了一个对象 obj，并定义了两个属性 a 和 b。其中，属性 a 的可枚举性设置为 true，属性 b 的可枚举性设置为 false。然后，我们使用 for...in 循环遍历对象 obj 的属性，只有属性 a 被输出到控制台上。

需要注意的是，`Object.keys()` 方法可以返回对象自身的所有可枚举属性的名称组成的数组，而 `Object.getOwnPropertyNames()` 方法可以返回对象自身的所有属性的名称组成的数组。

## 对象方法简写的区别

在 JavaScript 中，对象方法的定义方式可以分为两种：方法简写和普通函数。

方法简写是 ES6 引入的新语法，可以更简洁地定义对象方法。使用方法简写时，可以省略冒号和 function 关键字。例如：

```js
const obj = {
  foo() {
    console.log('foo');
  }
};
```

普通函数定义对象方法时，需要在对象上使用属性赋值语法，将函数作为属性值。例如：

```js
const obj = {
  foo: function() {
    console.log('foo');
  }
};
```

这两种方式定义的对象方法，在功能上没有本质区别。它们都是对象的属性，可以被调用。

但是，在一些细节方面，方法简写和普通函数定义有一些区别：

1. 方法简写语法更简洁。相比较于普通函数，方法简写语法可以更简洁地定义对象方法。

2. 方法简写语法更易读。使用方法简写语法可以更清晰地表达出对象的结构和属性。

3. 方法简写语法中的 `this` 指向问题。在方法简写语法中，方法内部的 `this` 关键字会指向该对象本身。而在普通函数中，`this` 关键字的指向则需要根据函数的调用方式来确定。

4. 简写的对象方法**不能用作构造函数**，会报错。

总之，在定义对象方法时，方法简写语法和普通函数都可以使用，具体选择哪一种方式，取决于开发者的个人习惯和项目需求。

## 可选连`?.`的使用

可选链 `?.` 语法有三种形式：

1、`obj?.prop` —— 如果 obj 存在则返回 obj.prop，否则返回 undefined。

2、`obj?.[prop]` —— 如果 obj 存在则返回 obj\[prop\]，否则返回 undefined。

3、`obj.method?.()` —— 如果 obj.method 存在则调用 obj.method()，否则返回 undefined。

正如我们所看到的，这些语法形式用起来都很简单直接。?. 检查左边部分是否为 null/undefined，如果不是则继续运算。

`?.`链使我们能够安全地访问嵌套属性。

> 但是，我们应该谨慎地使用 `?.`，根据我们的代码逻辑，仅在当左侧部分不存在也可接受的情况下使用为宜。以保证在代码中有编程上的错误出现时，也不会对我们隐藏。

## 访问对象的两种方式区别

在JavaScript中，我们可以使用两种方式来访问对象的属性和方法：点表示法和方括号表示法。

**1、点表示法（Dot Notation）：**

使用点表示法，我们使用对象名后面跟一个点（.），然后紧跟属性或方法的名称来访问对象的属性和方法。例如：`objectName.propertyName` 或者 `objectName.methodName()`

```javascript
var person = {
  name: 'John',
  age: 30,
  sayHello: function() {
    console.log('Hello!');
  }
};

console.log(person.name); // 输出：John
person.sayHello(); // 输出：Hello!
```

点表示法适用于属性名是合法的标识符（由字母、数字、下划线和美元符号组成，不能以数字开头）的情况。

**2、方括号表示法（Bracket Notation）：**

使用方括号表示法，我们使用对象名后面跟着方括号`[]`，在方括号中放入属性或方法的名称作为字符串来访问对象的属性和方法。

例如：`objectName['propertyName']` 或者 `objectName['methodName']()`

```javascript
var person = {
  name: 'John',
  age: 30,
  sayHello: function() {
    console.log('Hello!');
  }
};

console.log(person['name']); // 输出：John
person['sayHello'](); // 输出：Hello!
```

方括号表示法适用于属性名包含特殊字符、包含空格或者是通过变量来访问属性的情况。

**区别如下：**

- 语法形式：点表示法使用点来分隔对象和属性名，方括号表示法使用方括号来包裹属性名。
- 属性名类型：点表示法要求属性名是一个合法的标识符，即符合命名规则的变量名。方括号表示法可以接受任意字符串作为属性名，包括包含特殊字符的字符串。
- 动态属性访问：方括号表示法允许使用变量或表达式作为属性名，而点表示法只能使用静态的属性名。
- 使用场景：点表示法在属性名是确定的情况下更简洁，适合直接访问已知属性。方括号表示法更灵活，适合动态获取属性名或处理包含特殊字符的属性名。

## toString 和 valueOf方法

`toString()` 和 `valueOf()` 是 JavaScript 中两个常用的内置方法，它们都可以用于返回一个对象的字符串或基本类型值表示。但是，它们在使用和返回值方面有一些区别，并且都可以被重写。

**两者区别**

1、使用

`toString()` 方法用于将一个对象转换成一个字符串，而 `valueOf()` 方法用于将一个对象转换成一个基本类型值。

2、作用和返回值

（1）toString 方法

将对象转换为字符串，返回一个字符串类型的值。如果我们没有重写 toString 方法，它会返回一个 "\[object Object\]" 的字符串，表示该对象的类型。但是，我们可以重写 toString 方法，以自定义对象的字符串表示形式。

（2）valueOf 方法

返回对象的原始值，通常是一个数值、字符串或布尔值，通常用于将对象转换为原始值，以进行算术运算或其他类型的操作。

如果我们没有重写 valueOf 方法，它会返回对象本身。但是，我们可以重写 valueOf 方法，以改变对象的原始值。

例如，对于一个自定义对象，可以重写 `toString()` 方法和 `valueOf()` 方法，来分别返回该对象的字符串表示形式和基本类型值表示：

```js
const person = {
  name: 'John',
  age: 30,
  toString() {
    return `Name: ${this.name}, Age: ${this.age}`;
  },
  valueOf() {
    return this.age;
  }
};

console.log(person.toString()); // "Name: John, Age: 30"
console.log(person.valueOf()); // 30
```

在上面的示例中，`toString()` 方法返回一个字符串，表示该对象的字符串表示形式。`valueOf()` 方法返回一个数字，表示该对象的基本类型值表示。

## JS对象考题

JS对象注意点：

1. 对象是通过new操作符构建出来的，所以对象之间不相等(除了引用外)；
2. 对象注意：引用类型**（共同一个地址）**；
3. 对象的key都是字符串类型；
4. 对象如何找属性|方法；

查找规则：

先在对象本身找 ——> 构造函数中找 ——> 对象原型中找 ——> 构造函数原型中找 ——> 对象上一层原型查找

考题一：

```js
[1,2,3] === [1,2,3]   //false
```

考题二：

```js
var obj1 = {
  a: "hellow",
};
var obj2 = obj1;
obj2.a = "world";

console.log(obj1); //{a:world}

(function () {
  console.log(a); //undefined
  var a = 1;
})();

/* 由于 JavaScript 中存在变量提升（hoisting）的机 		制，所以实际执行的顺序是
 	 1. 声明变量 `a`，
 	 2. 执行 `console.log(a)` 
 	 3.  `a = 1`
*/
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

第一行代码定义了一个空对象 `a`。

第二行代码定义了一个对象 `b`，包含一个名为 `key`，值为 `'a'` 的属性。

第四行代码定义了一个对象 `c`，包含一个名为 `key`，值为 `'c'` 的属性。

第六、七行代码分别将对象 `a` 的属性 `b` 和 `c` 分别赋值为 `'123'` 和 `'456'`。需要注意的是，对象属性名在赋值时会自动转换为字符串类型，因此 `b` 和 `c` 在赋值时会被转换为字符串 `"[object Object]"`。

第九行代码打印了 `a[b]` 的值。由于 `b` 和 `c` 在赋值时都被转换为字符串 `"[object Object]"`，因此这两次赋值实际上是给对象 `a` 的同一个属性赋值，即 `a["[object Object]"]`。由于后一次赋值为 `'456'`，因此最后打印 `a[b]` 的值为 `'456'`。
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

- `Number.MAX_SAFE_INTEGER`      最大安全整数
- `Number.MIN_SAFE_INTEGER`       最小安全整数

**实例方法**

- `toString(base)`，将数字转成字符串，并且按照base进制进行转化
- `toFixed(digits)`，格式化一个数字，保留digits位的小数,会四舍五入

**类方法**

- `Number.parseInt(string[, radix])`，将字符串解析成整数，也有对应的全局方法parseInt；
- `Number.parseFloat(string)`，将字符串解析成浮点数，也有对应的全局方法parseFloat；

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

- `Math.floor`：向下舍入取整
- `Math.ceil`：向上舍入取整
- `Math.round`：四舍五入取整
- `Math.random`：生成0~1的随机数（包含0，不包含1）
- `Math.pow(x, y)`：返回x的y次幂

**公式: \[a,b)的随机数**

- `y=a,x=b-a, Math.floor(Math.random() \* x) + y`

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

10、判断字符串开头结尾

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

11、数组 => 字符串

`join()` 是 JavaScript 中数组对象的方法，它将数组的所有元素以指定的分隔符连接成一个字符串，并返回该字符串。

```js
const fruits = ["apple", "banana", "orange"];
const joinedFruits = fruits.join(", "); // 使用", "作为分隔符
console.log(joinedFruits); // "apple, banana, orange"
```

12、普通for循环遍历

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

13、`for...of...`循环

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

14、字符串不可变性

在 JavaScript 中字符串是不可变的，即一旦创建就不能修改。因此，任何修改字符串的操作都会返回一个新的字符串。例如，使用 replace() 方法替换字符串中的某个字符时，实际上是返回了一个新的字符串，而原始字符串并没有发生变化。

```js
const str = "Hello, World!";
const newStr = str.replace("World", "JavaScript");
console.log(str); // "Hello, World!"
console.log(newStr); // "Hello, JavaScript!"
```

15、创建方式 new String()

在 JavaScript 中，可以使用 new String() 构造函数来创建一个字符串对象。这种方式创建的字符串是一个对象，而不是基本数据类型的字符串。

一般来说，在 JavaScript 中创建字符串时，推荐使用基本字符串类型，而不是字符串对象。

```js
const strObj = new String("hello");
console.log(strObj); // 输出：[String: 'hello']
console.log(typeof strObj); // 输出：object
```

## 实例方法和类方法

在面向对象编程中，实例方法和类方法是两种不同的方法类型。

实例方法是在类实例上调用的方法，可以访问实例属性和实例方法。它们是通过在类的原型对象上定义方法来创建的，因此每个类实例都可以共享这些方法。实例方法通常用于处理实例特定的操作和数据。

示例代码：

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayHello() {
    console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
  }
}

const john = new Person("John", 25);
john.sayHello(); // Output: "Hello, my name is John and I'm 25 years old."
```

类方法是在类本身上调用的方法，而不是在类实例上调用的方法。它们通常用于处理与类实例无关的操作和数据。类方法在类本身上定义，而不是在原型对象上定义，因此不需要实例化类就可以访问这些方法。

示例代码：

```javascript
class MathUtils {
  static sum(a, b) {
    return a + b;
  }

  static square(num) {
    return num * num;
  }
}

console.log(MathUtils.sum(2, 3)); // Output: 5
console.log(MathUtils.square(4)); // Output: 16
```

注意到这里的方法是用 static 关键字定义的。类方法只能在类本身上调用，而不能在类实例上调用。在类方法内部，this 关键字指向类本身，而不是类实例。

## JS判断变量是不是数组，你能写出哪些方法？

1、使用`Array.isArray()`类方法：

ES6中新增了Array.isArray()方法，该方法返回一个布尔值，如果变量是数组，则返回true，否则返回false。

```js
const arr = [1, 2, 3];
if (Array.isArray(arr)) {
  console.log("arr is an array");
} else {
  console.log("arr is not an array");
}
```

2、使用 `instanceof` 操作符，该运算符检查变量是否是某个类的实例，因此可以用来判断变量是否是数组：

```js
const arr = [1, 2, 3];
if (arr instanceof Array) {
  console.log("arr is an array");
} else {
  console.log("arr is not an array");
}
```

3、使用 `Object.prototype.toString.call()` 方法，该方法返回一个表示变量类型的字符串，例如"[object Array]"表示数组类型：

```js
const arr = [1, 2, 3];
if (Object.prototype.toString.call(arr) === '[object Array]') {
  console.log("arr is an array");
} else {
  console.log("arr is not an array");
}
```

Object.prototype.toString.call() 方法第三种方式是最常用的，因为它可以用来检测所有类型的对象，而不仅仅是数组。

4、`isPrototypeOf()` 方法

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

- 通过`[index]`
- `arr.at(i)`
- i >= 0，`arr.at(i)`与`arr[i]` 完全相同；对于i为负数的情况，`arr.at(i)`则从数组的尾部向前数

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

- 在数组的尾端添加或删除元素，栈方法: push 在末端添加元素，pop 从末端取出一个元素
- 在数组的首端添加或删除元素，队列方法: shift 取出队列首端的一个元素，整个数组元素向前前移动; unshift 在首端添加元素，整个其他数组元素向后移动
- 添加,删除和替换元素:`arr.splice((start, deleteCount, item1, item2, itemN))`
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

- 数组的长度：`arr.length`
- 数组的遍历：`for`、`for..in`、 `for..of`

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

- `arr.slice(begin, end)` 方法：用于对数组进行截取
  - 包含begin元素，但是不包含end元素
  - slice不会修改原数组 splice 修改原数组

- `arr.concat`方法：创建一个新数组，其中包含来自于其他数组和其他项的值
- `arr.join`：将一个数组的所有元素连接成一个字符串并返回这个字符串

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

- `arr.indexOf(item, from)` —— 从索引 from 开始搜索 item，如果找到则返回索引，否则返回 -1。
- `arr.includes(item, from)` —— 从索引 from 开始搜索 item，如果找到则返回 true（译注：如果没找到，则返回 false）。
- `arr.find()`——返回提供的数组中满足提供的函数的第一个元素
- `arr.findIndex()`——返回提供的数组中满足提供的函数的第一个元素的索引

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

- `arr.sort()`方法：用于对数组进行排序, 直接改变原数组
- `arr.reverse()`方法：将数组中元素的位置颠倒，并返回该数组

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

- `arr.forEach()`：遍历数组，并且让数组中每一个元素都执行一次对应的方法
  - `forEach(func)` —— 对每个元素都调用 func，不返回任何内容。

- `arr.filter()`：过滤出满足函数条件的元素创建一个新数组
- `arr.map()`：返回由原数组中的每个元素都调用一次提供的函数后的返回值组成的新数组
- `arr.reduce()`：用于计算数组中所有元素的总和

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

`Array.from()` 方法是 ES6 中新增的方法，用于将类数组对象或可迭代对象转换成一个真正的数组。该方法接受两个参数：第一个参数是需要转换的对象，第二个参数是一个可选的 map 函数，用于对转换后的数组中的每个元素进行操作。

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

可以看到，`Array.from()` 方法非常方便地将各种类型的对象转换成了数组，这在处理数据时非常有用。

## sort背后原理是什么？

在 JavaScript 中，`sort()` 方法用于对数组进行排序。`sort()` 方法会修改原数组，并返回排序后的数组。`sort()` 方法使用的排序算法是快速排序（Quick Sort）。

快速排序是一种分治的排序算法，它的基本思想是选择一个基准元素，将数组分成两部分，一部分小于基准元素，一部分大于基准元素，然后对这两部分递归地进行排序。在实际应用中，快速排序通常是最快的排序算法之一。

`sort()` 方法的排序流程如下：

1. 首先选择一个基准元素（pivot），通常是数组的第一个元素或最后一个元素。
2. 然后将数组中小于基准元素的元素放在基准元素的左边，大于基准元素的元素放在基准元素的右边。这个过程称为分区（Partition）。
3. 接着递归地对左边的子数组和右边的子数组进行排序，直到整个数组都被排序。

在实际应用中，快速排序还需要考虑以下几点：

1. 对于小数组，快速排序的性能可能不如插入排序（Insertion Sort）。
2. 在分区时，为了避免最坏情况的出现（即分区后左边或右边的子数组长度为 0），可以采用随机选择基准元素或三数取中的方法来选择基准元素。
3. 对于具有相同元素的数组，为了避免快速排序出现退化情况（即分区不平衡），可以采用三路快速排序（Quick Sort 3-Way）。

> 总之，sort() 方法背后的原理是快速排序，它是一种高效的排序算法，并且在实际应用中有多种优化方式。

## find和filter的区别

在JavaScript中，`find()`和`filter()`都是用来筛选数组的方法

**主要区别如下：**

`find()`只会遍历数组中符合条件的元素，找到之后就会停止遍历，返回第一个符合条件的元素；

`filter()`会遍历整个数组，不管是否符合条件，都会进行处理。返回所有符合条件的元素组成的新数组。

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

## JS中的Array.splice()和Array.slice()方法有什么区别

`Array.splice()`和`Array.slice()`是 JavaScript 中常用的数组操作方法，它们的作用不同，具体区别如下：

1、Array.splice()

`Array.splice()`方法用于向数组中插入或删除元素。它可以==对原数组进行修改==，返回被删除的元素组成的数组。`Array.splice()`方法接受 2 个或 3 个参数：

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

2、Array.slice()

`Array.slice()`方法==返回一个新的数组==，其中包含原数组的一部分。它不会修改原数组，而是返回一个新的数组。`Array.slice()`方法接受 2 个参数：

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

`forEach()` 和 `map()` 两个方法都是ECMA5中Array引进的新方法，都是用来遍历数组中的每⼀项。

它们的主要区别是forEach是用来迭代数组中的每个元素，而map是用来对数组中的每个元素进行处理并返回新的数组。

**主要区别**

1、返回值不同

- `forEach`方法没有返回值或者说返回值为`undefined`，它的主要作用是迭代数组元素，而不是创建新的数组。
- `map`方法返回一个新的数组，数组的每个元素是对原数组的每个元素调用回调函数后的返回值。

2、使用方式不同

- `forEach`方法的回调函数有三个参数：当前元素、当前元素的索引和当前数组。这个回调函数可以改变当前元素的值，但是无法创建新的数组。
- `map`方法的回调函数有三个参数：当前元素、当前元素的索引和当前数组。这个回调函数可以创建新的数组，而且map方法会将每个回调函数的返回值组成一个新的数组。

3、用途不同

- `forEach`方法通常用于遍历数组并对每个元素执行一些操作，例如更新DOM元素等。
- `map`方法通常用于将一个数组转换为另一个数组，例如将一个数字数组的每个元素都乘以2，并返回一个新的数组。

总之，如果你需要遍历一个数组并对每个元素执行一些操作，使用forEach；如果你需要将一个数组转换为另一个数组并且每个元素都经过一些处理，使用map。

**其他区别：**

- `map`速度比`forEach`快
- `map`会返回⼀个新数组，不对原数组产生影响；`foreach`不会产生新数组，`forEach`返回`undefined`
- `map`因为返回数组所以可以链式操作，`forEach`不能
- `map`里可以用`return`（return的是什么，相当于把数组中的这⼀项变为什么（并不影响原来的数组，只是相当于把原数组克隆⼀份，把克隆的这⼀份的数组中的对应项改变了） 。
- `forEach`里用`return`不起作用，`forEach`不能用break，会直接报错。

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

1、使用`flat()`方法

ES6提供了数组的`flat()`方法，可以将多维数组扁平化为一维数组。`flat()`方法可以传入一个参数，用于指定扁平化的深度，默认为1。如果想要完全扁平化数组，可以传入`Infinity`作为参数。

示例代码：

```js
const arr1 = [1, 2, [3, 4]];
arr1.flat();
// [1, 2, 3, 4]

const arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

const arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

const arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

2、使用`reduce()`方法

使用`reduce()`方法，遍历数组的每个元素，如果元素是数组，则递归处理并将结果合并，否则将元素加入结果数组。例如：

示例代码：

```js
function flatten(arr) {
  return arr.reduce((result, item) => {
    if (Array.isArray(item)) {
      return result.concat(flatten(item));
    } else {
      return result.concat(item);
    }
  }, []);
}

const arr = [[1, 2], [3, [4, 5]]];
const flatArr = flatten(arr);

console.log(flatArr); // [1, 2, 3, 4, 5]
```

3、使用递归

使用递归方式，遍历数组的每个元素，如果元素是数组，则递归处理，否则将元素加入结果数组。例如：

示例代码：

```js
function flatten(arr) {
  const result = [];

  for (let i = 0; i < arr.length; i++) {
    if (Array.isArray(arr[i])) {
      result.push(...flatten(arr[i]));
    } else {
      result.push(arr[i]);
    }
  }

  return result;
}

const arr = [[1, 2], [3, [4, 5]]];
const flatArr = flatten(arr);

console.log(flatArr); // [1, 2, 3, 4, 5]
```

4、使用数组的`concat`方法

```js
let arr = [1,2,[3,4]]
let result = []
result = Array.prototype.concat.apply([], arr)
```

- `Array.prototype.concat` 是一个方法，表示调用 Array 对象原型上的 concat 方法，将多个数组或值合并为一个新数组，并返回该新数组。如果方法的参数是数组，则会将数组中的每个元素加入到新数组中。如果参数不是数组，则会将参数作为单独的元素加入到新数组中。
- `apply` 是一个方法，表示在指定的上下文中调用一个函数，并将一个数组作为参数传递给该函数。
- `[]` 表示一个空数组，表示将 `Array.prototype.concat` 方法中的 this 值设置为空数组，即将要合并的数组加入到一个空数组中。
- `arr` 表示要合并的数组，即将要将多维数组扁平化为一维数组。

因此，这段代码可以将嵌套数组 `arr` 扁平化为一维数组 `result`。

5、方法 4 简写为：使用数组的`concat`方法和`...`扩展运算符，只能将一层嵌套的数组扁平化，对于多层嵌套的数组，需要使用递归方式或其他方法来处理

```js
const arr = [1, 2, [3, 4, [5, 6]]];
const flatArr = [].concat(...arr);

console.log(flatArr); // [1, 2, 3, 4, 5, 6]
```

6、`Array.some`

利用`Array.some`方法判断数组中是否还存在数组，es6展开运算符连接数组

```js
let arr = [1,2,[3,4]]
while (arr.some(item => Array.isArray(item))) {
arr = [].concat(...arr);
}
```

## 数组去重，能用几种方法实现？

数组去重是指将数组中重复的元素去掉，只保留其中的一个。在 JavaScript 中，可以使用多种方法实现数组去重。

1、使用 Set 数据结构

Set 是 ES6 中引入的一种新的数据结构，它的特点是：类似于数组、不允许出现重复元素。可以利用这个特性，将数组转换为 Set，再将 Set 转换回数组，这样就能去除数组中的重复元素了。

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
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
//[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {}, {}]
```

2、使用 `filter()` 方法

可以使用数组的 `filter()` 方法，利用 `indexOf()` 方法判断元素是否重复来实现数组去重。

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
  return arr.filter(function (item, index, arr) {
    //当前元素，在原始数组中的第⼀个索引==当前索引值，否则返回当前元素
    return arr.indexOf(item, 0) === index;
  });
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr));
//[1, "true", true, 15, false, undefined, null, "NaN", 0, "a", {…}, {…}]

```

3、使用 reduce() 方法

可以使用数组的 `reduce()` 方法，利用 `includes()` 方法判断元素是否重复来实现数组去重。

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

Map 是一种 `key-value` 对应的数据结构，可以用来存储数组中的元素及其出现的次数，从而实现数组去重。

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

5、利用for嵌套for，然后splice去重（ES5中最常用）

```js
function unique(arr) {
  for (var i = 0; i < arr.length; i++) {
    for (var j = i + 1; j < arr.length; j++) {
      if (arr[i] == arr[j]) {
        //第⼀个等同于第⼆个，splice方法删除第⼆
        个;
        arr.splice(j, 1);
        j--;
      }
    }
  }
  return arr;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr));
//[1, "true", 15, false, undefined, NaN, NaN, "NaN", "a", {…}, {…}] //NaN和{}没有去重两个null直接消失了;
```

6、利用`indexOf`去重

这种方法使用 `indexOf` 方法查找元素在数组中第一次出现的位置，如果该位置不等于当前索引，则说明该元素已经重复出现过，需要删除。时间复杂度为 O(n^2)。

```js
function unique(arr) {
  if (!Array.isArray(arr)) {
    console.log("type error!");
    return;
  }
  var array = [];
  for (var i = 0; i < arr.length; i++) {
    if (array.indexOf(arr[i]) === -1) {
      array.push(arr[i]);
    }
  }
  return array;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr));
// [1, "true", true, 15, false, undefined, null, NaN, NaN, "NaN", 0, "a", {…},  {…}] //NaN、{}没有去重

```

7、利用 `sort()` 去重

先将数组排序，然后遍历数组，通过比较相邻元素的值来判断是否重复。这种方法时间复杂度为 O(nlogn)，但需要注意排序会改变原数组的顺序。

```js
function unique(arr) {
  if (!Array.isArray(arr)) {
    console.log("type error!");
    return;
  }
  arr = arr.sort();
  var arrry = [arr[0]];
  for (var i = 1; i < arr.length; i++) {
    if (arr[i] !== arr[i - 1]) {
      arrry.push(arr[i]);
    }
  }
  return arrry;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
// [0, 1, 15, "NaN", NaN, NaN, {…}, {…}, "a", false, null, true, "true",  undefined] // NaN、{}没有去重

```

8、`includes`

```js
function unique(arr) {
  if (!Array.isArray(arr)) {
    console.log("type error!");
    return;
  }
  var array = [];
  for (var i = 0; i < arr.length; i++) {
    if (!array.includes(arr[i])) {
      //includes 检测数组是否有某个值
      array.push(arr[i]);
    }
  }
  return array;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr));
//[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {…}, {…}]
// {} 没有去重

```

9、利用递归去重

```js
function unique(arr) {
  return arr.reduce(
    (prev, cur) => (prev.includes(cur) ? prev : [...prev, cur]),
    []
  );
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined,null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
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

> 代码中的`fnArr()`函数使用了`forEach()`方法遍历二维数组中的每一个子数组，然后调用`Math.max()`方法找出子数组中的最大值，并将其放入一个新数组中。最后返回这个新数组。
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

![dom-class-hierarchy](E:\coder\09_OneNote\image\dom-class-hierarchy.svg)

在DOM中，Element和Node都是对象，但它们代表不同的东西。

Element 继承于 Node，具有 Node 的方法，同时又拓展了很多自己的特有方法。

Node是DOM中所有节点类型的基类，包括元素节点、文本节点、注释节点等。Node对象具有许多常用属性和方法，例如nodeValue，nodeName，parentNode等。但是，Node对象不具有访问元素节点特定属性和方法的能力。

Element对象是表示文档中元素的节点类型，是Node的子类。Element对象继承了Node的所有属性和方法，并添加了许多专门用于元素节点的属性和方法，例如getAttribute，setAttribute，tagName等。因此，Element对象可以访问和修改元素节点的属性和内容。

在DOM中，元素节点是文档的主要组成部分，它包含了HTML或XML文档中的所有标记内容。因此，Element对象通常是DOM中最常用的对象之一。

综上所述，Node是DOM中所有节点类型的基类，而Element是表示文档中元素节点的节点类型，它们都具有许多属性和方法，但Element对象还可以访问和修改元素节点的特定属性和内容。

## 整理节点、元素的导航有哪些？

1、节点之间的导航:

- 父节点：`parentNode`
- 前兄弟节点：`previousSibling`
- 后兄弟节点：`nextSibling`
- 所有子节点：`childNodes`
- 第一个子节点：`firstChild`
- 最后一个子节点：`lastChild`

![dom-links](E:\coder\09_OneNote\image\dom-links.svg)

2、元素之间的导航:

- 父元素：`parentElement`
- 前兄弟元素：`previousElementSibling`
- 后兄弟元素：`nextElementSibling`
- 所有子元素：`children`
- 第一个子元素：`firstElementChild`
- 最后一个子元素：`lastElementChild`

![dom-links-elements](E:\coder\09_OneNote\image\dom-links-elements.svg)

## 节点（Node）常见的属性

节点（Node）是DOM树中的基本单元，具有以下常见的属性：

- nodeName：节点名称，对于元素节点，其值为标签名（大写），对于属性节点，其值为属性名称，对于文本节点，其值为#text，对于注释节点，其值为#comment等。
- nodeValue：节点的值，对于元素节点、属性节点和注释节点，其值为null，对于文本节点，其值为节点所包含的文本。
- nodeType：节点类型，具体值为一个整数，可以使用常量值来表示不同类型的节点，例如1表示元素节点，2表示属性节点，3表示文本节点，8表示注释节点等。
- parentNode：父节点，返回当前节点的父节点。
- childNodes：子节点列表，返回一个类数组对象，包含当前节点的所有子节点。
- firstChild：第一个子节点，返回当前节点的第一个子节点，如果没有子节点，则返回null。
- lastChild：最后一个子节点，返回当前节点的最后一个子节点，如果没有子节点，则返回null。
- previousSibling：前一个兄弟节点，返回当前节点的前一个兄弟节点，如果没有前一个兄弟节点，则返回null。
- nextSibling：后一个兄弟节点，返回当前节点的后一个兄弟节点，如果没有后一个兄弟节点，则返回null。
- ownerDocument：文档节点，返回表示整个文档的文档节点。
- attributes：属性节点列表，返回一个类数组对象，包含当前节点的所有属性节点。

这些属性可以帮助我们操作DOM树中的节点，并获取它们的相关信息。

## 元素常见的属性

元素（Element）是DOM树中的一种节点类型，除了节点（Node）的属性外，它还具有以下常见的属性：

- tagName：标签名，返回当前元素的标签名，以小写形式表示。
- id：元素的id，返回当前元素的id属性值。
- className：元素的class，返回当前元素的class属性值。
- innerHTML：元素的HTML内容，返回当前元素包含的所有子元素和文本内容的HTML表示形式。可以用来读取或设置元素的HTML内容。
- style：元素的样式，返回一个CSSStyleDeclaration对象，包含所有应用于元素的样式属性。
- attributes：元素的属性列表，返回NamedNodeMap对象，包含所有应用于元素的属性节点。
- childElementCount：子元素的数量，返回当前元素的子元素数量，不包括文本节点和注释节点。
- children：子元素列表，返回HTMLCollection对象，包含当前元素的所有子元素，不包括文本节点和注释节点。
- firstElementChild：第一个子元素，返回当前元素的第一个子元素，如果没有子元素，则返回null。
- lastElementChild：最后一个子元素，返回当前元素的最后一个子元素，如果没有子元素，则返回null。
- previousElementSibling：前一个兄弟元素，返回当前元素的前一个兄弟元素，如果没有前一个兄弟元素，则返回null。
- nextElementSibling：后一个兄弟元素，返回当前元素的后一个兄弟元素，如果没有后一个兄弟元素，则返回null。

这些属性可以帮助我们获取和操作元素的各种信息，包括元素的标签名、样式、子元素、属性等。

## 说说attribute和Property的区别和关系

在JavaScript中，attribute（属性）和property（属性）是两个概念。

attribute是元素在HTML中定义的属性，例如class、id、title等。在HTML中，属性可以写在元素的标签上，例如`<div id="myDiv"></div>`，此时id就是该元素的一个attribute。在JavaScript中，我们可以使用element.getAttribute('id')方法获取该元素的id属性的值。类似地，我们也可以使用element.setAttribute('id', 'newId')方法设置该元素的id属性的值。

property是元素在DOM中对应的属性，例如tagName、id、className等。在DOM中，每个元素都是一个对象，每个对象都有一些属性和方法。例如，我们可以使用element.tagName获取元素的标签名，使用element.id获取元素的id属性的值，使用element.className获取元素的class属性的值等。

**两者的区别**

attribute是元素在HTML中定义的属性，而property是元素在DOM中对应的属性。

attribute的值是一个字符串，而property的值可以是任意类型的JavaScript值，例如字符串、数字、布尔值、对象等。

同时，当我们使用element.getAttribute方法获取属性的值时，它始终返回一个字符串；而当我们使用element.propertyName获取属性的值时，它返回的是一个JavaScript值。

**两者的关系**

当我们设置元素的attribute时，它也会影响到对应的property。

例如，当我们使用element.setAttribute('id', 'newId')方法设置元素的id属性时，它也会影响到element.id属性的值。

反之，当我们设置元素的property时，它并不会影响到对应的attribute。

例如，当我们使用element.id = 'newId'方法设置元素的id属性时，它并不会影响到元素的HTML代码中的id属性。

**注意**

需要注意的是，有些属性名在JavaScript中与关键字重名，例如class、for等，此时我们可以在JavaScript中使用property的名称，例如element.className、element.htmlFor等。

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

而style是直接为单个元素设置CSS样式属性值，可以通过修改元素的style属性值来修改元素的样式，会直接覆盖元素原来的CSS样式，比较适合用于修改单个元素的样式。

此外，class可以通过CSS样式表中的选择器来实现更加复杂的样式匹配和样式继承，而style则比较适合用于动态生成或修改单个元素的样式。

## DOM常见的操作方法

DOM（Document Object Model）提供了许多方法和属性，可以用来访问和操作HTML和XML文档的内容。以下是常见的DOM操作方法：

**1、获取元素**

- `document.getElementById('id')`：根据id获取元素
- `document.getElementsByClassName('class')`：根据类名获取元素
- `document.getElementsByTagName('tag')`：根据标签名获取元素
- `document.querySelector('selector')`：根据选择器获取元素
- `document.querySelectorAll('selector')`：根据选择器获取所有符合条件的元素

**2、创建元素**

- `document.createElement('tag')`：创建一个新的元素节点

**3、插入和删除元素**

- `parentElement.appendChild(childElement)`：将子元素添加到父元素的末尾
- `parentElement.insertBefore(newElement, referenceElement)`：将新元素插入到参考元素之前
- `parentElement.removeChild(childElement)`：从父元素中删除子元素

**4、修改元素**

- `element.innerHTML`：设置或获取元素的HTML内容
- `element.innerText`：设置或获取元素的纯文本内容
- `element.setAttribute(name, value)`：设置元素的属性值
- `element.getAttribute(name)`：获取元素的属性值
- `element.style.property = value`：设置元素的样式属性值

**5、查询元素信息**

- `element.tagName`：获取元素的标签名
- `element.id`：获取或设置元素的id属性值
- `element.className`：获取或设置元素的类名
- `element.parentElement`：获取元素的父元素
- `element.children`：获取元素的子元素列表
- `element.getAttribute(name)`：获取元素的指定属性值

**6、事件操作**

- `element.addEventListener('event', function)`：为元素添加事件监听器
- `element.removeEventListener('event', function)`：为元素移除事件监听器

## 常见对DOM的增删改查

常见对DOM的增删改查操作如下：

增加元素：通过`createElement()`创建新元素，通过`appendChild()`将新元素添加到现有元素中。

```js
// 创建新的div元素
const newDiv = document.createElement('div');
// 添加新的div元素到现有的body元素中
document.body.appendChild(newDiv);
```

删除元素：通过`removeChild()`方法删除一个现有的元素。

```js
// 获取要删除的元素
const el = document.getElementById('my-element');
// 从父元素中移除该元素
el.parentNode.removeChild(el);
```

修改元素：通过`innerHTML`属性设置元素的HTML内容。

```js
// 获取要修改的元素
const el = document.getElementById('my-element');
// 设置元素的HTML内容
el.innerHTML = '<h1>New heading</h1>';
```

查询元素：通过`querySelector()`、`getElementById()`、`getElementsByClassName()`等方法获取现有的元素。

```js
// 获取单个元素
const el = document.querySelector('#my-element');
// 获取多个元素
const els = document.getElementsByClassName('my-class');
```

这些常见的DOM操作可以帮助我们实现动态的页面交互和内容更新。需要注意的是，频繁的DOM操作可能会导致性能问题，应尽量减少DOM操作的次数，可以考虑使用文档片段（DocumentFragment）等技术来优化。

## className和classList的区别

`className` 和 `classList` 都是用于操作 HTML 元素的 class 属性，但它们的使用方式和功能上有一些区别。

`className` 是元素节点的一个属性，用于获取或设置元素的 class 属性值。当需要添加、删除或替换 class 属性值时，需要通过字符串拼接或正则表达式等方式来操作 className 属性。例如，以下代码将给一个元素添加一个名为 "active" 的类：

```javascript
var el = document.getElementById("my-element");
el.className += " active";
```

`classList` 是元素节点的一个只读属性，它返回一个 DOMTokenList 对象，其中包含了元素的所有 class 属性值。`classList` 提供了一组方法来操作元素的 class 属性值，包括 `add`、`remove`、`toggle` 和 `contains` 等。例如，以下代码将给一个元素添加一个名为 "active" 的类：

```javascript
var el = document.getElementById("my-element");
el.classList.add("active");
```

除了操作 class 属性值之外，`classList` 还提供了一些有用的方法，如 `length` 属性用于获取 class 属性值的数量，`item` 方法用于获取指定索引位置的 class 属性值等。

需要注意的是，`classList` 在一些旧版本的浏览器中不被支持，如果需要兼容旧版本的浏览器，可以使用 `className` 属性来操作元素的 class 属性值。

## 动态创建html元素，并插入到body

可以使用JavaScript中的`createElement()`和`appendChild()`方法来动态创建HTML元素，并将其插入到body中。

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

在这个例子中，首先使用`createElement()`方法创建一个div元素。然后使用className属性设置其class，使用textContent属性设置文本内容。最后，使用`appendChild()`方法将其插入到body元素中。

为什么不用 innerText 设置文本内容?

```js
div.innerText = 'This is my div.';
```

虽然innerText可以用于设置元素的文本内容，但是它的行为可能不同于预期，因为它会忽略隐藏元素，同时也会将HTML解析为纯文本，因此在某些情况下可能会引起安全问题。比如，如果将用户输入的HTML代码设置为元素的innerText，那么该HTML代码将会被解析为纯文本并显示在页面上，而不是被浏览器解析为HTML标记。这可能会导致一些安全问题，比如XSS攻击。

相比之下，使用textContent可以更安全地设置元素的文本内容，因为它只会将文本解析为纯文本，而不会将其解析为HTML标记。同时，textContent也不会忽略隐藏元素，因此可以确保元素的文本内容是准确的。

## setTimeout和setInterval的区别

setTimeout和setInterval都是JavaScript中常用的定时器函数，它们的主要区别在于触发的次数和时间间隔的处理方式。

setTimeout函数用于在指定的时间后执行一次代码。它接受两个参数：要执行的代码和等待的时间（以毫秒为单位）。当指定的时间到达时，setTimeout函数会执行一次代码，然后停止计时器。

例如，以下代码将在3秒后向控制台输出一条消息：

```javascript
setTimeout(function() {
  console.log("Hello, world!");
}, 3000);
```

setInterval函数用于在指定的时间间隔内重复执行一段代码。它接受两个参数：要执行的代码和重复执行的时间间隔（以毫秒为单位）。当指定的时间间隔到达时，setInterval函数会执行一次代码，然后再次启动计时器。

例如，以下代码将每隔1秒向控制台输出一条消息：

```javascript
setInterval(function() {
  console.log("Hello, world!");
}, 1000);
```

需要注意的是，setInterval函数会一直重复执行代码，直到计时器被清除。因此，如果代码的执行时间超过了重复执行的时间间隔，就会出现连续触发的情况，导致性能问题。为了避免这种情况，我们可以使用setTimeout函数来实现定时重复执行代码。

例如，以下代码将每隔1秒向控制台输出一条消息，并使用setTimeout函数来实现定时重复执行：

```javascript
function repeat() {
  console.log("Hello, world!");
  setTimeout(repeat, 1000);
}

setTimeout(repeat, 1000);
```

总的来说，setTimeout函数适用于需要延迟执行一次的代码，而setInterval函数适用于需要重复执行的代码。如果需要定时重复执行代码，可以使用setTimeout函数来实现。

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

`target` 和 `currentTarget` 是事件对象的两个属性，它们都指向触发事件的元素，但在事件流中的位置不同。

`target` 指向触发事件的元素，它是事件流中最先触发的元素。在事件冒泡阶段中，事件从最具体的元素开始向上传播，`target` 一般指向最内层被点击的元素，而在事件捕获阶段中，事件从最外层的元素开始向下传播，`target` 一般指向最外层的元素。在事件处理函数中，我们可以通过 `event.target` 来获取触发事件的元素。

`currentTarget` 指向绑定事件监听函数的元素，它是事件流中当前正在处理事件的元素。在事件冒泡阶段中，`currentTarget` 一般指向绑定事件监听函数的元素，而在事件捕获阶段中，`currentTarget` 一般指向最外层的元素。在事件处理函数中，我们可以通过 `event.currentTarget` 来获取绑定事件监听函数的元素。

下面是一个例子，通过点击 `<li>` 元素来触发事件并展示 `target` 和 `currentTarget` 的区别：

```html
<ul id="my-list">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

```javascript
var list = document.getElementById("my-list");
list.addEventListener("click", function(event) {
  console.log("target:", event.target);
  console.log("currentTarget:", event.currentTarget);
});
```

在这个例子中，当点击 `<li>` 元素时，`target` 和 `currentTarget` 会分别指向该元素和 `<ul>` 元素。

## EventTarget的使用

**前言**

- `addEventListener`:注册某个事件类型以及事件处理函数
- `removeEventListener` : 移除某个事件类型以及事件处理函数
- `dispatchEvent` : 派发某个事件类型到EventTarget上

**EventTarget**

EventTarget 接口是一个非常重要的接口，因为在 Web 应用程序中，几乎所有的事件都是由它来处理的。一个实现了 EventTarget 接口的对象可以被用作事件的目标对象，也就是说，可以向这个对象注册事件监听器，当事件发生时，目标对象会自动触发相应的事件监听器，并调用相应的处理函数。

在 JavaScript 中，常见的实现了 EventTarget接口的对象包括 window对象、document对象以及 DOM 元素。这些对象都具有相应的事件处理能力，可以用来处理用户的交互、实现动画效果、异步数据请求等等。

**常用方法**

EventTarget 接口定义了以下常用的方法：

- `addEventListener(type, listener, options)`：向目标对象注册事件监听器。type 表示事件类型，listener 表示事件处理函数，options 是一个可选的参数对象，用于配置事件监听器的一些属性，例如 capture、once、passive 等。默认情况下，事件监听器是在事件冒泡阶段处理的，如果需要在事件捕获阶段处理事件，可以将 capture 属性设置为 true。
- `removeEventListener(type, listener, options)`：从目标对象中移除事件监听器。和 addEventListener() 方法类似，需要指定要移除的事件类型和处理函数，同时也可以指定一些可选参数。
- `dispatchEvent(event)`：手动触发事件。event 表示要触发的事件对象，通常是一个 Event 子类的实例。触发事件时，事件会沿着 DOM 树进行传递，直到到达目标元素。

**其他属性和方法**

除了上面这些方法之外，EventTarget 还有一些其他的属性和方法，包括：

- `on[event]`：这是一个简便的方式来为目标对象注册事件监听器，例如 onclick、onload 等。实际上，这些属性就是 `addEventListener()` 方法的语法糖，例如 `element.onclick = function() { ... }` 就相当于 `element.addEventListener('click', function() { ... })`
- `eventPhase`：表示当前事件所处的阶段，可能的值有 0（未初始化）、1（事件捕获阶段）、2（事件目标阶段）和 3（事件冒泡阶段）。
- `dispatchEvent(event)`：手动触发事件。event 表示要触发的事件对象，通常是一个 Event 子类的实例。触发事件时，事件会沿着 DOM 树进行传递，直到到达目标元素。

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

## mouseenter和mouseover的区别

1、mouseenter

- 不会冒泡
- 进入子元素的时候不会有任何行为

mouseenter事件只有在鼠标指针进入事件的目标元素时才被触发。它不会冒泡，也就是说，当鼠标指针进入一个元素时，如果该元素有子元素，那么这个事件只会在目标元素上触发一次，不会在子元素上触发。同时，当鼠标指针从目标元素内部移动到其子元素上时，不会触发该事件。

2、mouseover

- 会进行冒泡行为
- 进入子元素，会先out父元素，再over子元素，再over父元素

而mouseover事件在鼠标指针进入事件目标元素或其子元素时都会被触发。它会进行冒泡，也就是说，当鼠标指针进入一个元素时，该事件会在目标元素和其所有祖先元素上触发，而当鼠标指针从目标元素内部移动到其子元素上时，会先触发一次mouseout事件在目标元素上，然后再在子元素上触发一次mouseover事件，最后再在目标元素及其祖先元素上触发一次mouseover事件。

> 因此，mouseenter事件和mouseover事件在处理鼠标指针进入和离开元素时有所不同，mouseenter事件更加严格，而mouseover事件更加灵活。

## 说说load和DOMContentLoaded的区别

`load` 和 `DOMContentLoaded` 都是针对页面加载事件的。

**load**

- 浏览器加载完所有的HTML，还加载完所有的外部资源、样式、图片等；

`load` 事件在页面及其所有相关资源（如图片、脚本、样式等）都加载完成后触发。如果在 `load` 事件触发之前添加了新的资源，那么这些新的资源也需要加载完成后才能触发 `load` 事件。

**DOMContentLoaded**

- HTML文档所有资源都加载完成，并构建了DOM树，但是一些外部资源还没有加载完成时触发：如图片的src；

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

JSON（JavaScript Object Notation）是一种轻量级的数据交换格式，易于阅读和编写，也易于机器解析和生成。JSON 在Web应用中广泛使用，它通常用于在客户端和服务器之间传输数据。

JSON 的语法与 JavaScript 对象字面量语法类似，但是它不是 JavaScript，而是一种独立的数据格式。在 JSON 中，可以表示以下数据类型：

- 对象（Object）：一组无序的键值对，用花括号 `{}` 表示。
- 数组（Array）：一组有序的值的集合，用方括号 `[]` 表示。
- 字符串（String）：一串由双引号或单引号括起来的字符。
- 数值（Number）：一个整数或浮点数。
- 布尔值（Boolean）：`true` 或 `false`。
- 空值（null）：表示没有值的值。

**三种用法**

- 简单值：可以是数字、字符串、布尔类型，也可以是 null 和 undefined。
- 对象值：由 key-value 组成，key 必须添加双引号，value 可以是简单值、对象值或数组值。
- 数组值：由多个值组成，内容可以是对象值、简单值或其他数组值。

**常见用法**

将 JavaScript 对象转换为 JSON 字符串：

```js
var obj = {name: "Alice", age: 20};
var jsonString = JSON.stringify(obj);
console.log(jsonString); // 输出 {"name":"Alice","age":20}
```

将 JSON 字符串转换为 JavaScript 对象：

```js
var jsonString = '{"name":"Alice","age":20}';
var obj = JSON.parse(jsonString);
console.log(obj.name); // 输出 Alice
console.log(obj.age); // 输出 20
```

发送 JSON 数据到服务器：

```jsp
var xhr = new XMLHttpRequest();
var obj = {name: "Alice", age: 20};
xhr.open("POST", "/api/users");
xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
xhr.send(JSON.stringify(obj));
```

从服务器获取 JSON 数据：

```js
var xhr = new XMLHttpRequest();
xhr.open("GET", "/api/users");
xhr.responseType = "json";
xhr.onload = function() {
  var users = xhr.response;
  console.log(users);
};
xhr.send();
```

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

```js
function sum(a, b) {
  return a + b;
}
```

如果我们在调用这个函数时传递的参数不是数字类型，那么JavaScript会抛出一个TypeError异常。例如：

```js
sum(2, '3'); // 抛出异常
```

如果我们不进行有效的异常处理，这个异常会中断代码流程，并导致后续代码无法执行，这对于网站的用户体验和安全性都是不利的。

如果我们使用try-catch语句来捕获和处理这个异常，我们就可以避免这个问题，如下图所示：

```js
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