# [Front End Web Development Quiz](http://davidshariff.com/quiz/)

### 1.css部分

#### 1.1 Are CSS property names case-sensitive?

​	译： CSS属性名称区分大小写吗？

```css
ul {
    MaRGin: 10px;
}
```

解析：CSS属性名称不区分大小，JS区分大小写

#### 1.2 Does setting `margin-top` and `margin-bottom` have an affect on an inline element?

译：设置margin-top和margin-bottom是否对内联元素有影响？

解析：No

#### 1.3 Does setting `padding-top` and `padding-bottom` on an inline element add to its dimensions?

译：设置内联元素上的padding-top和padding-bottom属性是否改变其宽高？

解析：No

#### 1.4 If you have a `<p>` element with `font-size: 10rem`, will the text be responsive when the user resizes / drags the browser window?

译：如果你有一个p标签设置字体大小为10rem，调整大小/拖动浏览器窗口会改变其字体大小吗？

解析：No

#### 1.5 The pseudo class `:checked` will select inputs with type radio or checkbox, but not `<option>`elements.

译：伪类：checked选中可用于radio 或者checkbox，但不是用于option元素？

解析：错误，

#### 1.6 In a HTML document, the pseudo class `:root` always refers to the `<html>` element.

译：在HTML文档中，伪类：根始终是指向html？

解析：对

#### 1.7 The `translate()` function can move the position of an element on the z-axis.

译：CSS中的translate属性可以改变元素Z轴上的位置？

解析：错误

#### 1.8 What is the color of the text Sausage ?

译：Sausage文本的颜色是

```html
<ul class="shopping-list" id="awesome">
    <li>
      	<span>Milk</span>
  	</li>
    <li class="favorite" id="must-buy">
      	<span class="highlight">Sausage</span>
  	</li>
</ul>
```

```css
ul {
    color: red;
}
li {
    color: blue;
}
```

解析：blue

#### 1.9 What is the color of the text Sausage ?

```html
<ul class="shopping-list" id="awesome">
    <li>
    	<span>Milk</span>
    </li>
    <li class="favorite" id="must-buy">
    	<span class="highlight">Sausage</span>
    </li>
</ul>
```

```css
ul li {
    color: red;
}
#must-buy {
    color: blue;
}
```

解析：blue

#### 1.10 What is the color of the text Sausage ?

```html
<ul class="shopping-list" id="awesome">
    <li>
    	<span>Milk</span>
    </li>
    <li class="favorite" id="must-buy">
    	<span class="highlight">Sausage</span>
    </li>
</ul>
```

```css
.shopping-list .favorite {
    color: red;
}
#must-buy {
    color: blue;
}
```

解析：blue

#### 1.11 What is the color of the text Sausage ?

```html
<ul class="shopping-list" id="awesome">
    <li>
      	<span>Milk</span>
  	</li>
    <li class="favorite" id="must-buy">
      	<span class="highlight">Sausage</span>
  	</li>
</ul>
```

```css
ul#awesome {
    color: red;
}
ul.shopping-list li.favorite span {
    color: blue;
}
```

解析：blue

#### 1.12 What is the color of the text Sausage ?

```html
<ul class="shopping-list" id="awesome">
    <li>
      	<span>Milk</span>
  	</li>
    <li class="favorite" id="must-buy">
      	<span class="highlight">Sausage</span>
  	</li>
</ul>
```

```css
ul#awesome #must-buy {
    color: red;
}
.favorite span {
    color: blue!important;
}
```

解析：blue

#### 1.13 What is the color of the text Sausage ?

```html
<ul class="shopping-list" id="awesome">
    <li>
      	<span>Milk</span>
  	</li>
    <li class="favorite" id="must-buy">
      	<span class="highlight">Sausage</span>
  	</li>
</ul>
```

```css
ul.shopping-list li .highlight {
    color: red;
}
ul.shopping-list li .highlight:nth-of-type(odd) {
    color: blue;
}
```

解析：blue

#### 1.14 What is the color of the text Sausage ?  **

