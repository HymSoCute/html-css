# DOM

## 1、概念、作用、顶级对象

**在 DOM 中一切皆对象**  
DOM 就是文档对象模型，是一个使程序和脚本有能力动态地访问和更新文档的内容、结构以及样式的平台和语言中立的接口。接口可以理解为就是函数（函数 方法 API 接口 本质上都是一个函数  
**描述了处理网页内容的方法和接口**

- window 是浏览器窗口对象，所有东西都被当作是 window 的子对象
- 文档对象 document 是 window 下的一个属性 代表整个 DOM 文档对象

### 文档树

文档树(dom 树)：以 HTML 为根节点 形成的一棵倒立的树状结构，我们称作 DOM 树；这个树上所有的东西都叫节点，节点有很多类

- 元素节点 标签
- 属性节点 属性
- 文本节点 内容
- 注释节点 注释

这些节点如果我们通过 DOM 方法去获取或者其它的操作去使用的话，就叫 DOM 对象

## 2、等待页面加载完成事件

```
	window.onload = function(){
        (等待页面加载完成，系统会自动执行函数当中的代码；)
			}
```

一般情况我们都是等待页面加载完成之后才去操作 dom 元素，如果页面没有加载完成就去获取 dom 元素，有可能获取不到；

## 3、获取 DOM 元素对象，操作元素属性

### （1）获取 DOM 对象的方法

**拿元素的时通过指定的属性去拿(比较局限)**

- 通过 id 获取到相关元素 封装为 dom 对象返回，如果没有 id 没办法获取，这个方法只能获取一个 dom 元素对象（document 下的一个方法）**只能通过 ID 去获取元素 并且只能获取一个元素返回**

```
    var box = document.getElementById('box');
```

- 通过标签拿: 只能通过标签名去获取，并且获取到是多个返回一个伪数组，哪怕标签只有一个也是伪数组

```
    var pNodes = document.getElementsByTagName('p');
    console.log(pNodes);
    console.log(pNodes[2]);
```

- 通过类名拿:只能通过类名去获取，并且获取到是多个返回一个伪数组，哪怕只有一个标签是这个类也是伪数组

```
    var pList = document.getElementsByClassName('pp');
    console.log(pNodes);
    console.log(pNodes[2]);
```

**根据选择器拿到想要的**
querySelector 和 querySelectorAll 也可以获取元素，但是他们和上面不同的是，他们根据选择器去获取。也就是说只要选择器写的对就可以获取到；

- querySelector 专门用来获取选择器选中只有一个元素；返回的是单个元素 dom 对象;
- querySelectorAll 专门用来获取选择器选中多个元素，返回也是伪数组；

```
    var p4 = document.querySelector('#p4');
    console.log('p4');

    var pp = document.querySelectorAll('pp');
    console.log('pp');
```

### (2)事件

事件三要素

- 事件源 （承受事件的对象）
- 事件类型 onclick
- 事件处理回调函数

事件处理三大步

- 获取事件源 DOM 对象
- 添加对应事件监听
- 书写处理回调

事件写好之后可以重复触发执行；

### (3)修改元素的属性

- 通过 js 修改标签属性，这个属性和属性值一样的属性，此时，要用 ture。

```
    check.checked = true;
```

- class 是 js 的特殊属性，由于是 js 中的关键字，没办法使用，在操作时，将 classs 改为 className 使用。

```
    pNode.className = 'p2';
```

- 在操作元素属性的时候，.语法只能操作元素天生具有的属性，如果是自定义的属性，通过.语法是无法操作的；只能通过 setAttribute 和 getAttribute 去操作； setAttribute 和 getAttribute 是通用的方法，无论元素天生的还是自定义的属性都可以操作；

```
    pNode.setAttribute('aa', 'cc');
    console.log(pNode.getAttribute('aa'));
```

### (4)修改 p 标签的内容

**innerHTML 和 innerText**

```
    pNode.innerHTML = '<h2>haha<h2>';
    pNode.innerText = '<h2>haha<h2>';

    console.log(pNode.innerText);
    console.log(pNode.textContent);
```

**区别**

- 设置内容的时候：如果内容当中包含标签字符串 innerHtml 会有标签的特性，也就是说标签会在页面上生效，如果内容当中包含标签字符串 innerText 会把标签原样展示在页面上，不会让标签生效，如果内容当中没有其它标签，他们两个一致；都是设置文本内容

- 读取内容的时候：如果标签内部还有其它标签，innerHtml 会把标签内部带着其它的标签全部输出， 如果标签内部还有其它标签，innerText 只会输出所有标签里面的内容或者文本，不会输出标签，如果标签内部没有其它标签，他们两个一致；都是读取文本内容，innerHtml 会带空白和换行

