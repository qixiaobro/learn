


## 常用方法

1. delete : 删除指定对象属性，返回true.
``` javascript
    var object = {a:1,b:2,c:3};
    delete object['a']
```

2. Object.keys :返回指定对象的可枚举属性组成的字符数组
``` javascript
    var objects={ a:1,b:2,c:3};
    Object.keys(objects);

    /*['a','b','c']*/
```

3. JQuery的 $each循环可以使用 return true 退出当前each循环，使用return false退出整个each循环.

4. Math.min & Math.max 求传入参数的最小值、最大值,返回对应值
``` javascript
    Math.min(1,2,3);

    Math.min(...[1,2,3]);/*传入数组则要使用扩展运算符*/
```

    
    

            