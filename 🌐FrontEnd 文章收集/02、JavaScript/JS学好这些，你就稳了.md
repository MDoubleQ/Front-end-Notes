## 前言

一、一年一度的毕业季又来了，不知各位胸怀大志的小伙伴们是否找到了自己心仪的工作呢，不管是继续考研学习，还是直接进入公司工作，都不要忘记继续努力噢♥

二、下面我对JavaScript中的部分基础知识做了一些梳理和总结，希望各位友友能够温故而知新，力创新高！

三、这一篇文章进一步巩固 JavaScript 的有关基础知识点

## 1.事件委托

### 一、定义

1、把一个元素响应事件（click、keydown......）的函数委托到另一个元素

前面讲到，事件流的都会经过三个阶段： 捕获阶段 -> 目标阶段 -> 冒泡阶段，而事件委托就是在冒泡阶段完成

事件委托，会把一个或者一组元素的事件委托到它的父层或者更外层元素上，真正绑定事件的是外层元素，而不是目标元素

当事件响应到目标元素上时，会通过事件冒泡机制从而触发它的外层元素的绑定事件上，然后在外层元素上去执行函数

2、利用了浏览器事件冒泡的机制。因为事件在冒泡过程中会上传到父节点，并且父节点可以通过事件对象获取到 目标节点

因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件，这种方式称为事件代理

### 二、使用

1、使用事件代理我们可以不必要为每一个子元素都绑定一个监听事件，这样减少了内存上的消耗

2、并且使用事件代理我们还可以实现事件的动态绑定

比如说新增了一个子节点，我们并不需要单独地为它添加一个监听事件，它所发生的事件会交给父元素中的监听函数来处理。

### 三、优缺点

### 1、优点：

减少整个页面所需的内存，提升整体性能

动态绑定，减少重复工作

### 2、缺点：

focus、blur这些事件没有事件冒泡机制，所以无法进行委托绑定事件

mousemove、mouseout这样的事件，虽然有事件冒泡，只能不断通过位置去计算定位，对性能消耗高，也是不适合于事件委托的

## 2.事件传播 事件捕获 事件冒泡

### 一、事件传播

### 1、定义：

当事件发生在DOM元素上时，该事件并不完全发生在那个元素上

### 2、阶段：

捕获阶段：事件从 window 开始，然后向下到每个元素，直到到达目标元素事件或event.target

目标阶段：事件已达到目标元素

冒泡阶段：事件从目标元素冒泡，然后上升到每个元素，直到到达 window

### 二、事件捕获

1、在捕获阶段，事件从window开始，一直到触发事件的元素

window----> document----> html----> body ---->目标元素

### 三、事件冒泡

是一种从下往上的传播方式，由最具体的元素（触发节点）然后逐渐向上传播到最不具体的那个节点，也就是DOM中最高层的父节点

事件捕获与事件冒泡相反，事件最开始由不太具体的节点最早接受事件, 而最具体的节点（触发节点）最后接受事件

## 3.继承

### 一、原型链的方式

但是这种实现方式存在的缺点是，在包含有引用类型的数据时，会被所有的实例对象所共享，容易造成修改的混乱

还有就是在创建子类型的时候不能向超类型传递参数

### 二、构造函数的方式

这种方式是通过在子类型的函数中调用超类型的构造函数来实现的，这一种方法解决了不能向超类型传递参数的缺点

但是它存在的一个问题就是无法实现函数方法的复用，并且超类型原型定义的方法子类型也没有办法访问到

### 三、组合继承的方式

组合继承是将原型链和借用构造函数组合起来使用的一种方式

通过借用构造函数的方式来实现类型的属性的继承，通过将子类型的原型设置为超类型的实例来实现方法的继承，解决了上面的两种模式单独使用时的问题

但是由于我们是以超类型的实例来作为子类型的原型，所以调用了两次超类的构造函数，造成了子类型的原型中多了很多不必要的属性。

### 四、原型式继承的方式

原型式继承的主要思路就是基于已有的对象来创建新的对象

