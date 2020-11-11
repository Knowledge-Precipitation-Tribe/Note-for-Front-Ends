## ECMAScript6

### ES6简介

ECMAScript发展历史：

ES1.0 => 1997	ES2.0 => 1998	ES3.0 => 1999	ES4.0 => 2007	ES3.1=>2008	ES5=>2009	ES6=>2015

ES2016		(ES7)=>2016	ES2017=>2017	ES2018=>2018......<br>

&emsp;&emsp;由于ES每年新增的特性非常之多，所以开始以年为单位，定义其版本，从ES6开始，吸取了ES4失败的教训，没有强制浏览器实现这些语法，而是将这些语法编译成ES5（ES3.1）版本，这样浏览器就支持了。所以ES6受到各大浏览器厂商广泛的认可，并开始实现其语法，因此好的浏览器就能支持90%以上的语法了，所以很多语法可以直接用浏览器测试。ES6着眼于未来，是为企业大型项目的开发而设计的。由于还有很多浏览器（IE6,7,8）没有实现ES6语法，所以我们要编译ES6，<font color=red>ES6支持面向对象编程方式</font>(class, extends关键字)，但是又保留了弱类型语言，动态语言的特征。<br>

&emsp;&emsp;ECMA组织为了让制定的规范被编译成可被浏览器支持的版本，<font color=red>提供了babel编译库，ES每次发布版本，babel都会更新一个版本，</font>在新版本中提供的功能，通过babel拓展来实现编译。<br>

&emsp;&emsp;<font color=red>在node.js端，在6.0版本之后，开始支持ES6，所以我们可以在的node课程中直接使用ES6了。(以后node.js中使用ES6开发。)</font><br>

&emsp;&emsp;<font color=red>在浏览器端，为了兼容更多的浏览器，我们需要将ES6的代码，编译成浏览器支持的版本。（可以使用ES6语法，但最终还是会被编译成ES5语法来兼容更多的浏览器）</font><br>

注：当前的语法浏览器支持，因此可以用浏览器直接测试。

### 1.let关键字

用来定义<font color=red>块作用域变量</font>的<br>

&emsp;&emsp;var定义函数级作用域变量<br>

&emsp;&emsp;&emsp;&emsp;在函数内部定义的变量，外部无法访问。<br>

&emsp;&emsp;&emsp;&emsp;在代码块(if , for等)中定义的变量，外部可以访问。<br>

&emsp;&emsp;let 定义代码块作用域变量的：<br>

&emsp;&emsp;&emsp;&emsp;在函数内部定义的变量，外部无法访问。<br>

&emsp;&emsp;&emsp;&emsp;在代码块（if, for等）中定义的变量，外部仍然无法访问。<br>

<font color=red>let与var比较(在工作中建议使用let)：</font><br>

作用域：	var函数级作用域		let块级作用域<br>

重复定义：var可以重复定义变量	let不可以重复定义变量<br>

```javascript
var color = 'red';
var color = 'green';
//而
let color = 'red';
let color = 'green';//报错，这是let的优点，因为重复定义并不好
```

声明前置: var支持声明前置		let不支持声明前置（即不能在变量的声明前访问变量）

for循环中存储数据：var 不能存储数据	let可以存储数据

```javascript
//循环中存储数据
var arr = []
for(var i=0;i<5;i++){
    arr[i] = function(){
        console.log(i);
    }
}
arr[3]()//输出结果为5，因为i是函数级作用域，在上面的循环结束后i变成了5.
//应该改成(利用闭包存储数据)
for(var i=0;i<5;i++){
    arr[i] = (function(i){
        return function(){
        console.log(i);
    }
    })(i)
}
```

```javascript
//循环中存储数据
var arr = []
for(let i=0;i<5;i++){
    arr[i] = function(){
        console.log(i);
    }
}
arr[3]()//输出结果为3,因为i是块级变量，每次循环就是一个块。
```

被window挂载：var 可以被挂载		let不能被挂载

```javascript
//window挂载
var a = 10;
let b = 20;
console.log(window.a)//输出：10；
console.log(window.b)//输出：undefined；
```

### 2.const关键字

const关键字是用于定义常量（一旦定义无法改变的变量，通常是表示一些固定不变的数据，例如Math.PI）。<br>

&emsp;&emsp;使用const关键字的特点：<br>

&emsp;&emsp;&emsp;&emsp;1.无法被修改	<font color=red>2.支持块作用域</font>	3.无法重复定义	4.无法声明前置	5.不能被window挂载	6.不能作为for循环中的变量使用	7.值只能是值类型，如果是引用类型则可以被修改。<br>

工作中，通常是将用大写字母表示，并且横线分割单词，常用于定义配置量。<br>

<font color=red>在ES5中，我们可以通过冻结对象技术，或者设置writable:false特性，来模拟静态变量。但问题是：值如果是引用类型依然会被修改。</font>

<font color=red>在ES3.1中，我们可以通过单例模式来模拟静态变量。在方法中只定义取值方法，而不定义赋值方法即可。</font>

