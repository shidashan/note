## 一 jQuery初步使用
#### 1.1 jQuery简介
原生JS痛点：
- window.onload事件只能出现一次，多次出现会覆盖之前的事件
- 兼容性复杂
- 简单功能原生实现复杂（比如各种循环，jQuery隐式迭代帮我们做了）
jQuery的API都是方法，即要加小括号()，小传入的参数不同，功能不同。
```
版本一：1.x版本，兼容IE6/7/8
版本二：2.x版本，不兼容IE6/7/8
版本三：3.x版本，更精简，不再兼容低版IE
```
#### 1.2 jQuery使用步骤
```javascript
<script src="./jQuery-1.11.3.min.js"></script> <!-- 引包 -->
<script>
    $(document).ready(function () { //入口函数
        //代码
    });
    //也可以简写为：
    $(function(){
        $('#div').click(function () {
            console.log(1)
        });
    });
</script>
```
注意：
- \$实际上表示的是一个函数，即jQuery函数：  jQuery ===$;
- jQuery事件不带on

#### 1.3 jQuery入口函数与JS入口函数
JS的入口函数是：window.onload = function() { };
jQuery的入口函数是：$(function(){ });
区别：
- JS入口函数只能出现一次，出现多次会存在事件覆盖的问题，jQuery入口函数可以书写多次，没有覆盖问题。
- S入口函数是在所有的 文件资源 加载完成后才执行，jQuery入口函数在 文档 加载完后执行，即无需外部资源加载，DOM树加载完成就执行
#### 1.4 jQuery对象和DOM对象
DOM对象：使用JS操作DOM返回的对象；
jQuery对象：使用jQuery操作DOM获得的对象，内部是一个对DOM对象进行包装后的伪数组
jQuery对DOM对象封装后，就不需要大量重复的遍历，且能更好的实现兼容问题。
DOM对象与jQuery对象转换：
```
DOM对象转换为jQuery对象方式：
$(DOM对象);
jQuery对象转换为DOM对象：
方式一：var btn = jQuery对象[0];		//推荐使用该方式
方式二：var btn = jQuery对象.get(0);

```
## 二 jQuery选择器
#### 2.1 基本选择器
```
id选择器        $('#btn');
类选择器        $('.btn');
标签选择器      $('div');
选择器的交集    $(.div,.green')		选择class为div，或class为green的元素
选择器的并集    $('.div.green')		选择class为div，且class为green的元素
```
#### 2.2 层级选择器
```
后代选择器（空格）：	$('#ul li')		选择id为ul的元素的所有后代li 
子代选择器（>）：		$('#ul > li')	选择id为ul的元素的直系后代li
```
#### 2.3 过滤选择器
```
:eq(index)	选择匹配索引的元素		$('li:eq(2)')	选择索引号为2的li
:odd		选择匹配奇数索引元素		$('li:odd')
:even		选择匹配偶数索引元素		$('li:even')
```
#### 2.4 筛选选择器
```
find(selector)
查找所有后代元素	
$(“#j_wrap”).find(“li”).css(“color”, “red”);

children()
查找直接子代元素	
$(“#j_wrap”).children(“ul”).css(“color”, “red”);

siblings()	
查找所有兄弟元素（不包括自己）	
$(“#j_liItem”).siblings().css(“color”, “red”);

parent()	
查找父元素	
$(“#j_liItem”).parent(“ul”).css(“color”, “red”);    //选择id为j_liItem的父元素

eq(index)	
查找指定元素的第index个元素	
$(“li”).eq(2).css(“color”, “red”);                  //选择所有li元素中的第二个
```
## 三 jQuery的DOM操作
#### 3.1 jQuery操作样式
```javascript
// 注意点：操作类样式的时候，所有的类名都不带点

//获取样式
$(selector).css(“font-size”);	
//设置样式:可以设置单个、多个										
$(selector).css({“color”: “red”, “font-size”: “30px”});	

//添加样式
$(selector).addClass(“liItem”);

//移除样式：无参表示移除被选中元素的所有类名
$(selector).removeClass(“liItem”);

//判断有没有类样式：返回true或false
$(selector).hasClass(“liItem”);

//切换类样式：该元素有类则移除，没有指定类则添加
$(selector).toggleClass(“liItem”);

```
#### 3.2 节点操作
```javascript

```
