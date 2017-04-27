# js面试的知识点，排序不分难易,答案仅供参考
## 简述js基本数据类型和引用数据类型，以及存储在内存哪里？
基本数据类型：Undefined、Null、Boolean、Number和String，基本型数据存在栈中
引用数据类型：Object、Array和Function，引用型数据引用地址存在栈中，而实体对象存在堆中。

## 什么是 NaN和Undefined，它的类型是什么？怎么测试一个值是否等于 NaN?
### NaN
NaN 是 Not a Number 的缩写，JavaScript 的一种特殊数值，其类型是 Number，可以通过 isNaN(param) 来判断一个值是否是 NaN：
```bash
console.log(isNaN(NaN)); //true
console.log(isNaN(23)); //false
console.log(isNaN('ds')); //true
console.log(isNaN('32131sdasd')); //true
console.log(NaN === NaN); //false
console.log(NaN === undefined); //false
console.log(undefined === undefined); //false
console.log(typeof NaN); //number
console.log(Object.prototype.toString.call(NaN)); //[object Number]
```
### Undefined
Undefined类型只有一个值，即特殊的undefined。在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined。

## ==和===有什么不同？
首先，== equality 等同，=== identity 恒等。 ==， 两边值类型不同的时候，要先进行类型转换，再比较。 ===，不做类型转换，类型不同的一定不等。

先说 ===，这个比较简单。下面的规则用来判断两个值是否===相等：

如果类型不同，就[不相等]
如果两个都是数值，并且是同一个值，那么[相等]；(！例外)的是，如果其中至少一个是NaN，那么[不相等]。（判断一个值是否是NaN，只能用isNaN()来判断）
如果两个都是字符串，每个位置的字符都一样，那么[相等]；否则[不相等]。
如果两个值都是true，或者都是false，那么[相等]。
如果两个值都引用同一个对象或函数，那么[相等]；否则[不相等]。
如果两个值都是null，或者都是undefined，那么[相等]。 
再说 ==，根据以下规则：
如果两个值类型相同，进行 === 比较。
如果两个值类型不同，他们可能相等。根据下面规则进行类型转换再比较： 
1.如果一个是null、一个是undefined，那么[相等]。 
2.如果一个是字符串，一个是数值，把字符串转换成数值再进行比较。 
3.如果任一值是 true，把它转换成 1 再比较；如果任一值是 false，把它转换成 0 再比较。 
4.如果一个是对象，另一个是数值或字符串，把对象转换成基础类型的值再比较。对象转换成基础类型，利用它的toString或者valueOf方法。js核心内置类，会尝试valueOf先于toString；例外的是Date，Date利用的是toString转换。
5.任何其他组合，都[不相等]。

## 请指出document.onload和document.ready两个事件的区别。
页面加载完成有两种事件，一是ready，表示文档结构已经加载完成（不包含图片等非文字媒体文件），二是onload，指示页面包含图片等文件在内的所有元素都加载完成。

## 什么是三元表达式？“三元”表示什么意思？
三元表达式：? :。三元–三个操作对象。
在表达式boolean-exp ? value0 : value1 中，如果“布尔表达式”的结果为true，就计算“value0”，而且这个计算结果也就是操作符最终产生的值。如果“布尔表达式”的结果为false，就计算“value1”，同样，它的结果也就成为了操作符最终产生的值。

## JavaScript里函数参数arguments是数组吗？
在函数代码中，使用特殊对象 arguments，开发者无需明确指出参数名，通过使用下标就可以访问相应的参数。
arguments虽然有一些数组的性质，但其并非真正的数组，只是一个类数组对象。其并没有数组的很多方法，不能像真正的数组那样调用.jion(),.concat(),.pop()等方法。

## data-属性的作用是什么？
data-* 属性用于存储页面或应用程序的私有自定义数据。data-* 属性赋予我们在所有 HTML 元素上嵌入自定义 data 属性的能力。存储的（自定义）数据能够被页面的 JavaScript 中利用，以创建更好的用户体验（不进行 Ajax 调用或服务器端数据库查询）。

