# ES6简介

## 变量
### 变量声明let const
    注：变量声明方法    var-function-let-const-import-class

* 变量声明后形成，块级作用域即{}，变量只在作用域内被声明后使用。

* 不存在变量提升,所有的变量的访问都在声明后

* 暂时性死区:

    `var tmp = 123;
    if (true) {
        tmp = 'abc'; // ReferenceError
        let tmp;
    }`

* 不允许重复声明

* let const声明的变量脱离了顶层对象window

    `var a = 1;`

    // 如果在 Node 的 REPL 环境，可以写成 global.a

    // 或者采用通用方法，写成 this.a

    `window.a // 1`

    `let b = 1;`
    `window.b // undefined`


## 变量的结构
解构(所有拥有iterator接口的对象都可使用数组解构)，如下常用解构：

* `let [o = 1] = []` 设置默认值

* `let {a:b} = {b:123}` 取b值重命名为a

* `const [s] = '123'` //1

* `[x, y] = [y, x];` 交换位置

* 设置方法的参数默认值

## 变量的拓展

* 模板字符串

* 将变量当参数调用
    `console.log'123' = console.log([123])`

* 方法相关

    String.fromCodePoint()  
    String.raw()  
    实例方法：codePointAt()  
    实例方法：normalize()  
    实例方法：includes(), startsWith() , endsWith()  
    实例方法：repeat()  
    实例方法：padStart()，padEnd()  
    实例方法：trimStart()，trimEnd()  
    实例方法：matchAll()  

* 箭头函数
    1.函数内的this对象，就是定义时的对象，而不是使用时的对象。

    2.不可以当作构造函数，无法使用new命令

    3.不能使用arguments，要使用可以使用rest替代

    4.不可以使用yield命令

    5.对象中的属性方法中this指向全局对象，非该对象。

    6.尾调用，内部函数不使用外部函数自有变量下，尾调用可以减少函数调用帧，节省内存好用。


* try catch 中 catch的参数可以省略。

* arr.concat() 复制数组

* rest ... 用途：复制 解构 去重数组

* arr.from()  对象 => 数组

* super 用在对象的方法中，将对象属性指向原型对象

    const proto = {  
    foo: 'hello'  
    };  

    const obj = {  
        foo: 'world',  
        find() {  
            return super.foo;  
        }  
    };  

    Object.setPrototypeOf(obj, proto）;  
    obj.find() // "hello"  

* `Object.assign([1, 2, 3], [4, 5])`
// [4, 5, 3]


* apply方法可以接受三个参数，分别是目标对象、目标对象的上下文对象（this）和目标对象的参数数组。

## promise 

* f = Promise.all([promise1,promise2]);

所有的promise成功,f成功
任意一个promise返回失败，p失败

* ff  = Promise.race([promise1,promise2])

任意promise有返回不管成功失败，ff都将被赋值

* fff = Promise.allSettled([pm1,pm2])

所有的promise都有返回，fff才会被赋值，值未数组[{status,value}]

* ffff = Promise.any([pm1,pm2])

有任意pomise成功，ffff成功

所有promise失败，ffff失败

## iterator 可以使用for of去验证对象是否有iterator接口


## Generator 
Generator 函数有多种理解角度。语法上，首先可以把它理解成，Generator 函数是一个状态机，封装了多个内部状态。


    function* f() {
    for(var i = 0; true; i++) {
        var reset = yield i;
        if(reset) { i = -1; }
    }
    }

    var g = f();

    g.next() // { value: 0, done: false }
    g.next() // { value: 1, done: false }
    g.next(true) // { value: 0, done: false } 


## async await

可以分开使用，用法如下

    async function getInfo(){ //async返回一个promise
        const id = await getUserId(); //await表示线程挂起等待返回，阻塞脚本执行
        const name = await getUserName(id);
    }

    getInfo().then(res => res-await函数返回值).catch(error => 程序错误);


