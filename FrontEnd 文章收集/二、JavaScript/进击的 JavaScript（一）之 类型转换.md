### 说起 js 类型转换，都是头疼吧，晕晕的，但是不行啊，这东西很重要滴！

## 基础知识

**JavaScript的数据类型分为六种，分别为null, undefined, boolean, string, number, object。**

**object是引用类型，包含数组，其它的五种是基本类型或者是原始类型(原始值)。**

**我们可以用typeof方法打印来某个是属于哪个类型的。不同类型的变量比较或者运算，要先转类型，叫做类型转换。**

**注意，`typeof null` 返回 `"object"`，它是一个特殊的对象值，含义是“非对象”。实际上，我们通常认为`null`是自有类型的唯一成员。**





## 一、显式转换

**parseInt()和parseFloat()  字符串转数字**

js提供了`parseInt()`和`parseFloat()`两个转换函数。前者把值转换成整数，后者把值转换成浮点数。只有对String类型调用这些方法，这两个函数才能正确运行；对其他类型返回的都是`NaN(Not a Number)`。

`parseInt()`：

```javascript
parseInt("1234blue");   //1234 
parseInt("0xA");   //10 
parseInt("22.5");   //22 
parseInt("blue");   //NaN

```

`parseInt()`方法还有第二个参数，可以把二进制、八进制、十六进制或其他任何进制的字符串转换成整数。所以要解析十六进制的值，需如下调用`parseInt()`方法：

```javascript
parseInt("AF",   16);   //175 

```

当然，对二进制、八进制，甚至十进制（默认模式），都可以这样调用`parseInt()`方法：

```javascript
parseInt("10",   2);    //2 
parseInt("66",   8);    //54 
parseInt("10",   10);   //10 

```

`parseFloat`字符串转**浮点**数字，**没有第二个参数**。 下面是使用`parseFloat()`方法的示例：

```javascript
parseFloat("1234blue");  //1234.0 
parseFloat("0xA");       //NaN 
parseFloat("22.5");      //22.5 
parseFloat("22.34.5");   //22.34 
parseFloat("0908");      //908 
parseFloat("blue");      //NaN

```

**toFixed()     数字转成字符串**

根据参数保留小数点后几位   会四舍五入，如果无参，默认为0； 例：

```scss
(66.55).toFixed();    //"67"
(66.64).toFixed(1);   //"66.6"

```

**toExponenttial()     数字转成字符串**

根据参数保留小数点后几位   **指数形式**  会四舍五入 这个我不就不举例了，感兴趣的，自己百度下把。

**Number对象的   toString()  方法，  数字转字符串**

根据2  8   16   （范围2  -  36）分别转为二进制   八进制   十六进制字符串,， 不带参，就默认为10，  转十进制。 例：

```scss
(6).toString(2);     //"110"
(66).toString(8);    //"102"
(66).toString(16);   //"42"

```

**下面三个构造函数，当没有使用 new  时，表示类型转换函数，使用new 时，表示转对象（创建一个对应对象），即转换得到的值  创建一个对应的对象。**

**Boolean()**

它会把 “真值”  转为 `true` ， “假值”  转为  `false`。

Boolean()方法的示例：

```scss
Boolean("");               //false   “假值”
Boolean("zdx");            //true    “真值” 
Boolean(66);               //true    “真值” 
Boolean(null);             //false   “假值”
Boolean(0);                //false   “假值”
Boolean(new Object());     //true    “真值” 

```

**Number()**

有以下规律：

1. `false`、`null`、`""`、`[]`，转为0
2. `true` ， 转1
3. **数字**转数字
4. **全是数字的字符串**转数字
5. **数组内全是数字（不能有逗号）**转数字
6. **数组内字符串全是数字（不能有逗号）**转数字
7. 其他都是 `NaN`

大栗子：

```scss
Number(false);            //0 
Number(null);             //0 
Number("");               //0 
Number([]);               //0
Number(true);             //1 
Number("66");             //66 
Number("66f");            //NaN 
Number(new Object());     //NaN 
Number([66]);             //66
Number(["66"]);           //66       
Number([6,6]);            //NaN
Number(["6f6"]);          //NaN

```

**String()**

String()可把任何值转换成字符串。它就是调用**传进参数**的 `toString()`方法。使用`String()`转换成字符串和调用`toString()`方法的唯一不同之处在于，对`null`或`undefined`值转换可以生成字符串而不引 发错误：