data-* 属性包括两部分：
属性名不应该包含任何大写字母，并且在前缀 “data-” 之后必须有至少一个字符
属性值可以是任意字符串

## 请描述一下cookies，sessionStorage和localStorage的区别？
sessionStorage和localStorage是HTML5 Web Storage API提供的，可以方便的在web请求之间保存数据。有了本地数据，就可以避免数据在浏览器和服务器间不必要地来回传递。sessionStorage、localStorage、cookie都是在浏览器端存储的数据，其中sessionStorage的概念很特别，引入了一个“浏览器窗口”的概念。sessionStorage是在同源的同窗口（或tab）中，始终存在的数据。也就是说只要这个浏览器窗口没有关闭，即使刷新页面或进入同源另一页面，数据仍然存在。关闭窗口后，sessionStorage即被销毁。同时“独立”打开的不同窗口，即使是同一页面，sessionStorage对象也是不同的cookies会发送到服务器端。其余两个不会。Microsoft指出InternetExplorer8增加cookie限制为每个域名50个，但IE7似乎也允许每个域名50个cookie。

Firefox每个域名cookie限制为50个。
Opera每个域名cookie限制为30个。
Firefox和Safari允许cookie多达4097个字节，包括名（name）、值（value）和等号。
Opera允许cookie多达4096个字节，包括：名（name）、值（value）和等号。
InternetExplorer允许cookie多达4095个字节，包括：名（name）、值（value）和等号。

## 关于HTTP请求GET和POST的区别
1.GET提交，请求的数据会附在URL之后（就是把数据放置在HTTP协议头＜request-line＞中），以?分割URL和传输数据，多个参数用&连接;例如：login.action?name=hyddd&password=idontknow&verify=%E4%BD%A0 %E5%A5%BD。如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，则直接把字符串用BASE64加密，得出如： %E4%BD%A0%E5%A5%BD，其中％XX中的XX为该符号以16进制表示的ASCII。

POST提交：把提交的数据放置在是HTTP包的包体＜request-body＞中。上文示例中红色字体标明的就是实际的传输数据
因此，GET提交的数据会在地址栏中显示出来，而POST提交，地址栏不会改变

2.传输数据的大小：
首先声明，HTTP协议没有对传输的数据大小进行限制，HTTP协议规范也没有对URL长度进行限制。 而在实际开发中存在的限制主要有：
GET:特定浏览器和服务器对URL长度有限制，例如IE对URL长度的限制是2083字节(2K+35)。对于其他浏览器，如Netscape、FireFox等，理论上没有长度限制，其限制取决于操作系统的支持。
因此对于GET提交时，传输数据就会受到URL长度的限制。
POST:由于不是通过URL传值，理论上数据不受限。但实际各个WEB服务器会规定对post提交数据大小进行限制，Apache、IIS6都有各自的配置。

3.安全性：
POST的安全性要比GET的安全性高。注意：这里所说的安全性和上面GET提到的“安全”不是同个概念。上面“安全”的含义仅仅是不作数据修改，而这里安全的含义是真正的Security的含义，比如：通过GET提交数据，用户名和密码将明文出现在URL上，因为(1)登录页面有可能被浏览器缓存， (2)其他人查看浏览器的历史纪录，那么别人就可以拿到你的账号和密码了。

## js跨域请求的方式，能写几种是几种
1、通过jsonp跨域   
2、通过修改document.domain来跨子域     
3、使用window.name来进行跨域     
4、使用HTML5中新引进的window.postMessage方法来跨域传送数据（ie 67 不支持）   
5、CORS 需要服务器设置header ：Access-Control-Allow-Origin。  
6、nginx反向代理 这个方法一般很少有人提及，但是他可以不用目标服务器配合，不过需要你搭建一个中转nginx服务器，用于转发请求   

