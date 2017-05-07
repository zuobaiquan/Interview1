# [滴滴出行前端面试总结](https://itwanggj.github.io/2017/04/08/滴滴出行前端面试总结/)

## 技术面试

### 1.【CSS】如何实现单行文本结尾以省略号显示，多行文本以省略号显示：

单行省略号显示代码：

```css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```

多行省略号显示代码：

```css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```

### 2.【CSS】居中显示有哪些方式：

- text-align: center;
- margin: 0 auto; （固定宽度）
- position: absolute; left: 50%; margin-left: -（宽度)/2;
- flex来实现；

### 3.【CSS】讲讲flex布局：

Flex布局是“弹性布局”，用来为盒装模型提供最大的灵活性；
采用Flex布局的元素，称为Flex容器（flex container），简称”容器”。它的所有子元素自动成为容器成员，称为Flex项目（flex item），简称”项目”。
[![img](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170507095737.bmp)](https://itwanggj.github.io/images/bg2015071004.png)
容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。
项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

### 4.【CSS】清除浮动有哪些方式：

- 添加一个空的div标签，添加clear:both属性；
- 父级div添加overflow:hidden;
- 父级div添加:after伪类;
- 父级div添加overflow:auto;

### 5.【JavaScript】讲一下如何深拷贝对象：

对象的深拷贝和浅拷贝的区别：
浅拷贝：仅仅复制对象的引用，而不是对象本身；
深拷贝：把复制的对象所引用的全部对象都复制一遍。

<1>. 浅拷贝的实现：

浅拷贝实现较为简单，只要使用简单的复制语句即可；

方法一：简答的复制语句：

```javascript
/* ================ 浅拷贝 ================ */
function simpleClone(initalObj) {
    var obj = {};
    for ( var i in initalObj) {
        obj[i] = initalObj[i];
    }
    return obj;
}
```

客户端调用：

```javascript
/* ================ 客户端调用 ================ */
var obj = {
    a: "hello",
    b: {
        a: "world",
        b: 21
    },
    c: ["Bob", "Tom", "Jenny"],
    d: function() {
        alert("hello world");
    }
}
var cloneObj = simpleClone(obj); // 对象拷贝
  
console.log(cloneObj.b); // {a: "world", b: 21}
console.log(cloneObj.c); // ["Bob", "Tom", "Jenny"]
console.log(cloneObj.d); // function() { alert("hello world"); }
  
// 修改拷贝后的对象
cloneObj.b.a = "changed";
cloneObj.c = [1, 2, 3];
cloneObj.d = function() { alert("changed"); };
  
console.log(obj.b); // {a: "changed", b: 21} 
// 原对象所引用的对象被修改了
  
console.log(obj.c); // ["Bob", "Tom", "Jenny"] 
// 原对象所引用的对象未被修改
console.log(obj.d); // function() { alert("hello world"); } 
// 原对象所引用的函数未被修改
```

方法二：Object.assign()
Object.assign() 方法可以把任意多个的源对象自身的可枚举属性拷贝给目标对象，然后返回目标对象。但是 Object.assign() 进行的是浅拷贝，拷贝的是对象的属性的引用，而不是对象本身。

```javascript
var obj = { a: {a: "hello", b: 21} }; 
var initalObj = Object.assign({}, obj); 
initalObj.a.a = "changed"; 
console.log(obj.a.a); // "changed"
```

<2>. 深拷贝的实现
要实现深拷贝有很多办法，有最简单的 JSON.parse() 方法，也有常用的递归拷贝方法，和ES5中的 Object.create() 方法。

方法一：使用 JSON.parse() 方法

```javascript
/* ================ 深拷贝 ================ */
function deepClone(initalObj) {
    var obj = {};
    try {
        obj = JSON.parse(JSON.stringify(initalObj));
    }
    return obj;
}
/* ================ 客户端调用 ================ */
var obj = {
    a: {
        a: "world",
        b: 21
    }
}
var cloneObj = deepClone(obj);
cloneObj.a.a = "changed";
  
console.log(obj.a.a); // "world"
```

这种方法简单易用。
但是这种方法也有不少坏处，譬如它会抛弃对象的constructor。也就是深拷贝之后，不管这个对象原来的构造函数是什么，在深拷贝之后都会变成Object。
这种方法能正确处理的对象只有 Number, String, Boolean, Array, 扁平对象，即那些能够被 json 直接表示的数据结构。RegExp对象是无法通过这种方式深拷贝。

方法二：递归拷贝

```javascript
/* ================ 深拷贝 ================ */
function deepClone(initalObj, finalObj) {
    var obj = finalObj || {};
    for (var i in initalObj) {
        if (typeof initalObj[i] === 'object') {
            obj[i] = (initalObj[i].constructor === Array) ? [] : {};
            arguments.callee(initalObj[i], obj[i]);
        } else {
            obj[i] = initalObj[i];
        }
    }
    return obj;
}
```

上述代码确实可以实现深拷贝。但是当遇到两个互相引用的对象，会出现死循环的情况。
为了避免相互引用的对象导致死循环的情况，则应该在遍历的时候判断是否相互引用对象，如果是则退出循环。
改进版代码如下：

```javascript
/* ================ 深拷贝 ================ */
function deepClone(initalObj, finalObj) {
    var obj = finalObj || {};
    for (var i in initalObj) {
        var prop = initalObj[i];
  
        // 避免相互引用对象导致死循环，如initalObj.a = initalObj的情况
        if(prop === obj) {
            continue;
        }
  
        if (typeof prop === 'object') {
            obj[i] = (prop.constructor === Array) ? [] : {};
            arguments.callee(prop, obj[i]);
        } else {
            obj[i] = prop;
        }
    }
    return obj;
}
```

方法三：使用Object.create()方法
直接使用var newObj = Object.create(oldObj)，可以达到深拷贝的效果。

```javascript
/* ================ 深拷贝 ================ */
function deepClone(initalObj, finalObj) {
    var obj = finalObj || {};
    for (var i in initalObj) {
        var prop = initalObj[i];
  
        // 避免相互引用对象导致死循环，如initalObj.a = initalObj的情况
        if(prop === obj) {
            continue;
        }
  
        if (typeof prop === 'object') {
            obj[i] = (prop.constructor === Array) ? [] : Object.create(prop);
        } else {
            obj[i] = prop;
        }
    }
    return obj;
}
```

### 6.【Webpack】讲讲Webpack：

Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。通过 loader 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等。

### 7.【requirejs】讲讲requirejs，以及使用它的好处：

RequireJS是一个Javascript 文件和模块框架，可以从 [http://requirejs.org/](http://requirejs.org/)下载，如果你使用Visual Studio也可以通过Nuget获取。它支持浏览器和像node.js之类的服务器环境。使用RequireJS,你可以顺序读取仅需要相关依赖模块。

RequireJS所做的是，在你使用script标签加载你所定义的依赖时，将这些依赖通过head.appendChild()函数来加载他们。当依赖加载以后，RequireJS计算出模块定义的顺序，并按正确的顺序进行调用。这意味着你需要做的仅仅是使用一个“根”来读取你需要的所有功能，然后剩下的事情只需要交给RequireJS就行了。为了正确的使用这些功能，你定义的所有模块都需要使用RequireJS的API，否者它不会像期望的那样工作。

### 8.【JavaScript】组件化开发，对外暴漏什么接口：

无论前端也好，后端也好，都是整个软件体系的一部分。软件产品也是产品，它的研发过程也必然是有其目的。绝大多数软件产品是追逐利润的，在产品目标确定的情况下，成本有两个途径来优化：减少部署成本，提高开发效率。

减少部署成本的方面，业界研究得非常多，比如近几年很流行的“去IOE”，就是很典型的，从一些费用较高的高性能产品迁移到开源的易替换的产品集群，又比如使用Linux + Mono来部署.net应用，避开Windows Server的费用。

提高开发效率这方面，业界研究得更多，主要途径有两点：加快开发速度，减少变更代价。怎样才能加快开发速度呢？如果我们的开发不是重新造轮子，而是每一次做新产品都可以利用已有的东西，那就会好很多。怎样才能减少变更代价呢？如果我们能够理清模块之间的关系，合理分层，每次变更只需要修改其中某个部分，甚至不需要修改代码，仅仅是改变配置就可以，那就更好了。我们先不看软件行业，来看一下制造行业，比如汽车制造业，他们是怎么造汽车的呢？造汽车之前，先设计，把整个汽车分解为不同部件，比如轮子，引擎，车门，座椅等等，分别生产，最后再组装，所以它的制造过程可以较快。如果一辆汽车轮胎被扎破了，需要送去维修，维修的人也没有在每个地方都修一下，而是只把轮胎拆下来修修就好了，这个轮胎要是实在坏得厉害，就干脆换上个新的，整个过程不需要很多时间。

### 9.【Html5】Canvas如何绘制饼状图

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>06绘制饼状图</title>
</head>
<body>
 <canvas id="canvas">
    抱歉，您的浏览器不支持Canvas。请升级您的浏览器！
 </canvas>

 <script>
    (function(){
        var canvas = document.getElementById("canvas");
        canvas.border = "1px solid #000";
        canvas.width = 600;
        canvas.height = 600;
        var ctx = canvas.getContext("2d");

        var data = [{
                "value": .2,
                "color": "red",
                "title": "应届生"
            },{
                "value": .3,
                "color": "blue",
                "title": "社会招生"
            },{
                "value": .4,
                "color": "green",
                "title": "老学员推荐"
            },{
                "value": .1,
                "color": "#ccc",
                "title": "公开课"
            }];

        var x0 = 300;
        var y0 = 300;
        var radius = 100;
        var tempAngle = -90;
        for(var i=0;i<data.length;i++){
            // 开始绘制新状态的扇形
            ctx.beginPath();
            ctx.moveTo(300, 300);
            ctx.fillStyle = data[i].color;
            var angle = data[i].value*360;
            var startAngle = tempAngle*Math.PI/180; 
            var endAngle = (tempAngle + angle)*Math.PI/180;
            ctx.arc(300, 300, 100, startAngle, endAngle);
            ctx.fill();

            tempAngle+=angle;
        }
    }());
 </script>
</body>
</html>
```

效果图：

[![img](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170507095755.bmp)](https://itwanggj.github.io/images/qqqq.png)

### 10.【JavaScript】promise的实现：

ES6 原生提供了 Promise 对象。

所谓 Promise，就是一个对象，用来传递异步操作的消息。它代表了某个未来才会知道结果的事件（通常是一个异步操作），并且这个事件提供统一的 API，可供进一步处理。

Promise 对象有以下两个特点。

（1）对象的状态不受外界影响。Promise 对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和 Rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是 Promise 这个名字的由来，它的英语意思就是「承诺」，表示其他手段无法改变。

（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise 对象的状态改变，只有两种可能：从 Pending 变为 Resolved 和从 Pending 变为 Rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果。就算改变已经发生了，你再对 Promise 对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

有了 Promise 对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise 对象提供统一的接口，使得控制异步操作更加容易。

Promise 也有一些缺点。首先，无法取消 Promise，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，Promise 内部抛出的错误，不会反应到外部。第三，当处于 Pending 状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

```javascript
var promise = new Promise(function(resolve, reject) {
 if (/* 异步操作成功 */){
 resolve(value);
 } else {
 reject(error);
 }
});
promise.then(function(value) {
 // success
}, function(value) {
 // failure
});
```

Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 方法和 reject 方法。

如果异步操作成功，则用 resolve 方法将 Promise 对象的状态，从「未完成」变为「成功」（即从 pending 变为 resolved）；

如果异步操作失败，则用 reject 方法将 Promise 对象的状态，从「未完成」变为「失败」（即从 pending 变为 rejected）。

### 11.【JavsScript】异步加载有几种方式：

JS异步加载有三种方式：

js加载的缺点：加载工具方法没必要阻塞文档，过多js加载会影响页面效率，一旦网速不好，那么整个网站将等待js加载而不进行后续渲染等工作。 有些工具方法需要按需加载，用到再加载，不用不加载，。

默认正常模式下下，JS是同步加载的，即优先加载JS，只有当JS文件下载完，dom和css才开始加载，当某些时候我们需要JS异步加载，我们可以通过以下方式来设置异步加载,不同情况下选取不同方式即可

1.defer:defer

- JS异步下载，dom结构解析完（标签 + 样式（内容不一定下载完））才异步执行
- 仅IE能用
- 内部JS也能用该属性
- 异步加载js不允许使用document.write，因为document.write会清除文档流，js标签还未加载就会被清除
- document.write()可用于初始化页面

2.(h5)async:async（asynchronous） ajax(asynchronous javascript and XML)

- JS异步加载，加载完毕后立刻异步执行
- IE8及以下不兼容
- 内部JS不能用该属性

3.除了以上两种方法，还有一种兼容自己封装的异步加载方式，即动态添加script标签也能实现异步加载。

### 12.【Gulp、Grunt、Webpack】讲一下Gulp、Grunt、Webpack的区别：

gulp是工具链、构建工具，可以配合各种插件做js压缩，css压缩，less编译 替代手工实现自动化工作

```
1.构建工具
2.自动化
3.提高效率用
```

webpack是文件打包工具，可以把项目的各种js文、css文件等打包合并成一个或多个文件，主要用于模块化方案，预编译模块的方案

```
1.打包工具
2.模块化识别
3.编译模块代码方案用
```

所以定义和用法上来说 都不是一种东西，无可比性 ，更不冲突！【当然，也有相似的功能，比如合并，区分，但各有各的优势】

Gulp解释图：
[![img](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170507095833.bmp)](https://itwanggj.github.io/images/20160629120335463.jpg)

[![img](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170507095855.bmp)](https://itwanggj.github.io/images/20160629120359221.jpg)

Webpack解释图：

[![img](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170507095904.bmp)](https://itwanggj.github.io/images/20160629120502503.png)

怎么解释呢？因为 Gulp 和 browserify / webpack 不是一回事

Gulp应该和Grunt比较，他们的区别我就不说了，说说用处吧。Gulp / Grunt 是一种工具，能够优化前端工作流程。比如自动刷新页面、combo、压缩css、js、编译less等等。简单来说，就是使用Gulp/Grunt，然后配置你需要的插件，就可以把以前需要手工做的事情让它帮你做了。

说到 browserify / webpack ，那还要说到 seajs / requirejs 。这四个都是JS模块化的方案。其中seajs / require 是一种类型，browserify / webpack 是另一种类型。

1. seajs / require : 是一种在线”编译” 模块的方案，相当于在页面上加载一个 CMD/AMD 解释器。这样浏览器就认识了 define、exports、module 这些东西。也就实现了模块化。
2. browserify / webpack : 是一个预编译模块的方案，相比于上面 ，这个方案更加智能。没用过browserify，这里以webpack为例。首先，它是预编译的，不需要在浏览器中加载解释器。另外，你在本地直接写JS，不管是 AMD / CMD / ES6 风格的模块化，它都能认识，并且编译成浏览器认识的JS。这样就知道，Gulp是一个工具，而webpack等等是模块化方案。Gulp也可以配置seajs、requirejs甚至webpack的插件。　　

### 13.【JavaScropt】如何区分整数与浮点数（如：3与3.0）：

使用正则表达式：

```javascript
"^\\d+$"　　//非负整数（正整数+0）      
"^[0-9]*[1-9][0-9]*$"　　//正整数      
"^((-\\d+)|(0+))$"　　//非正整数（负整数+0）      
"^-[0-9]*[1-9][0-9]*$"　　//负整数      
"^-?\\d+$"　　　　//整数      
"^\\d+(\\.\\d+)?$"　　//非负浮点数（正浮点数+0）      
"^(([0-9]+\\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\\.[0-9]+)|([0-9]*[1-9][0-9]*))$"　　//正浮点数      
"^((-\\d+(\\.\\d+)?)|(0+(\\.0+)?))$"　　//非正浮点数（负浮点数   +   0）      
"^(-(([0-9]+\\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\\.[0-9]+)|([0-9]*[1-9][0-9]*)))$"　　//负浮点数      
"^(-?\\d+)(\\.\\d+)?$"　　//浮点数
```

### 14.【JavaScript】跨域请求有多少种方式：

注：单独在一篇博客中分析。

### 15.最后一个问题：是否了解目前最火的技术：Vue、React、NodeJs、ES6、ES7.

面试总结：问的问题比较基础，但每个问题都会往深了问，一般都是刚开始能回答上来，越往深入问，越回答不上来。本文所有的答案都是博主自己面试后的分析、总结，有不对的地方，欢迎大家及时指出，共同进步。

转自：[https://itwanggj.github.io/2017/04/08/滴滴出行前端面试总结/](https://itwanggj.github.io/2017/04/08/滴滴出行前端面试总结/)