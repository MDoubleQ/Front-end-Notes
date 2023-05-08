记得刚开始，我理解 `this` 的时候   也是云里雾里的，哈哈，希望通过这篇文章，对你有帮助吧。

关于 `this`  最多的说法，就是：谁调用它，this就指向谁。这话呢，不能说它错了，只能说它讲的不严谨，为什么呢？我们先来了解下 `this` 的几种绑定规则。

#### 一、默认绑定

默认绑定  发生在全局环境 。

全局环境中，`this` 默认绑定到 `window`。（严格模式下一样）

```javascript
console.log(this === window);
//true

"use strict";    //使用严格模式执行代码
var a = 666;
console.log(this.a)

//666

```

#### 二、隐式绑定

隐式绑定  发生在 方法调用（执行）。

什么是方法呢？通常把 对象的属性值   是函数的，称为方法。

```kotlin
var obj = {
    fun: function(){}
}

//这里obj 对象里 的fun 属性值是个函数， 就把 这个fun 属性称为方法了。

```

通常，方法调用时，`this` 隐式绑定到其  **所属的对象** 上。

```kotlin
var a = "window";

var obj = {
    a: "obj",
    
    fun: function(){
        console.log(this.a);
    }
}

obj.fun();

//"obj"

```

来个难一点的：

```kotlin
var obj1 = {
    a: "obj1",
   
    obj2: {
        a: "obj2",
        fun: function(){
            console.log(this.a);
        }
    }
}

obj1.obj2.fun();

//"obj2"

```

这里的答案  跟你想的一样吗？ 出现这个答案的关键   就是于，`fun` 函数 在作为对象方法执行时， `this` 绑定的是它的  **所属对象**，也就是 `obj2` 。 而非外层 的 `obj1`。

#### 三、隐式绑定丢失

在判断是否是隐式绑定的时候，最容易出问题的地方就是发生在 隐式绑定丢失。

隐式丢失是指被隐式绑定的函数丢失绑定对象，从而绑定到window。这种情况容易出错却又常见。（严格模式下，绑定到undefined）

隐式绑定丢失 一般 发生在  函数**独立调用**时。

啥是**独立调用**呢？就是一个简单的函数执行. 函数名的前面没有任何引导内容。

```scss
function ff(){};

ff();   //独立调用

```

当函数独立调用（执行）时，`this`  就会隐式绑定丢失，而绑定到 `window` 对象上。（非严格模式下）

```kotlin
function fun(){
    console.log(this === window);
}
fun();
//true

```

那么严格模式下呢？是指向 `undefined` 的。

```kotlin
function fun(){
    "use strict";    //使用严格模式执行代码
    console.log(this);
}
fun();

//undefined

```

考考你：

```ini
var a = "window";

var obj = {
    a: "obj",
    
    fun1: function(){
        console.log(this.a);
    }
}

var fun2 = obj.fun;

fun2();
//"window"

```

**判断是否隐式绑定丢失的关键就在于， 判断函数  是否是哪种调用。**

上面的例子，关键点就在  最后两行代码。 先看其中的第一行：

```ini
var fun2 = obj.fun;

```

这里把 obj 的fun 方法  赋值给了 一个变量  fun2，这里的 fun  并没有作为对象的方法来执行，因为，fun 方法这里没有执行。

其后：

```scss
fun2()；

```

再执行  fun2，它保存着 fun1 方法，这时候执行  fun2（等于fun1） ，但是，它是独立调用。因为，没有作为对象的方法来调用。所以 this 就被指向 window了。

**那么怎么解决隐式丢失问题呢？**

```kotlin
var a = "window";

var obj = {
    a: "obj",
    
    fun: function(){
        return function(){
            console.log(this.a);
        }
    }
}

obj.fun()();

//"window"

//这里我们想要的是 obj里 a 的值，可是，隐式绑定丢失导致获取到了 window 里 a 的值。

```

可以基础好的已经知道答案了：

```kotlin
var a = "window";

var obj = {
    a: "obj",
    
    fun: function(){
        var that = this;
        return function(){
            console.log(that.a);
        }
    }
}

obj.fun()();

//"obj"

```

因为 `fun` 是作为方法调用的，所以  `this` 绑定到 `obj` 对象上，因此，我们就可以先用一个变量 `that` 来保存 `this`，然后  在内部的 匿名函数中 使用 `that`  就可以了。它保存着 上面 `this` 的绑定对象。

