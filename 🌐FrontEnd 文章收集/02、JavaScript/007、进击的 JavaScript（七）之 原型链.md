## 函数创建的相关知识

在JavaScript中，我们创建一个**函数A**(就是声明一个函数), 那么 **js引擎** 就会用**构造函数**`Function`来创建这个函数。所以，所有的**函数**的`constructor`属性都指向 **构造函数**`Function`。`A.constructor === Function; //true`（函数本身并没有这个属性，后面介绍。记住，这里是函数，重点，要考，哈哈） 然后会在内存中创建一个**原型对象B**，**原型对象**这个东西，看不见，摸不着，只能通过函数的 `prototype` 来获取这个对象。( 即：prototype的属性的值是这个对象 )。

## 对象创建的相关知识

对象的创建，有三种方式 **1、字面量方式**(又称直接量)

啥是字面量呢？可以理解为，没用`new`出来的都属于字面量创建。

举个栗子：

```ini
var c = {};     //c 是变量， {} 就是字面量了

```

**字面量对象的创建过程跟函数的过程相似，当你声明一个对象字面量时，js引擎就会构造函数 Object 来创建这个对象，所以 效果等同 `new Object()`**

**2、构造器方式**

这个呢，就是用 `new` 创建。

栗子在此：

```ini
var c = new Object();

```

**3、Object.create**

这是个ES5中新增的方法，这个方法是创建一个新对象，把它的__proto__指向传进来的函数或者对象。到底是怎么回事呢，下面，咱们来简单实现下它的功能

```ini
function create(proto, options){     //proto表示传入的函数或者对象，options表示给子类添加的属性
    var obj = {};
    obj.__proto__ = proto;
    if(options == null){
        return obj;
    }
    return Object.defineProperties(obj,options);    //Object.defineProperties方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象。所以这里就直接return了
    }

```

检验一下：

```ini
var a = function(){};

//自制的create
var b = create(a);
console.log(b.__proto__ === a);   //true;
var c = create(a.prototype);
console.log(c.__proto__ === a.prototype);   //true

//Object.create
var d = create(a);
console.log(d.__proto__ === a);   //true;
var e = create(a.prototype);
console.log(e.__proto__ === a.prototype);   //true

```

**这里说明一下，你可以在别处看到的create的实现是这样的：**

```javascript
//这里就简化第二个参数了。就写第一个参数的实现
function create(proto){
    function f(){};
    f.prototype = proto;
    return new f();
}

```

这个是兼容的写法，因为，`__proto__` 属性是非标准的，部分现在浏览器实现了该属性。其实，你要是明白，`new`到底干了啥，  你就明白，这两个实际是一个东西了。

1. 创建一个新的对象（即实例对象）
2. 把新对象的`__proto__` 指向 `new` 后面构造函数 的原型对象。
3. 把构造函数中的 `this` 指向 实例对象。
4. 做一些处理，然后返回该实例对象。

下面，手写一个方法  实现new 的功能：

```javascript
function New(func){    //func 指传进来的构造函数,关于构造函数，我个人理解来就是用来生成一个对象实例的函数。

    var obj = {};   //这里就直接新建一个空对象了，不用new Object了，效果一样的，因为我感觉这里讲实现new的功能   再用 new 就不太好。
    
    if(func.prototype != null){
        obj.__proto__ = func.prototype;
    }
  
    func.apply(obj,Array.prototype.slice.call(arguments, 1));
    //把func构造函数里的this 指向obj对象，把传进来的第二个参数开始，放入func构造函数里执行，比如：属性赋值。

    return obj;
    
}

```

**不知各位看客是否看明白了呢，简单指明一下把**

```ini
function create(proto){
    var f = function(){};
    f.prototype = proto;
    return new f();

//就等于
function create(proto){
    var f = function(){};
    var obj = {};
    f.prototype = proto;
    obj.__proto__ = f.prototype;
    return obj;
}

//就等于
function create(proto){
    var obj = {};
    obj.__proto__ = proto;
    return obj;
}

//看明白了吗， 就是用 function f 做了一下过渡。

//验证
function a(){};
var b = create(a);
console.log(b.__proto__ === a);     //true;

```