## 请解释JSONP的工作原理，以及它为什么不是真正的AJAX。
JSONP (JSON with Padding)是一个简单高效的跨域方式，HTML中的script标签可以加载并执行其他域的javascript，于是我们可以通过script标记来动态加载其他域的资源。例如我要从域A的页面pageA加载域B的数据，那么在域B的页面pageB中我以JavaScript的形式声明pageA需要的数据，然后在 pageA中用script标签把pageB加载进来，那么pageB中的脚本就会得以执行。JSONP在此基础上加入了回调函数，pageB加载完之后会执行pageA中定义的函数，所需要的数据会以参数的形式传递给该函数。JSONP易于实现，但是也会存在一些安全隐患，如果第三方的脚本随意地执行，那么它就可以篡改页面内容，截获敏感数据。但是在受信任的双方传递数据，JSONP是非常合适的选择。

AJAX是不跨域的，而JSONP是一个是跨域的，还有就是二者接收参数形式不一样！

##  js深度复制的方式
1、使用jq的$.extend(true, target, obj)   
2、newobj = Object.create(sourceObj)，// 但是这个是有个问题就是 newobj的更改不会影响到 sourceobj但是 sourceobj的更改会影响到newObj   
3、newobj = JSON.parse(JSON.stringify(sourceObj))   

## 在严格模式(‘use strict’)下进行 JavaScript 开发有什么好处？
- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为; 
- 消除代码运行的一些不安全之处，保证代码运行的安全； 
- 提高编译器效率，增加运行速度； 
- 为未来新版本的Javascript做好铺垫。  

## 请描述下事件冒泡和事件捕获机制。
- 冒泡型事件：事件按照从最特定的事件目标到最不特定的事件目标(document对象)的顺序触发。
- 捕获型事件：事件从最不精确的对象(document 对象)开始触发，然后到最精确(也可以在窗口级别捕获事件，不过必须由开发人员特别指定)。

## 什么是哈希表？
散列表（也叫哈希表），是根据关键码值直接进行访问的数据结构。也就是说，它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度。这个映射函数叫做散列函数，存放记录的数组叫做散列表。

## 什么是闭包，如何使用它，为什么要使用它？
闭包就是能够读取其他函数内部变量的函数。由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成“定义在一个函数内部的函数”。
所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。闭包可以用在许多地方。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。

### 使用闭包的注意点
由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。 
（关于闭包，详细了解请看JavaScript之作用域与闭包详解）

## 请解释变量声明提升。
在JS里定义的变量，存在于作用域链里，而在函数执行时会先把变量的声明进行提升，仅仅是把声明进行了提升，而其值的定义还在原来位置。示例如下：
```bash
 var test = function() {
     console.log(name); // 输出：undefined
     var name = "jeri";
     console.log(name); // 输出：jeri
 }
 
 test();
```
上述代码与下述代码等价。
```bash
 var test = function() {
     var name;
     console.log(name); // 输出：undefined
     name = "jeri";
     console.log(name); // 输出：jeri
 }
 
 test();
```
由以上代码可知，在函数执行时，把变量的声明提升到了函数顶部，而其值定义依然在原来位置。

## 简述AMD、CMD和UMD区别
Commonjs 在Nodejs服务端上运行，无法在浏览器端运行。为了满足浏览器端模块化的要求，才有了AMD和CMD。
### AMD
AMD (Asynchronous Module Definition)是 RequireJS 在推广过程中对模块定义的规范化产出。对于依赖的模块，AMD 是提前执行。AMD 推崇依赖前置，把依赖参数以数组形式保存在前半部分。使用规则如下：
```bash
define(id?, dependencies?, factory);
```
### CMD
CMD (Common Module Definition)是 Seajs 在推广过程中对模块定义的规范化产出。 CMD 是延迟执行，CMD 推崇依赖就近，使用规则如下：
```bash
define(function(require, exports, module) {
  // 模块代码
});
```
### UMD
UMD (Universal Module Definition)，AMD，CommonJS规范是两种不一致的规范，虽然他们应用的场景也不太一致，但是人们仍然是期望有一种统一的规范来支持这两种规范，对两种情况进行判断，UMD兼容两个规范。
```bash
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery'], factory);
    } else if (typeof exports === 'object') {
        // Node, CommonJS-like
        module.exports = factory(require('jquery'));
    } else {
        // Browser globals (root is window)
        root.returnExports = factory(root.jQuery);
    }
}(this, function ($) {
    //    methods
    function myFunc(){};

    //    exposed public method
    return myFunc;
}));
```
### Require.js 和Sea.js区别
Require.js 和Sea.js都是模块加载器，两者的主要区别如下：

