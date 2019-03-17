# JavaScript学习笔记

主要学习资源包括廖雪峰博客 &《JavaScript语言精粹》

## 快速入门 ##
JavaScript代码可以直接嵌在网页的任何地方，不过通常我们都把JavaScript代码放到<head>中：<br>
```
<html>
<head>
    <script>
    	alert('Hello World!');
    </script>
</head>
<body>
    ...
</body>
</html>
```
<br>或js文件放在外部，使用```<script src = "/*.js"></script>```引入。
## 基本语法 ##


- 每个语句以；结束（虽不强制使用，但建议如此）

- 语句块用{...}
### 语法 ###
``var x = 1;``
语句块是一组语句的集合，例如，下面的代码先做了一个判断，如果判断成立，将执行{...}中的所有语句：
```
	if(2>1){
	x = 1;
	y = 2;
	z = 3;
	}
```
### 注释 ###


1. 以//开头直到行末的字符视为行注释
```
//这是一行注释
alert('hello!');//这也是注释
```
2. ```/* */```多行注释
```
/*从这里开始块注释
var x = 1;
document.getElementById("demo").innerHTML("Hello!");
注释结束*/
```
> 用```/* */```包围的注释可能存在的安全性风险（如出现在正则表达式中）
> ```
> /*
> var rm_a = /a*/.match(s);
> */
> ```
> 上面的注释导致了一个语法错误。在《JavaScript精粹》一书中作者建议避免使用```/* */```注释而用//注释代替它。

### 大小写 ###
注意，JavaScript严格区分大小写.

## 数据类型和变量 ##

### 数字 ###
JavaScript只有一个数字类型，无论整数还是浮点数在内部均被表示为64位的浮点数。
- NaN 也是一个数值，它表示一个不能产生正常结果的运算结果，它**不等于任何值包括它自己**，不过可以用isNaN()函数检测NaN。所以```NaN === NaN为false,isNaN(NaN)为true```
- Infinity(无穷大)表示大于1.79769313486231570e+308的值
```
123;//整数123
0.456;//浮点数0.456
1.2345e3;//科学计数法表示1.2345x1000，等同于1234.5
-99;//负数
NaN;//无法计算的结果
Infinity;//无穷大，计算溢出
```
- 数字拥有方法。如JavaScript的Math对象，包括数字的一些方法。如，可用Math.floor()方法把浮点数转换为整数。
- 四则运算：+ * / %，其中%为取余。