### 3.字符串拓展

#### 多行字符串

单行字符串：由一组单引号或者双引号定义的字符串<br>

&emsp;&emsp;单行字符串的问题：<br>

&emsp;&emsp;&emsp;1.单行字符串不能换行		2.一些特殊的按键要使用转义字符\n  <br>

&emsp;&emsp;&emsp;3.一些特殊的字符要使用转义字符\x20		4.字符串标志符号不能直接嵌套（''不能嵌套''，“”不能嵌套“”）<br>

&emsp;&emsp;&emsp;单引号中不能直接写单引号，要转义\'		双引号中不能直接写双引号，要转义\"  ......

ES6为了解决单行字符串中的问题，提供了多行字符串<br>

&emsp;&emsp;通过\`定义，在多行字符串中，只有 \`需要转义\\'，其他的字符，都可以直接书写。<br>

```javascript
//多行字符串
var str = `hello
""d''dafda4314\``;
```

&emsp;&emsp;并且ES6多行字符串支持插值语法：${key}<br>

&emsp;&emsp;${}提供了js环境，因此我们可以js表达式<br>

&emsp;&emsp;ES6的插值语法，让其他框架的插值语法的重要性，大打折扣。<br>

```javascript
//数据
let size = {
    width: 10,
    height: 20
}
var str = `面积：${size.width}*${size.height}=${size.width*size.height}`;//结果：面积：10*20=200
```

<font color=red>插值语法处理视图模板</font>

```javascript
<div id = 'app'></div>

var app = document.getElementById('app')

//数据
let data =[
    {
    	title:'1313',
        type:'推荐'
    }，
    {
    	title:'1313',
        type:'推荐'
    }，
    {
    	title:'1313',
        type:'推荐'
    }
  ]
  //定义字符串
  let html = '';
//遍历数据
for(let i = 0;i<data.length;i++){
    //字符串拼接
    html + = `<li><span>${data[i].title}</span><span>${data[i].type}</span></li>`
}
app.innerHTML = html
```

#### 原始字符串

在使用转义字符之后，并且在浏览器查看的时候，我们只能看到结果，不能看到原始完整的字符串（包含转义字符），于是ES6中拓展了String.raw方法，用于查看完整的原始字符串。<br>

&emsp;&emsp;使用方式：String.raw``<br>

参数通过多行字符串的形式传递，字符串中的转义字符串不会被转义。<br>

```javascript
//转义字符
let  str1 = `hello\nic\nkt`;
console.log(str1)
//输出:
//hello
//ic
//kt

//原始字符串
let str2 = String.raw`hello\nic\nkt`
console.log(str2)//输出: hello\nic\nkt
```

<font color=red>转义字符是一个整体，要匹配就应该匹配整体</font>

```javascript
//转义字符
let  str1 = `hello\nic\nkt`;
//不让\n生效，要改成\\n
//  \n转义字符是一个整体，要匹配该整体
console.log(str1.replace(/\n/g,'\\n'));
```

#### 重复字符串

ES6中拓展了repeat方法用于重复输出字符串<br>

&emsp;&emsp;参数就是要重复的次数<br>

&emsp;&emsp;返回值就是重复的结果<br>

&emsp;&emsp;<font color=red>对原字符串没有影响</font>

```javascript
let str = `hello ||`;
console.log(str.repeat(3))//输出: hello ||hello ||hello ||
```

实现：

```javascript
let str = `hello ||`;
//实现repeat
String.prototype.icktRepeat = function(num){
    //this代指字符串
    //定义结果字符串
    var result = ``;
    //循环拼接
    for(var i = 0;i<num;i++){
        resut +=this;
    }
    //返回结果
    return result;
}
console.log(str.icktRepeat(3))//输出: hello ||hello ||hello ||
```

#### 判断字符串位置

startsWith(str, pos)	是否以参数字符串开头<br>

&emsp;&emsp;截取<font color=red>后面</font>的部分，并且<font color=red>包含</font>截取位置字符<br>

&emsp;&emsp;str	参数字符串（子字符串）<br>

&emsp;&emsp;pos	字符串截取位置<br>

&emsp;&emsp;返回值都是布尔值<br>

```javascript
//定义字符串
let str =  "这是一个神奇的网站-我们的"；
//判断开头
console.log(str.startsWith('这是'))；//true
//截取后面的部分，并且包含截取位置字符
console.log(str.startsWith('我们',10))；//true
console.log(str.startsWith('我们',9))；//false
```

endsWith(str, pos)	是否以参数字符串结尾<br>

&emsp;&emsp;截取<font color=red>前面</font>的部分，并且<font color=red>不包含</font>截取位置字符<br>

includes(str, pos)	是否包含参数字符串<br>

&emsp;&emsp;截取<font color=red>后面</font>的部分，并且<font color=red>包含</font>截取位置字符<br>

### 4.数组拓展

#### isNaN

ES6中为数字拓展了几个方法：isNaN, isFinite, isInteger<br>

全局中有一个isNaN方法



