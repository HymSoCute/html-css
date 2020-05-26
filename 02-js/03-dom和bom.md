# DOM 和 BOM

## 一、事件绑定和解绑（要对应）

### 1.DOM 0 1 2 3

- dom 0 和 dom2 有自己独立的事件绑定和解绑方式
- dom0 事件所有的浏览器都可以使用
- dom2 事件高级浏览器和低级浏览器用的添加方法不同
- dom1 和 dom3 没有事件绑定方式;

### 2.Dom0 事件绑定和解绑

- 不可以同时添加同一类事件多次，如果添加后面覆盖前面；
- dom0 事件解绑:本质上就是把事件回调函数和事件对象的事件属性断开指向；

```
    btn.onclick = function(){
	    box.onclick = null;
    }
```

### 3.Dom2 事件绑定和解绑

- dom2 事件添加同一类型事件多次，会依次执行事件，不会覆盖
- dom2 事件解绑，函数必须放在外面去定义,如果不放在外面定义，直接在参数当中写匿名函数表达式，那么绑定和解绑，传的回调函数不是同一个，所以解绑不了；

* dom2 事件添加方式和 dom0 完全不一样，它需要使用事件添加方法去做
* dom2 事件添加的时候，高级浏览器和低级浏览器使用的方法不一样；

**高级浏览器**

添加

```
	box.addEventListener('click',function(){
		console.log('i love you~ zhao li ying~');
    })
```

解绑

- 解绑的时候，有解绑的方法，而且方法当中传的参数 必须和绑定的时候参数完全一样才能解绑
- 如果你的事件需要解绑，那么函数必须在外面定义成有名函数，才能保证绑定和解绑的是同一个函数；

* 当绑定的事件需要解绑，那么事件回调定义在外面，写成有名函数

```
	function fn(){
        console.log('i love you~ zhao li ying~');
	}
    //绑定
    box.addEventListener('click',fn);
    //解绑
    btn.onclick = function(){
		box.removeEventListener('click',fn);
	}
```

**注:** 以下代表的不是同一个东西

- [] == []
- {} == {}
- function(){} == function(){}

**低级浏览器**

添加

```
    box.attachEvent('onclick',function(){
        console.log('i love you~  tangyan');
	})
```

解绑

- 和高级浏览器一样，添加的时候如果需要解绑，函数在外面定义成有名函数

```
    function fn1(){
        console.log('i love you~  tangyan');
	}
    //绑定
    box.attachEvent('onclick',fn1);
    /解绑  也是要和绑定的时候，咱叔完全一致；
		btn.onclick = function(){
            box.detachEvent('onclick',function(){
			console.log('i love you~  tangyan');
			})
		}
		btn.onclick = function(){
			box.detachEvent('onclick',fn1);
		}
```

- 和高级浏览器一样 绑定多个同类型事件，也是会按照一定顺序依次执行
- 高级浏览器是从上到下去执行，低级浏览器从下到上去执行

* 最终我们要注意：高级浏览器 don2 绑定解绑方法 addEventListener 和 removeEventListener
* 低级浏览器 dom2 绑定解绑方法 attachEvent 和 detachEvent

**兼容性处理元素绑定 dom2 事件**

绑定

```
    function addEvent(node,eventType,callback,isBubble){
        if(node.addEventListener){
		    //高级
		    //高级浏览器添加事件的时候，第三个参数代表的是事件流，捕获(true)还是冒泡（false）
		    node.addEventListener(eventType,callback,isBubble);
		}else{
			//低级
			//低级浏览器添加事件的时候，没有第三个参数，因为ie浏览器事件流主张的就是冒泡
			node.attachEvent('on'+eventType,callback);
		}
	}
    //添加dom2事件使用兼容添加方式
    addEvent(box,'click',function(){
		console.log('heihei');
	},false)

```

解绑

```
    function removeEvent(node, eventType, callback) {
		if (node.removeEventListener) {
			node.removeEventListener(eventType, callback);
        } else {
			ode.detachEvent('on' + eventType, callback);
		}
	}
    function fn() {
		console.log('heihei');
	}
	addEvent(box, 'click', fn, false)
	btn.onclick = function () {
		removeEvent(box, 'click', fn);
	}
```

