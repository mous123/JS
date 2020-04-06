#### 一、什么是BOM

​			BOM的核心对象是window，它表示浏览器的一个实例。在浏览器中，window对象有双重角色，它既是通过JavaScript访问浏览器窗口的一个接口，又是ECMScript规定的Global（全局）对象。

​			这意味着网页中定义的任何一个对象、变量个函数，都以window作为其Global对象，因此有权访问parseInt()等方法。

​			1、全局作用域

​					

```JavaScript
var age = 29；
function sayAge(){
    alert(this.age);
}
alert(window.age);
asyAge();
window.sayAge();
```

我们在全局作用域中定义了一个变量age 和一个函数sayAge()， 它们被自动归在了window 对象名下。于是，可以通 过window.age 访问变量age，可以通过window.sayAge()访问函 数sayAge()。由于sayAge()存在于全局作用域中，因 此this.age 被映射到window.age，最终显示的仍然是正确的结 果。 

```JavaScript
var age = 29；
window.color= "red";
delete window.age;//返回false
delete window.color;//返回false
alert(window.age);
alert(window/color);
```

抛开全局变量会成为window 对象的属性不谈，定义全局变量 与在window 对象上直接定义属性还是有一点差别： 全局变量不能通过delete 操作符删除，而直接在window 对象 上的定义的属性可以

**需要注意的是：let指令创造的变量不会挂在window对象名下**

#### 二、浏览器窗口设置

​		1、浏览器窗口大小获取

​				浏览器软件界面可视区域大小

​				1.1、window.outerWidth

​				1.2、window.outerHeight

​		2、浏览器窗口位置获取

​					2.1、window.screenTop/window.screenY

​					2.2、window.screenLeft/window.screenX

​					window.moveTo()接受的是新位置的x和y的坐标值

​					window.moveBy()接受的是在水平方向和垂直方向上移动的像素数；**这个方法现在的谷歌浏览器是禁用的。**

​		3、打开窗口window.open()

​						window.open(url，target，attr，boolean)；

​			3.1、url是想要打开的网页的网址

​			3.2、target是目标地址，是想在哪里打开这个网页，参数可以是：_self、blank等

​			3.3、第三个是新窗口特性

​					![image-20200407015934324](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200407015934324.png)

​			4、关闭窗口window.close()

​					浏览器主窗口目前绝大多数浏览器是不允许用户通过js来关闭的, 只有用户自己创造的小窗口才可以用window.close关 闭

#### 三、location对象

​			1、location对象

​					location是最有用的BOM对象之一，它提供了当前窗口中加载的文档有关的信息，还提供了一些导航功能。

​					事实上，location对象是很特别的一个对象，因为它既是window对象的属性，也是document对象的属性：换句话说，window.location和document.location引用的是同一个对象。

![image-20200407020346812](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200407020346812.png)

​		2、location对象的字符串参数查询

​				

```JavaScript
function getSearchMsg(){
    if(location.search.length > 0){
        let qs = location.search,//获取当前网页的参数
            items = qs.split("&"),//将搜索参数的每一组参数都独立成一个数组的数组项目
            args = {},//存储后期经过信息转码后的,参数名/参数值
            item = null,//预存中间数据的临时数组
            name,//预存中间数据的参数名称
            value;//预存中间数据的参数值
        for(let i = 0;i < items.length:i++){
			item = items[i].split("=");//将每一组参数再次分割
            name = window.decodeURIComponent(item[0]);//获得每一组参数的参数名称,并将名称进行转码
            value = window.decodeURIComponet(item[1]);//获得每一组参数的值,并进行转码
            args[name] = value;//将得到的转码后的参数名称和值存储在对象中
        }
         return args;   
    }
}
```

​				通过上面的属性可以访问到location 对象的大多数信息，但其中访问URL 包含的查询字符串的属性并不 方便。尽管location.search 返回从问号到URL 末尾的所有内容，但却没有办法逐个访问其中的每个查 询字符串参数。为此，可以像下面这样创建一个函数，用以解析查询字符串，然后返回包含所有参数的一 个对象

#### 四、时间冒泡和时间捕捉

​			1、时间冒泡

​					时间冒泡（event   bubbling），即事件开始时有最具体的元素（文档中嵌套层次最深的那个节点）接受，然后逐级向上传播到较为不具体的节点。

​					如果你单击了页面中的<div>元素，那么这个click 事件 会按照如下顺序传播： 

​					(1) <div>被点击

​					 (2) <body>被点击 

​					(3) <html>被点击 

​					(4) document被点击

​		2、事件捕获

​				事件捕获的思想是不太具体的节点应该更早接受到事件，而最具体的节点应该最后接受到事件。事件捕获的用意在于事件达到预定目标之前捕获它。

​				仍以前面的HTML 页面作为演示事件捕获的例 子，那么单击<div>元素就会以下列顺序触 发click 事件。

​				（1） document

​				（2）<html>

​				 （3）<body>

​				（4）<div>

​		3、事件监听方法

​					element.addEventListener(event,  function(){  }, boolean);

​					第一个参数是事件的类型（如 click，mousedown等等）

​					第二个参数是事件触发后调用的函数

​					第三个参数是个布尔值。默认是false（冒泡阶段执行函数），true（捕获阶段产生）