### 字符串 ###
字符串被包在一对 ' ' 或 " " 中。
- **JavaScript没有字符类型**。要表示一个字符，仅需创建一个包含一个字符的字符串即可。
- **转义字符 ```\```** 用来把哪些正常情况下不允许被插入的字符插入到字符串中。如反斜线、引号和控制字符。\u是指定数学字符编码。
```"A" === "\u0041"```
- **求字符串的长度**，length属性。如 "seven".length是5。
- 通过 **+ 进行字符串连接**。'c' + 'a' + 't' === 'cat'为true
- 一些字符串方法。如小写字母转大写，'cat'.toUpperCase() === 'CAT'

### 数组 ###
数组是一组按顺序排列的集合，JavaScript的数组可以包含任一数据类型。即**JavaScript数组的元素类型是混杂类型。**如：
```
[1, 2, 3.14, 'Hello', null, true];
```
- 也可通过```Array()```函数实现：
```new Array(1, 2, 3);//创建数组[1, 2, 3]```
- 数组的元素可以通过索引来访问，索引的起始值为 0 ：
```
var arr = [1, 2, 3.14, 'hello', null, true];
arr[0];//返回1
arr[5];//返回true
arr[6];//返回undefined
```
- 求数组长度，通过array.length获得
> **注意**：Array.prototype和Object.prototype的区别：
> ```
> var numbers = ['zero', 'one', 'two', 'three', 'four', 'five',
>                'six', 'seven', 'eight', 'nine'];
> var numbers_object = ['0':zero','1':'one', '2':'two', '3':'three', '4':'four',                      
>                       '5':'five', '6':'six',7':'seven',8':'eight','9':'nine'];
> numbers.length; //返回10
> numbers_object.length;//出错
> ```
> 本例中numbers继承自Array.prototype,而numbers_object继承自Object.prototype，所以numbers继承了大量有用的方法。故numbers有length属性，而numbers_Object则没有。
- JavaScript**数组的length是没有上界的**。如果用大于或等于当前length的数字作为下标来存储一个元素，那么length值会被增大以容纳新元素，不会发生数组越界错误。
```
var = myArray = [];
myArray.length; // 返回0
var myArray[10000] = true;
myArray.length; //返回长度为10001
```
- 可以直接设置length的值。设置更大的length不会给数组分配更多的空间。而把length设小将导致所有下标大于等于新length的属性被删除。
```
var numbers = ['zero', 'one', 'two', 'three', 'four', 'five',
               'six', 'seven', 'eight', 'nine'];
numbers.length = 3;//直接将数组长度人为设小
//numbers 是 ['zero', 'one', 'two'],即人为设小长度，则大于等于该长度的元素被删除
```
- 通过把下标指定为一个数组的当前length，可以附加一个新元素到该数组的尾部
```
var numbers = ['zero', 'one', 'two'];
numbers[numbers.length] = 'shi';//尾部添加一个元素，很好的技巧
//numbers 是 ['zero', 'one', 'two', 'shi']
```
- 用push方法也可以更方便地完成数组元素尾插
```
numbers.push('go');
// numbers 是 ['zero', 'one', 'two', 'shi', 'go']
```
- splice方法删除数组元素，删除的元素将被后面的其他元素替换;Array.splice(数组下标，要删除元素个数)
```
numbers.splice(2, 1);
// numbers 是 ['zero', 'one', 'shi', 'go']
```
> 注意： delete方法也可以删除元素，不过被删除的元素会留下一个空洞，不会自动被后面的元素替换
> ```
> var numbers = ['zero', 'one', 'two', 'shi', 'go']
> delete numbers[2]; 
> // numbers 是 ['zero', 'one', undefined, 'shi', 'go']
> ```
- 枚举（遍历）数组：通过for循环
```
var i;
for(i = 0; i < numbers.length; i += 1)
{
	document.writeln(myArray[i]);
}
```
### Map ###
Map是一组键值对的结构，具有极快的查找速度。ES6标准新增数据类型。
- 定义和查找
```
var m = new Map([['Michael',95], ['Bob', 75], ['Tracy', 85]]);
m.get('Michael');//返回95
```
- 初始化和添加元素
```
var m = new Map();	//空Map
m.set('Adm', 67);	//添加新的key-value
m.has('Adam');		//是否存在key 'Adam':true
m.get('Adam');		//67
m.delete('Adam');	//删除key 'Adam'
m.get('Adam');		//undefined
```
### Set ###
Set是一组key的集合，且key不能重复，可以理解为无重复值得数组。ES6标准新增的数据类型。
- 创建
```
var s1 = new Set();//空Set
var s2 = new set([1,2,3]);//含1,2,3
```
- 重复元素在Set中自动被过滤：
```
var s = new Set([1, 2, 3, 3, '3']);
s; // Set {1, 2, 3, "3"}
//注意数字3和字符串'3'是不同的元素。
```
- 通过add(key)方法可以添加元素到Set中，可以重复添加，但不会有效果：
```
s.add(4);
s; // Set {1, 2, 3, 4}
s.add(4);
s; // 仍然是 Set {1, 2, 3, 4}
```
- 通过delete(key)方法可以删除元素：
```
var s = new Set([1, 2, 3]);
s; // Set {1, 2, 3}
s.delete(3);
s; // Set {1, 2}
```
### iterable ###
遍历Array可以采用下标循环，遍历Map和Set就无法使用下标。为了统一集合类型，ES6标准引入了新的iterable类型，Array、Map和Set都属于iterable类型。
具有iterable类型的集合可以通过新的for ... of循环来遍历。
for ... of循环是ES6引入的新的语法，请测试你的浏览器是否支持：
```
'use strict';
var a = [1, 2, 3];
for (var x of a) {
}
```
- 更好的方式是直接使用iterable内置的forEach方法，它接收一个函数，每次迭代就自动回调该函数。以Array为例：
```
'use strict';
var a = ['A', 'B', 'C'];
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
});
```
### 对象 ###
对象是属性的容器，其中每个属性都拥有名字和值。
 
- 一个对象就是包围在一对花括号中的零或多个“名/值”对
```
var empty_object = {};
var stooge = {
	"first_name": "Jerome",
	"last_name": "Howard"
};
```

