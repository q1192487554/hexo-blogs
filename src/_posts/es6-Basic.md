---
title: es6 基本语法
date: 2021-01-19 11:10:00
categories: es6
tags: [es6]
comments: false
---

本篇文章将简单介绍 es6 基础语法

<p id="div-border-left-green">记录一些比较常用的js语法主要是自己平时复制啊粘贴啊使用。</p>


## 导入导出
``` javascript
export const name = "张三";                          //导出
export default const name = "张三";                  //导出

import * as parent from './module'                  //全部引入
import { obj1, obj2 } as parent from './module'     //选择性引入
import obj1 as parent  from './module'              //单个引入
```


## 数组
``` javascript
var attr=[1,2,3,4]                     
var attr=new Array(1,2,3,4)            

<!--实例方法-->
attr.reverse()                          //数组反转
attr.includes(2)                        //查询2在不在数组中
attr.indexOf(2)                         //查询所在数组中的下标

Array.prototype.forEach
Array.prototype.map
Array.prototype.filter
Array.prototype.reduce
Array.prototype.some
Array.prototype.every
Array.prototype.indexOf
Array.prototype.lastIndexOf
```


## 箭头函数
``` javascript
let f = v => v;
let sum = (num1, num2) => num1 + num2;
let item = id => ({ id: id, name: "Temp" });
let func = () => { }
```


## 函数几种调用形式
``` javascript
func.call(this, 10, 20);                   //参数明确时可使用call,
func.apply(this, [10, 20])                 //参数不明确时使用apply传递参数数组
func.bind(this, [10, 20])()                //参数和call一样 他返回一个函数 
```



## Generator 函数
``` javascript
function* helloWorldGenerator() {
    var rs1 = yield 'hello';
    var rs2 = yield 'world';
    return 'ending';
}
var hw = helloWorldGenerator();
hw.next()                                   //* 第一次调用相当于执行helloWorldGenerator()
hw.next('rs1 的参数哦')                      //* 第二次调用，Generator 函数从上次yield表达式停下的地方
hw.next()                                   //* { value: 'ending', done: true }

<!--迭代器方法-->
hw.next()                                    //next()是将yield表达式替换成一个值。
hw.throw()                                   //throw()是将yield表达式替换成一个throw语句。
hw.return()                                  //return()是将yield表达式替换成一个return语句。
```

## Promise 对象
``` javascript
const promise = new Promise(function (resolve, reject) {
    true ? resolve(value) : reject(error)
})

promise
    .then(function (data) {       //监控成功状态
          
    })
    .catch(function (error) {     //监控失败状态
          
    })
    .finally(function (error) {   //不管状态 都会执行这个
          
    })
    
 var [v1,v2,v3] = Promise.all([p1, p2, p3]);     //传入多个Promise对象
 var p = Promise.race([p1, p2, p3]);             //那个率先改变的 Promise 实例的返回值，就传递给p的回调函数。
 var p = Promise.resolve();                      //返回一个 resolve 状态的 Promise		
 var p = Promise.reject('出错了');                //返回一个 reject 状态的 Promise
 
 <!--统一管理错误-->
 Promise.try(() => database.users.get({id: userId}))    
  .then(...)
  .catch(...)
```


## 对象
``` javascript
Object.defineProperty()                 //增加,修改属性  也可以添加get，set操作符
Object.setPrototypeOf()                 //设置原型链对象
Object.getPrototypeOf()                 //获取原型链对象
```

## class
``` javascript
class Point {}
class Foo extends Point {               //继承
    _name;
    _age;
    constructor(x, y) {
        super(x, y);                    //调用父类的constructor(x, y)
    }   
    static classMethod() {              //静态方法
      return 'hello';
    }
    
    get name() {}                       //get方法
    set name(value) {}                  //set方法
}
object instanceof Object                //来检测 constructor.prototype 是否存在于参数 object 的原型链上。 
```


## 对象冒充继承  以及结合 protytype继承
``` javascript
function fn1(name) {
    this.name = name
}
fn1.prototype.work = function () {
    console.log(this.name)
}
function fn2(name) {
    fn1.call(this, name)        //对象冒充继承
}
fn2.prototype = fn1.prototype   //原型链继承
var f2 = new fn2('小红')
f2.work()
f2.constructor                  //查看构造方法
```

## Object.assign()用法
``` javascript
//*  为对象添加属性
class Point {
    constructor(x, y) {
        Object.assign(this, { x, y });
    }
}

//*  为对象添加方法
function SomeClass(){}
Object.assign(SomeClass.prototype, {
    someMethod(arg1, arg2) {
        
    },
    anotherMethod() {
        
    }
});
```


## Set
``` javascript
let set= new Set()
set.add(value)                              //给集合内添加某个元素
set.remove(value)                           //移除集合中某个元素
set.clear(value)                            //清空集合
set.has(value)                              //检测集合内是否有某个元素
set.size()                                  //返回集合长度
set.values()                                //返回键值的遍历器
set.keys()                                  //返回键名的遍历器
set.entries()                               //返回键值对的遍历器
set.constructor                             //构造函数，默认就是Set函数。
```

## Map
``` javascript
var m = new Map()
m.set('Adam', 67)                           //添加新的key-value
m.has('Adam')                               //是否存在key 'Adam': true
m.get('Adam')                               //输出
m.delete('Adam')                            //删除
m.keys()                                    //返回所有key
m.values()                                  //返回所有value

m.forEach((value, key) => {
  console.log(`${key}=${value}`)            //遍历map
})
for (var x of m)                            //其实map就是一个二维数组而已
for (let [key, value] of map) 			   
for (let [, value] of map) 	            
```