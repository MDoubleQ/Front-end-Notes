**前面讲完原型链，现在来讲继承，加深理解下。**

## 一、对象的相关知识

什么是对象？ 就是一些无序的 key : value 集合， 这个value 可以是 基本值，函数，对象。(注意 key 和 value 之间 是冒号 **`:`** ,每个 key : value 之间 是逗号 **`,`** )

```kotlin
var person = {
    name: 'zdx',
    age: 18,
    get: function(){
        return '名字：' + this.name + '年纪：' + this.age;
    }
}

```

**这时的 person 就是一个对象**

读取对象的属性，有两种方式：**点** 和  **[' ']**，（使用中括号，里面是有引号的）

```less
person.name   //'zdx'
person['age']    //18

```

之前说过，对象的创建 有三种 方式： 字面量，new，Object.create；

但是，这种简单的创建，并不能满足，我们实际开发的要求。

比如，每个人的名字，年纪不一样，我们不可能，每个人都写一个对象，那不得炸了。

```css
var personA = {
    name: 'A',
    age: 28
}

var personB = {
    name: 'B',
    age: 22
}

```

所以，这时候，我们就需要一些创建模式。



### （一）、工厂模式

工厂模式呢，就是我们写一个**方法**，然后通过这个**方法**复制出我们需要的对象。我们需要多少个，就复制多少个。(注意这里是用**方法（函数）** 来生成对象)

```ini
var createPerson = function(name,age){
    var obj = {},
    obj.name = name,
    obj.age = age
}

```

然后我们就可以这样使用了。

```ini
var personA = createPerson('A', 28);
var personB = createPerson('B', 22);

```

但是呢，这种模式，创建的对象，无法归类。也就是说，并不知道 personA，personB 等 是 属于哪个对象的（哪个构造函数或者类）。

具有相同特性的一类事物，把它总结成一个  **类**；比如，人类，有男人，女人，小孩。把他们总结成了人类。

比如:

```javascript
var obj = {};
obj instanceof Object;    //true
//instanceof  方法 可以判断 前者是否是 后者的实例对象

var arr = [];
arr instanceof Array;    //true

```

于是，构造函数模式来了。



### （二）、构造函数模式（类）

要想知道，男人，女人  属于什么类，  人类？ 兽类？ 这时候就需要  构造函数（类）了。

```javascript
function Person(name, sex){     //注意，我们通常把构造函数（类）的首字母大写！
    this.name = name;
    this.sex = sex;
}
var personA = new Person('张三', '男');
var personB = new Person('李四', '女');

console.log( personA instanceof Person );    //true
console.log( personB instanceof Person );    //true

```

这时候  创建出来的对象，  就知道  它属于哪个构造函数（类）了。



**这里为啥用了 this 呢？new  一个函数， 为啥会创建出 一个实例对象（我们把 new 出来的对象  称为 实例对象，简称实例）呢？**

- 这步，之前的原型链中说过，如果你懂了，可以简单过一眼，增强记忆。

这个呢，就要理解new 到底干了啥呢：

1. 新建一个对象；
2. 将该对象，即实例指向构造函数的原型；
3. 将构造函数的this，指向该新建的对象；
4. 返回该对象，即返回实例。下面，手写一个方法  实现new 的功能。



```javascript
function New(func){    //func 指传进来的构造函数
    var obj = {};   //这里就直接新建一个空对象了，不用new Object了，效果一样的，因为我感觉这里讲实现new的功能   再用 new 就不太好。
    
    if(func.prototype != null){
        obj.__proto__ = func.prototype;
    }
  
    func.apply(obj,Array.prototype.slice.call(arguments, 1));
    //把func构造函数里的this 指向obj对象（你可以理解成func构造函数的this 替换成 obj对象）；
    //Array.prototype.slice.call(arguments, 1)；这个就是把New 函数，func 之后传进来的参数，转成数组。
   //把该参数数组，传入func构造函数里，并执行func构造函数，比如：属性赋值。

    return obj;
    
}

```

**验证下：**

