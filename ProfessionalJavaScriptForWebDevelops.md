# 1.2 JavaScript实现

```
ECMAScript
DOM Document Object Model
BOM Browser Object Model
```

## ECMAScript 提供核心语言功能

规定了语法，类型，语句，关键字，保留字，操作符，对象

## DOM -- Document Object Model 文档对象模型 提供访问和操作网页内容的方法和接口



## BOM -- Browser Object Model 浏览器对象模型 提供与浏览器交互的方法和接口

弹出新浏览器窗口
移动、缩放和关闭浏览器窗口
浏览器的详细信息：navigator对象
浏览器所加载页面的详细信息：location对象
用户显示器分辨率的详细信息：screen对象
cookie

# 2.1 <script> 标签元素

例子：
```
    <!DOCTYPE html>
    <html>
        <head>
            <title>网页标题</title>
        </head>
        <body>
            <script src = "./example.js" type = "text/javascript"></script>
        </body>
    </html>
```

属性：
```
    async：表示应该立即下载脚本，但不应妨碍页面中的其他操作，比如下载其他资源或者等待加载其他脚本。只对外部脚本文件有效。即在script属性中有src。
    charset：表示通过src属性的指定的代码的字符集。由于大多数浏览器会忽略它的值，因此该属性很少有人使用。
    defer：表示脚本可以延迟到文档完全被解析和显示之后再执行。只对外部脚本文件有效。
    src：表示包含要执行代码的外部文件。
    type：表示编写代码使用的脚本语言的内容类型（也被称为MIME类型）。
```

通过<script>元素的src属性还可以包含来自外部域的JavaScript脚本文件。
这一点<script>和<img>元素非常相似，即它的src属性可以是指向当前页面所在所在域之外的某个域的完整链接。
利用这一点就可以在必要时通过不同域来提供JavaScript脚本文件。不过，在访问自己不能控制的服务器上的JavaScript脚本文件时则需要多加小心。如果不幸遇到了怀有恶意的程序员，那他们随时都有可能替换该文件中的代码。
可以利用这一点进行跨域操作。

无论如何包含代码，只要不存在defer和async属性，浏览器都会按照<script>元素在页面中出现的先后顺序对它们依次进行解析。


一般将<script>标签放在页面内容的后面，防止页面先将<script>中的内容下载，解析和执行完成之后再开始渲染页面。

## 延迟脚本

<script defer = "defer" type = "text/javascript" src = "./example.js"></script>

## 异步脚本

<script async type = "text/javascript" src = "./example.js"></script>


# 文档模式

DOCTYPE
<!--  HTML5  -->
<!DOCTYPE html>

## 混杂模式

## 标准模式

# <noscript>标签

当
```
浏览器不支持脚本
浏览器支持脚本，但是脚本被禁用。
```
时，会显示其中的内容。

# 数据类型

简单数据类型:
undefined
null
boolean
string
number
复杂数据类型:
function
object

object为空时，是null。function也是object,Array也是object。
number为空时，是Nan（Not A Number）。

### 字符串加减运算操作原理

两个字符串相加，先创建一个能容纳两个字符串之和的空间，然后再按先后顺序将两个字符串填充进去，最后销毁原来的两个字符串。

### 前置递增和递减 与 后置递增和递减 的区别
```
    var num1 = 2;
    var num2 = 2;
    var num3 = 20;
    var num4 = num1-- + num3;  //22
    var num5 = --num2 + num3;  //21
```
#### 递增递减操作符规则：
```
    var s1 = "2";
    var s2 = "z";
    var b = false;
    var f = 1.1;
    var o = {
        valueOf: function () {
            return -1;
        }
    }

    s1++ //3
    s2++ //Nan
    b++  //1
    f--  //0.10000000000000009
    o--  //-2
```

### 布尔操作符

#### !

```
  !false       //true
  !"blue"      //false
  !0           //true
  !Nan         //true
  !""          //true
  !1234        //false
  !!false      //false
  !!"blue"     //true
  !!0          //false
  !!Nan        //false
  !!""         //false
  !!1234       //true
```

#### &&

逻辑与规则:

