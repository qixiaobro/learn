
* ```Object.prototype.toString.call```  判断数据类型终极解决办法
 该方法本质就是依托```Object.prototype.toString()```方法得到对象内部属性 ```[[Class]]```
传入原始类型却能够判定出结果是因为对值进行了包装
```null``` 和 ```undefined``` 能够输出结果是内部实现有做处理

```js
var type = function(data) {
      var toString = Object.prototype.toString;
      var dataType = toString
              .call(data)
              .replace(/\[object\s(.+)\]/, "$1")
              .toLowerCase()
      return dataType
};
```

* 既然有了```indexOf```方法，为什么又造一个```includes```方法，```arr.indexOf(x)>-1```不就等于```arr.includes(x)```？看起来是的，几乎所有的时候它们都等同，唯一的区别就是```includes```能够发现```NaN```，而```indexOf```不能。

* ```Object.prototype.hasOwnProperty(prop)```
该方法仅在目标属性为对象自身属性时返回true,而当该属性是从原型链中继承而来或根本不存在时，返回false。

* 判定元素是否滚动到底
如果元素滚动到底，下面等式返回true，没有则返回false.
```js
element.scrollHeight - element.scrollTop === element.clientHeight
```