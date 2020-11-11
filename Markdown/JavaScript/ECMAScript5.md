## ECMAScript5

### 1.简介

&emsp;&emsp;javascript最早是由网景公司推出的，极其简单，被很多开发者接受，逐渐流行起来，后来IE为了抢占市场，将IE浏览器内置在windows系统中，所以IE的市场占有率相当的高。IE脚本语言是Jscript(vbscript)。<br>

&emsp;&emsp;网景公司为了推广js，与sun公司合作，为了让js更流行，借助当时极其流行的语言java,将js更名为javascript，所以java与javascript关系就像雷锋与雷峰塔。网景公司做了一件好事，将js的语言规范提交给ECMA组织，所以我们学习ECMAScript规范就是学习javascript规范，所以ECMAScript是js语法的未来。<br>

&emsp;&emsp;微软很有个性，非要研制一套规范，研制的非常不好用，后来自己内部工程师都不干了，非要重新研制新的浏览器，所以微软决定放弃xp系统（放弃IE6,7）。重新研制了IE9浏览器，完全遵循ECMAScript语言规范，所以IE9是微软的第一代高级浏览器（是所有高级浏览器中，最差的一款）。<br>

&emsp;&emsp;在国内，我们还要维护IE6,7,8，原因是国内一些企业决定维护xp系统，所以IE6,7就无法淘汰，所以就苦了国内的前端工程师了，还要维护IE6,7,8。<br>

&emsp;&emsp;好消息是移动端基本都是webkit内核，因此我们可以放心的使用html5,css3，ES5规范等等。<br>

&emsp;&emsp;在pc端，由于高就浏览器都实现了html5,css3,ES5规范等，所以我们可以直接用高级浏览器测试它们。<br>

&emsp;&emsp;ES规范版本ES1，ES2，ES3，ES4，ES3.1，ES5，ES6，ES2016，ES2017，ES2018。<br>



#### JSON--parse

将json字符串解析成js对象的<br>

使用方式：parse(str,fn)<br>

&emsp;&emsp;str处理的字符串<br>

&emsp;&emsp;fn回调函数<br>

&emsp;&emsp;&emsp;&emsp;返回值表示这次处理的结果<br>

&emsp;&emsp;&emsp;&emsp;第一个参数表示属性名称<br>

&emsp;&emsp;&emsp;&emsp;第二个参数表示属性值<br>

&emsp;&emsp;&emsp;&emsp;this指向当前遍历的对象<br>

&emsp;&emsp;<font color=red>是从叶子节点到根节点的方向遍历的，从外部向内部遍历的</font><br>

```javascript
var str = '{"a":1, "b":"2", "c":{"d":4}}';
//解析成对象
//从叶子节点到根节点的方向遍历的，从外部向内部遍历
//遍历顺序,a,b,d,c  因为c不是叶子节点。
var obj = JSON.parse(str, function(key, value){
    //console.log(arguments, this);
    //如果可以转成数字，将其转换
    if(typeof value === 'string'){
        return +value;
    }
    return value;
})
```

#### JSON--stringify

将js对象转换成json字符串<br>

使用方式：stringify(obj, fn)<br>

&emsp;&emsp;obj处理的对象<br>

&emsp;&emsp;fn回调函数<br>

&emsp;&emsp;&emsp;&emsp;返回值表示本次处理的结果<br>

&emsp;&emsp;&emsp;&emsp;第一个参数表示属性名称<br>

&emsp;&emsp;&emsp;&emsp;第二个参数表示属性值<br>

&emsp;&emsp;&emsp;&emsp;作用域是当前遍历的对象<br>

<font color=red>是从根节点到叶子节点的方向遍历的，从内部向外部遍历的</font><br>

```javascript
var obj = {
    a:1,
    b:'2',
    c:{
        d:4
    }
}
//json字符串
//遍历顺序，从根节点到叶子节点的方向遍历的，从内部向外部遍历
//遍历顺序,a,b,c,d
var str = JSON.string(obj, function(key, value){
    if(typeof value ==== 'string'){
        return +value;
    }
    return value;
})
console.log(str)
```

#### 数组--判断数组

第一种方式，判断对象类型是数组<br>

Object.prototype.toString.call(obj)<br>

```javascript
var arr = [];
var obj = {};
console.log(Object.prototype.toString.call(arr));//输出[object Array]
console.log(Object.prototype.toString.call(obj));//输出[object Object]
```



第二种方式，判断构造函数是否是Array<br>

obj.constructor === Array<br>

第三种方式，判断是否是实例化对象<br>

obj instanceof Array<br>

第四种方式，判断数组的静态方法isArray<br>

Array.isArray(obj)<br>



#### 数组--获取数组索引值

ES5为数组拓展了两种方法：indexOf, lastIndexOf来获取数组成员的索引值<br>

&emsp;&emsp;参数就是这个成员，返回值就是索引值，如果成员存在，返回索引值（大于等于0），如果成员不存在，返回-1；<br>

<font color=red>查找成员的时候，不会做数据类型的转换，是真正的全等查找，indexOf是从前向后查找的，lastIndexOf是从后向前查找的</font><br>

## 由于这些都可以在网上查到，这里就不再详细写它们了，只记录一下，它们的作用

#### 数组--forEach

作用：用来代替for循环，遍历数组，是数组遍历器方法，并没有移除循环，而是将循环封装在遍历器方法forEach的内部。<br>

#### 数组--map

作用：遍历数组并映射结果，与forEach非常类似，区别是它的返回值有意义。map方法返回值就是一个<font color=red>新数组</font>，每个成员就是每一次遍历成员时，回调函数的返回值。

```javascript
//实现map方法(IE6下不能使用自带的map方法，需要自己实现，如下：)
if(!Array.prototype.map){
    Array.prototype.map = function(callback){
        //定义返回的结果
        var result = [];
        //遍历数组
        for(var i = 0; i<this.length; i++){
        //执行回调函数，存储其结果
            result.push(callback(this[i], i, this))
        }
        //返回结果
        return result;
    }     
}
```

#### 数组--fill

填充数组方法<br>

作用：我们通过new Array(len)，或者Array(len)创建的数组只有长度，没有成员，所以我们不能用迭代器方法(如forEach, map等等)遍历，为了遍历数组，我们可以向数组中填充成员<br>

参数就是填充的成员，即使是函数也不会执行。<font color=red>fill方法返回值是原数组</font>

```javascript
//实现fill方法(IE6下不能使用自带的map方法，需要自己实现，如下：)
if(!Array.prototype.fill){
    //拓展
    Array.prototype.fill = function(item){
        //遍历
    }
}
```