## 二、事件流（事件传播）\*\*

### 1.事件流的发展：

1. 捕获事件流（网景） 最终很少用几乎不用
2. 冒泡事件流（ie） 最终我们所用的事件传播都是冒泡
3. 标准 DOM 事件流 这个是我们现用的标准事件流，里面包含三个阶段： 有捕获 再去获取元素 最后冒泡，这个三个阶段当中的捕获和冒泡可以由程序员自己选择。但是通常情况我们都是使用默认 （冒泡）；

- 事件流（事件传播）是客观存在的，但是事件监听要看程序员给谁添加了；
- 事件流和事件监听，没关系

## 2.事件冒泡和事件捕获

## 3.阻止事件冒泡

事件流（事件传播）每个事件都是必不可免的，也就是说每个事件都会进行冒泡；冒泡的情况下，如果是父子元素都添加了相同的事件监听，那么事件处理会从内到外依次执行；但是有些时候，我们确实是这样的结构，但是又不想让父元素事件进行处理；此时：我们就要用到阻止事件冒泡；

阻止冒泡的时候，想在哪个元素阻止，需要在哪个元素的事件回调处理函数当中加上这一行；

> event.stopPropagation();//专门用来阻止事件冒泡用的；

## 三、事件委派 \*\*

### 1.什么是事件委派

- 事件委派过程当中依赖了事件冒泡；
- 阻止事件冒泡:是为了解决冒泡给我们带来的困扰
- 事件冒泡的好处就是可以进行事件委派（事件委托，事件代理）；把子元素的事件监听添加给共同的父（祖先）元素,把子元素发生的事件委托给父元素进行处理；

### 2.事件委派用法，

**什么时候用**

1.  当一个元素内部儿子很多，并且每个儿子都要添加相同的事件的时候，我们可以使用事件委派来提高效率；
2.  出现新添加的东西，并且新添加的东西要和老的拥有同样的行为；此时我们就想事件委派；不用事件委派，老的身上会有想要的行为，而新添加的没有；

**用法:**

给爹添加事件监听，不给元素本身添加，事件发生后通过 event 去找真正发生事件的目标元素进行处理；

**好处:**

可以大大降低内存的占用，并且可以提高效率。

**总结**

事件委派其实是借用事件冒泡去做的，因为事件冒泡导致内部所有的元素发生事件都会冒泡到祖先身上，我们不在子元素身上去添加事件监听和处理，而是在共同的祖先身上去添加，让祖先去处理子元素发生的事件；祖先去处理其实就是通过事件对象当中的 target 去获取到真正发生事件的子元素；对子元素进行处理；

**例子**

- 当子元素有很多的时候，并且子元素的事件监听里面的逻辑是相同的，最好使用事件委派
  1.  把事件监听不再给子元素，而是给父元素
  2.  当我们对目标元素触发事件的时候，这个事件会冒泡到父元素身上，父元素刚好有事件监听，我们在父元素的事件监听当中
  3.  去获取事件的目标元素，然后处理目标元素；目标元素代表鼠标真正触发事件的那个元素（代表最确切的，最内部的）

```
    var ulNode = document.querySelector('ul');
    ulNode.onmouseover = function(event){
	//event.target就代表的是目标元素节点
		if(event.target.nodeName == 'LI'){//为什么要判断，确保拿到的就是我们所需要的目标元素，不能是ul
			event.target.style.backgroundColor = 'red';
		}else if(event.target.parentNode.nodeName == 'LI'){
			event.target.parentNode.style.backgroundColor = 'red';
		}
	};
    ulNode.onmouseout= function(){
		if(event.target.nodeName == 'LI'){//为什么要判断，确保拿到的就是我们所需要的目标元素，不能是ul
			event.target.style.backgroundColor = 'white';
		}else if(event.target.parentNode.nodeName == 'LI'){
			event.target.parentNode.style.backgroundColor = 'white';
		}
	};
```