忽然灵机一动，想出个题目，看人家都玩出题，我也试试，哈哈:

```kotlin
var a = "window";

function fun(){
	var a = "fun";

	return (function(){
	    return this.a;
	})()
}

fun()

//“你猜”

```

这道题中  有立即执行函数、this问题，哈哈，乍一看挺恶心，其实看完上面的，应该可以看出来的。

#### 四、显示绑定

通过call()、apply()、bind()方法把 `this` 绑定到**对象**上，叫做显式绑定。对于被调用的函数来说，叫做**间接调用**。

```kotlin
var a = "window"

var obj = {
    a:"obj",
}

function fun(){
    console.log(this.a);
}

fun.call(obj);
//"obj";

```

这里使用了  call 方法，把fun 中的 this 绑定到  obj 对象上。

javascript内置的一些函数，具有显式绑定的功能，如数组的5个迭代方法：map()、forEach()、filter()、some()、every()，以及创建对象的 Object.create() 函数（后面原型链中会细说），都可以手动绑定this。

大家可以去看下API文档，数组的这几个函数的最后一个参数，就是指定函数内  this 的绑定，如果不指定，则是`window`，严格模式下是`undefined`。

```css
var a = [1,2,3];

a.forEach(function(){
    console.log(this)
},a);

//绑定 this  为 a 这个数组

//(3) [1, 2, 3]
//(3) [1, 2, 3]
//(3) [1, 2, 3]

```

#### 五、new 绑定

如果 使用 `new` 来创建对象，因为 后面跟着的是构造函数，所以称它为构造器调用。对于`this`绑定来说，称为`new`绑定。

想知道 构造器调用 中 `this` 的绑定，就要知道 `new`  到底做了啥了。

先来个 new 的实现。看不懂不要紧，在后面原型链那篇，还会说的。

```javascript
function New(proto){  //proto 为传进来的构造函数
    var obj = {};
    obj.__proto__ = proto.prototype;

    proto.apply(obj, Array.prototype.slice.call(argument,1));
    //你这要看懂这步就行。这里把构造函数里的 this  绑定到了 新的obj 对象上，最后 返回了该新对象，作为实例对象。

    return obj;
}

```

所以在使用  new 来创建实例对象时，new  内部把 **构造函数的 this** 绑定到 返回的**新对象** 上了。

```ini
function Person(name){
    this.name = name;
}
var c = new Person("zdx");
c.name;

```

总结： this的四种绑定规则：隐式绑定、隐式绑定丢失、显式绑定和new绑定，分别对应函数的四种调用方式：方法调用、独立调用、间接调用和构造器调用。



#### 附录：

1、关于this绑定 的优先级问题。

简单提一下吧：

**new 绑定 > 显示绑定 > 隐式绑定 > 默认绑定** 。

2、ES6 中，箭头函数的 this  绑定。

**箭头函数内的 this 绑定的  是所属的环境（函数或者对象）， 它是固定不变的。**

先看下上面的这个例子

```kotlin
var a = "window";

var obj = {
    a: "obj",
    
    fun: function(){
        return function(){
            console.log(this.a);
        }
    }
}

obj.fun()();

//"window"

```

上面我们使用  一个变量来保存 this 的绑定，下面我们来用 箭头函数解决问题

```kotlin
var a = "window";

var obj = {
    a: "obj",
    
    fun: function(){
        return () => {
            console.log(this.a);
        }
    }
}

obj.fun()();

//"obj"

```

实际上，箭头函数内部是没有`this` 的，所以，它不能使用 `new` 构造器调用，`call` 等**显示绑定**。所以它内部就是使用了一个变量来保存 箭头函数  **所属环境的（函数或者对象）** `this`。

就相当于：

```kotlin
var a = "window";

var obj = {
    a: "obj",
    
    fun: function(){
            that = this;
            return function(){
                console.log(that.a);
            }
    }
}

obj.fun()();

//"obj"

```

考考你：

```ini
var a = "window";

var obj = {
    a: "obj",
    
    fun1: function(){
        return () => {
            console.log(this.a);
        }
    }
}

var fun2  = obj.fun1;

fun2()();
```



作者：周大侠啊
链接：https://juejin.cn/post/6844903649055866887
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。