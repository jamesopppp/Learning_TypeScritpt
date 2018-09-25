# Learning_TypeScritpt
learning typescript~ 学习ts的小笔记

#### 安装tpyescript
`npm install typescript -g`

#### 手动编译ts文件
`tsc helloworld.ts`

### 如何在vscode自动编译ts文件

1. 生成配置文件

`tsc --init`

目录下运行tsc --init 生成配置文件tsconfig.json 

2. 配置编译输出目录

```
...
"outDir": "./js"
...
```

3. 启动监视

面板选择
Tasks => Run Task

选择 tsc: watch ... 选项启动监视,此时就会自动编译ts文件到outDir目录下

### typescript中的数据类型

>布尔类型 (boolean)
>
>数字类型 (number)
>
>字符串类型 (string)
>
>数组类型 (array)
>
>元组类型 (tuple)
>
>枚举类型 (enum)
>
>任意类型 (any)
>
>null undefined
>
>void 类型
>
>never 类型

typescript中强制增加了类型校验

#### 定义ts变量

example:
```
var flag:boolean = true; // :+数据类型 指定变量的数据类型

flag = 123; // error  不可改变数据类型
```

#### 如何定义数组
example:
```
// 定义数组1 
var arr1:number[] = [11,23,23];

// 定义数组2
var arr2:Array<number> = [11,23,11];

// 定义数组3
var arr3:any[] = [11,'23',true];

// 定义数组4
var arr4:[number,string] = [11,'123'];
```

#### 元组类型(tuple) 属于数组的一种类型
example:
```
let arr:[number,string] = [123,'123']

为数组每一个位置指定数据类型
```

#### 枚举类型
```
enum 枚举名 {
    标识符[=整型常数],
    标识符[=整型常数],
    ...,
    标识符[=整型常数]
}
```
* 标识符赋值,枚举返回赋值数

example:
```
enum Err {
    'undefined' = -1,
    'null' = -2,
    'success' = 1
};

let e:Err = Err.success;

console.log(e);  // 1
```
* 未赋值将返回该标识符下标

example:
```
enum Color {blu,red,'orange'};
let c:Color = Color.red;

console.log(c); // 1
```

* 前面赋值了,枚举返回下标

example:
```
enum Color {blue=4,red,'orange'};
let c:Color = Color.orange;
console.log(c); 6
```

#### 任意类型 (any)
example:
```
var num:any = 123;
num = 'str';
console.log(num); //str
```
改变类型不报错,任意类型可以如下场景使用:

example:
```
let oBox:any = document.getElementById('box');

oBox.style.color = 'red';
```
ts不存在Object类型所以这里指定类型为any就不会报错

#### undefined类型
example:
```
var num:number;
console.log(num); // undefined 报错

var num:undefined;
console.log(num); // undefined 不报错

var num:number | undefined;
console.log(num);  //可数字可undefined
```

#### null 空类型
example:
```
var num:null;

num = 123;
console.log(num); // 报错error
```

#### void 类型
* 定义没有返回值的方法

example:
```
function run():void {
    console.log('run');
}
run();   // run 正常编译

----

function run():void {
    return 'run';
}
run();   // 报错 error
```

* 需要返回值要指定类型

example:
```
function run():string {
    return 'abc';
}
console.log(run());  // 正常编译
```

#### never 类
属于其他类型 (包括null,undefined) 的子类型,代表从不会出现的值。

example:
```
var a:never;

a = 123;  // 报错

a=(()=>{
    throw new Error('错误');
})()   // 正常编译
```

### 函数定义
*ES5 定义函数

example: 
```
函数声明
function run(){
    return 'run';
}

匿名函数
var run2 = function(){
    return 'run2';
}
```

*TS 定义函数

example:
```
函数声明
function run():string{
    return 'run';
}
指定返回值类型的函数

匿名函数
var fun2 = function():number{
    return 123;
}
fun2(); 执行函数
```

#### ts方法传参
```
声明
function getInfo(name:string,age:number):string{
    return `${name} --- ${age}`;
}

alert(getInfo('james','20'));

匿名
var getInfo = function(name:string,age:number):string{
    return `${name} --- ${age}`;
}

没有返回值的方法
function run():void{
    console.log('run');
}
run();

传值可选参数
function getInfo(name:string,age?:number):string{
    if(age){
        return `${name} --- ${age}`;
    } else {
        return `${name} --- 年龄保密`;
    }
}

alert(getInfo('james'));
alert(getInfo('james',123));
```
