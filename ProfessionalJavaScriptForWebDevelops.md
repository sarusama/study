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

### do-while 语句

do-while语句是一种后测试语句，即只有在循环体中的代码执行之后，才会测试出口条件。换句话说，在对条件表达式求值之前，循环体内的代码至少会被执行一次。

```
  do {
      statement|语句
  } while ( expression|表达式 )
```

### while 语句

while语句属于前测试语句,也就是说，在循环体内的代码在被执行之前，就会对出口条件求值。因此循环体内的代码有可能永远不会被执行。
```
  while ( expression|表达式 ) {
      statement|语句
  }
```

### for 语句

for语句属于前测试循环语句，但它具有在执行循环之前初始化变量和定义循环后要执行的代码的能力。

```
  for (initialization|初始化; expression|表达式; post-loop-expression|循环后表达式) {
      statement|语句
  }
```

### for-in 语句

for-in语句是一种精准的迭代语句，可以用来枚举对象的属性。

```
   for ( property|属性 in expression|表达式 ) {
       statement|语句
   }
```

### label 语句

label语句可以在代码中添加标签，以便将来使用。
```
    label|标签: statement|语句
```

### break 和 continue 语句

break和continue语句用于在循环中精确的控制代码的执行。
break语句会立即退出循环，强制继续执行循环后面的语句。
continue语句虽然也是立即退出循环，但退出循环后会从循环的顶部继续执行。

### with 语句

with语句的作用是将代码的作用域设置到一个特定的对象中。

```
  with ( expression|表达式 ) {
      statement|语句
  }
  example:
  source code: {
    let hostname = window.location.hostname;
    let url = window.location.href;
  }
  use "with": {
      with ( window.location ) {
          let hostname = hostname;
          url = href;
      }
  }
```
由于大量使用with语句会导致性能下降，同时也会给调试代码造成困难，因此在开发大型应用程序时，不建议使用with语句。

### switch 语句

switch语句与if语句的关系最为密切，而且也是在其他语言中普遍使用的一种流控制语句。
```
    switch ( expression|表达式 ) {
        case value|值:
            statement|语句;
            break;
        default:
            statement|语句:
            break;
    }
```
switch语句中的每一种情形（case）的含义是：如果表达式等于这个值（value），则执行后面的语句（statement）。而break关键字会导致代码执行流跳出switch语句。如果省略break关键字，就会导致执行完当前case后，继续执行下一个case。最后的default关键字则用于在表达式不匹配前面任何一种情形的时候，执行机动代码。

其将按照代码从上往下的顺序进行执行语句，比如：
```
    switch ( 1 ) {
        case 2: 
            console.log(2);
            break;
        case 0:
            console.log(0);
            break;
        case 1:
            console.log(1);
        default:
            console.log("default");
            break;
    }
    /// 1 "default"

    switch ( 1 ) {
        case 2: 
            console.log(2);
            break;
        case 1:
            console.log(1);
        case 0:
            console.log(0);
            break;
        default:
            console.log("default");
            break;
    }
    // 1 0
```

注：switch语句在比较值时使用的是全等操作符。

```
    switch ( 1 ) {
        case "1":
            console.log("1");
            break;
        default:
            console.log("default");
            break;
    }
    /// "default"
```

## 函数
函数对任何语言来说都是一个核心的概念。通过函数可以封装任意多条语句，而且可以在任何地方、任何时间调用执行。
ECMAScript中的函数使用function关键字来声明，后跟一组参数以及函数体。
```
function functionName|函数名 ( argv0|参数0, argv1|参数1,..., argvN|参数N ) {
    statements|语句
}
var functionName|函数名 = function ( argv0|参数0, argv1|参数1,..., argvN|参数N ) {
    statements|语句
}
```

函数名也可以省略，变成匿名函数:
```
function ( argv0|参数0, argv1|参数1,..., argvN|参数N ) {
    statements|语句
};
```

ES6中加入了箭头函数：
箭头函数表达式的语法比函数表达式更简洁，并且没有自己的this, arguments, super, new.target。
箭头函数表达式更适用于那些本来需要匿名函数的地方，并且它们不能用作构造函数。
```
//  基础语法
var functionName|函数名 = ( argv0|参数0, argv1|参数1,..., argvN|参数N ) => {
    statements|语句
}
let functionName|函数名 = ( argv0|参数0,argv1|参数1,..., argvN|参数N ) => {
    statements|语句
}
( argv0|参数0, argv1|参数1,..., argvN|参数N ) => {
    statements|语句
}
当函数体为一个表达式时：
( argv0|参数0, argv1|参数1,..., argvN|参数N ) => expression|表达式
( argv0|参数0, argv1|参数1,..., argvN|参数N ) => {
    return expression|表达式
}
当参数数目为一时：
( argv0|参数0 ) => {
    statements|语句
}
argv0|参数0 => {
    statements|语句
}
没参数时，需要加上小括号：
() => {
    statements|语句
}
//  高级语法
todoList: 箭头函数高级语法
//  加括号的函数体返回对象字面表达式
( argv0|参数0 ) => ( { foo: bar } )
//  相当于
( argv0|参数0 ) => {
    return {
        foo: bar
    }
}

//  支持剩余参数和默认参数
( argv0|参数0, argv1|参数1, ...rest|剩下的 ) => {
    statements|语句
}
( argv0|参数0 = default0|默认值0, argv1|参数1 = default1|默认1,..., argvN|参数N = defaultN|默认值N ) => {
    statements|语句
}
//  支持参数结构
let f = ( [a, b] = [1, 2], { x: c } = { x: a + b } ) => a + b + c;
f() //  6
```
箭头函数与普通函数的区别：
* 更简短的函数并且不绑定this
* 在箭头函数出现之前，每个新定义的函数都有它自己的this值（在构造函数的情况下是一个新对象，在严格模式的函数调用中为undefined，如果该函数被作为“对象方法”调用则为基础对象等）。
```
与严格模式的关系：
鉴于this是词法层次上的，严格模式中与this相关的规则都会被忽略。
通过call和apply调用:
由于箭头函数没有自己的this指针，通过call()和apply()方法调用一个函数时，只能传递参数，他们的第一个参数会被忽略。
例：
`
var adder = {
    base : 1,
    add : function(a) {
        var f = v => v + this.base;
        return f(a);
    },
    addThruCall: function(a) {
        var f = v => v + this.base;
        var b = {
            base : 2
        };   
        return f.call(b, a);
    }
};
console.log(adder.add(1));         // 输出 2
console.log(adder.addThruCall(1)); // 仍然输出 2（而不是3）
`
```
* 不绑定arguments
```
箭头函数不绑定Arguments对象。因此，在本示例中，arguments只是引用了封闭作用域内的arguments:
`
var arguments = [1, 2, 3];
var arr = () => arguments[0];

