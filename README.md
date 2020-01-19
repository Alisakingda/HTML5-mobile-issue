# H5 项目常见问题及注意事项

## H5 页面窗口自动调整到设备宽度，并禁止用户缩放页面

> 方法一

```html
<meta
  name="viewport"
  content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"
/>
```

> 方法二

```js
var phoneWidth = parseInt(window.screen.width)
var phoneScale = phoneWidth / 640
var ua = navigator.userAgent
if (/Android (\d+\.\d+)/.test(ua)) {
  var version = parseFloat(RegExp.$1)
  if (version > 2.3) {
    document.write(
      '<meta name="viewport" content="width=640, minimum-scale = ' +
        phoneScale +
        ', maximum-scale = ' +
        phoneScale +
        ', target-densitydpi=device-dpi">'
    )
  } else {
    document.write('<meta name="viewport" content="width=640, target-densitydpi=device-dpi">')
  }
} else {
  document.write('<meta name="viewport" content="width=640, user-scalable=no, target-densitydpi=device-dpi">')
}
```

## meta 标签

```html
<!-- 设置缩放 -->
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no, minimal-ui" />
<!-- 可隐藏地址栏，仅针对IOS的Safari（注：IOS7.0版本以后，safari上已看不到效果） -->
<meta name="apple-mobile-web-app-capable" content="yes" />
<!-- 仅针对IOS的Safari顶端状态条的样式（可选default/black/black-translucent ） -->
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<!-- IOS中禁用将数字识别为电话号码/忽略Android平台中对邮箱地址的识别 -->
<meta name="format-detection" content="telephone=no, email=no" />
<!-- 清除缓存 -->
<meta http-equiv="pragma" content="no-cache" />
<meta http-equiv="cache-control" content="no-cache" />
<meta http-equiv="expires" content="0" />
<!-- 启用360浏览器的极速模式(webkit) -->
<meta name="renderer" content="webkit" />
<!-- 避免IE使用兼容模式 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true" />
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320" />
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait" />
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait" />
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes" />
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true" />
<!-- UC应用模式 -->
<meta name="browsermode" content="application" />
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app" />
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no" />
```

## font-family

```css
@ --------------------------------------中文字体的英文名称
@ 宋体      SimSun
@ 黑体      SimHei
@ 微信雅黑   Microsoft Yahei
@ 微软正黑体 Microsoft JhengHei
@ 新宋体    NSimSun
@ 新细明体  MingLiU
@ 细明体    MingLiU
@ 标楷体    DFKai-SB
@ 仿宋     FangSong
@ 楷体     KaiTi
@ 仿宋_GB2312  FangSong_GB2312
@ 楷体_GB2312  KaiTi_GB2312
@
@ 说明：中文字体多数使用宋体、雅黑，英文用Helvetica

body { font-family: Microsoft Yahei,SimSun,Helvetica; }
```

## 电话和短信

```html
// 一、打电话
<a href="tel:0755-10086">打电话给:0755-10086</a>

// 二、发短信，winphone系统无效
<a href="sms:10086">发短信给: 10086</a>
```

## 其他

### 点击元素产生背景或边框怎么去掉

```css
//ios用户点击一个链接，会出现一个半透明灰色遮罩, 如果想要禁用，可设置-webkit-tap-highlight-color的alpha值为0去除灰色半透明遮罩；
//android用户点击一个链接，会出现一个边框或者半透明灰色遮罩, 不同生产商定义出来额效果不一样，可设置-webkit-tap-highlight-color的alpha值为0去除部分机器自带的效果；
//winphone系统,点击标签产生的灰色半透明背景，能通过设置<meta name="msapplication-tap-highlight" content="no">去掉；
//特殊说明：有些机型去除不了，如小米2。对于按钮类还有个办法，不使用a或者input标签，直接用div标签
a,button,input,textarea {
	-webkit-tap-highlight-color: rgba(0,0,0,0);
	-webkit-user-modify:read-write-plaintext-only; //-webkit-user-modify有个副作用，就是输入法不再能够输入多个字符
}
// 也可以
* { -webkit-tap-highlight-color: rgba(0,0,0,0); }
//winphone下
<meta name="msapplication-tap-highlight" content="no">
```

