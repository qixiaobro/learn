# Promise及实现Promise

```promise```对象用于表示一个异步操作的最终完成（或失败），及其结果值。

## 状态

* pending 初始状态，既不是成功，也不是失败状态
* fulfilled 成功
* rejected 失败

### 状态图

![](D:\PEworkspace\learn\src\assets\Snipaste_2020-03-16_15-15-44.jpg)



## 语法

```javascript
new Promise(function(resolve,reject){})
```

```promise```里面的executor是一个接收```resolve```和```reject```两个参数的函数。executor通常是一些异步函数。执行此异步函数时，```promise```的状态为```pending```,在此异步函数成功后会调用```resolve```将```promise```的状态改为```fulfilled```,失败后会调用```reject```将```promise```的状态改为```rejected```.状态定好后则不能再改变。在状态定好后则会调用```promise```对象的```then```方法绑定的处理方法（```then```方法包含两个参数：```onfulfilled``` 和 ```onrejected```，它们都是 Function 类型。当```promise```状态为```fulfilled```时，调用 ```then``` 的 ```onfulfilled``` 方法，当```Promise```状态为```rejected```时，调用``` then``` 的``` onrejected``` 方法， 所以在异步操作的完成和绑定处理方法之间不存在竞争）。



**如果一个```promise```处于```fulfilled```或```rejected```态，那么也可以称为```settled```状态**

## 属性

```promise.length``` 值总为1（构造器参赛的数目）

```promise.prototype``` ```Promise```构造器的原型

## 方法

### ```Promise.all(iterable)``` 

返回一个`promise`实例,此实例在 `iterable` 参数内所有的 `promise` 都“完成（resolved）”或参数中不包含 `promise` 时回调完成（resolve）；如果参数中 `promise` 有一个失败（rejected），此实例回调失败（reject），失败原因的是第一个失败 `promise` 的结果。

#### 		返回值

1. 如果传入的参数是一个空的可迭代对象，则返回一个**已完成（already resolved）**状态的 [`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)。
2. 如果传入的参数不包含任何 `promise`，则返回一个**异步完成（asynchronously resolved）** [`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)。注意：Google Chrome 58 在这种情况下返回一个**已完成（already resolved）**状态的 `Promise`
3. 其它情况下返回一个**处理中（pending）**的[`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)。这个返回的 `promise` 之后会在所有的 `promise` 都完成或有一个 `promise` 失败时**异步**地变为完成或失败。

```javascript
const a = 42;
const b = Promise.resolve(1);
const c = new Promise((resolve,reject)=>{
    setTimeout(resolve(100),2000)
});

Promise.all([a,b,c]).then((values)=>{
    console.log(values)
})//[42,1,100]

console.log(Promise.all([])) 
/*
Promise {<resolved>: Array(0)}
__proto__: Promise
[[PromiseStatus]]: "resolved"
[[PromiseValue]]: Array(0)
length: 0
__proto__: Array(0)
*/
console.log(Promise.all([1,2,3]))
/* 对于第二条我不太理解，这是异步完成???
Promise {<pending>}
__proto__: Promise
[[PromiseStatus]]: "resolved"
[[PromiseValue]]: Array(3)
0: 1
1: 2
2: 3
length: 3
__proto__: Array(0)
*/
console.log(Promise.all([a,b,c]))
/*
Promise {<pending>}
__proto__: Promise
[[PromiseStatus]]: "resolved"
[[PromiseValue]]: Array(3)
0: 42
1: 1
2: 100
length: 3
__proto__: Array(0)
*/
```

**`Promise.all` **当且仅当**传入的可迭代对象为空时为同步**

### ```Promise.race(iterable)```

方法返回一个 `promise`，一旦迭代器中的某个`promise`解决或拒绝，返回的 `promise`就会解决或拒绝。

#### 返回值

一个**待定的** [`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 只要给定的迭代中的一个`promise`解决或拒绝，就采用第一个`promise`的值作为它的值，从而**异步**地解析或拒绝（一旦堆栈为空）

```js
var p1 = new Promise(function(resolve, reject) { 
    setTimeout(resolve, 500, "one"); 
});
var p2 = new Promise(function(resolve, reject) { 
    setTimeout(resolve, 100, "two"); 
});

Promise.race([p1, p2]).then(function(value) {
  console.log(value); // "two"
  // 两个都完成，但 p2 更快
});

var p3 = new Promise(function(resolve, reject) { 
    setTimeout(resolve, 100, "three");
});
var p4 = new Promise(function(resolve, reject) { 
    setTimeout(reject, 500, "four"); 
});

Promise.race([p3, p4]).then(function(value) {
  console.log(value); // "three"
  // p3 更快，所以它完成了              
}, function(reason) {
  // 未被调用
});

var p5 = new Promise(function(resolve, reject) { 
    setTimeout(resolve, 500, "five"); 
});
var p6 = new Promise(function(resolve, reject) { 
    setTimeout(reject, 100, "six");
});

Promise.race([p5, p6]).then(function(value) {
  // 未被调用             
}, function(reason) {
  console.log(reason); // "six"
  // p6 更快，所以它失败了
});
```

### ```Promise.reject(reason)```

方法返回一个带有拒绝原因的`Promise`对象。

### ```Promise.resolve(value)```

方法返回一个以给定值解析后的[`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象。如果这个值是一个 `promise` ，那么将返回这个 `promise` ；如果这个值是`thenable`（即带有[`"then" `](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)方法），返回的`promise`会“跟随”这个`thenable`的对象，采用它的最终状态；否则返回的`promise`将以此值完成。此函数将类`promise`对象的多层嵌套展平。

### `Promise.any(interable)`

### `Promise.allSettled(interanle)`

## Promise原型

### 属性

### ```Promise.prototype.constructor```返回被创建的实例函数，默认为```Promise```函数

### 方法

### `Promise.prototype.catch(onRejected)`

### `Promise.ptototype.then(onFulfilled,onRejected)`

### `Promise.protype.finally(onFinally)`