## 原型链开始！

我想，一说到JavaScript的原型是令人奔溃的，其中prototype容易和__proto__两者的联系就太头疼了，反正看图比看字舒服。 ![这里写图片描述](E:\coder\09_OneNote\image\166a021e11cb973etplv-t2oaga2asx-zoom-in-crop-mark4536000.webp) **我看大多数的教程都是把`prototype` 和 `__proto__`放一起讲，我觉得还是分开将比较好，本来就不是一个东西**



### 一、prototype属性

**这是个函数才有的属性，它保存着对其原型对像的引用，即指向原型对象。（任何函数都有原型对象。）它的原型对象是看不见，摸不着的，只能通过函数的`prototype`属性来获取它。**

比如

```javascript
function A(){};
A.prototype;     //这样就获取到了A的原型对象

```

**总结：你看到`prototype`，你就想着它对应着，它的原型对象就行。**

### 二、原型对象

**每当你创建一个函数，js 就会 对应的生成一个原型对象。它只能被函数的`prototype`属性获取到。（`A.prototype` 整体变现为`A`的原型对象）**

通过上面知识，我们知道了，对象无非就两种，实例对象（new 和 字面量创建的对象），和 原型对象。

### 三、_ _ proto _ _属性

这个是非标准的属性，现代部分浏览器支持，比如，火狐，谷歌。对应的标准属性是[[prototype]]，这是个隐藏属性，获取不到。 这个属性就是把所有的函数啊，对象啊，连成一条链的东西，我们称为**原型链**。这条链的终点是`Object.prototype.__proto__ === null`。

那它到底指向谁呢，我给了**两种记忆方式**吧：

1、**函数的`__proto__` 指向`Function.protoype`，原型对象的`__proto__`指向`Object.prototype`的。`字面量`  和 `new`出来的实例对象 ，指向其构造函数（谁 new 出来的）的原型对象（`prototype`）， `Object.create` 创建的对象呢，就是上面说的，你给它谁，它就指向谁。** 
 2、**除了`Object.create`创建的对象的`__proto__`指向你给定的，原型对象的`__proto__`指向`Object.prototype`，其他的`__proto__` 都是指向其构造函数的原型对象。（你要是看懂了上面的`new`的实现，就应该明白为啥了。 ）**

**第二点注意：所有函数都是 构造函数 `Function` 创建出来的，所以，函数的构造函数  就是  `Function`。**

选这两个中你喜欢的一个，对着下面的图找答案: ![原型链](E:\coder\09_OneNote\image\166a021e0ebe7b75tplv-t2oaga2asx-zoom-in-crop-mark4536000.webp)



### 四、constructor属性

`constructor` 属性是原型对象独有的，它指向的就是它的构造函数。上面的**一、prototype**中说，函数的`prototype`属性指向它的原型对象。此时的函数是构造函数了。**所以函数  和 它的原型对像 以这两个 属性  保持着 相互联系。** ![constructor](E:\coder\09_OneNote\image\166a021e0eda124btplv-t2oaga2asx-zoom-in-crop-mark4536000.webp) 比如：

```javascript
function A(){};
A.prototype.constructor === A   //true

Object.prototype.constructor === Object   //true

```

那函数的constructor 和 普通对象的 constructor 是怎么回事呢?

开头说的`function A(){};A.constructor`  不知道大家有没有点疑惑？不是原型对象才有的吗？

其实，  他们就是在一条原型链上的，也就是说，A 上没有 `constructor` 属性，它就会沿着原型链向上查找，到了 `Object`的原型对象上，就找到了`constructor` 属性，于是就可以用 `A.constructor` 了.

比如：

```javascript
var Person = function(name) {
    this.name = name;
}

Person.prototype.getName = function(){
    return this.name;
}

var p = new Person("666");

console.log(p.getName());    //666

```

看这里Person 构造函数里是不是没有getName 方法，但是 p 实例怎么可以用呢？ 因为p实例 的`__proto__`指向 的原型对象上有 getName 函数，所以 p 向原型链上查找到了 Person 的原型对象上， 它有getName 方法， 于是， p 就可以使用这个方法了。 ![这里写图片描述](E:\coder\09_OneNote\image\166a021e120003e7tplv-t2oaga2asx-zoom-in-crop-mark4536000.webp)

