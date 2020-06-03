# ECMAScript 6
### 2.7.rest 参数

ES6 引入 rest 参数，用于获取函数的实参，用来代替 arguments

```
    //作用与 arguments 类似
    function add(...args){
        console.log(args);
    }
    add(1,2,3,4,5);

    //rest 参数必须是最后一个形参
    function minus(a,b,...args){
        console.log(a,b,args);
    }
    minus(100,1,2,3,4,5,19);
```

**注意**：rest 参数非常适合不定个数参数函数的场景

### 2.8.spread 扩展运算符

扩展运算符（spread）也是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列，对数组进行解包。

```
    //展开数组
    let tfboys = ['德玛西亚之力','德玛西亚之翼','德玛西亚皇子'];
    function fn(){
        console.log(arguments);
    }
    fn(...tfboys)

    //展开对象
    let skillOne = {
        q: '致命打击',
    };
    let skillTwo = {
        w: '勇气'
    };
    let skillThree = {
        e: '审判'
    };
    let skillFour = {
        r: '德玛西亚正义'
    };

    let gailun = {...skillOne, ...skillTwo,...skillThree,...skillFour};
```

扩展运算符的应用：

- 数组的合并
- 新数组的创建（浅拷贝）
- 将伪数组转换为真正的数组

### 2.9.Symbol

#### 2.9.1.Symbol 基本使用

ES6 引入了一种新的原始数据类型 Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，是一种类似于字符串的数据类型。
**Symbol 特点**

- Symbol 的值是唯一的，用来解决命名冲突的问题
- Symbol 值不能与其他数据进行运算
- Symbol 定义的对象属性不能使用 for…in 循环遍历，但是可以使用 Reflect.ownKeys 来获取对象的所有键名

```
    //创建 Symbol
    let s1 = Symbol();
    console.log(s1, typeof s1);

    //添加标识的 Symbol
    let s2 = Symbol('hahaha');
    let s2_2 = Symbol('hahaha');
    console.log(s2 === s2_2);

    //使用 Symbol for 定义
    let s3 = Symbol.for('hahaha');
    let s3_2 = Symbol.for('hahaha');
    console.log(s3 === s3_2);
```

**注**: 遇到唯一性的场景时要想到 Symbol

#### 2.9.2.Symbol 内置值

除了定义自己使用的 Symbol 值以外，ES6 还提供了 11 个内置的 Symbol 值，指向语言内部使用的方法。可以称这些方法为魔术方法，因为它们会在特定的场景下自动执行。

- Symbol.hasInstance
  当其他对象使用 instanceof 运算符，判断是否为该对象的实例时，会调用这个方法
- Symbol.isConcatSpreadable
  对象的 Symbol.isConcatSpreadable 属性等于的是一个布尔值，表示该对象用于 Array.prototype.concat()时，是否可以展开。
- Symbol.species
  创建衍生对象时，会使用该属性
- Symbol.match
  当执行 str.match(myObject) 时，如果该属性存在，会调用它，返回该方法的返回值。
- Symbol.replace
  当该对象被 str.replace(myObject)方法调用时，会返回该方法的返回值。
- Symbol.search
  当该对象被 str. search (myObject)方法调用时，会返回该方法的返回值。
- Symbol.split
  当该对象被 str. split (myObject)方法调用时，会返回该方法的返回值。
- Symbol.iterator
  对象进行 for...of 循环时，会调用 Symbol.iterator 方法，返回该对象的默认遍历器
- Symbol.toPrimitive
  该对象被转为原始类型的值时，会调用这个方法，返回该对象对应的原始类型值。
- Symbol. toStringTag
  在该对象上面调用 toString 方法时，返回该方法的返回值
- Symbol. unscopables
  该对象指定了使用 with 关键字时，哪些属性会被 with 环境排除。

### 2.10.迭代器

遍历器（Iterator）就是一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作。

1. ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费
2. 原生具备 iterator 接口的数据(可用 for of 遍历)
   - Array
   - Arguments
   - Set
   - Map
   - String
   - TypedArray
   - NodeList
3. 工作原理
   - 创建一个指针对象，指向当前数据结构的起始位置
   - 第一次调用对象的 next 方法，指针自动指向数据结构的第一个成员
   - 接下来不断调用 next 方法，指针一直往后移动，直到指向最后一个成员
   - 每调用 next 方法返回一个包含 value 和 done 属性的对象

**注**: 需要自定义遍历数据的时候，要想到迭代器。

### 2.11.生成器

#### 2.11.1 生成器

生成器函数是 ES6 提供的一种异步编程解决方案，语法行为与传统函数完全不同

```
  function * gen(){//*位置没有严格限制
    yield '一只没有耳朵';
    yield '一只没有尾巴';
    return '真奇怪';
  }
  let iterator = gen();
  console.log(iterator.next());
  console.log(iterator.next());
  console.log(iterator.next());
```

代码说明：

1. \* 的位置没有限制
2. 生成器函数返回的结果是迭代器对象，调用迭代器对象的 next 方法可以得到 yield 语句后的值
3. yield 相当于函数的暂停标记，也可以认为是函数的分隔符，每调用一次 next 方法，执行一段代码
4. next 方法可以传递实参，作为 yield 语句的返回值