实现的原理是，向函数中传入一个对象，然后返回一个以这个对象为原型的对象

这种继承的思路主要不是为了实现创造一种新的类型，只是对某个对象实现一种简单继承，ES5 中定义的 Object.create() 方法就是原型式继承的实现

缺点与原型链方式相同

### 五、寄生式继承的方式

寄生式继承的思路是创建一个用于封装继承过程的函数，通过传入一个对象，然后复制一个对象的副本，然后对象进行扩展，最后返回这个对象

这个扩展的过程就可以理解是一种继承，这种继承的优点就是对一个简单对象实现继承，如果这个对象不是我们的自定义类型时

缺点是没有办法实现函数的复用

### 六、寄生式组合继承的方式

组合继承的缺点就是使用超类型的实例做为子类型的原型，导致添加了不必要的原型属性

寄生式组合继承的方式是使用超类型的原型的副本来作为子类型的原型，这样就避免了创建不必要的属性

## 4.数组

### 一、增

1、前三种是对原数组产生影响的增添方法，第四种则不会对原数组产生影响：

push()：接收任意数量的参数，并将它们添加到数组末尾，返回数组的最新长度

unshift()：在数组开头添加任意多个值，然后返回新的数组长度

splice()：传入三个参数，分别是开始位置、0（要删除的元素数量）、插入的元素，返回空数组

concat()：首先会创建一个当前数组的副本，然后再把它的参数添加到副本末尾，最后返回这个新构建的数组，不会影响原始数组

### 二、删

1、下面三种都会影响原数组，最后一项不影响原数组：

pop()：方法用于删除数组的最后一项，同时减少数组的length 值，返回被删除的项

shift()：方法用于删除数组的第一项，同时减少数组的length 值，返回被删除的项

splice()：传入两个参数，分别是开始位置，删除元素的数量，返回包含删除元素的数组

slice()：用于创建一个包含原有数组中一个或多个元素的新数组，不会影响原始数组

### 三、改

1、修改原来数组的内容：

splice()：传入三个参数，分别是开始位置，要删除元素的数量，要插入的任意多个元素，返回删除元素的数组，对原数组产生影响

### 四、查

1、查找元素，返回元素坐标或者元素值：

indexOf()：返回要查找的元素在数组中的位置，如果没找到则返回 -1

includes()：返回要查找的元素在数组中的位置，找到返回true，否则false

find()：返回第一个匹配的元素

### 五、排序

1、数组有两个方法可以用来对元素重新排序：

reverse()：将数组元素方向反转

sort()：接受一个比较函数，用于判断哪个值应该排在前面

### 六、转换

join()：方法接收一个参数，即字符串分隔符，返回包含所有项的字符串

### 七、迭代

1、不改变原数组：

some()：对数组每一项都运行传入的函数，如果有一项函数返回 true ，则这个方法返回 true

every()：对数组每一项都运行传入的函数，如果对每一项函数都返回 true ，则这个方法返回 true

forEach()：对数组每一项都运行传入的函数，没有返回值

filter()：对数组每一项都运行传入的函数，函数返回 true 的项会组成数组之后返回

map()：对数组每一项都运行传入的函数，返回由每次函数调用的结果构成的数组

## 5.字符串

### 一、增

1、并不是说直接增添内容，而是创建字符串的一个副本，再进行操作：

除了常用+以及${}进行字符串拼接之外，还可通过concat

concat：用于将一个或多个字符串拼接成一个新字符串

### 二、删

1、并不是说删除原字符串的内容，而是创建字符串的一个副本，再进行操作：

slice()、substr()、substring()：这三个方法都返回调用它们的字符串的一个子字符串，而且都接收一或两个参数

### 三、改

1、也不是改变原字符串，而是创建字符串的一个副本，再进行操作：

trim()、trimLeft()、trimRight()：删除前、后或前后所有空格符，再返回新的字符串

repeat()：接收一个整数参数，表示要将字符串复制多少次，然后返回拼接所有副本后的结果

padStart()、padEnd()：复制字符串，如果小于指定长度，则在相应一边填充字符，直至满足长度条件