**注意：所以，在找构造函数时，需要注意是在它的原型链上找，而不是原型对象上：**

```javascript
Object.constructor === Object.__proto__.constructor
//true

```



### 五、构造函数

啥是构造函数？其实每个函数都是构造函数，只是我们一般把  **生成实例对象**  的函数 称为**构造函数**（通过new ，new 后面的就是构造函数），**本质是函数**。

比如：

```javascript
var Person = function(name) {
    this.name = name;
    this.getName = function(){
        return this.name;
    }
}

var p1 = new Person("zdx");

console.log(p1.getName());     //zdx

var p2 = new Person("666");

console.log(p2.getName())     //666

console.log(Person.prototype.constructor === Person)    ///true

//这里的Person 是个函数对吧，然后外面用  new Person();
//创建了一个Person 的实例，此时，Person 就是一个构造函数了，也称它为类，我们把类的首字母都大写。
//因为，这个函数，使用 new 可以构造无数个实例来。

```

**说一下，怕有人不知道，实例就是实例对象，因为一个实例，它本身就是对象。**



### 六、原型链

开始放大招了，哈哈：

```javascript
function Person(name) {
    this.name = name;
}

var p = new Person("zdx");

console.log(p.__proto__ === Person.prototype);   //true
//p是实例对象, 它的构造函数是 Person，按照上面的所说的，它是new 出来的，所以指向它构造函数的prototype

console.log(Person.prototype.__proto__ === Object.prototype);   //true
//Person.prototype 是原型对象， 所以指向 Object.prototype.

console.log(Person.__proto__ === Function.prototype);   //true
//Person 是构造函数, 它的构造函数是Function， 所以它就指向 Function.prototype

console.log(Function.prototype.__proto__ === Object.prototype);   //true
//Function.prototype 是原型对象， 所以指向 Object.prototype.

console.log(Object.prototype.__proto__ === null);   //true   
//这里就是所有原型链的终端，原型链到这里就没了。

```

**所以说js 万物皆对象呢？ 所有的函数啊，对象啊，实例啊，它的原型链最终都到了Object.prototype原型对象**。

画成图就是酱样子滴： ![原型链](E:\coder\09_OneNote\image\166a021e0ebe7b75tplv-t2oaga2asx-zoom-in-crop-mark4536000.webp) **其实吧，有时候看图也不一样好，哈哈，你可以按照我说的规则，自己不看图画一下。**

简单来验证一下

```javascript
var a = {};   //等同与 new Object()
console.log(a.prototype);  //undefined   对象没有原型对象
console.log(a.__proto__ === Object.prototype);  //true

var b = function(){};
console.log(b.prototype);  //b的原型对像
console.log(b.__proto__ === Function.prototype);

var c = [];    //等同于 new Array(),构造函数是Array
console.log(c.__proto__ === Array.prototype);    //true

var d = "";    //等同于 new String()，构造函数是 String
console.log(d.__proto__ === String.prototype);    //true

```

### 七、原型链的作用

其实，原型链的根本作用就是为了 **属性** 的读取。放开了说，就是代码封装复用，继承。

**上面简单说过，当在一个 函数  或者 对象 上 读取属性时，它会先查找自身属性，如果有，就直接返回，如果没有呢，就会沿着原型链向上查找。**

举个简单的栗子，每个函数啊，对象啊，都有toString 方法，它是哪来的呢？ 球都麻袋！（等等），不是属性的读取吗。toString这个是方法（函数）呀！同学，你很有眼光嘛。事实上，我们把属性值为函数的，称之为 **方法**。其实呢，你要了解这些方法是怎么回事。

```javascript
function test(){};

test.toString();    //"function test(){}"

console.log(test.hasOwnProperty("toString"));   //false

console.log(test.__proto__.hasOwnProperty("toString"));   //true
//这就找到了，这里的hasOwnProperty 方法 是检查 该属性是否 是自身的属性

//而 （函数的__proto__）test.__proto__  都指向（等于） Function.prototype
console.log(test.__proto__ === Function.prototype);   //true

console.log(Function.prototype.hasOwnProperty("toString"));   //true
//看到这里，明白了吗。函数的内置方法(函数) 一部分是 Function.prototype 上的属性；
//一部分？ 是的，因为，原型链的终端 在  Object.prototype ;
//所以，在Object.prototype 上添加的属性，方法， 函数也是可以使用的；

//比如：
Object.prototype.say = function() { console.log(5666) };

function test(){};

test.say();   //5666

```