```html
<ul class="shopping-list" id="awesome">
    <li>
      	<span>Milk</span>
  	</li>
    <li class="favorite" id="must-buy">
      	<span class="highlight">Sausage</span>
  	</li>
</ul>
```

```css
#awesome .favorite:not(#awesome) .highlight {
    color: red;
}
#awesome .highlight:nth-of-type(1):nth-last-of-type(1) {
    color: blue;
}
```

解析：red

### 2.html部分

#### 2.1 Are unused style resources still downloaded by the browser?

译：对于未使用的样式资源，浏览器仍然会下载？

```html
<div id="test1">
    <span id="test2"></span>
</div>
```

```css
#i-am-useless {
    background-image: url('mypic.jpg');
}
```

解析：不会下载

#### 2.2 On page load, will `mypic.jpg` get downloaded by the browser?

译：页面加载时，浏览器会下载mypic.jpg图片吗？

```html
<div id="test1">
    <span id="test2"></span>
</div>
```

```css
#test2 {
    background-image: url('mypic.jpg');
    display: none;
}
```

解析：会

#### 2.3 On page load, will `mypic.jpg` get downloaded by the browser?

```html
<div id="test1">
    <span id="test2"></span>
</div>
```

```css
#test1 {
    display: none;
}
#test2 {
    background-image: url('mypic.jpg');
    visibility: hidden;
}
```

解析：不会

#### 2.4 What is the use of the `only` selector?  **

```css
@media only screen and (max-width: 1024px) {
    margin: 0;
}
```

A. Stops older browsers from parsing the remainder of the selector

B. Apply the style for ` screen` only and ignore the device `max-width`

C. It does nothing

解析：A

#### 2.5 Does `overflow: hidden` create a new block formatting context?

译：新创建隐藏的块级元素文本是否溢出？ **

```html
<div>
    <p>I am floated</p>
    <p>So am I</p>
</div>
```

```css
div {
    overflow: hidden;
}
p {
    float: left;
}
```

解析：是

#### 2.6 Does the `screen` keyword apply to the device's physical screen or the browser's viewport?

译：screen 是适用于设备的物理屏幕还是浏览器的视口？  **

A.Device's physical screen

B. Browser's viewport

```css
@media only screen and (max-width: 1024px) {
    margin: 0;
}
```

解析：B

### 3. html5部分

#### 3.1  Is `<keygen>` a valid HTML5 tag?

译：keygen是否是HTML5标签？

解析：是

#### 3.2 Does the `<bdo>` tag change the direction of text?

译：bdo是否能够改变文本的方向？

解析：是 

```
//补充 dir 必需。定义文本方向。
<bdo dir="rtl">some text</bdo> //txet emos
<bdo dir="ltr">some text</bdo> //some text

```

#### 3.3 Is the above HTML valid?

译：上面的html是否有效

```html
<figure>
	<img src="myimage.jpg" alt="My image">
	<figcaption>
		<p>This is my self portrait.</p>
	</figcaption>
</figure>
```

解析：有效

#### 3.4 In what situation should you use the `<small>` tag?

翻译：哪种情形，我们需要用small标签

A. When you want to create subheading after a `<h1>` element

B. When you want to add copyright information inside a `footer`

C. Both situations

解析 ：A

#### 3.5 If a web page contains organic, multiple `<h1>` tags, will it affect the SEO negativley?

译：如果一个网页包含多个`h1`标签，会影响SEO优化吗？

解析：不会

#### 3.6 If you have a page of search results and want to highlight the search term, what HTML tag would you use?

译：如果你有一个搜索结果页面，想突出搜索词，你会使用什么HTML标签？

A. `strong`        B. `mark `      C. `em`     D. `highlight`

解析 B

#### 3.7 What does the `scoped` attribute do?

译：scoped的作用？

A. Applies style rules to elements succeeding it, but with the same parent element

B. Applies style rules to all children of the `scoped` parent element

C. Applies style rules to IE browsers only

D. None of the above