toLowerCase()、toUpperCase()：大小写转化

### 四、查

1、除了通过索引的方式获取字符串的值，还可通过：

charAt()：返回给定索引位置的字符，由传给方法的整数参数指定

indexOf()：从字符串开头去搜索传入的字符串，并返回位置（如果没找到，则返回 -1 ）

startWith()、includes()：从字符串中搜索传入的字符串，并返回一个表示是否包含的布尔值

### 五、转换

split：把字符串按照指定的分割符，拆分成数组中的每一项

### 六、模板匹配

match()：接收一个参数，可以是一个正则表达式字符串，也可以是一个RegExp对象，返回数组

search()：接收一个参数，可以是一个正则表达式字符串，也可以是一个RegExp对象，找到则返回匹配索引，否则返回 -1

replace()：接收两个参数，第一个参数为匹配的内容，第二个参数为替换的元素（可用函数）

## 6.执行上下文 执行栈

### 一、执行上下文

#### 1、定义：

一种对Javascript代码执行环境的抽象概念，也就是说只要有Javascript代码运行，它就一定是运行在执行上下文中

#### 2、类型：

全局执行上下文：只有一个，浏览器中的全局对象就是 window对象，this 指向这个全局对象

函数执行上下文：存在无数个，只有在函数被调用的时候才会被创建，每次调用函数都会创建一个新的执行上下文

Eval 函数执行上下文： 指的是运行在 eval函数中的代码，很少用而且不建议使用

### 二、生命周期

#### 1、创建阶段：

创建阶段即当函数被调用，但未执行任何其内部代码之前。创建阶段做了三件事

This Binding（确定this的值）： this的值是在执行的时候才能确认，定义的时候不能确认

LexicalEnvironment（词法环境） ：组件被创建

VariableEnvironment（变量环境） ：组件被创建

#### 2、执行阶段：

在这阶段，执行变量赋值、代码执行

如果 Javascript 引擎在源代码中声明的实际位置找不到变量的值，那么将为其分配 undefined 值

#### 3、回收阶段：

执行上下文出栈等待虚拟机回收执行上下文

### 三、执行栈

#### 1、定义：

执行栈，也叫调用栈，具有 LIFO（后进先出）结构，用于存储在代码执行期间创建的所有执行上下文

#### 2、作用：

当Javascript引擎开始执行你第一行脚本代码的时候，它就会创建一个全局执行上下文然后将它压到执行栈中

每当引擎碰到一个函数的时候，它就会创建一个函数执行上下文，然后将这个执行上下文压到执行栈中

引擎会执行位于执行栈栈顶的执行上下文(一般是函数执行上下文)，当该函数执行结束后，对应的执行上下文就会被弹出，然后控制流程到达执行栈的下一个执行上下文

#### 3、流程：

创建全局上下文请压入执行栈

first函数被调用，创建函数执行上下文并压入栈

执行first函数过程遇到second函数，再创建一个函数执行上下文并压入栈

second函数执行完毕，对应的函数执行上下文被推出执行栈，执行下一个执行上下文first函数

first函数执行完毕，对应的函数执行上下文也被推出栈中，然后执行全局上下文

所有代码执行完毕，全局上下文也会被推出栈中，程序结束

## 7.DOM

### 一、定义

文档对象模型 (DOM) 是 HTML 和 XML 文档的编程接口

### 二、作用

它提供了对文档的结构化的表述，并定义了一种方式可以使从程序中对该结构进行访问，从而改变文档的结构，样式和内容

任何 HTML或XML文档都可以用 DOM表示为一个由节点构成的层级结构

节点分很多类型，每种类型对应着文档中不同的信息和标记，也都有自己不同的特性、数据和方法，而且与其他类型有某种关系

DOM像原子包含着亚原子微粒那样，也有很多类型的DOM节点包含着其他类型的节点

### 三、操作

#### 1、创建节点：

createElement：创建新元素，接受一个参数，即要创建元素的标签名

createTextNode：创建一个文本节点

createDocumentFragment：用来创建一个文档碎片