- 定位有差异。RequireJS 想成为浏览器端的模块加载器，同时也想成为 Rhino / Node 等环境的模块加载器。Sea.js 则专注于 Web 浏览器端，同时通过 Node 扩展的方式可以很方便跑在 Node 环境中。
- 遵循的规范不同。RequireJS 遵循 AMD（异步模块定义）规范，Sea.js 遵循 CMD （通用模块定义）规范。规范的不同，导致了两者 API 不同。Sea.js 更贴近 CommonJS Modules/1.1 和 Node Modules 规范。
- 推广理念有差异。RequireJS 在尝试让第三方类库修改自身来支持 RequireJS，目前只有少数社区采纳。Sea.js 不强推，采用自主封装的方式来“海纳百川”，目前已有较成熟的封装策略。
- 对开发调试的支持有差异。Sea.js 非常关注代码的开发调试，有 nocache、debug 等用于调试的插件。RequireJS 无这方面的明显支持。
- 插件机制不同。RequireJS 采取的是在源码中预留接口的形式，插件类型比较单一。Sea.js 采取的是通用事件机制，插件类型更丰富。

## 下面两个函数的返回值是一样的吗？为什么？
```bash
function foo1()
{
  return {
      bar: "hello"
  };
}
 
function foo2()
{
  return
  {
      bar: "hello"
  };
}
```
在编程语言中，基本都是使用分号（;）将语句分隔开，这可以增加代码的可读性和整洁性。而在JS中，如若语句各占独立一行，通常可以省略语句间的分号（;），JS 解析器会根据能否正常编译来决定是否自动填充分号：
```bash
var test = 1 + 2;
console.log(test);  //3
```
在上述情况下，为了正确解析代码，就不会自动填充分号了，但是对于 return 、break、continue 等语句，如果后面紧跟换行，解析器一定会自动在后面填充分号(;)，所以上面的第二个函数就变成了这样：
```bash
function foo2()
{
  return;
  {
      bar: "hello"
  };
}
```
所以第二个函数是返回 undefined。

## 使用 typeof bar === “object” 判断 bar 是不是一个对象有什么潜在的弊端？如何避免这种弊端？
使用 typeof 的弊端是显而易见的(这种弊端同使用 instanceof)：
```bash
let obj = {};
let arr = [];
 
console.log(typeof obj === 'object');  //true
console.log(typeof arr === 'object');  //true
console.log(typeof null === 'object');  //true
```
从上面的输出结果可知，typeof bar === “object” 并不能准确判断 bar 就是一个 Object。可以通过 Object.prototype.toString.call(bar) === “[object Object]” 来避免这种弊端：
```bash
let obj = {};
let arr = [];
 
console.log(Object.prototype.toString.call(obj));  //[object Object]
console.log(Object.prototype.toString.call(arr));  //[object Array]
console.log(Object.prototype.toString.call(null));  //[object Null]
```
另外，为了珍爱生命，请远离 ==： 
珍爱生命
而 [] === false 是返回 false 的。

## 下面的代码会在 console 输出什么？为什么？
```bash
(function(){
  var a = b = 3;
})();
 
console.log("a defined? " + (typeof a !== 'undefined'));   
console.log("b defined? " + (typeof b !== 'undefined'));
```
这跟变量作用域有关，输出换成下面的：
```bash
console.log(b); //3
console,log(typeof a); //undefined
```
拆解一下自执行函数中的变量赋值：
```bash
b = 3;
var a = b;
```
所以 b 成了全局变量，而 a 是自执行函数的一个局部变量。

