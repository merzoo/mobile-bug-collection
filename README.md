# mobile-bug-collection

> 移动端 bug 汇总，主要是日常收集的一些移动端 bug 和解决方案

## 目录

- [点击样式闪动](#1.1)
- [屏蔽用户选择](#1.2)
- [移动端如何清除输入框内阴影](#1.3)
- [禁止文本缩放](#1.4)
- [如何禁止保存或拷贝图像](#1.5)
- [解决字体在移动端比例缩小后出现锯齿的问题](#1.6)
- [设置 input 里面 placeholder 字体的大小](#1.7)
- [audio 元素和 video 元素在 ios 和 andriod 中无法自动播放](#1.8)
- [手机拍照和上传图片](#1.9)
- [输入框自动填充颜色](#1.10)
- [开启硬件加速](#1.11)
- [用户设置字号放大或者缩小导致页面布局错误](#1.12)
- [移动端去除 type 为 number 的箭头](#1.13)
- [实现横屏竖屏的方案](#1.14)
- [fastclick 导致下拉框焦点冲突](#1.15)
- [ios input 不能自动获取焦点](#1.16)
- [去除 webkit 默认的滚动条](#1.17)
- [video 不能自动播放](#1.18)
- [inline-block 元素使用 vertical-align 后，父元素高度被莫名撑开](#1.19)
- [背景图片没实现自适应](#1.20)
- [css3 translate3d 平移效果后的元素子元素闪动](#1.21)
- [position:fixed 固定效果](#1.22)
- [IOS 键盘字母输入，默认首字母大写](#1.23)
- [select 下拉选择设置右对齐](#1.24)
- [通过 transform 进行 skew 变形，rotate 旋转会造成出现锯齿现象](#1.25)
- [移动端点击延迟](#1.26)
- [移动端点透问题](#1.27)
- [关于 iOS 系统中，中文输入法输入英文时，字母之间可能会出现一个六分之一空格](#1.28)
- [Retina 屏的 1px 边框](#1.29)

### <span id="1.1">点击样式闪动</span>

Q: 当你点击一个链接或者通过 Javascript 定义的可点击元素的时候，它就会出现一个半透明的灰色背景。

A:根本原因是-webkit-tap-highlight-color，这个属性是用于设定元素在移动设备（如 Adnroid、iOS）上被触发点击事件时，响应的背景框的颜色。建议写在样式初始化中以避免所以问题：div,input(selector) {-webkit-tap-highlight-color: rgba(0,0,0,0);}另外出现蓝色边框：outline:none；

```css
-webkit-tap-highlight-color: rgba (255, 255, 255, 0);
// i.e . Nexus5/Chrome and Kindle Fire HD 7 ''
-webkit-tap-highlight-color: transparent;
```

### <span id="1.2">屏蔽用户选择</span>

Q: 禁止用户选择页面中的文字或者图片

A:代码如下

```css
-webkit-touch-callout: none;
-webkit-user-select: none;
-khtml-user-select: none;
-moz-user-select: none;
-ms-user-select: none;
user-select: none;
```

### <h3 id="1.3">移动端如何清除输入框内阴影</h3>

Q: 在 iOS 上，输入框默认有内部阴影，但无法使用 box-shadow 来清除，如果不需要阴影，可以这样关闭：

A:代码如下

```css
-webkit-appearance: none;
```

### <h3 id="1.4">禁止文本缩放</h3>

Q: 禁止文本缩放

A:代码如下

```css
-webkit-text-size-adjust: 100%;
```

### <h3 id="1.5">如何禁止保存或拷贝图像</h3>

Q: 如何禁止保存或拷贝图像

A:代码如下

```css
img {
  -webkit-touch-callout: none;
}
```

### <h3 id="1.6">解决字体在移动端比例缩小后出现锯齿的问题</h3>

Q: 解决字体在移动端比例缩小后出现锯齿的问题

A:代码如下

```css
-webkit-font-smoothing: antialiased;
```

### <h3 id="1.7">设置 input 里面 placeholder 字体的大小</h3>

Q: 设置 input 里面 placeholder 字体的大小

A:代码如下

```css
::-webkit-input-placeholder {
  font-size: 10pt;
}
```

### <h3 id="1.8">audio 元素和 video 元素在 ios 和 andriod 中无法自动播放</h3>

Q: audio 元素和 video 元素在 ios 和 andriod 中无法自动播放

A:代码如下,触屏及播放

```javascript
$("html").one("touchstart", function() {
  audio.play();
});
```

### <h3 id="1.9">手机拍照和上传图片</h3>

Q: 针对 file 类型增加不同的 accept 字段

A:代码如下

```html
<input type="file">的accept 属性
<!-- 选择照片 -->
<input type=file accept="image/*">
<!-- 选择视频 -->
<input type=file accept="video/*">
```

### <h3 id="1.10">输入框自动填充颜色</h3>

Q: 针对 input 标签已经输入过的，会针对曾经输入的内容填充黄色背景，这是 webkit 内核自动添加的，对应的属性是 autocomplete,默认是 on,另对应的样式是 input:-webkit-autofill 且是不可更改的。

A:方案如下
1 设置标签的 autocomplete="off",亲测无效可能
2 设置盒子的内阴影为你常态的颜色（下面以白色为例）

```css
box-shadow: 0 0 0 1000px #fff inset;
-webkit-box-shadow: 0 0 0px 1000px #fff inset;
```

### <h3 id="1.11">开启硬件加速</h3>

Q: 优化渲染性能

A:代码如下

```css
-webkit-transform: translate3d(0, 0, 0);
-moz-transform: translate3d(0, 0, 0);
-ms-transform: translate3d(0, 0, 0);
transform: translate3d(0, 0, 0);
```

### <h3 id="1.12">用户设置字号放大或者缩小导致页面布局错误</h3>

```html
 body  
    {  
        -webkit-text-size-adjust: 100% !important;  
        text-size-adjust: 100% !important;  
        -moz-text-size-adjust: 100% !important;  
    }
```

### <h3 id="1.13">移动端去除 type 为 number 的箭头</h3>

```css
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none !important;
  margin: 0;
}
```

### <h3 id="1.14">实现横屏竖屏的方案</h3>

- css 用 css3 媒体查询，缺点是宽度和高度不好控制

```css
@media screen and (orientation: portrait) {
  .main {
    -webkit-transform: rotate(-90deg);
    -moz-transform: rotate(-90deg);
    -ms-transform: rotate(-90deg);
    transform: rotate(-90deg);
    width: 100vh;
    height: 100vh;
    /*去掉overflow 微信显示正常，但是浏览器有问题，竖屏时强制横屏缩小*/
    overflow: hidden;
  }
}

@media screen and (orientation: landscape) {
  .main {
    -webkit-transform: rotate(0);
    -moz-transform: rotate(0);
    -ms-transform: rotate(0);
    transform: rotate(0);
  }
}
```

- js 判断屏幕的方向或者 resize 事件

```javascript
var evt = "onorientationchange" in window ? "orientationchange" : "resize";
window.addEventListener(
  evt,
  function() {
    var width = document.documentElement.clientWidth;
    var height = document.documentElement.clientHeight;
    $print = $("#print");
    if (width > height) {
      $print.width(width);
      $print.height(height);
      $print.css("top", 0);
      $print.css("left", 0);
      $print.css("transform", "none");
      $print.css("transform-origin", "50% 50%");
    } else {
      $print.width(height);
      $print.height(width);
      $print.css("top", (height - width) / 2);
      $print.css("left", 0 - (height - width) / 2);
      $print.css("transform", "rotate(90deg)");
      $print.css("transform-origin", "50% 50%");
    }
  },
  false
);
```

### <h3 id="1.15">fastclick 导致下拉框焦点冲突</h3>

Q: 移动端使用 fastclick 之后，在 ios 环境下，有几个连续的下拉框 第一个 select 框突然填充了第二个下拉框的内容。
A:根本原因是 Fastclick 导致 IOS 下多个 select ，点击某一个，焦点不停变换的 bug。修改源码，在 onTouchStart 事件内判断设备是否为 IOS，再判断当前 nodeName 是否为 select，如果是 return false 去阻止 fastClick 执行其他事件

```javascript
//line 391行
FastClick.prototype.onTouchStart = function(event) {
  //在其方法中添加判断 符合ios select的时候 不返回事件
  if (deviceIsIOS && this.targetElement == "select") this.targetElement = null;
  event.preventDefault();
};

//line521 或者讲源码中 有关touchEnd判断非ios或者非select的事件注释，
if (!deviceIsIOS || targetTagName !== "select") {
  this.targetElement = null;
  event.preventDefault();
}
```

### <h3 id="1.16">ios input 不能自动获取焦点</h3>

Q: 如题，希望在某个页面时可以自动让输入框获取焦点
A: 解决方案：

```javascript
document.addEventListener("touchstart", function(e) {
  document.getElementById("focus").focus();
});
```

> 不能把 focus 封装起来起来触发，那样也无效
> 备注：具体实现效果待验证，希望有时间的可以验证追加可能的问题以及补充方案

### <h3 id="1.17">去除 webkit 默认的滚动条</h3>

Q: 如题
A: 解决方案：

```css
element::-webkit-scrollbar {
  display: none;
}
```

### <h3 id="1.18">video 不能自动播放</h3>

Q: 如题
A: 解决方案：
(1) autoplay 及 js 控制播放，仍然有部分设备不起作用
(2)

```javascript
$("html").one("touchstart", function() {
  video.play();
});
```

### <h3 id="1.19">inline-block 元素使用 vertical-align 后，父元素高度被莫名撑开</h3>

Q: 如题，不一定出现在移动端，但是移动端会效果比较严重，一般是用于设置同行内容垂直居中的
A: 解决方案：

```css
.par {
  font-size: 0;
}
```

### <h3 id="1.20">背景图片没实现自适应</h3>

Q: 如题
A: 解决方案：用 background-size

```css
element {
  background-size: 100% 100%;
}
```

### <h3 id="1.21">css3 translate3d 平移效果后的元素子元素闪动</h3>

Q: 应用 css3 translate3d 平移效果后的标签元素，在 ios 上的 safari 以及 app 的 webview 中会出现页面加载完成后其子元素闪动现象，具体如下：

```html
<ul style=”-webkit-transform: translate3d(0, 0, 0); -webkit-transition: 0ms; “>
<li><img src=”http://pic2.58.com/m58/m3/img/imglogo_gray.png” ref=”http://1.pic.58control.cn/p1/big/n_22998799743506.jpg”></li>
</ul>
```

A: 解决方案：

1.  可在其子元素中统一添加和其相同的属性，具体如下：

```html
<ul style=”-webkit-transform: translate3d(0, 0, 0); -webkit-transition: 0ms; “>
<li style=”-webkit-transform: translate3d(0, 0, 0); “><img src=”http://pic2.58.com/m58/m3/img/imglogo_gray.png” ref=”http://1.pic.58control.cn/p1/big/n_22998799743506.jpg”></li>
</ul>
```

2.  在其元素中添加如下属性：

```css
-webkit-backface-visibility: hidden; (设置进行转换的元素的背面在面对用户时是否可见：隐藏）
-webkit-transform-style: preserve-3d; (设置内嵌的元素在3D 空间如何呈现：保留3D ）
```

### <h3 id="1.22">position:fixed 固定效果</h3>

Q: 当给指定元素添加 position:fixed 时首次加载页面完成后，滑动整个网页，添加此样式的元素会跟随页面滚动（目的是固定此元素）。
A: 解决方案：
为其元素添加如下 css 属性即可：

```css
-webkit-transform：translate3d(0,0,0)
```

备注：此方案不一定有效，需要后续验证或者提供更好的方案

### <h3 id="1.23">IOS 键盘字母输入，默认首字母大写</h3>

Q: 如题
A: 解决方案：

```html
<input type="text" autocapitalize="off" />
```

### <h3 id="1.24">select 下拉选择设置右对齐</span>

Q: 如题，默认是左对齐，产品有其他需求
A: 解决方案：

```css
select option {
  direction: rtl;
}
```

### <h3 id="1.25">通过 transform 进行 skew 变形，rotate 旋转会造成出现锯齿现象</h3>

Q: 如题
A: 解决方案：

```css
-webkit-transform: rotate(-4deg) skew(10deg) translateZ(0);
transform: rotate(-4deg) skew(10deg) translateZ(0);
outline: 1px solid rgba(255, 255, 255, 0);
```

### <h3 id="1.26">移动端点击延迟</h3>

Q: 如题
A: 解决方案：引用 fastclick.js

## <h3 id="1.27">移动端点透问题</h3>

Q: 如题,当点击绝对定位元素的时候，下面的元素虽然被遮盖，但也被触发了。
A: 原因是：touchstart 早于 touchend 早于 click。 亦即 click 的触发是有延迟的，这个时间大概在 300ms 左右，也就是说我们 tap 触发之后蒙层隐藏， 此时 click 还没有触发，300ms 之后由于蒙层隐藏，我们的 click 触发到了下面的 a 链接上。
解决方案：

1.  尽量都使用 touch 事件来替换 click 事件。例如用 touchend 事件(推荐)。
2.  用 fastclick，https://github.com/ftlabs/fastclick
3.  用 preventDefault 阻止 a 标签的 click
4.  延迟一定的时间(300ms+)来处理事件 （不推荐）
5.  以上一般都能解决，实在不行就换成 click 事件。

## <h3 id="1.28">关于 iOS 系统中，中文输入法输入英文时，字母之间可能会出现一个六分之一空格</h3>

Q: 如题
A: 解决方案：通过正则替换

```javascript
this.value = this.value.replace(/\u2006/g, "");
```

## <h3 id="1.29">Retina 屏的 1px 边框</h3>

Q: 如题
A: 解决方案：

```css
element {
  border-width: thin;
}
```
