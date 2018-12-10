## 一 DOM
#### 1.1 DOM解析过程与入口函数
HTML加载完毕，渲染引擎会在内存中把HTML文档，生成一个DOM树，getElementById是获取内中DOM上的元素节点。然后操作的时候修改的是该元素的属性。
DOM（document）即文档对象模型的一部分，DOM是一个复合的数据类型。

入口函数如下：
```javascript
window.onload = function(){ 

}
```
该函数解释：页面的结构、样式、节点等加载完毕后才去执行函数体。

在HTML当中一切都是节点，整个文档是一个文档节点，每一个HMTL标签都是一个元素节点，标签中的文字则是文字节点，标签的属性是属性节点。
#### 1.2 获取节点
```javascript
document.getElementById("demo");            //通过 id 找到 HTML 元素
document.getElementsByTagName("div")[0];    //通过标签名找到 HTML 元素	获得的是标签伪数组
document.getElementsByClassName("a");       //通过类名找到 HTML 元素，在部分IE中无效
节点.parentNode             //获取父节点，一个节点只有一个父节点
节点.nextSibling            //获取下一个节点（IE678中指下一个元素节点，标准浏览器包括空文档和换行节点）	
节点.nextElementSibling     //获取下一个节点（不支持IE678）	
```

## 二 事件

## 三 BOM