> 对象的属性值不强制要求用引号括住，如上例中empty_object对象的属性值first_name和last_name可以不加 " " 引号。但注意JavaScript的标识符中包含连接符 - 是不合法的，但允许包含下划线。
- 多个对象可以相互嵌套
```
var flight = {
	airline : "Oceanic",
	number: 815,
	departure:{
		IATA: "SYD",
		time: "2014-09-22 14:55",
		city: "Sydney"
	},
	arrival:{
		IATA: "LAX",
		time: "2004-09-23 10:42"
		city: "Los Angeles"
	}
};
```
- 查找对象中的值


1. 采用在[ ]后缀中括住一个字符串的方式。如果字符串表达式是一个字符串字面量，而且它是一个合法的JavaScript标识符且不是保留字，那么也可以用.表示法代替。
2. 优先考虑使用.表示法，因为它更紧凑且可读性更好。
```
//承上例
stooge["first_name"]; 	//"Jerome"
flight.departure.IATA; 	//"SYD"
```
- 对象里的值可以通过赋值语句来更新
```
stooge['first_name'] = 'Jerome';
```
如果对象之前没有拥有那个属性名，进行新的赋值后那么该属性就被扩充到对象中
```
stooge['middle_name'] = 'Leater';
stooge.nickname = 'Curly';
flight.equipment = {
	model: "Boeing 777"	
};
flight.status = 'overdue';
```
- 引用
对象通过引用来传递。它们永远不会被复制：
```
var x = stooge;
x.nickname = 'Curly';
var nick = stooge.nickname;
	// 因为 x 和 stooge 是指向同一个对象的引用，所以nick 为 'Curly'。    
var a = {}, b = {}, c = {};
	// a、b 和 c 每个都引用一个不同的空对象。
a = b = c = {};
    // a、b 和c 都引用同一个空对象。
```
- 检测对象属性
检查对象并确定对象有什么属性是很容易的事情，只要试着去检索该属性并验证取得的值。typeof操作符对确定属性的类型很有帮助：
```
    typeof flight.number      // 'number'
    typeof flight.status      // 'string'
    typeof flight.arrival     // 'object'
    typeof flight.manifest    // 'undefined'
```
另一个方法是使用hasOwnProperty方法，如果对象拥有独有的属性，它将返回true。hasOwnProperty方法不会检查原型链。
```
    flight.hasOwnProperty('number')      // true
    flight.hasOwnProperty('constructor') // false
```
### 函数 ###
- 定义方式一：
```
function abs(x){
	if(x > 0){
		return x;
	}
	else{
		return -x;
	}
}
```
function指出这是一个函数定义；
abs是函数的名称；
(x)括号内列出函数的参数，多个参数以,分隔；
{ ... }之间的代码是函数体，可以包含若干语句，甚至可以没有任何语句
- 定义方式二
```
var abs = function(x){
	if(x > 0){
		return x;
	}
	else{
		return -x;
	}
};
```
在这种方式下，function (x) { ... }是一个匿名函数，它没有函数名。但是，这个匿名函数赋值给了变量abs，所以，通过变量abs就可以调用该函数。
> 函数也可以被定义在其他函数中，一个内部函数除了可以访问自己的参数和变量，同时也能自由访问把它嵌套在其中的父函数的参数和变量。通过一个函数中创建另一个函数对象包含一个连接到外部上下文的连接，被称为**闭包**。
> **注意**：如果不是某些特定任务需要使用闭包，在其它函数中创建函数是不明智的，因为闭包在处理速度和内存消耗方面对脚本性能具有负面影响。

上述两种定义完全等价，注意第二种方式按照完整语法需要在函数体末尾加一个;表示赋值语句结束。
调用：
```
abs(10);	//返回10
abs(-9);	//返回9
abs(10,'hahahaha');	//返回10，JavaScript允许传入任意多参数不影响调用
abs();		//返回NaN
```
- 函数调用
调用一个函数会暂停当前函数的执行，并传递控制权和参数给新函数。除了声明时定义的形式参数，每个函数还接收两个附加的参数：this和arguments
参数this在面向对象编程中很重要，它的值取决于调用的模式。
JS中共有四种调用模式：方法调用、函数调用、构造器调用、apply调用。不同调用模式在初始化this参数时存在差异。
函数调用时当实际参数（arguments）的个数与形式参数（parameters）的个数不匹配时，不会导致运行时错误。如果实际参数值过多了，超出的参数值会被忽略。如果实际参数值过少，缺失的值会被替换为undefined。对参数值不会进行类型检查：任何类型的值都可以被传递给任何参数。