**textContent 及 innerText**

```
    console.log(pNode.innerText);
    console.log(pNode.textContent);
```

**区别**

- textContent 可以获取隐藏元素的文本，包含换行和空白，只有高级浏览器认识
- innerText 不可以获取，并且不包含换行和空格

### (5)鼠标事件

- onmousemove 鼠标移动
- onmouseover 鼠标移入（1）
- onmouseout 鼠标移出（1）
- onmounseenter 鼠标移入（2）
- onmouseleave 鼠标移出（2）
- onclick 鼠标点击
- onmousedown 鼠标按下
- onmouseup 鼠标抬起

```
    for (var i = 0; i < liNodes.length; i++) {
        liNodes[i].onmouseover = function () {
            this.style.backgroundColor = 'pink';
                }
        liNodes[i].onmouseout = function () {
            this.style.backgroundColor = 'indianred';
                }
            };
```

### (6)键盘事件

键盘事件要么就是给表单类元素添加，要么就是对 document，document 是页面最外层的元素（但是在 html 当中没有东西表示）
**事件对象**

- 任何的事件（包括鼠标事件）在触发的时候，系统都会给我们封装好一个和这个事件相关的对象，被称作事件对象
- 事件对象在高级浏览器触发的时候，都会把这个对象当做实参，传递给回调函数的第一个形参；
- 这个事件对象当中，包含了这一次触发事件所有相关的信息；

```
    //我们想要按回车键打印嘿嘿
    //按 shift 键打印哈哈
    window.onload = function () {
        var inputNode = document.querySelector('input');
        inputNode.onkeyup = function (event) {
            console.log('haha');
            console.log(event);//获取键值
            if (event.keyCode == 13) {
                console.log('嘿嘿');
            } else if (event.keyCode == 16) {
                console.log('哈哈');
            }
        }
    }
```

### (7)获取焦点事件

一般都是针对表单类元素得

**onfocus & onblur** ：获取焦点 & 失去焦点

**onkeyup & onkeydown**

一般用的都是 keyup 事件，它能够确保键盘事件只执行一次；

**keycode**

存在于事件对象当中，也就是我们回调函数的第一个形参；这个对象不是我们创建，当事件发生的时候，系统会创建好这个事件对象，并且传参（实参）调用；事件对象当中包含了和事件相关的一切；

## 4、操作元素思想

**排他思想**

```
    //点击任何一个p，点击的这个p变成哈哈，其他的变成嘿嘿
    window.onload = function () {
        var pNodes = document.querySelectorAll('p');
        for (var i = 0; i < pNodes.length; i++) {
            pNodes[i].onclick = function () {
            for (var j = 0; j < pNodes.length; j++) {
                pNodes[j].innerHTML = '嘿嘿';
            }
            this.innerHTML = 'haha';
        };
    }
```

**二级索引**

```
    window.onload = function () {
        var liNode = document.querySelectorAll('.list>li');
        var ulNodes = document.querySelectorAll('.list>li .listIn');
        for (var i = 0; i < liNode.length; i++) {
            liNode[i].index = i;
            liNode[i].onmouseover = function () {
            ulNodes[this.index].style.display = 'block';
            }
            liNode[i].onmouseout = function () {
                ulNodes[this.index].style.display = 'none';
            }
        }

    }
```

**开关**

```
    //开关状态改变div背景颜色
    window.onload = function () {
        var box = document.getElementById('box');
        var flag = true;
        box.onclick = function () {
            if (flag) {
                box.style.backgroundColor = 'green';
                flag = false;
            } else {
                box.style.backgroundColor = 'red';
                flag = true;
            }
        }
    }
```

## 5、兼容性封装设置读取内容函数

**浏览器兼容性讲解**

- 浏览器：chrome Firefox safari opera IE
- 高级浏览器和低级浏览器：是以 IE8 为分水岭，IE8 及以下的 IE 浏览器我们称作低级，其余的都是高级浏览器。

```
    //兼容性封装操作元素的内容（读  写）
    //功能多样；
    //用户是高级浏览器自动使用textContent 低级浏览器就使用innerText
    function setOrGetContent(node, content) {
        if (arguments.length == 1) {
        //代表在读取内容
            if (node.textContent) {
            //能拿到这个dom对象的textContent属性值，代表这个用户是高级浏览器
                return node.textContent;
            } else {
            //代表拿不到，就是undefined   那就是低级浏览器
                return node.innerText;
            }
        } else if (arguments.length == 2) {
        //代表在设置内容
            if (node.textContent) {
            //代表高级
                node.textContent = content;
            } else {
            //代表低级
                node.innerText = content;
            }

        }
    }
```
