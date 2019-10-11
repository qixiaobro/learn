


## 常用方法

1. delete : 删除指定对象属性，返回true.
```
    var object = {a:1,b:2,c:3};
    delete object['a']
    
```

2. Object.keys :返回指定对象的可枚举属性组成的字符数组
```
    var objects={ a:1,b:2,c:3};
    Object.keys(objects);

    /*['a','b','c']*/
