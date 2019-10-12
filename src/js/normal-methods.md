


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
```

3. JQuery的 $each循环可以使用 return true 退出当前each循环，使用return false退出整个each循环.

4. Math.min & Math.max 求传入参数的最小值、最大值,返回对应值
```
    Math.min(1,2,3);

    Math.min(...[1,2,3]);/*传入数组则要使用扩展运算符*/
```
5. Promise:  
    > ```Promise.then();  
    > Promise.catch();  
    > Promise.finally();  
    > Promise.all();  
    > Promise.allSettled();  
    > Promsie.any();
    > Promise.resolve();  
    > Promise.reject();           
    ```const p = Promise.all([p1, p2, p3]);```  
    p的状态由p1、p2、p3决定，分成两种情况。（1）只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。  
    （2）只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。  
    ```const p = Promise.race([p1, p2, p3]);```  
    只要p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给p的回调函数。    
    （3）```Promise.allSettled()```方法接受一组 Promise 实例作为参数，包装成一个新的 Promise 实例。只有等到所有这些参数实例都返回结果，不管是fulfilled还是rejected，包装实例才会结束。该方法由 ES2020 引入。返回的总是fulfilled。  
    （4）```Promise.any()```方法接受一组 Promise 实例作为参数，包装成一个新的 Promise 实例。只要参数实例有一个变成fulfilled状态，包装实例就会变成fulfilled状态；如果所有参数实例都变成rejected状态，包装实例就会变成rejected状态。该方法目前是一个第三阶段的提案 。
    
    

            