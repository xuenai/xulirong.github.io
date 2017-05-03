---
layout: post
title:  "call和apply的区别"
date:   2017-05-03 09:00:00
categories: IT
author : huanghui
---

# 一、方法的定义 
## call方法: 
* 语法：call(thisObj，Object)
	定义：调用一个对象的一个方法，以另一个对象替换当前对象。
* 说明：
	call 方法可以用来代替另一个对象调用一个方法。call 方法可将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。 
	如果没有提供 thisObj 参数，那么 Global 对象被用作 thisObj。 

## apply方法： 
* 语法：apply(thisObj，[argArray])
	定义：应用某一对象的一个方法，用另一个对象替换当前对象。 
* 说明： 
	如果 argArray 不是一个有效的数组或者不是 arguments 对象，那么将导致一个 TypeError。 
	如果没有提供 argArray 和 thisObj 任何一个参数，那么 Global 对象将被用作 thisObj， 并且无法被传递任何参数。

 

## 代码示例：
```javascript
function Animal(name) {
    this.name = name;
    this.showName = function() {
        alert(this.name);
    };
};

function Cat(name) {
    this.superClass = Animal;
    this.superClass(name);
    delete superClass;
}

var cat = new Cat("Black Cat");

cat.showName();
 ```

 

## 模拟call, apply的this替换
```javascript
function Animal(name) {
    this.name = name;
    this.showName = function() {
        alert(this.name);
    };
};

function Cat(name) {
    this.superClass = Animal;
    this.superClass(name);
    delete superClass;
}

var cat = new Cat("Black Cat");

cat.showName();
 ```