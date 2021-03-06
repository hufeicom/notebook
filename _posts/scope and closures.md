/**
title: 作用域与闭包
date: 2018-04-30
tags: JavaScript,作用域,闭包
*/

作用域与闭包
*什么是作用域？*
在当前运行环境下，可以访问的变量或函数的范围。
作用域分为**词法作用域**和**动态作用域**。
词法作用域是在js代码编译阶段就确定下来的； 对应的，`with`和`eval`语句会产生动态作用域。
> *词法作用域是在词法分析时被定义的作用域* ————[《你不懂JS：作用域与闭包》](https://github.com/getify/You-Dont-Know-JS/blob/1ed-zh-CN/scope%20%26%20closures/ch2.md)

会产生新的作用域的情况：
- 函数
- `{}`（ES6）
- `eval`

举个例子说明作用域
```javascript
var a = 'hello';
function f1(){
    var a = 1;
    console.log(a);
}
f1();  // 1
console.log(a); // hello
```
可以看到f1中的变量a只能在f1中有效，f1外部访问不到里面的a；所以在f1中的a，其作用域就只限定在f1中。

再来个新概念：**作用域链**
```javascript
var a = 'hello';
function f1(){
    console.log(a);// ps: f1中并未声明a
}
f1(); // hello
```
之所以输出hello, 是因为在f1中并未找到a的定义，此时程序并不会急于抛异常，而是会向调用f1的上一层寻找a的定义。如果没有，会继续再往上一层的上一层寻找，直到最顶层。
这样就形成了一个链式的作用域。

*什么是闭包？*

通常来讲，函数可以访问函数外面的变量；但是在函数外部，访问不到在函数里面定义的变量。
```javascript
function f1(){
    var a = 1;
}
console.log(a);  // Uncaught ReferenceError: a is not defined
```
那么有没有可能访问到f1中的a呢？当然是有的， 看例子：
```javascript
function f1(){
    var a = 1;
    function f2(){
        return a;
    }
    return f2;
}
var getA = f1();
console.log(getA()); // 1
```
我们在f1中，添加了一个函数f2(实际上f2就可以看做一个闭包)。
一般情况下，当函数执行完毕时，里面的变量会被自动销毁。但是因为我们把f2赋值给了外部的getA，所以f2不会被内存释放，同理f2中使用的a在f2的作用域中，也不会被释放，所以这个时候就可以访问到a。
而getA能够访问到a,这个在js的编译阶段就已经定型了（词法作用域）。

官方”的解释是：闭包是一个拥有许多变量和绑定了这些变量的环境的表达式（通常是一个函数），因而这些变量也是该表达式的一部分。
相信很少有人能直接看懂这句话，因为他描述的太学术。其实这句话通俗的来说就是：闭包就是能够读取其他函数内部变量的函数。


*闭包的特点*
闭包可以在函数外部改变函数中的变量的值，如果你把函数作为对象、闭包作为方法、局部变量作为私有属性使用，则会改变该变量的值；闭包还会把函数中的变量的值存储于内存中，对内存消耗很大，所以滥用闭包的结果就是影响网页性能，IE中则可能导致内存泄露

### 参考文章
[作用域](https://github.com/getify/You-Dont-Know-JS/blob/1ed-zh-CN/scope%20%26%20closures/ch1.md)