### 美化表单元素

```css
//一、使用appearance改变webkit浏览器的默认外观
input,
select {
  -webkit-appearance: none;
  appearance: none;
}

//二、winphone下，使用伪元素改变表单元素默认外观
//1.禁用select默认箭头，::-ms-expand修改表单控件下拉箭头，设置隐藏并使用背景图片来修饰
select::-ms-expand {
  display: none;
}

//2.禁用radio和checkbox默认样式，::-ms-check修改表单复选框或单选框默认图标，设置隐藏并使用背景图片来修饰
input[type='radio']::-ms-check,
input[type='checkbox']::-ms-check {
  display: none;
}

//3.禁用pc端表单输入框默认清除按钮，::-ms-clear修改清除按钮，设置隐藏并使用背景图片来修饰
input[type='text']::-ms-clear,
input[type='tel']::-ms-clear,
input[type='number']::-ms-clear {
  display: none;
}
```

### 超实用的 CSS 样式

```css
//去掉webkit的滚动条——display: none;
//其他参数
::-webkit-scrollba //滚动条整体部分
::-webkit-scrollbar-thumb   //滚动条内的小方块
::-webkit-scrollbar-track   //滚动条轨道
::-webkit-scrollbar-button  //滚动条轨道两端按钮
::-webkit-scrollbar-track-piece  //滚动条中间部分，内置轨道
::-webkit-scrollbar-corner       //边角，两个滚动条交汇处
::-webkit-resizer            //两个滚动条的交汇处上用于通过拖动调整元素大小的小控件

// 禁止长按链接与图片弹出菜单
a,img {
  -webkit-touch-callout: none;
}

// 禁止ios和android用户选中文字
html,
body {
  -webkit-user-select: none;
  user-select: none;
}

// 改变输入框placeholder的颜色值
::-webkit-input-placeholder {
  /* WebKit browsers */
  color: #999;
}
:-moz-placeholder {
  /* Mozilla Firefox 4 to 18 */
  color: #999;
}
::-moz-placeholder {
  /* Mozilla Firefox 19+ */
  color: #999;
}
:-ms-input-placeholder {
  /* Internet Explorer 10+ */
  color: #999;
}
input:focus::-webkit-input-placeholder {
  color: #999;
}

// android上去掉语音输入按钮
input::-webkit-input-speech-button {
  display: none;
}

// 阻止windows Phone的默认触摸事件
/*说明：winphone下默认触摸事件事件使用e.preventDefault是无效的，可通过样式来禁用，如：*/
html {
  -ms-touch-action: none;
} //禁止winphone默认触摸事件
```

### 取消 input 在 ios 下，输入的时候英文首字母的默认大写

```html
<input autocapitalize="off" autocorrect="off" />
```

### 手机拍照和上传图片

```html
//IOS有拍照、录像、选取本地图片功能，部分Android只有选择本地图片功能。Winphone不支持
<input type="file" accept="images/*" />
<input type="file" accept="video/*" />
```

### 屏幕旋转的事件和样式

```js
//JS处理
function orientInit(){
	var orientChk = document.documentElement.clientWidth > document.documentElement.clientHeight?'landscape':'portrait';
	if(orientChk =='lapdscape'){
		//这里是横屏下需要执行的事件
	}else{
		//这里是竖屏下需要执行的事件
	}
}

orientInit();
window.addEventListener('onorientationchange' in window?'orientationchange':'resize', function(){
	setTimeout(orientInit, 100);
},false)

//CSS处理
//竖屏时样式
@media all and (orientation:portrait){   }
//横屏时样式
@media all and (orientation:landscape){   }
```

### audio 元素和 video 元素在 ios 和 andriod 中无法自动播放

```js
//音频，写法一
<audio src="music/bg.mp3" autoplay loop controls>你的浏览器还不支持哦</audio>

//音频，写法二
<audio controls="controls">
	<source src="music/bg.ogg" type="audio/ogg"></source>
	<source src="music/bg.mp3" type="audio/mpeg"></source>
	优先播放音乐bg.ogg，不支持在播放bg.mp3
</audio>

//JS绑定自动播放（操作window时，播放音乐）
$(window).one('touchstart', function(){
	music.play();
})

//微信下兼容处理
document.addEventListener("WeixinJSBridgeReady", function () {
    music.play();
}, false);

//小结
//1.audio元素的autoplay属性在IOS及Android上无法使用，在PC端正常
//2.audio元素没有设置controls时，在IOS及Android会占据空间大小，而在PC端Chrome是不会占据任何空间
```