## 下面的代码会在 console 输出什么？为什么？
```bash
var myObject = {
    foo: "bar",
    func: function() {
        var self = this;
        console.log("outer func:  this.foo = " + this.foo);
        console.log("outer func:  self.foo = " + self.foo);
        (function() {
            console.log("inner func:  this.foo = " + this.foo);
            console.log("inner func:  self.foo = " + self.foo);
        }());
    }
};
myObject.func();
```
第一个和第二个的输出不难判断，在 ES6 之前，JavaScript 只有函数作用域，所以 func 中的 IIFE 有自己的独立作用域，并且它能访问到外部作用域中的 self，所以第三个输出会报错，因为 this 在可访问到的作用域内是 undefined，第四个输出是 bar。如果你知道闭包，也很容易解决的：
```bash
(function(test) {
  console.log("inner func:  this.foo = " + test.foo);  //'bar'
  console.log("inner func:  self.foo = " + self.foo);
}(self));
```

## 将 JavaScript 代码包含在一个函数块中有什么意思呢？为什么要这么做？
换句话说，为什么要用立即执行函数表达式（Immediately-Invoked Function Expression）。
IIFE 有两个比较经典的使用场景，一是类似于在循环中定时输出数据项，二是类似于 JQuery/Node 的插件和模块开发。
```bash
for(var i = 0; i < 5; i++) {
  setTimeout(function() {
      console.log(i);  
  }, 1000);
}
```
上面的输出并不是你以为的0，1，2，3，4，而输出的全部是5，这时 IIFE 就能有用了：
```bash
for(var i = 0; i < 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i);  
    }, 1000);
  })(i)
}
```
而在 JQuery/Node 的插件和模块开发中，为避免变量污染，也是一个大大的 IIFE
```bash
(function($) { 
        //代码
 } )(jQuery);
```

## 请指出JavaScript宿主对象和原生对象的区别？
### 原生对象
ECMA-262 把本地对象（native object）定义为“独立于宿主环境的 ECMAScript 实现提供的对象”。
“本地对象”包含哪些内容：Object、Function、Array、String、Boolean、Number、Date、RegExp、Error、EvalError、RangeError、ReferenceError、SyntaxError、TypeError、URIError。
由此可以看出，简单来说，本地对象就是 ECMA-262 定义的类（引用类型）。

### 内置对象
ECMA-262 把内置对象（built-in object）定义为“由 ECMAScript 实现提供的、独立于宿主环境的所有对象，在 ECMAScript 程序开始执行时出现”。这意味着开发者不必明确实例化内置对象，它已被实例化了。
同样是“独立于宿主环境”。根据定义我们似乎很难分清“内置对象”与“本地对象”的区别。而ECMA-262 只定义了两个内置对象，即 Global 和 Math （它们也是本地对象，根据定义，每个内置对象都是本地对象）。如此就可以理解了。内置对象是本地对象的一种。

### 宿主对象
何为“宿主对象”？主要在这个“宿主”的概念上，ECMAScript中的“宿主”当然就是我们网页的运行环境，即“操作系统”和“浏览器”。
所有非本地对象都是宿主对象（host object），即由 ECMAScript 实现的宿主环境提供的对象。所有的BOM和DOM都是宿主对象。因为其对于不同的“宿主”环境所展示的内容不同。其实说白了就是，ECMAScript官方未定义的对象都属于宿主对象，因为其未定义的对象大多数是自己通过ECMAScript程序创建的对象。

## call和.apply的区别是什么？
### call方法 
语法：call(thisObj，Object) 
定义：调用一个对象的一个方法，以另一个对象替换当前对象。 
说明：call 方法可以用来代替另一个对象调用一个方法。call 方法可将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。 如果没有提供 thisObj 参数，那么 Global 对象被用作 thisObj。 
### apply方法 
语法：apply(thisObj，[argArray]) 
定义：应用某一对象的一个方法，用另一个对象替换当前对象。 
说明：如果 argArray 不是一个有效的数组或者不是 arguments 对象，那么将导致一个 TypeError。如果没有提供 argArray 和 thisObj 任何一个参数，那么 Global 对象将被用作 thisObj， 并且无法被传递任何参数。

