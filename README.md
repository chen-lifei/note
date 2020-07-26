## HTML&CSS

#### flex布局

2009年，W3C 提出了一种新的布局----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持。Flex为Flexiable Box的缩写，就是弹性布局。设为flex布局后，子元素的float, clear, vertical-align都将失效。

```css
//容器的属性
flex-direction: row | row-reverse | column | column-reverse;
flex-wrap: nowrap | wrap | wrap-reverse;
flex-flow: <flex-direction> || <flex-wrap>; flex-flow: row nowrap(默认值);
justify-content: flex-start | flex-end | center | space-between | space-around(每个项目两端的间隔相等);
align-items: flex-start | flex-end | center | baseline(项目第一行文字的基线对齐) | stretch(如果项目未设置高度或设为auto将占满整个容器的高度);

//项目的属性
order: <integer>(数值越小则越靠前);
flex-grow: <number> /** default 0 (定义项目的放大倍数) **/;
flex-shrink: <number> /** default 1 (定义项目的缩小倍数) **/;
flex-basis: <length> | auto /** (在分配多余的空间之前，项目占据主轴的空间) **/;
flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ] /** flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选 **/;
align-self: auto | flex-start | flex-end | baseling | stretch /** 该属性允许单个项目与其他项目不一样的属性。默认属性为auto，表示默认与父元素的align-items一样的属性，若没有父元素，则为stretch **/;
```

#### 垂直居中

```css
/** 居中div **/
.div1 {
	width: 100px;
	height: 100px;
	margin: 0 auto;
	background-color: plum;
}

/** 居中浮动元素 **/
.Bx1 {
	height: 200px;
	width: 200px;
	background-color: purple;
}
.div3 {
	float: left;
	height: 50px;
	width: 50px;
	margin-left: 50%;
	margin-top: 50%;
	transform: translate(-50%,-50%);
	background-color: plum;
}

/** 居中绝对定位的div **/
.Bx {
	position: relative;
	height: 200px;
	width: 200px;
	background-color: pink;
}
.div2 {
	position: absolute;
	height: 50px;
	width: 50px;
	top: 50%;
	left: 50%;
	/*margin-left: -25px;
	margin-top: -25px;*/
	transform: translate(-50%,-50%);  /* 若translate的第二个参数未给出，则默认为0 */
	background-color: plum;
}

/** 使用flex弹性布局居中 **/
.Bx2 {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 200px;
	width: 200px;
	background-color: pink;
}
.div4 {
	height: 50px;
	width: 50px;
	background-color: plum;
}
```

#### 清除浮动

```css
.clearfix:after{
    content: "";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
```

#### BFC

BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

##### 创建BFC

- float的值不为none
- position的值不为static和relative
- display的值是inline-block、table-cell、flex、table-caption或者inline-flex
- overflow的值不是visible，而是auto, scroll, hidden

##### BFC解决的问题

- 浮动元素令父元素高度塌陷
- 两栏自适应布局
- 外边距垂直方向重合

#### 三栏布局

```css
/* float布局，此时需要清除main的浮动，以免影响其他布局 */
<div class="main clearfix">
	<div class="left">left</div>
	<div class="right">right</div>
	<div class="center">center</div>
</div>

.left {
	float: left;
	width: 200px;
	height: 200px;
	background-color: plum;
}
.right {
	float: right;
	width: 200px;
	height: 200px;
	background-color: plum;
}
.center {
	overflow: hidden;
	margin-left: 200px;
	margin-right: 200px;
	background-color: pink;
}
.clearfix::after {
	content: '';
	display: block;
	height: 0;
	clear: both;
	visibility: hidden;
}

<div class="main">
	<div class="left">left</div>
	<div class="center">center</div>
	<div class="right">right</div>
</div>
/* position */
.main {
	position: relative;
}
.left, .right, .center {
	position: absolute;
}
.left {
	left: 0;
	width: 200px;
	height: 200px;
	background-color: plum;
}
.center {
	left: 200px;
	right: 200px;
	background-color: pink;
}
.right {
	right: 0;
	width: 200px;
	height: 200px;
	background-color: plum;
}
/* table布局，没有兼容性问题，但不利于SEO */
.main {
	display: table;
}
.left,.center,.right{
    display: table-cell;
}

/* flex布局，存在兼容性问题，只能支持IE9以上版本 */
.main {
	display: flex;
}
.left {
	width: 200px;
	height: 200px;
	background-color: plum;
}
.center {
	width: calc(100% - 400px);
	height: 300px;
    word-break: break-all;
	background-color: pink;
}
.right {
	width: 200px;
	height: 200px;
	background-color: plum;
}

/* grid布局，兼容性很差 */
.main {
	display: grid;
	grid-template-columns: 1fr 4fr 1fr;
}
```

#### 两栏布局

#### 动画

##### transition

