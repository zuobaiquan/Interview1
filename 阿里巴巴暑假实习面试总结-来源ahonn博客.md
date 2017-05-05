# [阿里巴巴暑假实习面试总结](http://www.ahonn.me/2017/03/16/alibaba-summer-internship-interview-summary/)

## 一面

面试了大概20分钟左右，整体内容还是比较偏基础。一开始是正常流程的自我介绍，说是三分钟自我介绍，但是我语速比较快的不到两分钟的介绍完了。(刚好是临近中午，原本打算吃饭的，要是去吃饭的话就得在路上面了…）

### CSS 垂直居中

这个写过一篇博文专门总结过，不过面试的时候还是太过紧张没有答全。主要是 Flexbox 布局的垂直居中比较容易忘记。

具体就不再啰嗦了，详情可以查看：[CSS 实现垂直居中](http://www.ahonn.me/2016/06/29/vertical-center-for-css/)

### call 与 apply 的区别，以及性能差别

`call` 与 `apply` 的区别，这是一个老生常谈的面试题了。`call()` 与 `apply()` 都是用于在指定 this 值与参数的情况下调用函数，主要的区别在于除了传入 this 值之外，`apply()` 接收类数组或者类数组对象来作为调用的函数的参数，而 `call()` 则是需要分别传入函数的每一个参数（除第一个参数之外的其他参数）。

> call()方法与apply()方法的作用相同，它们的区别仅在于接收参数的方式不同。对于call()方法而言，第一个参数是this值没有变化，变化的是其余参数都直接传递给函数。换句话说，在使用call()方法时，传递给函数的参数必须逐个列举出来。—— 『JavaScript 高级程序设计』

区别的话基本上只要看过书或者刷过面试题都会知道，但 `call()` 与 `apply()` 之间的性能差别就不是那么常见了。
比较幸运的是，之前在阅读 underscore 源码的时候有注意到这个细节，为此也写过另外的文章：[从 optimizeCb 说起](http://www.ahonn.me/2016/05/03/starting-from-the-optimizeCb/)。

实践证明，在知道调用函数的参数数量时，使用 `call()` 的性能会优于 `apply()`。主要在实现的过程中 `apply()` 需要完成额外的操作（判断第二个参数类数组的长度，etc.）。具体为什么有这种差别，可以在 ECMAScript Language Specification 中查看 [Function.prototype.apply](https://www.ecma-international.org/ecma-262/5.1/#sec-15.3.4.3) 与 [Function.prototype.call](https://www.ecma-international.org/ecma-262/5.1/#sec-15.3.4.4) 的具体实现差异。

**参考链接**

- [javascript - What is the difference between call and apply? - Stack Overflow](http://stackoverflow.com/questions/1986896/what-is-the-difference-between-call-and-apply)
- [javascript - Why is call so much faster than apply? - Stack Overflow](http://stackoverflow.com/questions/23769556/why-is-call-so-much-faster-than-apply)
- [call vs apply · jsPerf](https://jsperf.com/call-apply-segu)

### 什么是闭包

又是一个老生常谈的问题。我的理解比较肤浅，就是 A 函数返回 B 函数，B 函数能够访问 A 函数中的局部变量，使得在 A 外部的作用域中能够使用 B 函数间接操作 A 函数中的局部变量，这样就形成了一个闭包。A 函数中的局部变量与返回的 B 函数一同存在，不会被垃圾回收机制清理（引用还存在）。

> 在计算机科学中，闭包（英语：Closure），又称词法闭包（Lexical Closure）或函数闭包（function closures），是引用了自由变量的函数。这个被引用的自由变量将和这个函数一同存在，即使已经离开了创造它的环境也不例外。—— 维基百科

建议阅读 [『你不知道的 JavaScript（上卷）』](https://book.douban.com/subject/26351021/) 中有关作用域与闭包的部分。

### 什么是尾递归

> 在计算机科学里，尾调用是指一个函数里的最后一个动作是一个函数调用的情形：即这个调用的返回值直接被当前函数返回的情形。这种情形下称该调用位置为尾位置。若这个函数在尾位置调用本身（或是一个尾调用本身的其他函数等等），则称这种情况为尾递归，是递归的一种特殊情形。—— 维基百科

一般递归实现阶乘：

```
function fact(n) {
  if (n == 0 || n == 1) {
    return 1;
  } else {
    return n * fact(n - 1);
  }
}
```

一般递归需要中栈上维护函数的调用信息直到函数返回后才释放，容易发生『栈溢出』错误。但对于尾递归来说，只需要维护一个调用记录。

尾递归实现阶乘：

```
function fact(n) {
  return fact-iter(n, 1);
}

function fact-iter(n, a) {
  if (n == 0) {
    return 1;
  } else if (n == 1) {
    return a;
  } else {
    return fact-iter(n - 1, n * a);
  }
}
```

关于递归与尾递归，在 [『计算机程序的构造和解释』](https://book.douban.com/subject/1148282/)中也有类似的讨论。

### React 的设计理念

这部分答得不是很好，只提到了组件化，单向数据流，Virtual DOM 之类的。

有关 React 的设计思想可以参考这一篇文章：[React 设计思想](https://github.com/react-guide/react-basic)。

### 前端安全（攻击方式与如何防范）

第一反应就是 `XSS` 与 `CSRF`，`XSS` 可以通过对输入数据进行转义来防范，而 `CSRF` 则通过使用 SSL 链接访问资源或者请求中添加验证码来进行防范。

除此之外我漏掉了网络劫持，控制台注入代码等攻击方式，这里有篇文章做了详细介绍：[聊一聊WEB前端安全那些事儿](https://segmentfault.com/a/1190000006672214)。

## 二面

第一次远程视频面试，好紧张。

一开始问了 CSS 中 position 属性的 absolute 的作用以及应用场景，这个基本上没有什么问题。接着叫我拿纸写冒泡排序（手写 T-T），飞快的写完。
然后跟一面一样也问了前端安全相关的问题，一下子都不紧张了.. 没有想象中的难。

### 实现 bind 函数

同样是让我写代码，同样是手写（T-T）。这个问题对我来说不算难，不过只是写了简单的实现，没有考虑其他情况。

```
Function.prototype.bind = Function.prototype.bind || function (context) {
  var self = this;
  return function () {
    return self.apply(context, arguments);
  }
}
```

基本原理就是使用 `apply()` 与闭包，返回包含 `apply()` 的闭包使得 `apply()` 绑定指定作用域，但并未执行。

### 阅读 Underscore 源码的经历

之前拖拖拉拉的阅读完了 Underscore 的源码，并提交了一个小 [Pull Request](https://github.com/jashkenas/underscore/pull/2630)。

在阅读的过程中学到了许多的东西，例如上面提到的 call 与 apply 的性能差别，除此之外还有如何去判断变量的类型，以及如何判断两个变量是否相等，等等。另外也了解到许多闭包的使用场景。

### 阅读其他类库的收获

除了 Underscore 之外还阅读过一点 Bootstrap 和 jQuery，这个博客主题的样式部分的组织方式就是参考了 Bootstrap 的组织方式，另外也稍微阅读过 jQuery中 `$.ajax` 以及事件相关的源码。

在阅读代码的过程中的收获就是学习了一些组织代码的方式，还有如何写才能有利于拓展，更加健壮。其中也学到了一些提高性能的技巧，函数缓存，事件队列之类的。

### 博客主题的开发经历

其实一开始写主题只是想给自己用，之后发现蛮多人也喜欢我这个主题的，并时不时有人中 Github 上提 Issue，这对我是莫大的鼓励。虽然我水平并不是很高，但是写出来的东西有人用感觉真的是特别开心，也特别有动力去改进。

从开始去写主题到现在差不多也一年了，这一年中我从前端小白变成前端大白。在维护的过程中学习到很多东西，虽然目前写得也不是很好，但是我还是会慢慢改进继续维护下去的。

维护的过程中的收获就是，当站在自己的角度看问题与在别人的角度看完全是不一样的，或许有个功能我并不需要，但是有人提了，我就得站在『用户』的角度去思考，去实现。『用户』只关心能不能用，好不好用，而并不关心代码写得怎么样。

### 实习期间遇到得难题

可能我做的工作相对简单，就算不会，基本上靠搜索引擎都能够解决。**我觉得能用 Google 解决的问题不算难题。**以我现在的水平，还达不到遇到的难题 Google 搜索不到的😹

## 三面

三面基本上没有问太过具体的前端相关的问题，大部分是在聊聊看法，聊聊项目。

开始让我用纸画出博客的设计，其实主要还是主题，没什么难度，毕竟代码都是我自己写的。

然后让我介绍一下我熟悉的一个框架，说的 React，提及到了 Vitrual DOM 和 diff 算法，说了一下 diff 算法的大概策略。还有说到组件化，单向数据流等等。幸运的是，我在二面之前刷了 『深入 React 技术栈』这本书，结合之前的实践能够说个大概。

中间有聊到兴趣爱好，我想了想好像只有写代码。听歌应该也算？写代码的时候必定要听歌。我记得去年国庆有一天从起床写到晚上睡觉，差不多写了 11 个小时，那时候正在折腾 React 与 Meteor。我自己都觉得不可思议。

## 总结

可能是运气问题，我觉得我的这几面难度都不高😹。得益于看的书，好多知识点都是书上有的。基本上基础的前端面试题都可以在红宝书上找到，真不愧为前端面试宝典。另外 Github 上的这个博客主题也帮了很大的忙，300+ star 果然还是有点用处的（虽然说 star 不能代表什么，而且的确写得也很水，但作用不可否认）。

最后，基础很重要，基础扎实是基本。但是如果想要有突出的表现还是需要更有深度的研究。需要经常思考总结，不仅仅是浮于表面，更要深入原理。