#### 2.11.2 生成器函数参数

- 调用生成器函数, 返回的结果是一个迭代器对象
- yield 后面表达式的值返回给 next（）方法。
- 下次调用 next 方法的实参，会作为整个 yield 表达式的返回值。

```
   function * gen(args){
            console.log(args);
            //yield 整体有返回值
            let res1 = yield 2;
            console.log(res1);
            let res2 = yield 4;
            console.log(res2);
        }

        //调用生成器函数  返回的是一个迭代器对象
        let iterator = gen(1);

        //调用 next 方法,此时命令行输出1，r1的值为{value: 2, done: false}
        let r1 = iterator.next();
        //第二次调用 next，此时命令行输出3，r2的值为{value: 4, done: false}
        let r2 = iterator.next(3);
        //第三次调用，此时输出100，r3的值为{value: undefined, done: true}
        let r3 = iterator.next(100);

```
**实例1**:可以解决回调地狱的问题

```
 //1s 后控制台输出 111  2s后输出 222  3s后输出 333
        function fn1(){
            setTimeout(()=>{
                console.log(111);
                iterator.next();
            },1000)
        }

        function fn2(){
            setTimeout(()=>{
                console.log(222);
                iterator.next();
            },2000)
        }

        function fn3(){
            setTimeout(()=>{
                console.log(333);
                iterator.next();
            },3000)
        }

        //声明生成器函数
        function * gen(){
            yield fn1();
            yield fn2();
            yield fn3();
        }

        let iterator = gen();
        iterator.next();

```
**实例2**
```
 // 获取 用户数据   文章数据   商品数据
        function getUser(){
            setTimeout(() => {
                let data = '用户数据';
                iterator.next(data);
            }, 1000);
        }

        function getArticles(user){
            setTimeout(() => {
                console.log(user);
                let data = '文章数据';
                iterator.next(data);
            }, 1000);
        }

        function getGoods(article){
            setTimeout(() => {
                console.log(article);
                let data = '商品数据';
                iterator.next(data);
            }, 1000);
        }

        //生成器函数
        function *gen(){
            let users = yield getUser();
            // console.log(users);
            let articles = yield getArticles(users);
            // console.log(articles);
            let goods = yield getGoods(articles);
            // console.log(goods);
        }

        //获取迭代器对象
        let iterator = gen();
        iterator.next();
```
### 2.12.Set

ES6 提供了新的数据结构 Set（集合）。它类似于数组，<font style="color: red;">但成员的值都是唯一的</font>，集合实现了 iterator 接口，所以可以使用『扩展运算符』和『for…of…』进行遍历，集合的属性和方法：

1. size 返回集合的元素个数
2. add 增加一个新元素，返回当前集合
3. delete 删除元素，返回 boolean 值
4. has 检测集合中是否包含某个元素，返回 boolean 值
5. clear 清空集合，返回 undefined

```

        //创建一个空集合
        let s = new Set();
        //创建一个非空集合
        let s1 = new Set([1,2,3,1,2,3]);

        //集合属性与方法
        //返回集合的元素个数
        console.log(s1.size);
        //添加新元素
        console.log(s1.add(4));
        //删除元素
        console.log(s1.delete(1));
        //检测是否存在某个值
        console.log(s1.has(2));
        //清空集合
        console.log(s1.clear());

```
实践
```
        //1. 数组去重
        let arr = [1,2,3,4,5,4,3,2];
        let s = new Set(arr);
        //创建一个新的数组
        let newArr = [...s];
        console.log(newArr);

        //2. 交集
        let arr1 = [1,2,3,8,9,0];
        let arr2 = [1,2,4];

        let s1 = new Set(arr1);
        let s2 = new Set(arr2);

        //计算交集   5 - 3 = 2 差
        <!-- let arr = [...s1].filter(function(item){
             return s2.has(item);
        }); -->
        let inter = [...s1].filter(item => s2.has(item));

        //3. 并集
        let union = [...(new Set([...s1, ...s2]))];

        //4. 差集
        let diff = [...s1].filter(item => !s2.has(item));

        console.log(diff);
```
### 2.13.Map

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。Map 也实现了 iterator 接口，所以可以使用『扩展运算符』和『for…of…』进行遍历。Map 的属性和方法：

1. size 返回 Map 的元素个数
2. set 增加一个新元素，返回当前 Map
3. get 返回键名对象的键值
4. has 检测 Map 中是否包含某个元素，返回 boolean 值
5. clear 清空集合，返回 undefined

```

        //创建一个空 map
        let m = new Map();
        //创建一个非空 map
        let m2 = new Map([
        ['name','尚硅谷'],
        ['slogon','不断提高行业标准']
        ]);

        //属性和方法
        //获取映射元素的个数
        console.log(m2.size);
        //添加映射值
        console.log(m2.set('age', 6));
        //获取映射值
        console.log(m2.get('age'));
        //检测是否有该映射
        console.log(m2.has('age'));
        //清除
        console.log(m2.clear());

```