- <' [transition-property](http://css.cuishifeng.cn/transition-property.html) '>：检索或设置对象中的参与过渡的属性
- <' [transition-duration](http://css.cuishifeng.cn/transition-duration.html) '>：检索或设置对象过渡的持续时间
- <' [transition-timing-function](http://css.cuishifeng.cn/transition-timing-function.html) '>：检索或设置对象中过渡的动画类型，linear、ease、ease-in、ease-out、ease-in-out、steps
- <' [transition-delay](http://css.cuishifeng.cn/transition-delay.html) '>：检索或设置对象延迟过渡的时间

##### animation

使用关键帧@keyframes：@keyframes move { 0% {} 50% {} 100%{}}

#### 盒模型

- w3c的标准盒模型，border-sizing：content-box，此时盒子大小=width+padding+border
- IE盒模型，border-sizing:border-box，此时盒子大小=width

#### H5新特性

- 语义化标签：语义化标签是指有自己的含义的标签，可以让机器和编程人员更好的理解和阅读，同时有利于搜索引擎优化，有article、header、footer、section、nav、aside等
- 视频video和音频audio
- 展示图形的canvas元素
- 新的表单特性和函数：placeholder、autocomplete、autofocus、required
- storage：localStorage(将数据保存在客户端本地，没有手动删除的话将一直存在；不与服务器通信)、sessionsStorage(将数据保存在session，浏览器关闭则立即消失；不与服务器通信)。（ps：cookie的大小只有4K，所以可以用来存储较小的数据，与服务器通信，在有效期限之前不会消失）
- WebSocket：WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。

## JavaScript

#### 继承

#### 原型链

![image-20200725180008009](F:\learn by myself\图片笔记\原型链.png)

#### this指向

普通函数调用：widow
构造函数调用：实例对象，原型对象里面的方法的this也指向实例对象
对象方法调用：该方法所属对象本身
事件绑定方法：绑定事件对象
定时器函数：window
立即执行函数：window

#### 设计模式

#### call, apply, bind, new实现

new：new创建了一个对象，并且继承了原型链上的属性和方法，若没有返回值，this就指向创建的实例对象

call：改变this的指向，第一个参数为this的指向，后面的参数为函数的参数，按顺序传入

apply：改变this的指向，第一个参数为this的指向，第二个参数为数组

bind：改变this的指向，返回一个函数。当函数只是普通调用时，this指向bind的第一个参数；若返回的函数被当作构造函数调用时，前面绑定的this无效，指向new操作符创建的对象

#### 防抖节流

防抖：对于短时间内连续触发的事件，防抖可以实现在某个时间期限内，事件处理函数只执行一次。

节流：指定时间间隔内只会执行一次任务，不管事件触发有多频繁，它只在周期内执行一次。

#### let, var, const 区别

- 使用 var 声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象
- 使用 let 声明的变量，其作用域为该语句所在的代码块内，不存在变量提升
- 使用 const 声明的是常量，在后面出现的代码中不能再修改该常量的值

#### Event Loop

JS可以执行同步和异步操作，也就是存在同步任务和异步任务。同步任务在主线程上执行，就形成了一个执行栈；异步任务是通过回调函数实现的，相关回调函数添加到消息队列中。

执行顺序：

1. 先执行执行栈里的同步任务；
2. 异步任务被放到消息队列中去，进入等待状态；
3. 当执行栈里的同步任务全部执行完毕后，系统就会按次序读取消息队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。

主线程不断重复上述三个步骤，这就是事件循环。

#### promise使用及实现

```javascript
const promise = new Promise((resolve, reject) {
    if(err) {
    	reject(err)
	} else {
        resolve(data)
    }
})

// promise生成实例后，可以使用then方法分别指定resolve状态和reject状态的回调函数
promise.then(function(data) {
    console.log(data);
}, function(erroe) {
    console.log(error);
})
```

#### promise并行执行和顺序执行

#### 闭包

闭包指有权访问另一个函数作用域的变量的函数。

缺点：闭包会由于变量没有释放内存而导致内存占用过高

#### 垃圾回收和内存泄漏

JS最常见的垃圾回收方式是标记清除

内存泄漏：全局变量、闭包、定时器

#### 数组方法

#### 数组乱序,数组扁平化

#### 事件委托

#### 事件监听

#### 事件模型

#### typescript



## Vue

#### vue数据双向绑定原理

#### vue computed原理

#### vue编译器结构图

#### 生命周期

#### vue组件通信

#### mmvm（mvvm）模式

#### mvc模式理解

#### vue dom diff

#### vuex

#### vue-router

## 网络

#### HTTP1, HTTP2, HTTPS

#### 浏览从输入网址到回车发生了什么

#### 前端跨域

#### 浏览器缓存

#### cookie, session, token, localstorage, sessionstorage

#### 状态码

#### TCP连接(三次握手, 四次挥手)