对于apply和call两者在作用上是相同的，但两者在参数上有以下区别： 
对于第一个参数意义都一样，但对第二个参数：apply传入的是一个参数数组，也就是将多个参数组合成为一个数组传入，而call则作为call的参数传入（从第二个参数开始）。如 func.call(func1,var1,var2,var3)对应的apply写法为：func.apply(func1,[var1,var2,var3])同时使用apply的好处是可以直接将当前函数的arguments对象作为apply的第二个参数传入。

## ”attribute”和”property”的区别是什么？
1.定义
Property：属性，所有的HTML元素都由HTMLElement类型表示，HTMLElement类型直接继承自Element并添加了一些属性，添加的这些属性分别对应于每个HTML元素都有下面的这5个标准特性: id,title,lang,dir,className。DOM节点是一个对象，因此，他可以和其他的JavaScript对象一样添加自定义的属性以及方法。property的值可以是任何的数据类型，对大小写敏感，自定义的property不会出现在html代码中，只存在js中。

Attribute：特性，区别于property，attribute只能是字符串，大小写不敏感，出现在innerHTML中，通过类数组attributes可以罗列所有的attribute。

2.相同之处
标准的 DOM properties 与 attributes 是同步的。公认的（非自定义的）特性会被以属性的形式添加到DOM对象中。如，id，align，style等，这时候操作property或者使用操作特性的DOM方法如getAttribute()都可以操作属性。不过传递给getAttribute()的特性名与实际的特性名相同。因此对于class的特性值获取的时候要传入“class”。

3.不同之处
1).对于有些标准的特性的操作，getAttribute与点号(.)获取的值存在差异性。如href，src，value，style，onclick等事件处理程序。 
2).href：getAttribute获取的是href的实际值，而点号获取的是完整的url，存在浏览器差异。

## 你如何从浏览器的URL中获取查询字符串参数。
```bash
function parseQueryString ( name ){
  name = name.replace(/[\[]/,"\\\[");
  var regexS = "[\\?&]"+name+"=([^&#]*)";
  var regex = new RegExp( regexS );
  var results = regex.exec( window.location.href );

  if(results == null) {
      return "";
  } else {
   return results[1];
  }
}
```

## 请解释一下JavaScript的同源策略。
在客户端编程语言中，如javascript和 ActionScript，同源策略是一个很重要的安全理念，它在保证数据的安全性方面有着重要的意义。同源策略规定跨域之间的脚本是隔离的，一个域的脚本不能访问和操作另外一个域的绝大部分属性和方法。那么什么叫相同域，什么叫不同的域呢？当两个域具有相同的协议, 相同的端口，相同的host，那么我们就可以认为它们是相同的域。同源策略还应该对一些特殊情况做处理，比如限制file协议下脚本的访问权限。本地的HTML文件在浏览器中是通过file协议打开的，如果脚本能通过file协议访问到硬盘上其它任意文件，就会出现安全隐患，目前IE8还有这样的隐患。

## 解释”chaining”。
jQuery方法链接。直到现在，我们都是一次写一条jQuery语句（一条接着另一条）。不过，有一种名为链接（chaining）的技术，允许我们在相同的元素上运行多条jQuery命令，一条接着另一条。
提示：这样的话，浏览器就不必多次查找相同的元素。
如需链接一个动作，您只需简单地把该动作追加到之前的动作上。

## 解释”deferreds”。
开发网站的过程中，我们经常遇到某些耗时很长的javascript操作。其中，既有异步的操作（比如ajax读取服务器数据），也有同步的操作（比如遍历一个大型数组），它们都不是立即能得到结果的。
通常的做法是，为它们指定回调函数（callback）。即事先规定，一旦它们运行结束，应该调用哪些函数。
但是，在回调函数方面，jQuery的功能非常弱。为了改变这一点，jQuery开发团队就设计了deferred对象。
简单说，deferred对象就是jQuery的回调函数解决方案。在英语中，defer的意思是”延迟”，所以deferred对象的含义就是”延迟”到未来某个点再执行。