String()方法的示例：

```javascript
String(null);            //"null" 

var   null   =   null; 
null.toString();        //报错

```

**Object()**

**这个函数，使用 和  不使用 new  是一样的。**

它会把原始值，根据它的类型，使用对应的构造函数，创建一个对象。`null` 和 `undefined` 和创建一个空对象。

```vbnet
Object(66);           //数字对象，等于  new Number(66)
Object("66");         //字符串对象，等于  new String("666")
Object(true);         //布尔对象， 等于  new Boolean(true)
Object(null);         //空对象，等于 new Object()
Object(undefined);    //空对象，等于 new Object()

```





## 二、隐式转换

### （一）、所有类型  转为 布尔

**JavaScript 的基础类型中   有布尔类型，这个类型的值，只有两个值---- true 和 false**

**任意的JavaScript 的值都可以转换为布尔值。但只有下面这六个值会转为false：**

```javascript
""
0
-0
null
undefined
NaN

```

**其他所有值，包括所有对象（数组）都会转换为 true。布尔值 false，和上面6个能转为false 的值，我们一般称为“假值”，其他值称为“真值”。（“真值”等价true，“假值”等价false）**

**注意！！！在JavaScript 中 ，任何希望使用布尔值的地方，都会将操作数当作 “真假” 或 “假值” 对待（即把“真值”当true，“假值”当false）。这句话你现在不懂没事，看完下面的，或许你就懂了，哈哈。** 
 

### （二）、原始值  转为 数字

**字符串 转 数字**

当字符串里，全为数字时，转数字，其他都为NaN。空字符串就转0

```arduino
+ "666";    //666
+ "66f";    //NaN
+ "";       //0

```

**布尔转数字**

这个比较简单了。 true  转 1；false 转 0；

```arduino
+ true;   //1
+ false;  //

```

**null 转数字**

null 转 0。

```csharp
+ null;        //0

```

**undefined 和 NaN 转数字**

undefined 和 NaN 都转 NaN。

```javascript
+ undefined;   //NaN
+ NaN;         //NaN

```





### （三）、原始值  转为 字符串

这个也比较简单，原始值 到 字符串，就原封不动的转（加个双引号）。

```ruby
"zdx" + true;    //"zdxtrue"

```





### （四）、 引用类型( 对象 )转为 原始值

**对象 转 布尔**

对象  转  布尔   都为  true；等同于  Boolean()

```ini
![];     //false    这里取反了，注意，取反会把操作值转布尔
!{};     //false

```

**对象 转 数字**

对象 转 数字 ，首先调用 `valueOf()`，如果返回的是原始值，再转数字（需要的话），并返回；否则调用 `toString()`， 如果返回的是原始值，再转数字，并返回;否则 抛出一个类型错误。

```vbscript
+ [];    //0
//[].valueOf();   返回数组本身[]，所以调用 [].toString(); 返回 空字符串"",""再转数字 0；
+ (new Date());   //1526008864094
//调用  (new Date()).valueOf(); 返回1526008864094

```

**对象 转 字符串**

对象 转 字符串 ，跟转数字的规则一样。只不过是转字符串。 首先调用 `valueOf()`，如果返回的是原始值，再转**字符串**（需要的话），并返回；否则调用 `toString()`， 如果返回的是原始值，再转**字符串**，并返回;否则 抛出一个类型错误。

```perl
"66" + [];    //"66"
"66" + {};    //"66[object Object]"

```

**总结：对象对原始值，除了布尔类型，其他都是先调用valueOf，然后根据需要调用toString。**

**想知道，js 每个内置对象的`valueOf()`  和  `toString()`方法，可以翻到最下面，`附录`。** 
 

## 三、隐式转换 发生的地方

**隐式转换通常发生在表达式  和  运算符 。**

### （1）加减乘除：

#### 加号 +

##### 二元运算符用法（两个操作数）

可以对数字做加法， 也可以做字符串连接操作。 **当两个操作数 都是 数字 或 字符串时，计算是显然的。其他情况下，有如下规则**

1. 对象转原始值，除了`Date` 对象 直接调用`toString`，其他对象，调用自身的`valueOf` 方法，但有的对象自身没有`valueOf`，或者得到的不是原始值，此时调用`toString`。
2. 第一步转换后，如果其中一个是字符串的话，另一个操作数也转字符串，进行字符串连接。
3. 否则，都转为数字(或者NaN),进行加法。

