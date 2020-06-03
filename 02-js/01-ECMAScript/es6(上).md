# ECMAScript 6
## ECMAScript 6整体介绍
### 1.1.什么是 ECMA

EMCA（European Computer Manufacturers Association）中文名称为欧洲计算机制造商协会，这个组织的目标是评估、开发和认可电信和计算机标准。1994 年后该组织改名为 Ecma 国际。

### 1.2.什么是 ECMAScript

ECMAScript 是由 Ecma 国际通过 ECMA-262 标准化的脚本程序设计语言。

### 1.3.什么是 ECMA-262

Ecma 国际制定了许多标准，而 ECMA-262 只是其中的一个，所有标准列表查看
http://www.ecma-international.org/publications/standards/Standard.htm

### 1.4.ECMA-262 历史

ECMA-262 历史版本查看网址
http://www.ecma-international.org/publications/standards/Ecma-262-arch.htm  
**注**：ECMA-262（ECMAScript）每年发布一个版本，版本号比年份最后一位大 1，

- ECMAScript 6 是 2015 年发布，又称为 ES2015，简称为 ES6
- ECMAScript 7 是 2016 年发布，又称为 ES2016，简称为 ES7
- ECMAScript 8 是 2017 年发布，又称为 ES2017，简称为 ES8

### 1.5.为什么要学习 ES6

ES6 规范加入了许多的语言特性，适当的场景使用新的语法特性会让编程变得简单、高效，还能提高代码的可读性 ，同时语言的发展也是向着更简洁、更标准的方向发展，学习 ES 新标准也是顺应技术的发展趋势。
### 1.6.总体结构
![img](.\img\20060301.PNG)
## ES5

### 严格模式

#### 介绍

ES5 除了正常运行模式（又称为混杂模式），还添加了第二种运行模式："[严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)"（strict mode）。

严格模式顾名思义，就是使 Javascript 在更严格的语法条件下运行。

#### 作用

1.  消除 Javascript 语法的一些不合理、不严谨之处，减少一些怪异行为
2.  消除代码运行的一些不安全之处，保证代码运行的安全
3.  为未来新版本的 Javascript 做好铺垫

#### 使用

- 在全局或函数的第一条语句定义为: `'use strict'`

- 如果浏览器不支持，只解析为一条简单的语句, 没有任何副作用

  ```js
  // 全局使用严格模式
  "use strict";
  girl = "迪丽热巴";

  // 函数中使用严格模式
  function main() {
    "use strict";
    boy = "吴亦凡";
  }
  main();
  ```

#### 语法和行为改变

- 必须用 var 声明变量，不允许使用未声明的变量
- 禁止自定义的函数中的 this 指向 window
- 创建 eval 作用域
- 对象不能有重名的属性（ES6 已经修复了这个 Bug，IE 还会出现）
- 函数不能有重复的形参

### Object 扩展方法

#### Object.create(prototype, [descriptors])

Object.create 方法可以以指定对象为原型创建新的对象，同时可以为新的对象设置属性, 并对属性进行描述

- value : 指定值
- writable : 标识当前属性值是否是可修改的, 默认为 false
- configurable：标识当前属性是否可以被删除 默认为 false
- enumerable：标识当前属性是否能用 for in 枚举 默认为 false
- get: 当获取当前属性时的回调函数
- set: 当设置当前属性时

```js
//创建一个汽车的对象
var car = {
  name: "汽车",
  run: function () {
    console.log("我可以行驶！！");
  },
};

//以 car 为原型对象创建新对象
var aodi = Object.create(car, {
  brand: {
    value: "奥迪",
    writable: false, //是否可修改
    configurable: false, //是否可以删除
    enumerable: true, //是否可以使用 for...in 遍历
  },
  color: {
    value: "黑色",
    wriable: false,
    configurable: false,
    enumerable: true,
  },
});
```

#### Object.defineProperties(object, descriptors)

直接在一个对象上定义新的属性或修改现有属性，并返回该对象。

- object 要操作的对象
- descriptors 属性描述
  - get 作为该属性的 getter 函数，如果没有 getter 则为 undefined。函数返回值将被用作属性的值。
  - set 作为属性的 setter 函数，如果没有 setter 则为 undefined。函数将仅接受参数赋值给该属性的新值。

```js
// 定义对象
var star = {
  firstName: "刘",
  lastName: "德华",
};

// 为 star 定义额外的属性
Object.defineProperties(star, {
  fullName: {
    get: function () {
      return this.firstName + this.lastName;
    },
    set: function (name) {
      var res = name.split("-");
      this.firstName = res[0];
      this.lastName = res[1];
    },
  },
});

// 修改 fullName 属性值
star.fullName = "张-学友";

// 打印属性
console.log(star.fullName);
```