createAttribute：创建属性节点，可以是自定义属性

#### 2、获取节点：

querySelector：传入任何有效的css 选择器，即可选中单个 DOM元素（首个）

querySelectorAll：返回一个包含节点子树内所有与之相匹配的Element节点列表，如果没有相匹配的，则返回一个空节点列表

#### 3、更新节点：

innerHTML：不但可以修改一个DOM节点的文本内容，还可以直接通过HTML片段修改DOM节点内部的子树

innerText、textContent：自动对字符串进行HTML编码，保证无法设置任何HTML标签

style：DOM节点的style属性对应所有的CSS，可以直接获取或设置。遇到-需要转化为驼峰命名

#### 4、添加节点：

innerHTML：如果这个DOM节点是空的，相当于添加了新的DOM节点。如果这个DOM节点不是空的，那就不能这么做，因为innerHTML会直接替换掉原来的所有子节点

appendChild：把一个子节点添加到父节点的最后一个子节点

insertBefore：把子节点插入到指定的位置

setAttribute：在指定元素中添加一个属性节点，如果元素中已有该属性改变属性值

#### 5、删除节点：

removeChild：删除一个节点，首先要获得该节点本身以及它的父节点，然后，调用父节点的removeChild把自己删掉

## 8.BOM

### 一、定义

BOM (Browser Object Model)，浏览器对象模型，提供了独立于内容与浏览器窗口进行交互的对象

### 二、作用

跟浏览器做一些交互效果

比如如何进行页面的后退，前进，刷新，浏览器的窗口发生变化，滚动条的滚动，以及浏览器品牌版本，屏幕分辨率

浏览器的全部内容可以看成DOM，整个浏览器可以看成BOM

### 三、window

#### 1、定义：

Bom的核心对象是window，它表示浏览器的一个实例

在浏览器中，window对象有双重角色，即是浏览器窗口的一个接口，又是全局对象

因此所有在全局作用域中声明的变量、函数都会变成window对象的属性和方法

#### 2、窗口控制方法：

moveBy(x,y)：从当前位置水平移动窗体x个像素，垂直移动窗体y个像素，x为负数，将向左移动窗体，y为负数，将向上移动窗体

moveTo(x,y)：移动窗体左上角到相对于屏幕左上角的(x,y)点

resizeBy(w,h)：相对窗体当前的大小，宽度调整w个像素，高度调整h个像素。如果参数为负值，将缩小窗体，反之扩大窗体

resizeTo(w,h)：把窗体宽度调整为w个像素，高度调整为h个像素

scrollTo(x,y)：如果有滚动条，将横向滚动条移动到相对于窗体宽度为x个像素的位置，将纵向滚动条移动到相对于窗体高度为y个像素的位置

scrollBy(x,y)： 如果有滚动条，将横向滚动条向左移动x个像素，将纵向滚动条向下移动y个像素

#### 3、导航到一个特定的url，也可以打开一个新的浏览器窗口：

如果 window.open() 传递了第二个参数，且该参数是已有窗口或者框架的名称，那么就会在目标窗口加载第一个参数指定的URL

window.open() 会返回新窗口的引用，也就是新窗口的 window 对象

window.close() 仅用于通过 window.open()打开的窗口

#### 4、新创建的 window 对象有一个 opener 属性，该属性指向打开他的原始窗口对象

### 四、location