栗子来了：

```javascript
1 + new Date();     //"1Fri May 11 2018 14:20:50 GMT+0800 (中国标准时间)"

1 + new Number(2);    //3  (new Number).valueOf(); 返回2， 和1 做加法

"66" + 6;       //666    6 转 "6"

1 + {};         //"1[object Object]"   ({}).toString()

true + false;   //1    都转数字

1 + null;       //1    null 转数字

1 + undefined;  //NaN   undefined 转 NaN

```

实际代码中，经常这样

```ini
var x = 66;
x + "";     //"66"    等价于 String(x)

```

**注意：两点！**

1. 不要把对象字面量形式的值放在前面。
2. 从左到右的进行 + 运算。



```perl
//对象字面量形式放在前面的结果比较复杂，不建议使用。（下面的结果不是唯一的）
{} + 1;     //1
{} + "1";   //1
{} + {};    //"[object Object][object Object]"
{x:1} + {};  //NaN

//从左到右，逐个做 + 运算
1 + 2 + "";    //"3"
1 + "" + 2;    //"12"

```

##### 一元运算符用法（一个操作数）

把操作数转换为 **数字（或者NaN），并返回它。**

```javascript
+ "666";       //666   等价于 Number("666")
+ undefined;   //NaN

```

#### 减号 -

都是转数字。

```csharp
- "666";    //-666
- "66f";    //NaN
1 - null;   //1

```

#### 乘号 *

都是转数字

```csharp
1 * "666";     //666
1 * null;      //0

```

#### 除号 /

都是转数字

```arduino
"666" / 1;     //666
1 / true;      //1

```





#### （2）比较运算符 （> < >= <=）

比较运算符用来检测两个操作数（数字或字符串）的大小关系（数值大小或者**字符串首个字符的16位Unicode的大小** ）。

比较运算符的操作数可能是任意类型。但只有数字和字符串才能比较。因此，它会把别的操作数进行类型转换，规则如下：

1. 对象转原始值，如果valueOf()返回原始值，直接比较，否则，调用toString()进行转换。
2. 转原始值后，如果两个操作数都是字符串，那么将按**字符串首个字符的16位Unicode的大小** 进行比较。
3. 否则都转数字比较。Infinity比任何数字都大（除了自身），-Infinity 相反。如果一个操作数是NaN（或转NaN）,结果返回false。

```vbscript
11 < 3;

"11" < "3";   //true    "11" 首个字符串 "1" 的16位Unicode 值比 "3"的16位Unicode 小

//"11".charCodeAt(0).toString(16) 31

//"3".charCodeAt(0).toString(16)  33

"11" < 3;     //false   "11" 转 11，false

{} < 3;       //false   {}转原始值字符串，字符串转NaN， false

null < 3;     //true    null 转数字

```

**最后要注意的是，<=   和  >=  比较时，并不根据 == 和 === 的规则（在下方）比较，它就仅仅表示 数值 或 字符串 之间的比较。**

```javascript
 null >= undefined    //false

```





#### （3）in运算符

**把左操作数转 字符串**

in 运算符希望它的左操作数是一个**字符串或可以转换为字符串**，右操作数是一个**对象**。如果，右侧的对象拥有一个名为左侧操作数值的属性名，那么表达式返回true。

```ini
var point = { x:1, y:2};
"x" in point;    //true  point 有一个 x 的属性名

var arr = [a,b,c];
1 in arr;        //true   数组的索引就相当于 属性名

```





#### （4）！ 和  ！！

**！ 它会把操作值 转为 布尔值（“真值”为true，“假值”为false），对布尔值求反。（结果只有true，false）**

例：

```javascript
console.log(!"");           //true
console.log(!0);            //true
console.log(!-0);           //true
console.log(!null);         //true
console.log(!undefined);    //true
console.log(!NaN);          //true
console.log(!false);        //true

```

**！！ 得到操作值 等价的 布尔值（“真值”为true，“假值”为false）** **等同于 Boolean()，经常称！！ 为强制转换。** 例：

```javascript
console.log(!!"");           //false
console.log(!!0);            //false
console.log(!!-0);           //false
console.log(!!null);         //false
console.log(!!undefined);    //false
console.log(!!NaN);          //false
console.log(!!false);        //false

```