1.方法调用模式
当**函数被保存为对象的一个属性时**，称之为一个方法。当一个方法被调用时，this被绑定到该对象。如果调用表达式包含一个提取属性的动作（即包含一个.表达式），那么它就是被当做一个方法来调用。
```
//创建 myObject 对象。它有一个 value 属性和一个 increment 方法
// increment 方法接受一个可选的参数。如果参数不是数字，那么默认使用数字1
var myObject = {
	value: 0,
	increment: function (inc){
		this.value += typeof inc === 'number' ? inc : 1;
		}
	};

myObject.increment();
document.writeln(myObject.value); //1

myObject.increment(2);
document.writeln(myObject.value); //3
```
方法可以使用this访问自己所属的对象，所以它能从对象中取值或对对象进行修改。this到对象的绑定发生在调用的时候。这个“超级”延迟绑定（very late binding）使得函数可以对this高度复用。通过this可取得它们所属对象的上下文的方法称为公共方法（public method）。

2.函数调用模式
要指定函数的this指向哪个对象，可以用函数本身的apply方法，它接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是Array，表示函数本身的参数。
```
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}

var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

xiaoming.age(); // 25
getAge.apply(xiaoming, []); // 25, this指向xiaoming, 参数为空
```
- 参数（arguments）
当函数被调用时，会得到一个“免费”配送的参数，那就是arguments数组。函数可以通过此参数访问所有它被调用时传递给它的参数列表，包括那些没有被分配给函数声明时定义的形式参数的多余参数。这使得编写一个无须指定参数个数的函数成为可能：
```
    // 构造一个将大量的值相加的函数。    
    // 注意该函数内部定义的变量 sum 不会与函数外部定义的 sum 产生冲突。
	// 该函数只会看到内部的那个变量。    
    var sum = function ( ) {
       var i, sum = 0;
       for (i = 0; i < arguments.length; i += 1) {
          sum += arguments[i];
       }
       return sum;
    };
    
    document.writeln(sum(4, 8, 15, 16, 23, 42)); // 108
```
因为语言的一个设计错误，arguments并不是一个真正的数组。它只是一个“类似数组（array-like）”的对象。arguments拥有一个length属性，但它没有任何数组的方法。
- 返回
当一个函数被调用时，它从第一个语句开始执行，并在遇到关闭函数体的}时结束。然后函数把控制权交还给调用该函数的程序。
return语句可用来使函数提前返回。当return被执行时，函数立即返回而不再执行余下的语句。
一个函数总是会返回一个值。如果没有指定返回值，则返回undefined。
如果函数调用时在前面加上了new前缀，且返回值不是一个对象，则返回this（该新对象）。

- 异常
JavaScript提供了一套异常处理机制。异常是干扰程序的正常流程的不寻常（但并非完全是出乎意料的）的事故。当发现这样的事故时，你的程序应该抛出一个异常：
```
    var add = function (a, b) {
       if (typeof a !== 'number' || typeof b !== 'number') {
         throw {
            name: 'TypeError',
            message: 'add needs numbers'
         }
       }
       return a + b;
    }
```
throw语句中断函数的执行。它应该抛出一个exception对象，该对象包含一个用来识别异常类型的name属性和一个描述性的message属性。你也可以添加其他的属性。
该exception对象将被传递到一个try语句的catch从句：
```
    // 构造一个 try_it 函数，以不正确的方式调用之前的 add 函数。
    
    var try_it = function ( ) {
       try {
          add("seven");
       } catch (e) {
          document.writeln(e.name + ': ' + e.message);
       }
    }
    
    try_it( );
```
如果在try代码块内抛出了一个异常，控制权就会跳转到它的catch从句。
一个try语句只会有一个捕获所有异常的catch代码块。如果你的处理手段取决于异常的类型，那么异常处理器必须检查异常对象的name属性来确定异常的类型。
### 箭头函数 ###
ES6标准新增函数。
```
x => x * x
```
上面的箭头函数相当于
```
function(x){
	return x * x;
}
```
当包含多条语句时，不能省略{...}和return：
```
x => {
	if(x > 0){
		return x * x;
	}
	else{
		return -x * x;
	}
}
```
如果参数不是一个，需要用括号()括起来：
```
(x, y) => x * x + y * y;
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}
```
### 标准对象 ###
1.Date
```
在JavaScript中，Date对象用来表示日期和时间。
要获取系统当前时间，用：
var now = new Date();
now; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
now.getFullYear(); // 2015, 年份
now.getMonth(); // 5, 月份，注意月份范围是0~11，5表示六月
now.getDate(); // 24, 表示24号
now.getDay(); // 3, 表示星期三
now.getHours(); // 19, 24小时制
now.getMinutes(); // 49, 分钟
now.getSeconds(); // 22, 秒
now.getMilliseconds(); // 875, 毫秒数
now.getTime(); // 1435146562875, 以number形式表示的时间戳
```
2.RegExp正则表达式
略
3.JSON
JSON字符集必须是UTF-8。
为了统一解析，JSON的字符串规定必须用双引号""，Object的键也必须用双引号""。
JavaScript内置了JSON的解析，可以直接使用JSON
- 序列化
```
'use strict';
var xiaoming = {
    name: '小明',
    age: 14,
    gender: true,
    height: 1.65,
    grade: null,
    'middle-school': '\"W3C\" Middle School',
    skills: ['JavaScript', 'Java', 'Python', 'Lisp']
};
var s = JSON.stringify(xiaoming);
console.log(s);
//{"name":"小明","age":14,"gender":true,"height":1.65,"grade":null,"middle-school":"\"W3C\" Middle School","skills":["JavaScript","Java","Python","Lisp"]}
```
- 反序列化
拿到一个JSON格式的字符串，我们直接用JSON.parse()把它变成一个JavaScript对象：
```
JSON.parse('[1,2,3,true]'); // [1, 2, 3, true]
JSON.parse('{"name":"小明","age":14}'); // Object {name: '小明', age: 14}
JSON.parse('true'); // true
JSON.parse('123.45'); // 123.45
```
### 浏览器对象 ###
1.window
表示浏览器的窗口。
   有innerWidth和innerHeight这两个属性。可以获取浏览器的内部宽高。

   window.innerWidth;
   window.innerHeight;

   对应的还有outWidth和outHeight这两个属性，获取浏览器窗口的整体的宽高。
   window.outWidth;
   window.outHeight;