```javascript
function Person(name, sex){
    this.name = name;
    this.sex = sex;
    this.getName = function(){
        return this.name;
    }
}

var p = New(Person,"周大侠啊", "男");

console.log( p.getName() );   //"周大侠啊"

console.log( p instanceof Person );    //true

```



**去掉new  的写法就是这样：**

```ini
function Person(name, sex){
    var obj = {};
    obj.__proto__ = Person.prototype;
    obj.name = name;
    obj.sex = sex;
    obj.getName = function(){
        return obj.name;
    }
    return obj;
}

var p = Person("周大侠啊", "男");

console.log( p.getName() );   //"周大侠啊"

console.log( p instanceof Person );    //true

```



**使用  new   就简化了步骤。**

这种模式，也有弊端，你看出来了吗？  有木有发现，每个实例对象  都有 相同 的 getName 方法，这样，是不是就但占资源了呢，100个实例对象，就新建了  100 个 getName 方法。

原型模式开始！



### （三）、原型模式

之前的原型链说过，属性、方法的**读取**是沿着原型链查找的，也就是说，在构造函数的原型对象上 创建的 属性、方法，它的实例对象都能够使用。

```javascript
function Person(){};
Person.prototype.name = "周大侠啊";
Person.prototype.sex = "男";
Person.prototype.getName  = function(){
    return Person.prototype.name;
}

var p = new Person();
console.log( p.getName() );   //"周大侠啊"
console.log( p.hasOwnProperty("getName") );   //false   getName 不是 p实例的属性

```

这样，创建的实例对象  都能使用  getName  ，并且，也不会给每个实例对象，添加该属性。

不过，你发现了吗，这样创建的实例对象，都是固定的属性值， 一更改，所有的实例对象获取的值，也都改变了。

那么说了半天，这都是啥呢，别急，正因为上面做的铺垫，才有更好的 方法。我觉得，眼尖的同学，可能已经知道了。



**构造函数模式  与  原型模式  相结合的模式。**

构造函数模式，可以创建  每个  实例对象  自己的属性，  而原型模式，可以共享，同一个方法。

所以，我们一般，把对象自己的属性、方法 ，用构造函数模式创建； 公共的方法，用原型模式  创建。

```ini
function Person(name, age){
    this.name = name;
    this.age = age;
}

Person.prototype.getName = function(){
    return this.name;
}

var p = new Person("周大侠啊", 22);
p.getName();

```



这样就可以完美的创建对象了。

要是你有余力，可以想想，这里的 `this.name` 中  `this` 是怎么回事。

但是，上面这个还可以优化，要是 Person.prototype 上有很多方法， 这种写法就很不好，一般，我们用这种写法：

```javascript
function Person(name, age){
    this.name = name;
    this.age = age;
}
//新建一个对象，给该对象添加 方法， 然后把该对象 赋值给Person.prototype ，该对象就成为 Person （构造函数）的原型对象了。

Person.prototype = {
    constructor : Person,   //给新建的对象，添加constructor 属性，建立与构造函数之间的联系。
    getName : function(){
        return this.name;
    },
    getAge : function(){
        return this.age;
    }
}

var p = new Person("周大侠啊", 22);

p.getName();

```



**这里的 this 又看懂是怎么回事了吗？ 那我就简单说一下  this 的知识吧。**

关于 this 估计都听说过  **谁调用它，this就指向谁**，这种说法，不严谨，this 的指向，是 **在函数调用（运行）时确定的**！

上面的:

```ini
Person.prototype = {
    constructor : Person, 
    getName : function(){
        return this.name;
    },
}
var p = new Person("周大侠啊", 22);
p.getName();

```

**`this`  在`getName` 函数里，而`getName` 真正运行  的地方   是  `p.getName`**，p 是调用者，所以， this 就指向 p（换句话说，这时的this   就是 p）。

你要理解 精髓，  **函数调用（运行）时 确定的调用者 之间的关系。**

看这个：

```ini
var a = 10;
var b = {
    a : 20,
    say : function(){
        console.log(this.a);
    }
}

var c = b.say;
c();    //10   非严格模式下，独立调用（无调用者）this 指向全局对象

```