**总结：“假值” 取反都是true， “真值”取反为false；“假值” 强制转换 都是 false， “真值”强制转换为 true**





#### （5）==  和  ===

**都知道 == 是判断 左右值 是否想等的。而 === 不仅判断 右右值是否想等，还要判断，类型是否一样。结果返回布尔值**

**==  的用法** **NaN是JavaScript中唯一一个不等于任何值的（包括它自己）。`(NaN == NaN) // false`**

一般对NaN的判断：

```dart
function isNaN(num){
    return typeof num === "number" && num !== num;
}

```

**注意，跟js 自带的 isNaN 方法 不一样。**

#### 左右两边类型相同

**1、原始值的比较**

它们的比较，就是值的直接比较。 比如：

```ini
console.log(null == null);               //true
console.log(undefined == undefined);     //true
console.log(666 == 666);                 //true
console.log(666 == 1);                   //false
console.log("周大侠啊" == "周大侠啊");      //true
console.log("周大侠啊" == "大佬");         //false
console.log(true == true);               //true
console.log(true == false);              //false

```

**2、对象的比较**

对象和原始值不同，首先，它们是可变的-----它们的值是可修改的：

```ini
var o = { x:1 };   //定义一个对象
o.x = 2;           //修改x的值

var a = [1,2,3];   //数组也是可修改的
a[0] = 0;          //修改数组第一个元素

```

**对象的比较并非值的比较，而是引用（内存地址）的比较。 **

```ini
var o1 = { x:1 };
var o2 = { x:1 };
console.log( o1 == o2 );    //false
//即使 对像的属性，值完全相同， 也不相等

var o3 = o1;
console.log( o1 == o3 );    //true
//o3 和  o1 引用的是同一对象。（即指向的是同一块储存地址）

//数组同上

```



#### 左右两边类型不同

如果 == 两边的 类型不同，则比较时，有以下两个个规则：

1. undefined等于null
2. 其他都转数字比较

**对象通过valueOf 或 toString 转换为原始值，原始值在对应转数字。**

**总结:左右两边类型不同， ==  在比较时，除了(null == undefined)，NaN，其他都是转为数字比较， 从来不会转为布尔值！**

举个大栗子：

```javascript
//1. undefined等于null
undefined == null; //ture

//2. 字符串和数字比较时，字符串转数字
"0" == 0;  //true
"f" == 0;  //false
//字符串转数字时，只有在字符串是纯数字时，转对应数字，其他都转为 NaN。

// 3. 字符串和布尔比较时，都转为数字
"0" == false;   //true
"1" == true;    //true

//4. 数字和布尔比较时，布尔转数字
1 == true;    //true
0 == false;   //true
//true 转 1， false 转0；

//5.对象 和 字符串，数字比较， 都转数字。
new String("66") == "66";      //true
new String("zdx") == "zdx";    //false
new String("66") == 66;        //true

```



### === 的用法

**这个比较，首先，看两边类型是否一致，不一致， 直接false，一致的话，再根据  == 的使用规则， 进行比较。** 
 

#### （6）！=  和  ！==

这两个  运算 跟 取反（！） 操作是 **不一样** 的！，注意区分。

**这两个运算，是在 ==  和  ===  比较过后的结果，进行取反（就是对 true 和 false 取反，因为，==  和  ===  的返回值  只有  true 和 false）。**

简单栗子:

```arduino
"0" == 0;  //true
"f" === 0;  //false

"0" != 0;  //false
"f" !== 0;  //true

```





#### （7）&&、||

**&& 逻辑与**

1. 如果两侧都是布尔值， 进行布尔（AND）运算。
2. 否则它会先计算左侧表达式，如果为 “假值”，返回这个值，如果是“真值”，计算右侧表达式，并返回计算结果。

看：

```csharp
true && false;       //false
1 && 2;              //2
null && 2;           //null
1-1 && 2;            //0
2-1 && 0;            //0

```

所以，有时候就会这样写代码：

```scss
if( a==b ) start();
a == b && start();    //效果同上

```

**|| 逻辑或**

它跟 && 的行为是一样的，只是它的做的是布尔（OR）运算，返回的情况**相反**。

1. 如果两侧都是布尔值， 进行布尔（OR）运算。
2. 否则它会先计算左侧表达式，如果为 “真值”，返回这个值，如果是“假值”，计算右侧表达式，并返回计算结果。

