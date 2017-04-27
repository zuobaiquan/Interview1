# css面试的知识点，排序不分难易,答案仅供参考

## 描述一下渐进增强和优雅降级之间的不同吗?
- 优雅降级：Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会检查以确认它们是否能正常工作。由于IE独特的盒模型布局问题，针对不同版本的IE的hack实践过优雅降级了,为那些无法支持功能的浏览器增加候选方案，使之在旧式浏览器上以某种形式降级体验却不至于完全失效.
- 渐进增强：从被所有浏览器支持的基本功能开始，逐步地添加那些只有新式浏览器才支持的功能,向页面增加无害于基础浏览器的额外样式和功能的。当浏览器支持时，它们会自动地呈现出来并发挥作用。

## 在书写高效CSS时会有哪些问题需要考虑？
1.样式是：从右向左的解析一个选择器；
2.ID最快，Universal最慢有四种类型的key selector，解析速度由快到慢依次是：ID、class、tag和universal ；
3.不要tag-qualify（永远不要这样做ul#main-navigation{}ID已经是唯一的，不需要Tag来标识，这样做会让选择器变慢。）；
4.后代选择器最糟糕（换句话说，下面这个选择器是很低效的：html body ul li a{}）；
5.想清楚你为什么这样写；
6.CSS3的效率问题（CSS3选择器（比如:nth-child）能够漂亮的定位我们想要的元素，又能保证我们的CSS整洁易读。但是这些神奇的选择器会浪费很多的浏览器资源。）；
7.我们知道#ID速度是最快的，那么我们都用ID，是不是很快。但是我们不应该为了效率而牺牲可读性和可维护性。

## 解释一下你对盒模型的理解，以及如何在CSS中告诉浏览器使用不同的盒模型来渲染你的布局。
CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。
### 组成部分
- Margin(外边距) - 清除边框外的区域，外边距是透明的。
- Border(边框) - 围绕在内边距和内容外的边框。
- Padding(内边距) - 清除内容周围的区域，内边距是透明的。
- Content(内容) - 盒子的内容，显示文本和图像。

## 解释下浮动和它的工作原理。
关于浮动我们需要了解，浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。要想使元素浮动，必须为元素设置一个宽度（width）。虽然浮动元素不是文档流之中，但是它浮动后所处的位置依然是在浮动之前的水平方向上。由于浮动框不在文档的普通流中，所以文档的普通流中的块框表现得就像浮动框不存在一样，下面的元素填补原来的位置。有些元素会在浮动元素的下方，但是这些元素的内容并不一定会被浮动的元素所遮盖，对内联元素进行定位时，这些元素会考虑浮动元素的边界，会围绕着浮动元素放置。也可以把浮动元素想象成是被块元素忽略的元素，而内联元素会关注浮动元素的。

## 列举不同的清除浮动的技巧，并指出它们各自适用的使用场景。
1.使用空标签清除浮动。这种方法是在所有浮动标签后面添加一个空标签定义css clear:both.弊端就是增加了无意义标签。
2.使用overflow。给包含浮动元素的父标签添加css属性overflow:auto;zoom:1;zoom:1用于兼容IE6。
3.使用after伪对象清除浮动。该方法只适用于非IE浏览器。具体写法可参照以下示例。使用中需注意以下几点。一、该方法中必须为需要清除浮动元素的伪对象中设置height:0，否则该元素会比实际高出若干像素；二、content属性是必须的，但其值可以为空，content属性的值设为”.”，空亦是可以的。
4.浮动外部元素 
此三种方法各有利弊，使用时应择优选择，比较之下第二种方法更为可取。

## 请解释一下relative、fixed、absolute和static元素的区别？
自行google，答案太多

## 请解释一下inline和inline-block的区别？
自行google，答案太多

## 解释下CSS sprites，以及你要如何在页面或网站中使用它，写个例子。
CSS Sprites其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的“background-image”，“background-repeat”，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。

## 如何视觉隐藏网页内容，只让它们在屏幕阅读器中可用？
- display:none;的缺陷搜索引擎可能认为被隐藏的文字属于垃圾信息而被忽略屏幕阅读器（是为视觉上有障碍的人设计的读取屏幕内容的程序）会忽略被隐藏的文字。
- visibility:hidden;的缺陷这个大家应该比较熟悉就是隐藏的内容会占据他所应该占据物理空间
- overflow:hidden;一个比较合理的方法

## 你用过媒体查询，或针对移动端的布局/CSS吗？
媒体查询，就是响应式布局。通过不同的媒介类型和条件定义样式表规则。媒介查询让CSS可以更精确作用于不同的媒介类型和同一媒介的不同条件。
语法结构及用法：@media 设备名 only （选取条件） not （选取条件） and（设备选取条件），设备二{sRules}。
示例如下：
```bash
/* 当浏览器的可视区域小于980px */
@media screen and （max-width： 980px） {
  #wrap {width： 90%; margin:0 auto;}
  #content {width： 60%;padding： 5%;}
  #sidebar {width： 30%;}
  #footer {padding： 8% 5%;margin-bottom： 10px;}
}

/* 当浏览器的可视区域小于650px */
@media screen and （max-width： 650px） {
 #header {height： auto;}
 #searchform {position： absolute;top： 5px;right： 0;}
 #content {width： auto; float： none; margin： 20px 0;}
 #sidebar {width： 100%; float： none; margin： 0;}
 }
```
##　你会哪些CSS预处理器？
1. sass
2. less

## 简单布局
一个页面上两个div左右铺满整个浏览器，要保证左边的div一直为100px，右边的div跟随浏览器大小变化（比如浏览器为500，右边div为400，浏览器为900，右边div为800），请写出大概的css代码。
### 方法一
```bash
<div id="left">Left sidebar</div>
<div id="content">Main Content</div>
```
```bash
<style type="text/css">
* {
    margin: 0;
    padding: 0;
}
#left {
    float: left;
    width: 220px;
    background-color: green;
}
#content {
    background-color: orange;
    margin-left: 220px;
    /*==等于左边栏宽度==*/
}
</style>
```

### 方法二
```bash
//html
<div class='box'>
	<div class='left'></div> 
	<div class='right'></div>
</div>
```
```bash
//css
.box {
    width: 400px;
    height: 100px;
    display: flex;
    flex-direction: row;
    align-items: center;
    border: 1px solid #c3c3c3;
}
.left {
    flex-basis：100px;
    -webkit-flex-basis: 100px;/* Safari 6.1+ */
    background-color: red;
    height: 100%;
}
.right {
    background-color: blue;
    flex-grow: 1;
}
```