### call、apply 和 bind

- call 方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数

- apply 方法调用一个具有给定 this 值的函数，以及作为一个数组（或类似数组对象）提供的参数

- bind 同 call 相似，不过该方法会返回一个新的函数，而不会立即执行

```js
function main() {
  console.log(this);
}
/*1. 直接调用函数*/
main(); //  window
/*2. 创建一个对象*/
var company = { name: "hahaha", age: 10 };
/*使用这个对象调用 main 方法*/
main.call(company); // company
main.apply(company); // company
/*bind 修改 this 的值，返回一个新的函数*/
var fn = main.bind(company);
fn(); // company
```

## ECMASript 6 新特性

### 2.1.let 关键字

let 关键字用来声明变量，使用 let 声明的变量有几个特点：

1. 不允许重复声明
2. 块儿级作用域

   - ES5 只存在全局作用域和函数作用域
   - 块儿级作用域指的是变量只在当前代码块生效
   - 块儿的情况包括但不限于以下几种情况

     - if…else… 条件语句
     - for…in 循环语句
     - while 循环语句
     - function 函数代码体
     - {} 直接的花括号

3. 不存在变量提升

**注意**：以后声明变量使用 let 就对了, <font style="color: red;">let 可以解决循环中索引变化的问题</font>

### 2.2.const 关键字

const 关键字用来声明常量，const 声明有以下特点

- 不允许重复声明
- 值不允许修改
- 块儿级作用域

**注意**：对象属性修改和数组元素变化不会出发 const 错误(由于定义 const 变量的地址并没有改变)，声明优先使用 const，其次选择 let

### 2.3.变量的结构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构赋值。

```
//数组的解构赋值
const arr = ['张学友', '刘德华', '黎明', '郭富城'];
let [zhang, liu, li, guo] = arr;

//对象的解构赋值
const lin = {
name: '林志颖',
tags: ['车手', '歌手', '小旋风', '演员']
};
let {name, tags} = lin;

//复杂解构
let wangfei = {
name: '王菲',
age: 18,
songs: ['红豆', '流年', '暧昧', '传奇'],
husband: [
{name: '窦唯'},
{name: '李亚鹏'},
{name: '谢霆锋'}
]
};
let {songs: [one, two, three], husband: [first, second, third]} = wangfei;
```

**注意**：频繁使用对象方法、数组元素，就可以使用解构赋值形式

### 2.4.模板字符串

模板字符串（template string）是增强版的字符串，用反引号（\`）标识，特点：

- 字符串中可以出现换行符
- 可以使用 \${xxx} 形式输出变量

```
    // 定义字符串
    let str =`<ul>
                <li>沈腾</li>
                <li>玛丽</li>
                <li>魏翔</li>
                <li>艾伦</li>
            </ul>`;

    // 变量拼接
    let star = '王宁';
    let result = `${star}在前几年离开了开心麻花`;
```

**注意**：当遇到字符串与变量拼接的情况使用模板字符串

### 2.5.简化对象写法

ES6 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```
    let name = '尚硅谷';
    let slogon = '永远追求行业更高标准';
    let improve = function () {
        console.log('可以提高你的技能');
    }
    //属性和方法简写
    let atguigu = {
        name,
        slogon,
        improve,
        change() {
            console.log('可以改变你')
        }
    };
```

**注意**：对象简写形式简化了代码，所以以后用简写就对了

### 2.6.箭头函数

ES6 允许使用「箭头」（=>）定义函数。

```
    //1、通用写法
    let fn = (arg1, arg2, arg3) => {
        return arg1 + arg2 + arg3;
    }
```

箭头函数的注意点

- 如果形参只有一个，则小括号可以省略
- 函数体如果只有一条语句，则花括号可以省略，函数的返回值为该条语句的执行结果
- 箭头函数 this 指向声明时所在作用域下 this 的值
- 箭头函数不能作为构造函数实例化

```
    //2、省略小括号的情况
    let fn2 = num => {
        return num _ 10;
    };

    //3、省略花括号的情况
    let fn3 = score => score _ 20;

    //4、this 指向声明时所在作用域中 this 的值
    let fn4 = () => {
        console.log(this);
    }

    //箭头函数的指向问题
    let school = {
        name: 'hahaha',
        getName(){
            let fn5 = () => {
                console.log(this);
            }
            fn5();
        }
    };
```

**注意**：箭头函数不会更改 this 指向，用来指定回调函数会非常合适