```csharp
true || false;       //true
1 || 2;              //1
null || 2;           //2
1-1 || 2;            //2
2-1 || 0;            //1

```





#### （8）if 语句

它会计算操作数的值，“真值” 表现为true ， “假值” 表现为false。





## 附录

#### 一、Object

**1、valueOf** 返回对象本身。

```scss
({x:1,y:2}).valueOf();    //{x: 1, y: 2},返回的是对象！

```

**2、toString** 返回 "[object type]"，其中type是对象的类型。

```vbnet
//这里使用函数的call方法，指定 this的指向
var toString = Object.prototype.toString;

toString.call(new Date); // [object Date]
toString.call(new String); // [object String]
toString.call(Math); // [object Math]

toString.call(undefined); // [object Undefined]
toString.call(null); // [object Null]

```





#### 二、Boolean

**1、valueOf** 返回布尔值。

```scss
(true).valueOf();    //true , 返回的是原始值，Boolean类型

```

**2、toString** 返回该对象的字符串形式。

```vbscript
(true).toString();     //"true"，返回的是原始值，string类型

```





#### 三、Date

**1、valueOf** 返回存储的时间是从 1970 年 1 月 1 日午夜开始计的毫秒数 UTC。

```javascript
(new Date()).valueOf();    //1525943413141  一串数字

```

**2、toString** 返回一个美式英语日期格式的字符串.

```vbscript
(new Date()).toString();    //"Fri May 11 2018 10:26:16 GMT+0800 (中国标准时间)"  原始值，string类型

```





#### 四、Number

**1、valueOf** 返回数字值。

```scss
(66).valueOf();    //66   返回的是原始值，Number类型

```

**2、toString** 返回的是原始值，String类型 根据2  8   16   （范围2  -  36）分别转为二进制   八进制   十六进制字符串,， 不带参，就默认为10，  转十进制。 例：

```scss
(66).toString(2);    //"1000010"
(66).toString(8);    //"102"
(66).toString(16);   //"42"

```





#### 五、String

**1、valueOf** 返回字符串值。

```perl
("666").valueOf();    //"666"   返回的是原始值，String类型
("zdx").valueOf();    //"zdx"   返回的是原始值，String类型

```

**2、toString** 和valueOf  效果一样，返回字符串值。

```vbscript
("666").toString();    //"666"   返回的是原始值，String类型
("zdx").toString();    //"zdx"   返回的是原始值，String类型

```

------





#### 六、Array

**1、valueOf** 自身没有该方法，继承Object.prototype.valueOf。返回的是数组对象！

```scss
([1,2,3]).valueOf();     //(3) [1, 2, 3]，

```

**2、toString** 返回表示该数组的字符串，跟使用 Array.prototype.join(",")，效果等同

```scss
([1,2,3]).toString();     //"1,2,3",    原始值，string类型
([1,2,3]).join(",");      //"1,2,3",

```





#### 七、Function

**1、valueOf** 自身没有该方法，继承Object.prototype.valueOf。 返回的是函数,使用typeof 返回 function，但注意原始值没有function类型

```javascript
function a(){ console.log(666) };
a.valueOf();    //ƒ a(){ console.log(666) };  

```

**2、toString** 返回当前函数源代码的字符串。

```lua
function a(){ console.log(666) };
a.toString();    //"function a(){ console.log(666) }";返回的是原始值，string类型

```





#### 八、Error

**1、valueOf** 自身没有该方法，继承Object.prototype.valueOf。 返回Error  对象本身

```vbnet
(new Error("fatal error")).valueOf();   //Error: fatal error

```

**2、toString** 返回一个指定的错误对象（Error object）的字符串表示。

```vbscript
var e = new Error("fatal error");
print(e.toString()); // "Error: fatal error"

```

#### 九、Math

它是全局对象， 不属于函数。 **1、valueOf** 自身没有该方法，继承Object.prototype.valueOf。

```javascript
Math.valueOf();     //返回Math 对象本身

```

**2、toString** 自身没有该方法，继承Object.prototype.toString。

```vbscript
Math.toString();    //"[object Math]"

```



![这里写图片描述](E:\coder\09_OneNote\image\1638c2be582196eatplv-t2oaga2asx-zoom-in-crop-mark4536000.png)



作者：周大侠啊
链接：https://juejin.cn/post/6844903605615460365
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
