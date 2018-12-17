## 一 HTML5初识
#### 1.1 HTML5语法变化
HTML5不仅仅是一个标记语言，而是制定了Web应用的标准：更多的语义化标签，新的表单，多媒体，canvas，数据存储，地理应用等等。
HTML5特性验证地址：https://validator.w3.org/
```
标签不再区分大小写
单标签可统一写为<img />，常见的有：area，base，br，col，hr，img，input，link，mata
省略结束标签元素：dt，dd，li，option，p，thead，tbody，tr，td，t
可省略全部标签元素：html，head，body，tbdy
允许省略属性名
允许省略属性值的引号
删除了少量的元素和属性，如 font，HTML5推荐使用CSS来控制
```
H5同样扩展了很多标签的功能：
```js
<figure>
    <figcaption>这是图片</figcaption>		//这里会换行
    <img src="./1.jpg">
</figure>
```

#### 1.2 HTML5网页结构
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
</body>
</html>

```
可以设置多个meta标签：
```js
// 过期时间
<meta http-equiv="Expires" content="Sat Sep 27 16:12:33 CST 2009">
// 禁止从缓存中读取页面
<meta http-equiv="Pragma " content="no-cache ">
// 自动刷新
<meta http-equiv="Refresh" content="2" URL="http://www.a.com"> 
// 网页过期删Cookie
<meta http-equiv="Set-cookie" content="name=value expires=Sat Sep 27 16:12:33 CST 2009,path=/">
```
#### 1.3 HTML5新增元素
```
文档结构元素：
<article>   代表一片文章，内部可包含<article><header><footer><section>
<section>   页面内容进行分块，内部可包含：<h1><article><section>
<nav>       导航条
<aside>     侧边栏
<header>    头部
<footer>    脚注
<hgroup>    组织多个<h1>这样的标题
<figure>    一个独立的图片区域，包含多个图片标签，<figcaption>表示图片区域标题

语义元素：
<mark>      显示页面中重点关注的内容，浏览器通常使用黄色显示
<time>      标注时间，向用户展示，
                datatime属性：标注时间，向计算机展示
                <time datetime="2012-04-01">2012年4月</time>
                <time>2012-02-03</time>

功能元素：
<meter>     表示一个已知最大值和最小值的技术仪表，如电池剩余电量。
<progress>  表示进度条
```
#### 1.4 HTML5新增属性
```
contentEditable
    如果将该属性设为true，那么浏览器会允许开发者直接编辑该HTML元素里的内容，且如果一个HTML元素的父元素是可编辑的，那么他自己默认也是可编辑的。

isContentEditable
    用返回值true、false来判断

designMode
    相当于一个全局的contentEditable属性，如果把整个页面的designMode设置为on，那么所有支持编辑的元素都会变为可编辑状态，除非设置为off，如下所示：
	<body ondbclick="document.designMode='on'">

hidden
    hidden属性可以代替CSS样式中的display属性

spellcheck
    HTML5为<input><textarea>等元素增加了spellcheck属性，支持true、false属性值，以判断是否需要浏览器对文本进行校验，如：对拼错的单词进行提示。

disabled
    新属性disabled直接就可以让input无法选择，而老版的html中要使用:
    disabled="disabled"
```
#### 1.5 语义化标签
本质上新语义标签与<div>、<span>没有区别，使用时除了在HTML结构上需要注意外，其它和普通标签的使用无任何差别，可以理解成<div class="nav"> 相当于 <nav>。尽量避免全局使用header、footer、aside等语义标签。
常见语义化标签有：
```
header 			定义 section 或 page 的页眉。页面的头部
nav 			定义导航链接。一般定义导航
main			定义主要区域 
section 		定义文档中的节 
aside			定义内容之外的内容 侧边栏
footer 			定义 section 或 page 的页脚。
article 		定义文章。
mark 			定义记号文本，自带可改变的背景色，带UI，不常用
figure 			定义媒介内容的分组，以及它们的标题。
figcaption		定义 figure 元素的标题
details			定义元素的细节
summary		    定义可见的 <details> 元素的标题。
progress		定义任何类型的任务的进度，带UI，不常用
```
在不支持HTML5新标签的浏览器里，会将这些新的标签解析成行内元素(inline)对待，所以我们只需要将其转换成块元素(block)即可使用。
但是在IE9版本以下，并不能正常解析这些新标签，但是可以通过
 document.createElement('footer')创建的自定义标签（创建出来的元素是行内元素，因此一般情况下要给：display:block）。
在实际开发中，一般使用第三方兼容文件html5shiv来解决上述问题：
```
<script src="html5shiv.js"></script>
<!--[if lte IE 9]>
<script type="text/javascript" src="htmlshiv.js"></script>
<![endif]--
```
## 二 表单
#### 2.1 表单自动联想
```js
    <input type="text" list="data">
    <datalist id="data">
        <option>男</option>
        <option>女</option>
    </datalist>
