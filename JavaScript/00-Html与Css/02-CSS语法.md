## 一 CSS简介
CSS即层叠样式表（Cascading  Style  Sheets），也称为级联样式表。
CSS书写位置：
- 内嵌式：在head标签中直接书写
```Html
<style type="text/css"></style>
```
- 外连式：
```Html<link rel="stylesheet" href="1.css">
```
- 行内式：通过给标签直接设置style属性来设置样式。
## 二 CSS选择器
#### 2.1 选择器分类
CSS选择器用来选择Html中的标签元素，常见的选择器有：
- 基础选择器：id选择器，类选择器，标签选择器，通配符选择器
- 复合选择器：标签指定选择器，后代选择器，并集选择器
#### 2.2 基础选择器
```Html
<style type="text/css">
    * {}                         /*通配符选择器，控制所有*/
    p { color: red; }           /*标签选择器*/
    .test { color: green;}      /*类选择器*/
    #oDiv { color: blue;}       /*id选择器*/
</style>
<div class="test"></div>
<div id="oDiv"></div>
```
id选择器：多个标签不要同时使用同一id选择器，一个标签只能调用一个id。
类选择器：多个标签可以同时调用一个类样式， 一个标签可以调用多个类样式。
类选择器命名规范：
- 不能以纯数字或者以数字开头定义类名
- 不推荐使用汉字定义类名
- 不能以特殊符号或者以特殊符号开头（“_”除外）定义类名
- 不建议使用标签名或者属性名定义类名
#### 2.3 复合选择器-标签指定选择器
特点关系：既.....又.....   如下案例使用id p#id也可以实现：
```Html
<style type="text/css">
   p.one{ color: red;}
</style>
........
<p class="one">one</p>
<p class="two">two</p>
```
#### 2.4 复合选择器-后代选择器
特点关系：标签之间必须属于嵌套关系，选择器之间用空格隔开，如下案例，选择p标签下的类名为p1的标签。
```Html
<style type="text/css">
   p #p1{ color: red;}
</style>
```
#### 2.5 复合选择器-并集选择器
```Html
<style type="text/css">
   div,p,span{ color: red;}
</style>
```
#### 2.5 属性选择器
```Html
<style>
    input[type=text][class="password"] {
        background-color: red;
    }
</style>

<input type="text" id="username">
<input type="password">
```
## 三 CSS与文字
#### 3.1 常见文字设置
```
设置居中    text-align: center  
            设置盒子内文本居中，不能让标签居中，当然我们可以把行内元素、行内块元素看成文本
设置大小    font-size: 
设置字体    font-family:"宋体","微软雅黑";
            可以设置单个值，也可以设置多个，即浏览器不支持第一个字体，则会尝试下一个，如果都不支持，那么使用系统默认的字体。
设置加粗    font-weight
            直接设置数字   100-900，也可以设置英文：
            bold  (字体加粗)   效果在700-900
            normal(文字字体正常显示)
            推荐使用 font-weight:700;
设置倾斜    font-style
            italic     文字斜体显示；
            normal   文字正常显示

```
#### 3.2 属性连写
```Html
p {  font: italic 700 30px 宋体; }
```
注意： 联写必须有 font-size和font-family(其他属性可以不写)，且顺序不能更换。
#### 3.3 行高 line-height
浏览器默认文字大小：16px，
浏览器默认行高大小：18px。
行高的定义：两行文本基线的距离，就是行高（这里才是正确量取行高的方法）
行高 = 文字大小 + 上间距 + 下间距   
三者加起来如果等于盒子高度，正好文字居中！
![](/images/JavaScript/01-02-01.png)
当行高值为父容器的高度时，可以让父容器中的文字垂直显示。
如果单独给一个元素设置行高：

| 行高单位 | 赋值 | 文字大小 | 行高值 |
| :------| ------: | :------: |:------: |
| px | 20px | 20px |20px|
| em | 2em | 20px |40px|
| % | 120%	| 20px | 24px |
| 不带单位 | 2 | 20px | 40px |
总结：当给一个独立的元素设置行高值的时候，除了以px为单位的行高值与文字大小无关，其他都与文字大小有关（与文字大小的积）。
盒子嵌套，给父元素设置行高值，子元素的行高问题：
|行高单位|设置行高|父文字|子文字|行高|
| :------| ------: | :------: |:------: |:------: |
||px|	20px|	20px|	30px|	20px
em|	2em|	20px|	30px|	40px
|%|	120%|	20px|	30px|	24px
|不带单位|	2	|20px	|30px|	60px
总结：行高可以继承。当父元素设置了行高值（不带单位除外），子元素的行高值都是父元素行高值乘以父元素文字大小。

