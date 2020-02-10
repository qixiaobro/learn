<!--
 * @Author: Do not edit
 * @Date: 2020-02-10 14:51:00
 * @LastEditors  : zxd
 * @LastEditTime : 2020-02-10 17:32:29
 * @FilePath: \hello-node\learn.md
 -->
## node

### 创建服务  
```js
var http = require('http');

http.createServer(function(request,response){


    response.writeHead(200,{'Content-type':'text/plain'});

    response.end('node test\n');
}).listen(8888);
```

异步操作的函数将回调函数作为最后一个参数， 回调函数接收错误对象作为第一个参数。
### REPL  
REPL 表示一个环境  
Node 自带了交互式解释器，可以执行以下任务：

读取 - 读取用户输入，解析输入了Javascript 数据结构并存储在内存中。

执行 - 执行输入的数据结构

打印 - 输出结果

循环 - 循环操作以上步骤直到用户两次按下 ctrl-c 按钮退出

### node.js事件循环  
Node.js 是单进程单线程应用程序，但是因为 V8 引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。

Node.js 几乎每一个 API 都是支持回调函数的。

Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。

Node.js 单线程类似进入一个while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数.

### EventEmitter  
EventEmitter 的每个事件由一个事件名和若干个参数组成，事件名是一个字符串，通常表达一定的语义。对于每个事件，EventEmitter 支持 若干个事件监听器。

当事件触发时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。  
EventEmitter 提供了多个属性，如 on 和 emit。on 函数用于绑定事件函数，emit 属性用于触发一个事件。
```js
var EventEmitter = require('events').EventEmitter;

var event = new EventEmitter();

event.on('some_event',function(){
    console.log('lll')
})
setTimeout(() => {
    event.emit('some_event')
}, 1000);
```