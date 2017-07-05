# [腾讯前端面试题](http://blog.csdn.net/bedisdover/article/details/70163587)

### 1. 写出以下程序的输出

```javascript
var test =  {
  foo: "test",
  a: function() {
    var self = this;
    console.log(this.foo);
    console.log(self.foo);

    (function() {
      console.log(this.foo);
      console.log(self.foo);
    })();
  }
}

test.a();
```

### 2. 以下程序输出

```javascript
console.log(1);
setTimeout(function() {
  console.log(2);
}, 1000);
setTimeout(function() {
  console.log(3);
}, 0);
console.log(4);

```

### 3. 点击button后，发生什么

```javascript
for (var i = 0; i < 5; i++) {
  var button = document.createElement("button");
  button.innerHTML="click";
  document.body.appendChild(button);
  button.onclick = function() {
    alert(i);
  }
}
```

### 4. 下列程序输出

考察 split(), join(), slice(), reverse()等函数的使用

### 5. 开放性试题

1. 对于20亿QQ号，每个QQ号都有若干标签，如： 
   12345678：王者荣耀、电影、足球 
   12345679：足球、音乐 
   … 
   设计一个检索系统，要求输入标签，输出所有拥有该标签的QQ号，输入多个标签时，输出检索结果的并集
2. 广告投放包含广告位、时间、性别、年龄分布、地域等因素，广告不可重复投放，如： 
   广告A：1号广告位、2017年4月1日、上海 
   广告B：1号广告位、2017年4月1日、20~30岁男性 
   上述广告A与广告B重复，设计系统检查是否存在重复的广告