2.navigator
表示浏览器信息。
navigator.appName:浏览器名称；
navigator.appVersion:浏览器版本
navigator.language:浏览器设置的语言
navigator.platform：操作系统类型；
navigator.userAgent:浏览器设定的Use-Agent字符串

3.screen
表示屏幕信息。
screen.width; //屏幕宽度
screen.height;  //屏幕宽度
screen.colorDepth;  //颜色位数

4.location
表示当前页面的URL信息。
location.href;  //获取当前页面URL整体信息

5.document
表示当前的页面信息。
还可以获取当前页面的Cookie信息。
document.cookie;

6.history
表示页面的历史纪录。
但在任何情况下不使用该对象。
### 操作DOM ###
- 更新DOM
'use strict';
// 获取<p>javascript</p>节点:
var js = document.getElementById('test-js');
// 修改文本为JavaScript:
// TODO:
js.innerHTML = 'JavaScript';
// 修改CSS为: color: #ff0000, font-weight: bold
// TODO:
js.style.color = '#ff0000';
js.style.fontWeight = 'bold';
- 插入DOM
```
<!-- HTML结构 -->
<p id="js">JavaScript</p>
<div id="list">
    <p id="java">Java</p>
    <p id="python">Python</p>
    <p id="scheme">Scheme</p>
</div>
//把<p id="js">JavaScript</p>添加到<div id="list">的最后一项：
var
    js = document.getElementById('js'),
    list = document.getElementById('list');
list.appendChild(js);
//现在，HTML结构变成了这样：
<!-- HTML结构 -->
<div id="list">
    <p id="java">Java</p>
    <p id="python">Python</p>
    <p id="scheme">Scheme</p>
    <p id="js">JavaScript</p>
</div>
```
从零创建一个新的节点，然后插入到指定位置：
```
var
    list = document.getElementById('list'),
    haskell = document.createElement('p');
haskell.id = 'haskell';
haskell.innerText = 'Haskell';
list.appendChild(haskell);
//这样我们就动态添加了一个新的节点：
<!-- HTML结构 -->
<div id="list">
    <p id="java">Java</p>
    <p id="python">Python</p>
    <p id="scheme">Scheme</p>
    <p id="haskell">Haskell</p>
</div>
```
- 删除DOM
要删除一个节点，首先要获得该节点本身以及它的父节点，然后，调用父节点的removeChild把自己删掉：
```
// 拿到待删除节点:
var self = document.getElementById('to-be-removed');
// 拿到父节点:
var parent = self.parentElement;
// 删除:
var removed = parent.removeChild(self);
removed === self; // true
```