### 2.14.class

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。基本上，ES6 的 class 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 class 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
知识点：

1. class 声明类
2. constructor 定义构造函数初始化
3. extends 继承父类
4. super 调用父级构造方法
5. static 定义静态方法和属性
6. 父类方法可以重写

```

    //父类
    class Phone {
    //构造方法
      constructor(brand, color, price) {
        this.brand = brand;
        this.color = color;
        this.price = price;
      }

      //对象方法
      call() {
        console.log('我可以打电话!!!')
       }

    }

    //子类
    class SmartPhone extends Phone {
      constructor(brand, color, price, screen, pixel) {
        super(brand, color, price);
        this.screen = screen;
        this.pixel = pixel;
      }

      //子类方法
      photo(){
        console.log('我可以拍照!!');
      }

      playGame(){
        console.log('我可以玩游戏!!');
      }

      //方法重写
      call(){
        console.log('我可以进行视频通话!!');
      }

      //静态方法
      static run(){
        console.log('我可以运行程序')
      }

      static connect(){
        console.log('我可以建立连接')
      }

    }

    //实例化对象
    const Nokia = new Phone('诺基亚', '灰色', 230);
    const iPhone6s = new SmartPhone('苹果', '白色', 6088, '4.7inch','500w');

    //调用子类方法
    iPhone6s.playGame();
    //调用重写方法
    iPhone6s.call();
    //调用静态方法
    SmartPhone.run();

```

### 2.15.数值扩展

- 二进制和八进制:ES6 提供了二进制和八进制数值的新的写法，分别用前缀 0b 和 0o 表示。
- Number.isFinite() 用来检查一个数值是否为有限的
- Number.isNaN() 用来检查一个值是否为 NaN
- Number.parseInt() 将字符串提取数字为
- Number.parseFloat()
- Math.trunc 用于去除一个数的小数部分，返回整数部分。
- Number.isInteger() 用来判断一个数值是否为整数
- 幂运算 ES7 中新增了『\*\*』完成幂运算

### 2.16.对象扩展

ES6 新增了一些 Object 对象的方法

1. Object.is 比较两个值是否严格相等，与『===』行为基本一致（+0 与 NaN）
2. Object.assign 对象的合并，将源对象的所有可枚举属性，复制到目标对象
3. **proto** 可以直接设置对象的原型
   
### 2.17深拷贝和浅拷贝
所谓拷贝就是复制一份新的数据，这里数组是指数组与对象。
- 浅拷贝：新数据的改变会影响到原来的数据
- 深拷贝：新数据的改变不会影响到原来的数据

浅拷贝的情况：
- 对象或数组直接赋值。
- array.prototype.concat
- array.prototype.slice
- 扩展运算符

深拷贝的情况：
- JSON.stringify 将JS对象转为 JSON 字符串：不能处理方法（函数）类型的属性
- 
```
  let school = {
            name: '尚硅谷',
            slogon:'不断提高行业标准',
            cities: ['北京','深圳','上海'],
            founder: {
                name: '刚哥',
                age: 42
            },
            change(){
                console.log('改变你!!');
            }
        };

        let newObject = {};

        //如果是原始类型
        newObject.name = school.name;
        //判断如果是数组
        newObject.cities = [];
        newObject.cities[0] = school.cities[0];
        newObject.cities[1] = school.cities[1];
        newObject.cities[2] = school.cities[2];

        // newObject.name = 'atguigu';
        // newObject.cities[0] = 'BEIJING';
        // console.log(school);    
        // console.log(newObject);

        //如果是对象
        newObject.founder = {};
        newObject.founder['name'] = school.founder['name'];
        newObject.founder['age'] = school['founder']['age'];

        //如果是函数呢
        newObject.change = school.change.bind(newObject);
```
- 递归
```
let school = {
            name: '尚硅谷',
            slogon: '不断提高行业标准',
            cities: ['北京', '深圳', '上海'],
            founder: {
                name: '刚哥',
                age: 42
            },
            change() {
                console.log('改变你!!');
            }
        };

        /**
         * 深拷贝
         * @params data 待拷贝的数据
         */
        function deepClone(data) {
            //创建一个初始化数据 用来保存目标对象的数据
            let result;
            //判断 data 的数据类型
            let type = getDataType(data);
            //如果数据类型为数组, 则容器初始值也是数组
            if (type === 'Array') {
                result = [];
            }
            //如果数据类型为对象, 则容器初始值也是对象
            if (type === 'Object') {
                result = {};
            }
            
            //遍历目标数据 
            for (let i in data) {
                //对键值进行类型检测
                let type = getDataType(data[i]);
                //判断键值是否为对象和数组
                if (type === 'Array' || type === 'Object') {
                    result[i] = deepClone(data[i])
                } else if (type === 'Function') {
                    result[i] = data[i].bind(result);
                } else {
                    result[i] = data[i]
                }
            }

            return result;
        }

        function getDataType(data) {
            return Object.prototype.toString.call(data).slice(8, -1);
        }

        let result = deepClone(school);

        //打印结果
        school.cities[0] = 'BEIJING';
        console.log(school);
        console.log(result);
```