总结图表：
| 给父元素设置行高 | 子元素行高结果 | 
| :------| ------: | 
| px | 行高=父元素行高|
| em | 行高=父元素文字大小*行高|
| % | 行高=父元素文字大小*行高 |
| 不带单位 | 行高=子元素文字大小*行高|
## 四 标签分类
#### 4.1 块级元素
代表：div  p  li   h1
特点：
- 元素独占一行显示，与宽度无关，即不给宽度直接占满一行
- 支持所有CSS命令（可以设置宽度和高度）
- 当嵌套一个块级元素，子元素如果不设置宽度，子元素的宽度为父元素的宽度。
#### 4.2 行内元素
 代表:  span，a，font，strong
 特点：
 - 元素可以在同一行上显示
 - 宽高由内容撑开
- 不支持上下margin
- 代码换行会被解析
#### 4.3 行内块元素
代表： Image,  input(表单控件)
特点： 元素在一行上显示，可以设置宽高，没有宽度时由内容撑开。
案例：给下列的div设置text-align:center一样能居中，所以行内块元素可以当做文字来处理。
```html
<div style="text-align:center">
    <span>111</span
></div>
```
#### 4.4 元素转换
display: inline 将元素转化为行内元素
display：inline-block   将元素转化行内块元素
display: block  将元素转化为块元素
## 五 CSS特性
- 层叠性：某个元素同时出现了多个同级别的同名样式，那么书写在后面的样式将会覆盖之前的样式。
- 继承性：子元素会继承父元素的：颜色、大小、字体、行高。注意：a标签不能继承父元素文字颜色（层叠掉了），h标签不能继承父元素文字大小。
- 优先级：
默认样式 0 < 标签选择器 1 < 类选择器 10 < id选择器 100 < 行内样式 1000 < !important 1000以上
注意：继承的权重为0；权重可以叠加
## 六 伪类
a:link{属性:值;}    超链接默认状态，与a{}一样
a:visited{属性:值;} 超链接访问过后的样式
a:hover{属性:值;}	鼠标放到超链接上的样式
a:active{}      	超链接激活状态下的样式
:focus{}            获取焦点的时候的样式
## 七 CSS与背景
#### 7.1 背景色 背景图
注意：插入背景图一定要设置高度和宽度
```Html
div{
    background-color: red;
    background-image: url("1.jpg");
    width: 200px;
    height: 200px;
}
```
#### 7.2 背景平铺
repeat 		默认值 
no-repeat 	不平铺
repeat-x  	横向平铺
repeat-y 	纵向平铺
#### 7.3 背景位置
设置具体值： left| right| top| bottom| cneter
background-position: top right;	
设置具体值时不区分顺序，分别为水平、垂直方向
#### 7.4 背景固定于滚动
background-attachment:fixed;
fixed：图片固定   scroll：滚动（默认）
#### 7.5 属性连写
没有数量限制和先后顺序限制：
```html
background: url("1.png") red no-repeat 30px 40px;
```
## 八 盒模型
#### 8.1 盒模型简介
盒模型主要用来网页布局，盒子包括：border(边框)、内边距（padding）、外边距（margin）：
![](/images/JavaScript/01-02-02.png)
#### 8.2 边框border
border-width:边框宽度
border-style:边框样式，solid（实线）、dotted（点线）、dashed（虚线）
border-color：边框颜色
border书写方式：
- border-left: 1px solid green  同理设置其他边框；
- border-top-color:green 		同理设置其他属性；
- border: solid 1px red;    联写
注意：border属性联写：没有先后顺序限制，边框颜色、宽度可以不写。
#### 8.3 内边距 padding
内边距设置内容距离盒子边框之间的距离。
padding-left:左边距
padding-right:右边距
padding-top:上边距
padding-bottom:下边距
属性联写：
padding: 10px;上，右，下，左的距离为10px
padding: 10px 20px; 上下10px，左右20px
padding: 10px 20px 30px;上10px  左右20px   下30px
padding: 10px 20px 30px 40px;上， 右 ， 下， 左
#### 8.4 盒子大小计算
盒子宽度=内容宽度+左右边框+左右内边距；
注意：进行页面布局时，如果给盒子设置了内边距，对应的要将内容宽度或者高度减去相应的值。
子盒子在父盒子宽度范围内，父盒子的padding不会影响子盒子大小。
#### 8.5 外边距 margin
外边距设置盒子与盒子之间的距离。属性同padding。
注意：当两个盒子垂直显示的时候，外边距以设置的最大值为准。
行内元素只有左右margin，没有上下margin，同理padding也是。
注意：当两个盒子垂直显示的时候，外边距以设置的最大值为准。行内元素只有左右margin，没有上下margin，同理padding也是。
## 九 浮动
#### 9.1 文档流与浮动
元素默认的显示方式（如块级元素独占一行）就是标准流（文档流）。
浮动的目的是为了让块级元素能够在一行显示。
浮动常用来解决文字环绕图片问题，也可用来制作导航栏、网页布局。
浮动用法：float:left| right    元素默认是没有浮动的，即 float:none
特点：
- 设置了浮动的元素不占原来的位置（脱标）    
- 浮动可以行内元素转化为行内块元素
#### 9.2 清除浮动
浮动后，后续的盒子会浮上来，经常采取的做法是：浮动的元素都被包裹在一个透明的父盒子中，父盒子只要拥有自己的宽高，那么就不会对整体布局造成影响。
当然也可以选择清除浮动，清除浮动不是删除浮动，而是清除浮动对布局的影响。
当子元素设置了浮动，父元素没有高度的时候，会造成页面布局混乱，这种情况下进行清除浮动。即解决 父盒子高度为0 的问题。
如果父盒子没有设置高度，那么高度由子盒子撑开；
如果子盒子这时使用了浮动，那么父盒子就无法撑开，不显示。
清除浮动方式：
方式一：谁出问题给谁加一个clearfix类名，使用clear:left|  right  | both
```html
    <style>
        #div1 {
            width: 500px;
            background-color: red;
        }
        #div2 {
            width: 200px;
            height: 200px;
            background-color: green;
            float:right;
        }
        .clearfix {
            clear: both;
        }
    </style>
</head>
<body>
<div id="div1">
    <div id="div2"></div>
    <div class="clearfix"></div>
</div>
```
方式二：给父盒子设置overflow:hidden 使用此属性用来触发bfc。
如果父盒子中有定位的元素，一般不推荐使用该种方式清除浮动，因为子盒子中的元素如果超出了父盒子的高度，超出部分会被切掉。
方式三：使用伪元素清除浮动
```html
    <style>
        .div1 {
            width: 500px;
            background-color: red;
        }
        .div2 {
            width: 200px;
            height: 200px;
            background-color: green;
            float:right;
        }
        .clearfix:after {
            content: "";
            display: block;
            clear: both;
            height: 0;
            line-height: 0;
            visibility: hidden;
        }
        .clearfix {
            zoom: 1;    /*兼容IE*/
        }
    </style>
</head>
<body>
<div class="div1 clearfix">
    <div class="div2"></div>
</div>
```
方式四：使用双伪元素清除浮动（淘宝、小米采用）
```html
.clearfix:before,.clearfix:after{
    display: table;
    content: "";
}
.clearfix:after {
    clear: both;
}
.clearfix {
    zoom: 1;
}  

```
## 十 定位position
#### 10.1 简介
元素默认的定位是 position:static， 我们称之为静态定位，即元素标准流的显示方式，静态定位约等于标准流，静态定位的作用就是用来取消定位。
postion方位名称：left, right,top,bottom  
#### 10.2 相对定位 relative
相对定位：设置了相对定位后，新的展示位置根据自己原来的位置 +或者- 定位位置。但是该元素在CSS中仍然是占据着原来的位置。
注意：	相对定位不能进行元素的模式转换
子元素设置绝对定位，父元素设置相对定位（子绝父相，也要看情况）
```html
 div {
    width: 200px;
    height: 200px;
    background: aqua;
    margin: 100px;
    position: relative;
    top: 10px;
    left: 10px;
}
```
#### 10.3 绝对定位 absolute
绝对定位position:absolute; 类似浮动不再占据位置
特点：
- 给单独的元素设置绝对定位，以浏览器左上角（body）为基准
- 给行内元素设置绝对定位后，该元素转化为了行内块元素
- 给盒子设置了绝对定位，该盒子不占位置（脱标）
- 当盒子发生嵌套关系的时候：
    - 父盒子没有定位，子盒子定位，以浏览器左上角为基准; 
    - 父盒子设置定位，子盒子设置定位，以父盒子左上角为基准。
#### 10.4 固定定位 fixed
固定定位不占位置（脱标），将行内元素转化为行内块元素，且不会随着浏览器的滚动条滚动而变化。







       	