![这里写图片描述](E:\coder\09_OneNote\image\166a021e11e5c020tplv-t2oaga2asx-zoom-in-crop-mark4536000.webp)

**那么属性的赋值是怎么一回事呢？**

首先函数 或 对象 会查找 **自身属性**， 如果有，就会 **覆盖该属性** 的值， 如果没有，它就会创建 一个 **自身的属性**，总之，赋值是不会对原型链进行**查找**。

```javascript
function Person(){};
var p = new Person();
//如果你用的同一个窗口运行这个，结果可能是上面的 5666，因为刚刚更改了该函数，您重新打开个浏览器窗口即可。
p.toString();    //"[object Object]"  

//有疑惑吗，其实，toString 这个方法， Function.prototype, 和 Object.prototype 都有；
Function.prototype.toString = function(){
    console.log("我是Function原型对象的");
}
Person.toString();    //我是Function原型对象的
p.toString();       //"[object Object]"
//Object上的toString 方法并没有改变。

```

### 八、实际代码中 原型链 的运用

运用 最常见的就是 继承了。

```javascript
function Person(name){   //父类（构造函数）
	this.name = name;
}
Person.prototype.getName = function(){   //在父类的原型对象上添加方法
	return this.name;
}

function Son(name,age){    //子类（构造函数）
    this.name = name;    //为了减轻读者压力，就不使用 call 了, Person.call(this, name);
	this.age = age;
}

Son.prototype = new Person();    //把子类（构造函数） 的原型对象  挂到 原型链上去。

Son.prototype.getAge = function(){
	return this.age;
}
var s = new Son("zdx",666);
s.getName();    //Son.prototype 上没有 getName方法，现在能使用了，就完成了 继承。

```

需要解读一下嘛？

```ini
Son.prototype = new Person();

//就等于
var obj = {};
obj.__proto__ = Person.prototype;
Son.prototype = obj;
//这样,就把Son.prototype 挂到原型链上去了。
Son.prototype.__proto__ === Person.prototype  //ture

```

**然后Son 的实例对象  上使用方法 时，就沿着链查找， Son.prototype 没有， 上级Person.prototype 上有。ok，继承了。** ![继承](E:\coder\09_OneNote\image\166a021e1221ef40tplv-t2oaga2asx-zoom-in-crop-mark4536000.webp)



### 九、解读jq 的原型链

简单写一个：

```javascript
var jQuery = function(name) {
    return new jQuery.fn.init();
}

jQuery.fn = jQuery.prototype = {
    constructor: jQuery,
    init: function(name) {
        this.name = name;
    },
    each: function() {
        console.log('each');
        return this;
    }
}

jQuery.fn.init.prototype = jQuery.fn;


```

估计看起来有点困难，没事，我们简化一下

```javascript
function jQuery(name){
	return new init(name);
}

function init(name){
	this.name = name;
}

jQuery.prototype = {
    constructor: jQuery,
	each: function(){ 
	    console.log('each')
	}
}

init.prototype = jQuery.prototype;


```

看懂了吗，你使用`jQuery()`, 就相当于与  `new jQuery()`； 其实   你 new init()    和   new jQuery(); 是一样的；因为  `init.prototype = jQuery.prototype` ，所以它们的实例对象是一样的。它这样写，就是为了你使用方便，不需要你使用  new 来创建jq对象。

使用起来就是这样的：

```javascript
$();
//是不是比

new $();
//方便多了。

```

![这里写图片描述](E:\coder\09_OneNote\image\166a021ea7252584tplv-t2oaga2asx-zoom-in-crop-mark4536000.webp)

**最后要说的就是，别把原型链和作用域链搞混了！！！哈哈哈**



作者：周大侠啊
链接：https://juejin.cn/post/6844903605607071752
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。