| 属性名   | 例子                                                         | 说明                                |
| -------- | ------------------------------------------------------------ | ----------------------------------- |
| hash     | #contents                                                    | utl中#后面的字符，没有则返回空串    |
| host     | [www.wrox.com:80](www.wrox.com:80)                           | 服务器名称和端口号                  |
| hostname | [<a href="http://www.wrox.com](http:/www.wrox.com)">www.wrox.com](http://www.wrox.com)</a> | 域名，不带端口号                    |
| href     | http://www.wrox.com:80/WileyCDA/?q=javascript#contents       | 完整url                             |
| pathname | /WileyCDA/                                                   | 服务器下面的文件路径                |
| port     | 80                                                           | url的端口号，没有则为空             |
| protocol | http:                                                        | 使用的协议                          |
| search   | ?q=javascript                                                | url的查询字符串，通常为？后面的内容 |

1、除了 hash之外，只要修改location的一个属性，就会导致页面重新加载新URL

2、location.reload()，此方法可以重新刷新当前页面：

这个方法会根据最有效的方式刷新页面，如果页面自上一次请求以来没有改变过，页面就会从浏览器缓存中重新加载

如果要强制从服务器中重新加载，传递一个参数true即可

### 五、navigator

navigator 对象主要用来获取浏览器的属性，区分浏览器类型。属性较多，且兼容性比较复杂

### 六、screen

保存的纯粹是客户端能力信息，也就是浏览器窗口外面的客户端显示器的信息，比如像素宽度和像素高度

### 七、history

#### 1、定义：

history对象主要用来操作浏览器URL的历史记录，可以通过参数向前，向后，或者向指定URL跳转

#### 2、属性：

history.go()：接收一个整数数字或者字符串参数：向最近的一个记录中包含指定字符串的页面跳转，

history.go('maixaofei.com')

当参数为整数数字的时候，正数表示向前跳转指定的页面，负数为向后跳转指定的页面

history.go(3) //向前跳转三个记录

history.go(-1) //向后跳转一个记录

history.forward()：向前跳转一个页面

history.back()：向后跳转一个页面

history.length：获取历史记录数

## 9.本地存储

### 一、cookie

#### 1、定义：

某些网站为了辨别用户身份而储存在用户本地终端上的数据。

#### 2、作用：

是为了解决 HTTP无状态导致的问题

作为一段一般不超过 4KB 的小型文本数据，它由一个名称（Name）、一个值（Value）和其它几个用于控制 cookie有效期、安全性、使用范围的可选属性组成

但是cookie在每次请求中都会被发送，如果不使用 HTTPS并对其加密，其保存的信息很容易被窃取，导致安全风险。举个例子，在一些使用 cookie保持登录态的网站上，如果 cookie被窃取，他人很容易利用你的 cookie来假扮成你登录网站

#### 3、属性：

Expires：用于设置 Cookie 的过期时间

Max-Age：用于设置在 Cookie 失效之前需要经过的秒数（优先级比Expires高）

Domain：指定了 Cookie 可以送达的主机名

Path：指定了一个 URL路径，这个路径必须出现在要请求的资源的路径中才可以发送 Cookie 首部

标记为 Secure的 Cookie只应通过被HTTPS协议加密过的请求发送给服务端

### 二、localStorage

#### 1、定义：

HTML5新方法，IE8及以上浏览器都兼容

#### 2、特点：

生命周期：持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的

存储的信息在同一域中是共享的

当本页操作（新增、修改、删除）了localStorage的时候，本页面不会触发storage事件,但是别的页面会触发storage事件。

大小：5M（跟浏览器厂商有关系）

localStorage本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，会导致页面变卡

受同源策略的限制

#### 3、使用：

设置：localStorage.setItem()

获取：localStorage.getItem()

获取键名：localStorage.key()

删除：localStorage.removeItem())

一次性清除所有存储：localStorage.clear()

#### 4、缺点：

无法像Cookie一样设置过期时间

只能存入字符串，无法直接存对象

### 三、sessionStorage

#### 1、定义：

sessionStorage和 localStorage使用方法基本一致，唯一不同的是生命周期，一旦页面关闭，sessionStorage 将会删除数据

### 四、indexedDB

#### 1、定义：

一种低级API，用于客户端存储大量结构化数据(包括, 文件/ blobs)。该API使用索引来实现对该数据的高性能搜索

虽然 Web Storage对于存储较少量的数据很有用，但对于存储更大量的结构化数据来说，这种方法不太有用

#### 2、优点：

储存量理论上没有上限

所有操作都是异步的，相比 LocalStorage 同步操作性能更高，尤其是数据量较大时

原生支持储存JS的对象

是个正经的数据库，意味着数据库能干的事它都能干

#### 3、缺点：

操作非常繁琐

本身有一定门槛