包含 `this` 的函数   正在调用（运行） 的时候  是 `c();` 此时，无调用者，指向全局对象。





## 二、继承

**上面做了辣么多铺垫，终于要开始继承的讲解啦！什么是继承呢，其实呢，就是你 想要使用 别人的属性，或者方法； 这时候就要利用继承来实现。**

既然是 得到别人的属性，方法，就是继承，那么不就是  除了 Object.prototype  其他都是继承了？ dui ！ 你说的没错...哈哈

**所以，继承的一种就是基于 原型链的了 ，就是属性的查找，读取。**

**另一种就是  构造函数继承了。**

**首先来一个需要被继承的目标**

```javascript
//父类：
function Person(name) {
    this.name = name;
}

Person.prototype = {
    constructor: Person,
    getName : function() {
        return this.name;
    }
}

```



### （一）、构造函数的继承

```javascript
//子类：
function Son(name, age) {   
    Person.call(this, name);    //call 方法，把前面函数的this 指向 给定的对象，第二个参数开始，传入 参数，并执行函数。
    this.age = age;
}

//就相当于
function Son(name, age) {
    //Person(name); 此时 Person 里的 this  等于当前的this
    this.age = age;
}

//等同于
function Son(name, age) {
    this.name = name,
    this.age = age
}

```

**下面检验一下：**

```javascript
var s1 = new Son('周大侠啊', 22);
console.log(s1.name);  //'周大侠啊' 
console.log(s1.getName());   //报错，这是Person原型对象上的方法


```



### （二）、原型链的继承

#### 1、通过new一个父类实例

这种是，new 一个父类实例，然后把son.prototype  添加到原型链上去。

```javascript
//new 一个 Person 实例 赋给 Son.prototype
Son.prototype = new Person();

//给子类的原型加方法：
Son.prototype.get = function() {
        return this.name + this.age;
}

```

**上面的 Son.prototype = new Person() 实际上就是这样的**

```ini
//内部就是
var obj = {};

obj.__proto__ = Person.prototype;

Son.prototype = obj

//把 obj 赋给 Son.prototype 。而obj 这个实例  又指向了Person的原型对象，
//这样，Son 就添加到了 Person 的原型链上了。

```



**所以：**

```kotlin
//给子类的原型加方法：
Son.prototype.get = function() {
        return this.name + this.age;
} 

//就是:
obj.get = function(){    //通过给obj添加方法 然后赋值给Son的原型对象
	return this.name + this.age;
};

```

验证：

```javascript
var s2 = new Son('周大侠啊', 22);

console.log(s2.get());  //'周大侠啊22' 

console.log(s2.getName());   //'周大侠啊'

```



#### 2、于是乎，我们就可以自己封装一个继承方法

```javascript
function create(proto, options){     //proto表示父类的原型对象，options表示给子类添加的属性
    var obj = {};
    obj.__proto__ = proto;
    return Object.defineProperties(obj,options);    //Object.defineProperties方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象。所以这里就直接return了
    }
    
//继承  就这样写了
Son.prototype = create(Person.prototype,{
    constructor: {    //这种格式的赋值写法， 是 defineProperties 方法规定的写法。
        value: Son
    },
    get: {
        value: function(){
            return this.name + this.age;
        }
    }
})

//验证一下
var s3 = new Son("zdx",22);

console.log(s3.getName());     //'zdx'

console.log(s3.get());         //'zdx22'

```

Object.defineProperties具体用法点[这里](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2FdefineProperties)



#### 3、ES5中就有个Object.create 方法 它就实现了刚刚封装的create 方法

[这里](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2Fcreate)是它具体用法

可以直接使用它来完成继承：

```javascript
Son.prototype = Object.create(Person.prototype,{
    constructor: {
        value: Son
    },
    get: {
        value: function(){
            return this.name + this.age;
        }
    }
})

//验证一下
var s4 = new Son("zdx",22);

console.log(s4.getName());     //zdx

console.log(s4.get());         //zdx22
```



作者：周大侠啊
链接：https://juejin.cn/post/6844903605615460360
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。