```
#### 2.2 表单type
```js
email 		输入email格式
tel 		手机号码，移动设备上得到焦点后会弹出键盘
url 		只能输入url格式
number 	    只能输入数字，此时有属性 min  max  step等
search 		搜索框，输入内容时候会出现清除按钮
range 		范围 滑动条
color 		拾色器
time		时间，可控制时间，且有增减按钮
date 		日期，可控制日期，且有日期控件！
month 	    月份，同上
week 		星期，同上
datetime    时间日期
```
部分类型是针对移动设备生效的，且具有一定的兼容性，在实际应用当中可选择性的使用，比如：
```js
<form>
    <label>
        邮箱：<input type="email" name="email" class="email">
    </label>
    <input type="submit" value="提交">
</form>
```
上述表单类型设置为email后，可以验证邮箱书写的合法性。
#### 2.3 表单属性
```
placeholder 	占位符
autofocus 		获取焦点
multiple 		文件上传多选或多个邮箱地址  
autocomplete    自动完成，用于表单元素，也可用于表单自身(on/off)
form 			指定表单项属于哪个form，处理复杂表单时会需要
novalidate 		关闭验证，可用于<form>标签
required 		必填项
pattern 		正则表达式 验证表单

autocapitalize	iOS独有属性，设置为off关闭首字母大写
autocorrect     iOS独有属性，设置为off关闭输入自动修正
```
#### 2.4 表单事件
```
oninput         用户输入内容时触发，可用于移动端输入字数统计
oninvalid       验证不通过时触发
```
## 三 多媒体
在HTML5之前，在网页上播放音频/视频的通用方法是利用Flash来播放，但是大多情况下，并非所有用户的浏览器都安装了Flash插件，由此使得处理音频/视频播放变的非常复杂，并且移动设备的浏览器并不支持Flash插件。
#### 3.1 音频
```js
<audio src="./test.mp3"></audio>
//由于版权问题，不同浏览器可以播放的音频格式不同，适配方案如下：
<audio controls>
    <source src="./test.mp3">
    <source src="./test.wav">
    <source src="./test.ogg">
    您的浏览器不支持播放该格式多媒体
</audio>
```
音频支持的属性：
```
muted			静音
controls		显示控制条
autoplay 		自动播放
controls 		是否显不默认播放控件
loop 			循环播放
preload 		预加载 同时设置autoplay时些属性失效
auto：          加载；
none：          不加载；
metadata：      加载元数据（封面、歌词、作者）

```
#### 3.2 视频
```js
<video src="./test.mp4"></video>
//由于版权问题，不同浏览器可以播放的视频格式不同，适配方案如下：
<video controls>
    <source src="./test.mp4">
    <source src="./test.ogg">
    <source src="./test.ogg">
    您的浏览器不支持播放该格式多媒体
</video>
```
视频支持的属性：
```
autoplay        自动播放
controls        是否显示默认播放控件
loop            循环播放
preload         预加载，同时设置了autoplay，此属性将失效
width           设置播放窗口宽度
height          设置播放窗口的高度

```
#### 3.3 多媒体控制
```
方法：
    load()			加载
    play()			播放
    pause()			暂停
属性：
    currentTime 	视频播放的进度
    paused			视频播放的状态
    duration		视频总时长
事件：
    oncanplay		是否能播放
    ontimeupdate	播放时触发，报告当前的播放进度
    onended		    播放完时触发