#### 4、步骤：

打开数据库并且开始一个事务

创建一个 object store

构建一个请求来执行一些数据库操作，像增加或提取数据等。

通过监听正确类型的 DOM 事件以等待操作完成。

在操作结果上进行一些操作（可以在 request对象中找到）

## 10.攻击方式

### 一、定义

Web攻击（WebAttack）是针对用户上网行为或网站服务器等设备进行攻击的行为

如植入恶意代码，修改网站权限，获取网站用户隐私信息等等

### 二、XSS（Cross Site Scripting）

#### 1、定义：

跨站脚本攻击，允许攻击者将恶意代码植入到提供给其它用户使用的页面中

XSS涉及到三方，即攻击者、客户端与Web应用

XSS的攻击目标是为了盗取存储在客户端的cookie或者其他网站用于识别客户端身份的敏感信息

一旦获取到合法用户的信息后，攻击者甚至可以假冒合法用户与网站进行交互

#### 2、来源：

存储型：常见于带有用户保存数据的网站功能，如论坛发帖、商品评论、用户私信等

反射型：常见于通过 URL 传递参数的功能，如网站搜索、跳转等

DOM 型：取出和执行恶意代码由浏览器端完成，属于前端 JavaScript 自身的安全漏洞，而其他两种 XSS 都属于服务端的安全漏洞

#### 3、预防：

XSS攻击的两大要素：攻击者提交而恶意代码、浏览器执行恶意代码

针对第一个要素，我们在用户输入的过程中，过滤掉用户输入的恶劣代码，然后提交给后端，但是如果攻击者绕开前端请求，直接构造请求就不能预防了，而如果在后端写入数据库前，对输入进行过滤，然后把内容给前端，但是这个内容在不同地方就会有不同显示

### 三、CSRF（Cross-site request forgery）

#### 1、定义：

跨站请求伪造：攻击者诱导受害者进入第三方网站，在第三方网站中，向被攻击网站发送跨站请求

利用受害者在被攻击网站已经获取的注册凭证，绕过后台的用户验证，达到冒充用户对被攻击的网站执行某项操作的目

#### 2、流程：

受害者登录a.com，并保留了登录凭证（Cookie）

攻击者引诱受害者访问了b.com

b.com 向 a.com 发送了一个请求：a.com/act=xx。浏览器会默认携带a.com的Cookie

a.com接收到请求后，对请求进行验证，并确认是受害者的凭证，误以为是受害者自己发送的请求

a.com以受害者的名义执行了act=xx

攻击完成，攻击者在受害者不知情的情况下，冒充受害者，让a.com执行了自己定义的操作

#### 3、特点：

攻击一般发起在第三方网站，而不是被攻击的网站。被攻击的网站无法防止攻击发生

攻击利用受害者在被攻击网站的登录凭证，冒充受害者提交操作；而不是直接窃取数据

整个过程攻击者并不能获取到受害者的登录凭证，仅仅是“冒用”

跨站请求可以用各种方式：图片URL、超链接、CORS、Form提交等等

部分请求方式可以直接嵌入在第三方论坛、文章中，难以进行追踪

#### 4、预防：

阻止不明外域的访问：同源检测、Samesite Cookie

提交时要求附加本域才能获取的信息：CSRF Token、双重Cookie验证

### 四、SQL注入

#### 1、定义：

通过将恶意的 Sql查询或添加语句插入到应用的输入参数中，再在后台 Sql服务器上解析执行进行的攻击

#### 2、流程：

找出SQL漏洞的注入点

判断数据库的类型以及版本

猜解用户名和密码

利用工具查找Web后台管理入口

入侵和破坏

#### 3、预防：

严格检查输入变量的类型和格式

过滤和转义特殊字符

对访问数据库的Web应用程序采用Web应用防火墙

结尾

好了，本篇的所有内容就介绍到这里了，希望大家能够在未来的日子里继续加油！

---

版权声明：本文为CSDN博主「懵懵懂懂学前端」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。

原文链接：https://blog.csdn.net/qq_56966124/article/details/124907713