### 定位的坑

```js
//fixed定位
//1.ios下fixed元素容易定位出错，软键盘弹出时，影响fixed元素定位
//2.android下fixed表现要比iOS更好，软键盘弹出时，不会影响fixed元素定位
//3.ios4下不支持position:fixed
//解决方案：使用[Iscroll](http://cubiq.org/iscroll-5)，如：
<div id="wrapper">
        <ul>
               <li></li>
               .....
        </ul>
</div>
<script src="iscroll.js"></script>
<script>
	var myscroll;
	function loaded(){
		myscroll=new iScroll("wrapper");
	}
	window.addEventListener("DOMContentLoaded",loaded,false);
</script>


//position定位
//Android下弹出软键盘弹出时，影响absolute元素定位
//解决方案:
var ua = navigator.userAgent.indexOf('Android');
if(ua>-1){
	$('.ipt').on('focus', function(){
		$('.css').css({'visibility':'hidden'})
	}).on('blur', function(){
		$('.css').css({'visibility':'visible'})
	})
}
```

### JS 判断设备

```js
function deviceType() {
  var ua = navigator.userAgent
  var agent = ['Android', 'iPhone', 'SymbianOS', 'Windows Phone', 'iPad', 'iPod']
  for (var i = 0; i < len, (len = agent.length); i++) {
    if (ua.indexOf(agent[i]) > 0) {
      break
    }
  }
}
deviceType()
window.addEventListener('resize', function() {
  deviceType()
})
```

### 消除 transition 闪屏

```css
.css {
  -webkit-transform-style: preserve-3d;
  -webkit-backface-visibility: hidden;
  -webkit-perspective: 1000;
}
```

### 开启硬件加速

```css
.css {
  -webkit-transform: translate3d(0, 0, 0);
  -moz-transform: translate3d(0, 0, 0);
  -ms-transform: translate3d(0, 0, 0);
  transform: translate3d(0, 0, 0);
}
```

### 渲染优化

```
//1.禁止使用iframe（阻塞父文档onload事件）
//2.禁止使用gif图片实现loading效果（降低CPU消耗，提升渲染性能）
//使用CSS3代码代替JS动画；
//开启GPU加速；
//使用base64位编码图片(不小图而言，大图不建议使用)
	// 对于一些小图标，可以使用base64位编码，以减少网络请求。但不建议大图使用，比较耗费CPU。小图标优势在于：
	//1.减少HTTP请求；
	//2.避免文件跨域；
	//3.修改及时生效；
```

### 腾讯方案(确保转屏时宽高获取正确)

```js

var autoScale = function(){
    var ratio = 320/504,   //这是设计稿的宽高比（504是Iphone的高度去掉标题栏高度）
        winW = document.getElement.clientWidth,
        winH = document.getElement.clientHeight,
        ratio2 = winW/winH,
        scale;
    if(ratio<ratio2){
        scale = (winH/504).toString().substring(0, 6);
    }else{
        scale = (winW/320).toString().substring(0, 6);
    }
    var cssText = '-webkit-transform: scale('+scale+');-webkit-transform-origin: top; opacity:1;'
    $('.wrap').attr('style', cssText);
}
setTimeout(function(){
    if(document.documentElement.clientWidth/document.documentElement.clientHeight !== 320/504){
        autoScale();
    }else{
        $('.page').css({'opacity': 1});
    }
}, 300)  //添加一定时长以确保宽高获取正确
window.addEventListener('onorientationchange' in window?'orientationchange':'resize', autoScale, false){
        detectOrientatioin();
}   //切换横竖屏

function detectOrientatioin(){
    if(window.orientation==180 || window.orientation==0){
        //竖屏
    }
    if(window.orientation==90 || window.orientation==-90){
        //横屏
    }
}
```