## 你如何给一个事件处理函数命名空间，为什么要这样做？
任何作为type参数的字符串都是合法的；如果一个字符串不是原生的JavaScript事件名，那么这个事件处理函数会绑定到一个自定义事件上。这些自定义事件绝对不会由浏览器触发，但可以通过使用.trigger()或者.triggerHandler()在其他代码中手动触发。如果type参数的字符串中包含一个点(.)字符，那么这个事件就看做是有命名空间的了。这个点字符就用来分隔事件和他的命名空间。举例来说，如果执行.bind(‘click.name’,handler)，那么字符串中的click是事件类型，而字符串name就是命名空间。命名空间允许我们取消绑定或者触发一些特定类型的事件，而不用触发别的事件。参考unbind()来获取更多信息。

jQuery的bind/unbind方法应该说使用很简单，而且大多数时候可能并不会用到，取而代之的是直接用click/keydown之类的事件名风格的方法来做事件绑定操作。

但假设如下情况：需要在运行时根据用户交互的结果进行不同click事件处理逻辑的绑定，因而理论上会无数次对某一个事件进行bind/unbind操作。但又希望unbind的时候只把自己绑上去的处理逻辑给释放掉而不是所有其他地方有可能的额外的同一事件绑定逻辑。这时候如果直接用.click()/.bind(‘click’)加上.unbind(‘click’)来进行重复绑定的话，被unbind掉的将是所有绑定在元素上的click处理逻辑，潜在会影响到该元素其他第三方的行为。

当然如果在bind的时候是显示定义了function变量的话，可以在unbind的时候提供function作为第二个参数来指定只unbind其中一个处理逻辑，但实际应用中很可能会碰到各种进行匿名函数绑定的情况。对于这种问题，jQuery的解决方案是使用事件绑定的命名空间。即在事件名称后添加.something来区分自己这部分行为逻辑范围。

比如用.bind(‘click.myCustomRoutine’,function(){…});同样是把匿名函数绑定到click事件（你可以用自己的命名空间多次绑定不同的行为方法上去），当unbind的时候用.unbind(‘click.myCustomRoutine’)即可释放所有绑定到.myCustomRoutine命名空间的click事件，而不会解除其他通过.bind(‘click’)或另外的命名空间所绑定的事件行为。同时，使用命令空间还可以让你一次性unbind所有此命名空间下的自定义事件绑定，通过.unbind(‘.myCustomRoutine’)即可。要注意的是，jQuery的命名空间并不支持多级空间。

因为在jQuery里面，如果用.unbind(‘click.myCustomRoutine.myCustomSubone’)，解除的是命名空间分别为myCustomRoutine和myCustomSubone的两个并列命名空间下的所有click事件，而不是”myCustomRoutine下的myCustomSubone子空间”。


## 简述常见js设计模式
总体来说设计模式分为三大类：
- 创建型模式，共五种：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。
- 结构型模式，共七种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。
- 行为型模式，共十一种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模

## 简述JS深浅拷贝的原理及项目应用
[答案我已总结出来，点击查看参考地址](https://manlili.github.io/2017/04/17/JS%E7%9A%84%E6%B5%85%E6%8B%B7%E8%B4%9D%E4%B8%8E%E6%B7%B1%E6%8B%B7%E8%B4%9D%E7%A0%94%E7%A9%B6/)

## 写出下面的输出结果
```bash
var p = new Promise((resolve, reject)=> {reject()}).then(()=>{console.info('resolve1')}, ()=>{console.info('reject1')})
p.then(()=>{console.info('resolve2')}, ()=>{console.info('reject2')})
```
输出结果reject1, resolve2

## 请解释Function.prototype.bind的作用,如果浏览器不支持Function.prototype.bind特性，请实现一个让浏览器支持？

## 解释“JavaScript模块模式”以及你在何时使用它？

## 请尽可能详尽的解释AJAX的工作原理？

## 你能解释一下JavaScript中的继承是如何工作的吗？

## 为什么扩展JavaScript内置对象不是好的做法？

## 描述一种JavaScript中实现memoization(避免重复运算)的策略。

## 解释ES6中Promise

## 写一个算法实现麻将的随机