arr(); // 1

function foo(n) {
    var f = () => arguments[0] + n; // 隐式绑定 foo 函数的 arguments 对象. arguments[0] 是 n
    return f();
}

foo(1); // 2
`
在大多数情况下，使用剩余参数是相较使用arguments对象的更好选择。
`
function foo(arg) { 
    var f = (...args) => args[0]; 
    return f(arg); 
}
foo(1); // 1

function foo(arg1, arg2) { 
    var f = (...args) => args[1]; 
    return f(arg1,arg2); 
} 
foo(1,2);  //2
`
```
* 箭头函数表达式对非方法函数是最合适的。
* 箭头函数不能用作构造器，和new一起使用会抛出错误。
* 箭头函数没有proptype属性。
* yield关键字通常不能在箭头函数中使用（除非是嵌套在允许使用的函数内）。因此，箭头函数不能用作生成器。
* 箭头函数在参数和箭头之间不能换行。
* 箭头函数解析顺序
```
let callback = undefined;
callback = callback || function () {};
// no Error
callback = callback || () => {};
// error
callback = callback || (() => {});
// no Error
```

箭头函数体：
```
let functionName = ( argv ) => argv + argv;
let functionName = ( argv ) => {
    return argv + argv;
}
```
返回对象字面量：
```
记住用params => { object: literal } 这种简单的语法返回对象字面量是行不通的。
如需返回对象字面量，需要将式子改为
params => ({ object: literal })
```

箭头函数例子：
```
// 空的箭头函数返回 undefined
let empty = () => {};

(() => 'foobar')(); 
// Returns "foobar"
// (这是一个立即执行函数表达式,可参阅 'IIFE'术语表) 

// 三元运算符
var simple = a => a > 15 ? 15 : a; 
simple(16); // 15
simple(10); // 10

let max = (a, b) => a > b ? a : b;

// Easy array filtering, mapping, ...
var arr = [5, 6, 13, 0, 1, 18, 23];

var sum = arr.reduce((a, b) => a + b);  
// 66

var even = arr.filter(v => v % 2 == 0); 
// [6, 0, 18]

var double = arr.map(v => v * 2);       
// [10, 12, 26, 0, 2, 36, 46]

// 更简明的promise链
promise.then(a => {
  // ...
}).then(b => {
  // ...
});

// 无参数箭头函数在视觉上容易分析
setTimeout( () => {
  console.log('I happen sooner');
  setTimeout( () => {
    // deeper code
    console.log('I happen later');
  }, 1000);
}, 1000);
```

箭头函数内定义的变量及其作用域
```
// 常规写法
var greeting = () => {
    let now = new Date(); 
    return ("Good" + ((now.getHours() > 17) ? " evening." : " day."));
}
greeting();          //"Good day."
console.log(now);    // ReferenceError: now is not defined 标准的let作用域

// 参数括号内定义的变量是局部变量（默认参数）
var greeting = ( now = new Date() ) => "Good" + (now.getHours() > 17 ? " evening." : " day.");
greeting();          //"Good day."
console.log(now);    // ReferenceError: now is not defined

// 对比：函数体内{}不使用var定义的变量是全局变量
var greeting = () => {
    now = new Date(); 
    return ("Good" + ((now.getHours() > 17) ? " evening." : " day."));
}
greeting();           //"Good day."
console.log(now);     // Fri Dec 22 2017 10:01:00 GMT+0800 (中国标准时间)

// 对比：函数体内{} 用var定义的变量是局部变量
var greeting = () => {
    var now = new Date(); 
    return ("Good" + ((now.getHours() > 17) ? " evening." : " day."));
}
greeting(); //"Good day."
console.log(now);    // ReferenceError: now is not defined
```

箭头函数也可以使用闭包：
```
// 标准的闭包函数
function A () {
    var i = 0;
    return function b () {
        return ( ++i );
    };
};

var v = A();
v();    //1
v();    //2


//箭头函数体的闭包（ i=0 是默认参数）
var Add = ( i = 0 ) => {
    return ( () => ( ++i ) );
};
var v = Add();
v();           //1
v();           //2

//因为仅有一个返回，return 及括号（）也可以省略
var Add = ( i = 0 ) => () => ( ++i );
```

箭头函数递归:
```
var fact = (x) => ( x == 0 ?  1 : x * fact( --x ) );
fact(5);       // 120
```

** 推荐的做法是要么让函数始终都返回值，要么永远都不要返回值。否则，如果函数有时候返回值，有时候不返回值，会给调试代码带来不便 **

严格模式下对函数有一些限制：
- 不能将函数命名为eval或arguments;
- 不能将参数命名为eval或arguments;
- 不能出现两个命名参数同名的情况。







