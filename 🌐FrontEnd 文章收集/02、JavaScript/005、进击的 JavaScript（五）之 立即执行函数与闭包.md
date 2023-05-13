前面的闭包中，提到与闭包相似的立即执行函数，感觉两者还是比较容易弄混吧，严格来说（因为犀牛书和高程对闭包的定义不同），立即执行函数并不属于闭包，它不满足闭包的三个条件。



#### 一、圆括号运算符

  圆括号运算符也叫分组运算符，它有两种用法：如果表达式放在圆括号中，作用是求值；如果跟在函数后面，作用是调用函数

  把表达式放在圆括号之中，将返回表达式的值

```arduino
console.log((1+2)); // 3

```

  将函数放在圆括号中，会返回函数本身。如果圆括号紧跟在函数的后面，就表示调用函数，即对函数求值

```lua
console.log((function testa(){return 666;}));
// function testa(){return 666;}

console.log(function testa(){return 666;}());
// 666

```

**注意:圆括号运算符不能为空，否则会报错**

```scss
();//SyntaxError: Unexpected token )

```

由于圆括号的作用是求值，如果将语句放在圆括号之中，就会报错，因为语句没有返回值

```javascript
(var a = function(){return 666});
// SyntaxError: Unexpected token var

```



#### 二、函数声明

使用 `function` 关键字创建一个函数，并且后面带有函数名，叫函数声明。

```csharp
function testa(){}

```



#### 三、匿名函数

那么使用 `function` 关键字创建的函数不带函数名呢？ 那就是匿名函数了。

```javascript
function (){}

```



#### 四、函数表达式

那么把匿名函数赋值给一个变量呢？那就是函数表达式了。

```javascript
var testa = function (){}

```

其实呢，函数表达式的根本所在，就是阻止了js引擎把 **用`function`创建的函数** 当作函数声明来解析。下面再详说。



#### 五、立即执行函数（IIFE）

那么立即执行函数呢？

用`function`定义函数之后，立即调用该函数。这种函数就叫做立即执行函数，全称为立即调用的函数表达式IIFE(Imdiately Invoked Function Expression)

1、在本系列进击的 JavaScript（三）中到过，代码执行时，会先对函数声明的函数 进行解析（函数声明提升），而函数表达式，当逐行执行到它时，才会解析。

2、正因为函数声明的提升，导致函数声明不能立即执行。因为，函数声明时，js只会解析到大括号（｝）就结束了，如果后面有`()`，只是一个圆括号运算符。

```javascript
function testa(){
    console.log("testa")
}("666")

//"666"
//如果后面是一个空的圆括号，会报错，上面提到过。

```

所以，不知道，你有没有发现，函数声明的函数，后面可以不用分号（;）分隔，也可以正常执行，而函数表达式的后面就必须加分号，不然会报错。你可以自己写个小栗子验证下。

3、匿名函数是不能单独写的，所以就提不上立即执行了。

```javascript
function (){}
//Uncaught SyntaxError: Unexpected token (

```

单独写匿名函数，是会报错的，js引擎 会把它当作函数声明来解析，而函数声明就必须要有个函数名，所以会报错。 所以，你通常看到使用匿名函数，都是当作参数传递的，或者把匿名函数转为函数表达式。

4、因此，只有函数表达式可以立即执行

```javascript
var testa = function (){
    console.log("testa")
}()
//"testa"

```

上面提到过，函数表达式，就是阻止了js引擎把 |用`function`创建的函数| 当作函数声明来解析。

**注：javascript引擎规定，如果function关键字出现在行首，一律解释成函数声明语句。**

所以，解决方法就是不要让function出现在行首，让引擎将其理解成一个表达式。

```javascript
//常用的两种,使用圆括号运算符
(function(){console.log("666")})()
(function(){console.log("666")}())

//一元运算符写法
!function(){console.log("666")}()
+function(){console.log("666")}()
-function(){console.log("666")}()
~function(){console.log("666")}()

```

都是都可以把函数声明  转为 函数表达式，也就是阻止了把其当作函数声明解析。 

#### 六、立即执行函数在闭包中的应用

1、立即执行函数能配合闭包保存状态。

来看下 上节内容中闭包的例子：

```javascript
function makeClosures(i){    
    var i = i;  
    return function(){
        console.log(i);     
    }
}

for (var i=1; i<=5; i++) {
    setTimeout(makeClosures(i),i*1000);  
}
//1
//2
//3
//4
//5

```

现在，我们来利用立即执行函数来简化它：

```css
for (var i=1; i<=5; i++) {
    setTimeout((function(i){
        return function(){
            console.log(i);
        }
    })(i),i*1000);
}

```

第一个匿名函数执行完毕后，返回了第二个匿名函数。第二个匿名函数被当做setTimeout 的第一个参数传入进去。因为 setTimeout函数执行了5次，所以立即执行函数里每次都会返回了一个没有被执行的匿名函数，（这里就是返回了5个匿名函数），每个匿名函数内部保存着每次传进来的i值，因此，每个i 都是不一样的，所以，就得到了想要的结果

2、立即执行函数配合闭包 模块化中应用

```ini
(function(){
    var meg = "hello zdx";
    
    function say(arg){
        arg = arg || meg;
        console.log(arg)
    }
    
    window.say = say;
})(window)

window.say();

//"hello zdx"

```

首先立即执行函数，它是个匿名函数，你是得不到它的函数引用，这样，就避免了全局变量污染。其次，由于函数作用域的规则，在匿名函数外部是访问不了函数内的变量，函数等的。所以，也经常用立即执行函数模拟块级作用域。



作者：周大侠啊
链接：https://juejin.cn/post/6844903638633037837
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。