```
#### 3.4 全屏
全屏:           video.webkitRequestFullScreen();
webkit: 	    webkit RequestFullscreen()
moz: 	        moz RequestFullScreen()
ms: 		    ms RequestFullscreen()
其他:	        RequestFullscreen()
出现浏览器前缀的原因：为了兼容低版本的自己的浏览器，比如说webkit为了兼容低版本 的chrome。
## 四 新增DOM操作
#### 4.1 选择器
```
//获取复合匹配条件的第1个元素，参数可以是标签、类、id
document.querySelector("div"); 
//获取复合匹配条件的所有元素，以伪数组形式     
document.querySelectorAll("div");  
```
#### 4.2 类名操作
```
Node.classList.add('class') 		添加class
Node.classList.remove('class') 	    移除class
Node.classList.toggle('class') 		切换class，有则移除，无则添加
Node.classList.contains('class') 	检测是否存在class
```
#### 4.3 自定义属性data
```js
    <ul id="items">
        <li data-flag="1" class="first"></li>
        <li data-rest="Monday" class="second"></li>
        <li data-week-li="test" class="third"></li>
    </ul>
    <script>
        //注意 json属性必须带""
        let json = {
            "name": "zs",
            "age": 30
        }

        let jsonStr = JSON.stri
        
    </script>
```
#### 4.4 JSON对象新增方法
json与字符串的转换我们之前一直使用的是eval方法，在H5中增加了以下两个方法：
```js
        //注意 json属性必须带""
        let json = {
            "name": "zs",
            "age": 30
        }

        let jsonStr = JSON.stringify(json);
        let jsonObj = JSON.parse(jsonStr);

        console.log(jsonStr);   //{"name":"zs","age":30}
        console.log(jsonObj);   //{name: "zs", age: 30}
```
#### 4.5 延迟加载 defer与async
defer：延迟加载，会按顺序执行，最好只在加载外部JS时使用，其他场合会有兼容问题。
async：异步加载，加载完就触发，有顺序问题。
```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script defer="defer"></script>
</head>
```
在head内的标签由于使用了defer，那么就不会先加载，而是onload之后再加载。
#### 4.6 拖拽
为元素增加属性 draggable="true" 可以设置此元素是否可以进行拖拽。其中图片、链接默认是开启的，但是这时候的拖动没有带走数据，可以设置ondragstart事件就可以携带数据。
```
拖拽元素事件（页面中设置了draggable="true"属性的元素）
ondragstart	    应用于拖拽元素，当拖拽开始时调用，只执行一次
ondrag 		    应用于拖拽元素，整个拖拽过程都会调用，一直执行
ondragleave	    应用于拖拽元素，当鼠标离开拖拽元素时触发一次
ondragend		应用于拖拽元素，当拖拽结束时调用

目标元素事件（页面中任何一个元素都可以成为目标元素）		
ondragenter	    应用于目标元素，当拖拽元素进入时触发一次
ondragover		应用于目标元素，当停留在目标元素上时调用
ondrop		    应用于目标元素，当在目标元素上松开鼠标时调用
ondragleave	    应用于目标元素，当鼠标离开目标元素时调用

火狐下拖拽对象（dataTransfer）兼容：
ev.dataTransfer.setData(key,value)
ev.dataTransfer.getData(key) 
```
## 五 Web存储
web存储即把数据存储在浏览器中。传统方式我们以document.cookie来进行存储的，但是由于其存储大小只有4k左右，并且解析也相当的复杂，HTML5规范则提出解决方案：Storage 存储（WebSQL、IndexDB已经被w3c 放弃了）。分别有两种存储方式：
```
会话存储：
    设置：window.sessionStorage.setItem("name","lisi");
    获取：window.sessionStorage.getItem("name");
    删除：window.sessionStorage.removeItem("name");
    清除：window.sessionStorage.clear();
    说明：生命周期为关闭浏览器窗口,在同一个窗口下数据可以共享，可存储大约5M
    
本地存储：
    获取：window.localStorage
    获取：window.localStorage.getItem("name");
    删除：window.localStorage.removeItem("name");
    清除：window.localStorage.clear();
    说明：永久生效，除非手动删除,可以多窗口共享,可存储大约20M
```

## 六 历史管理
window.history对象可以管理历史记录，可用于单页面应用（Single Page Application），可以无刷新改变网页内容。
## 七 其他API
#### 7.1 检测用户网络状态
我们可以通过window.onLine来检测，用户当前的网络状况，返回一个布尔值
```js
window.online       //用户网络连接时被调用
window.offline      //用户网络断开时被调用
window.addEventListener("online",function(){
    alert("已经建立了网络连接")
});
window.addEventListener("offline",function(){
    alert("已经失去了网络连接")
});
```
#### 7.2 离线缓存












