## 一 数组
#### 1.1 数组的简介
数组是最简单的数据结构，用来存储一系列相同的数据类型的值，在JS中，数组可以保存不同类型的值，但我们应当尽量保持最佳实践。
数组在内存中的存储方式：数组中的元素在申请到的内存中是紧密存储在一起的。
![](/images/数据结构与算法/js-01.png)
数组的创建：
- 方式一： var arr1 = new Array();
- 方式二： var arr2 = [];
数组元素的访问与迭代：
```JavaScript
/**
 * 求斐波那契数列的前20个数字
 * 斐波那契数列中第一个数字是1，第二个是2，其后依次是前两个之和
 */
var fibArr = [];
fibArr[0] = 1;
fibArr[1] = 2;
var num = 20;
for(var i = 2; i < 20; i++){
    fibArr[i] = fibArr[i-1] + fibArr[i-2];
}
console.log(fibArr)
```
#### 1.2 添加元素
```JavaScript
var arr = [1,2,3,4,5];
//给数组添加一个元素6，只需要赋值最后一个位置上的元素即可
arr[arr.length] = 6;
```
注意：在JS中，数组是一个可以修改的对象，添加元素可以让数组动态增长。但是在C语言和Java中，首先要决定数组的大小，添加元素要先创建一个全新的数组。
当然JS中还有便捷的添加元素的方法：
arr.push()      //向数组末尾添加元素
arr.unshift()   //向数组首位添加元素，传入多个值表示依次从首位开始添加数据

数组从首位开始添加元素的过程：
首先要腾出数组里第一个元素的位置，把所有元素向右移动一位，这时可以循环数组，从最后一位+1的长度开始，将其对应的前一个元素的值赋值给它
#### 1.3 删除元素
arr.pop()       //删除最后一个元素
arr.shift()     //删除首位元素

同理，数组删除首位元素也是将所有的元素都左移了一位，但是数组的长度是维持不变的，这意味着删除首位元素后，最后一个元素的值是undefined，所以循环时需要在arr.length-1处停止。
#### 1.4 任意位置处添加、删除元素
arr.splice(5,3)  //通过索引和数量来删除指定的数组元素
注意：delete方法也可以执行删除，但是删除的只是值，该位置上仍然存在元素，值为undefined
arr.splice(5,3,7,8) //从索引5开始删除3哥元素，再添加元素7和元素8
## 二 栈
#### 2.1 栈简介
数据结构：存在着一种或者多种特定关系的数据元素的组合。
我们常见的栈与队列，其实都可以用数组、链表等基础数据结构分别实现。
栈是一种后进先出（LIFO）的有序集合。新添加的或者待删除的元素都保存在栈顶，在栈里，新元素靠近栈顶，旧元素都接近栈低。
栈经常被编程语言用来存储变量、方法的调用。
栈类似于图书的堆放：
![](/images/数据结构与算法/js-02.jpeg)
后来者（新元素）总是放在最上面。
要拿走也是拿走最上面的书籍。
在JS中模拟一个栈的对象如下：
```JavaScript
function Stack() {
    //声明栈的增删改查
}
//我们还需要一个数据结构来保存栈里的元素，这里使用数组：
let items = [];
```
以上只是建立了栈的一个“壳”，我们需要实现栈对应的增删改查，且需要对应栈先进后出的特征。
#### 2.2 添加元素
```JavaScript
this.push = function(element){
    items.push(element);    //直接使用数组的push方法保存
}
```
#### 2.3 移除元素
```JavaScript
this.pop = function(){
    items.pop();
    return;
}
```
如上所示，使用数组的push和pop后，自然就遵循了LIFO原则。
#### 2.4 一些辅助方法
```JavaScript
//查看栈顶元素
this.peek = function() {
    return items[items.length - 1]
}
//检查栈长度
this.size = function() {
    return items.length;
}
//清空栈
this.clear = function(){
    items = [];
}
```
#### 2.5 栈的使用与理解
```JavaScript
let stack = new Stack();
stack.push(1)
stack.push(2)
stack.push(3)
stack.pop()
```
执行过程：
![](/images/数据结构与算法/js-03.png)
#### 2.6 ES6方式模拟栈
ES6提供了class类仿造Java中的类，但是却不具备私有属性的功能，用class声明一个Stack类，内部的items数组是可以被外界访问到的，我们需要制造一种私有化items的方案。
利用Symbol可以实现：
```JavaScript
let _items = Symbol();
class Statck {
    constructor(){
        this[_items] = [];
    }
    //各种方法
}
```
但是ES6同样也新增了Object.getOwnPropertySymbols方法获取类里面声明的所有Symbol属性。
最终方式：使用WeakMap，同时使用闭包方式将class外部声明的WeakMap实例包裹，防止别人随意改动该实例。
```JavaScript
let Stack = (function () {
    const items = new WeakMap();
    class Stack {
        constructor(){
            items.set(this, [])
        }
        //其他方法
    }
    return Stack;
})();
```
#### 2.7 栈的应用
在回溯问题中，栈可以用来存储访问过的任务、路径、撤销操作，在JAVA中，栈用来存储变量和方法调用，处理递归方法时，会抛出栈溢出异常。
转换十进制到二进制案例:
```JavaScript
function divi(num) {
    var remStack = new Stack(),
        rem,
        binaryString = '';
    while (num > 0) {
        rem = Math.floor(num % 2);
        remStack.push(rem);
        num = Math.floor(num % 2);
    }
    while (!remStack.length == 0) {
        binaryString += remStack.pop().toString();
    }
    return binaryString;
}
```
## 三 队列
#### 3.1 队列简介
队列式遵循FIFO（先进先出）的一组有序的项。队列在尾部添加元素，并从顶部移除元素，最新添加的元素必须排在队列的末尾。在现实中最常见的队列就是排队。
JS实现一个队列和实现栈一致，只不过内部的数组需要做一定的先进先出处理：
```javascript
let Queue = (function(){
    const items = new WeakMap();
    class Queue {
        constructor () {
            items.set(this, []);
        }
        enqueue (e) {
            items.get(this).push(e);
        }
        dequeue () {
            return items.get(this).shift();
        }
        //...
    }
    return Queue;
})();
```
#### 3.2 优先级队列