```
    如果第一个操作数是对象，则返回第二个操作数；
    如果第二个操作数是对象，则只有在第一个操作数的求值结果为true的情况下才会返回该对象；
    如果两个操作数都是对象，则返回第二个操作数；
    如果一个操作数为null，则返回null；
    如果一个操作数为undefined， 则返回undefined；
    如果一个操作数为Nan，则返回Nan。
```

注：逻辑与操作属于短路操作。

短路操作：即第一个操作数可以决定结果，那么就不会再对第二个操作数进行求值。

#### ||

逻辑或规则:
```
   如果第一个操作数是对象，则返回第一个操作数；
   如果第一个操作数的求值结果为false，则返回第二个操作数；
   如果两个操作数都是对象，则返回第一个操作数；
   如果两个操作数都是null，则返回null；
   如果两个操作数都是Nan，则返回Nan；
   如果两个操作数都是undefined，则返回undefined。
```

注：逻辑或操作也属于短路操作。

```
   var object1 = object2 || object3;
```
在上述例子中，如果object2不为null,那么将object2赋值给object1.反之，也就是object2为null,那么就将object3赋值给object1.

#### +

加性操作符规则：
```
   其他的就不多赘述了，就记录一些不是正常情况的。
   +0 + +0    // +0
   -0 + -0    // -0
   +0 + -0    // +0
```

#### -

减性操作符规则：
```
   和加性操作符一样，减性操作符也有一些不是正常情况：
   +0 - +0 // +0
   +0 - -0 // -0
   -0 - -0 // +0
```

#### ==, !=

相等操作符和不相等操作符:
```
   如果有一个操作数是布尔值，则在比较相等性之前先将其转换为数值--false转换为0，true转换为1;
   如果一个操作数是字符串，另一个操作数是数值，在比较相等性之前先将字符串转换为数值；
   如果一个操作数是对象，另一个操作数不是，则调用对象的valueof()方法，用得到的基本类型值按照前面的规则进行比较；

   null 和 undefined 是相等的;
   要比较相等性之前，不能将null和undefined转换为其他任何值。
   如果有一个操作数是NaN，则相等操作符返回false,而不相等操作符返回true。重要提示：即使两个操作数都是NaN，相等操作符也返回false,因为按照规则，NaN不等于NaN。
   如果两个操作数都是对象，则比较他们是不是同一个对象。如果两个操作数都指向同一个对象，则相等操作符返回true；否则，返回false。
```
例子:
```
   null == undefined   // true
   "NaN" == NaN        // false
   5 == NaN            // false
   NaN == NaN          // false
   NaN != NaN          // true
   false == 0          // true
   true == 1           // true
   true == 2           // false
   undefined == 0      // false
   null == 0           // false
   "5" == 5            // true
```

#### ===, !==

全等操作符和不全等操作符：
全等操作符并不会将操作数进行转换，只在两个操作数未经转换就相等的情况下返回true。

由于相等和不相等操作符存在类型转换问题，而为了保持代码中的数据类型的完整性，建议使用全等和不全等操作符。

### 条件操作符

variable = booleanExpression ? trueValue : falseValue;

### 赋值操作符

以下是符合赋值操作符:
```
   +=加赋值
   -=减赋值
   *=乘赋值
   /=除赋值
   %=模赋值|余赋值
   <<=左移赋值
   >>=无符号右移赋值
   >>>=有符号右移赋值
```

### 逗号操作符

使用逗号操作符可以在一条语句中执行多个操作。

```
  var num1 = 1,
      num2 = 2,
      num3 = 3;
```

逗号操作符多用于声明多个变量；逗号操作符还可以用于赋值。
在用于赋值时，逗号操作符总会返回表达式中的最后一项：
```
   var num = ( 0, 1, 2, 3 );
   console.log(num);            // 3
```

## 语句

### if 语句
if语句语法:
```
  if ( condition|条件 ) {
      statement1|语句1
  } else {
      statement2|语句2
  }
```

其中的condition（条件）可以是任意表达式；而且对这个表达式求值的结果不一定是布尔值。ECMAScript会自动调用Boolean()转换函数将这个表达式的结果转换为一个布尔值。如果对condition求值的结果为true,则执行statement1（语句1），如果对condition求值的结果为false,则执行statement2（语句2）。







