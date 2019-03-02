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