- 如果本身我们有一部分 li 后续我们还要动态的去添加一部分，如果这两部分都要具有相同的一些效果，那么此时事件最好是事件委派
  - 事件委派可以让 新的和老的都有效果；
  - 如果没用事件委派，只有老的有，新的没有
  - 以后工作当中，只要碰到了新老一致，用事件就考虑事件委派

**实际运用中**

```
    ulNode.onmouseover = function(e){
	//高级浏览器在调用回调的时候会把事件对象传递给第一个形参
	//低级浏览器在调用回调的时候不会事件对象给第一个形参，而是给了window下的属性叫event
		e = e || window.event;//高级浏览器和低级浏览器兼容写法
		var target = e.target || e.srcElement;//获取目标元素高级和低级浏览器兼容写法；
		if(target.nodeName == 'LI'){
			target.style.backgroundColor = 'red';
		}
	};
	ulNode.onmouseout= function(event){
		event = event || window.event;
		var target = event.target || event.srcElement;
		if(target.nodeName == 'LI'){
			target.style.backgroundColor = 'white';
		}
	};
	btn.onclick = function(){
		var liNode = document.createElement('li');
		liNode.innerHTML = '我是新的';
		ulNode.appendChild(liNode);
				}
```

### 3.两对移入移出事件的区别

- onmouseenter onmouseleave:如果是一个父子元素模型，对父元素添加移入和移出，当鼠标移入父元素里面的子元素的时候， 事件并没有移出然后再移入。也就是说事件元素没有切换；
- onmouseover onmouseout:如果是一个父子元素模型，对父元素添加移入和移出，当鼠标移入父元素里面的子元素的时候，事件会移出然后再移入。也就是说事件元素会有切换；事件委派的时候，必须使用这一对；
- 以后使用移入移出最好都使用 onmouseover onmouseout

## 四、 bom 的五个对象

### 1.window 对象（bom 的顶级对象）

- 等待页面加载完成事件
  > window.onload = function(){}
- 浏览器窗口大小发生改变的事件
  > window.onresize = function(){}
- 获取浏览器视口宽度
  > console.log(document.documentElement.clientWidth);
- 获取浏览器视口高度
  > console.log(document.documentElement.clientHeight);
- 系统滚动事件

  > window.onscroll = function(){console.log('滚');}

### 2.location

window.location 可以让用户获取当前页面地址以及重定向到一个新的页面。window.location.href 可以读也可以写，写的时候相当于转向另外一个页面

### 3.history

window.history 对象包含浏览器的历史记录，window 可以省略。这些历史记录以栈的形式保存。页面前进则入栈，页面返回则出栈。

### 4.navigator

是一个只读对象，它用来描述浏览器本身的信息，包括浏览器的名称、版本、语言、系统平台、用户特性字符串等信息。

### 5.screen

提供了用户显示屏幕的相关属性，比如显示屏幕的宽度、高度，可用宽度、高度。

## 五、 event 对象

### 1.event 概念，作用

系统给我们封装的，任何事件都会有这个 event 对象，就是回调函数的第一个形参；
这个对象当中封装了和这个事件相关的一切信息；

- 键盘事件键码 ：event.keyCode
- 事件委派获取目标元素：event.target

### 2.event 兼容性处理

如果是高级浏览器去调用函数的回调函数，它会把事件对象封装好传给回调函数的第一个形参;
如果是低版本浏览器去调用，它会把事件对象封装好作为 window 的一个属性 window.event;
所以我们在去拿事件对象的时候，要兼容性去拿

> event = event || window.event;

### 3.目标元素节点兼容处理

> event.target || event.srcElement

### 4.三种鼠标位置

- clientX & clientY:拿的是鼠标相对视口的 水平距离和垂直距离 相对的是视口的左上角（以视口左上角为原点）
- pageX pageY :拿的是鼠标相对页面的 水平距离和垂直距离 相对的是页面的左上角（以页面左上角为原点）
- offsetX offsetY:拿的是鼠标相对自身元素的 水平距离和垂直距离 相对的是自身元素左上角（以自身元素左上角为原点）
  鼠标跟随