```html
<article>
    <h1>Hello World</h1>
    <style scoped>
        p {
            color: #FF0;
        }
    </style>
    <p>This is my text</p>
</article>
 
<article>
    <h1>This is awesome</h1>
    <p>I am some other text</p>
</article>
```

解析：B

#### 3.8 Does HTML5 support block-level links?

译：HTML5支持块级链接吗？

```html
<article>
    <a href="#">
        <h1>Hello</h1>
        <p>I am some text</p>
    </a>
</article>
```

解析：支持

#### 3.9 Does the HTML above trigger a http request when the page first loads ?

译：上面的HTML是否在页面第一次加载时触发HTTP请求？

```html
<img src="mypic.jpg" style="visibility: hidden" alt="My picture">
```

解析：会

#### 3.10 Does the HTML above trigger a http request when the page first loads?

```html
<div style="display: none;">
    <img src="mypic.jpg" alt="My photo">
</div>
```

解析：会

#### 3.11 Does `main1.css` have to be downloaded and parsed before `Hello World` is alerted?

译：main1.css会在弹出‘Hello World’之前下载吗？

```
<head>
    <link href="main1.css" rel="stylesheet">
    <script>
        alert('Hello World');
    </script>
</head>
```

解析：会

#### 3.12 Does `main1.css` have to be downloaded and parsed before `main2.css` can be fetched?

译：main1.css会下载好后再获取main2.css吗？

```html
<head>
    <link href="main1.css" rel="stylesheet">
    <link href="main2.css" rel="stylesheet">
</head>
```

解析：不会

#### 3.13 Does `main2.css` have to be downloaded and parsed before `Paragraph 1` is rendered on the page?

译：main2.css下载好再渲染Paragraph 1页面吗？

```html
<head>
    <link href="main1.css" rel="stylesheet">
</head>
<body>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
    <link href="main2.css" rel="stylesheet">
</body>
```

解析：是

### 4.JavaScript部分

#### 4.1 What does the above statement evaluate to?

```javascript
"1" + 2 + "3" + 4;
```

A. 10      B.1234     C. 37

解析：B

#### 4.2 What does the above statement evaluate to?

```
4 + 3 + 2 + "1"
```

A. 10      B. 4321     C. 91 

解析：C

#### 4.3 What is alerted?

```javascript
var foo = 1;
function bar() {
	foo = 10;
	return;
	function foo() {}
}
bar();
alert(foo);
```

解析：1

#### 4.4 What is alerted?

```javascript
function bar() {
    return foo;
    foo = 10;
    function foo() {}
    var foo = 11;
}
alert(typeof bar());
```

解析：function

#### 4.5 What is the order of values alerted?

```
var x = 3;

var foo = {
    x: 2,
    baz: {
        x: 1,
        bar: function() {
            return this.x;
        }
    }
}

var go = foo.baz.bar;

alert(go());
alert(foo.baz.bar());
```

解析： 3     1

#### 4.6What value is alerted?

```javascript
var x   = 4,
    obj = {
        x: 3,
        bar: function() {
            var x = 2;
            setTimeout(function() {
                var x = 1;
                alert(this.x);
            }, 1000);
        }
    };
obj.bar();
```

解析：4

#### 4.7What value is alerted?

```javascript
x = 1;
function bar() {
    this.x = 2;
    return x;
}
var foo = new bar();
alert(foo.x);
```

解析：2

#### 4.8What value is alerted?

```javascript
function foo(a) {
    alert(arguments.length);
}
foo(1, 2, 3);
```

解析：3

#### 4.9What value is alerted?

```javascript
var foo = function bar() {}; 
alert(typeof bar);
```

解析：undefined

#### 4.10 What value is alerted?

```javascript
var arr = [];
arr[0]  = 'a';
arr[1]  = 'b';
arr.foo = 'c';
alert(arr.length);
```

解析：2

#### 4.11 What value is alerted?

```javascript
function foo(a) {
    arguments[0] = 2;
    alert(a);
}
foo(1);
```

解析：2

#### 4.12 What value is alerted?

```javascript
function foo(){}
delete foo.length;
alert(typeof foo.length);
```

解析：number