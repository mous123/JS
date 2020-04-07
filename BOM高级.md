#### 一、三种事件类型

​			在浏览器发生的事情统称为事件，比如点击事件，鼠标移动事件，键盘事件，点击事件，请求事件，加载完成事件。面对突发事件，我们都需要用函数处理。

​			函数可以处理事件但是函数摸不着事件的头脑.于是,浏览器出面帮助函数处理事件,浏览器整理了一 下事件触发的一状态,整理成了一个事件对象(也就是事件触发函数传入的ev参数或是window.event). 事 件对象存储了事件触发的各种状态 包括事件触发的主体对象,事件类型,事件触发的位置等等.

​		1、事件绑定

​				Obj.on+事件名称=function(){}

​				1.1、事件绑定同一个对象只能给同一个事件绑定唯一一个事件处理函数。如果绑定第二个，第一个会被清除掉，因为本质上只是给对象的on事件属性上添加了一个函数。

​				1.2、事件绑定函数的this指向挡墙调用事件的主题对象。

​				1.3、在绑定事件之前，事件属性的处理函数默认是null

​				1.4、清除事件的方式只需要将此事件的触发函数该为null

​		2、事件监听

​				Obj.addEventListener("事件名称"，function(){}，布尔值)

​				当事件触发的时候，我们不直接写明处理函数来响应事件。我们叫一个播报员去某个元素那守着，如果触发了某个事件，那就回来通知我，然后我指派函数执行。这种行为类似监听。我们管它叫事件监听

​				2.1、事件监听接受两个参数（三个）第一个是需要监听的事件类型，第二个是事件的触发的回调函数，第三个是是否事件冒泡

​				2.2、事件类型不需要加on+事件类型，直接事件类型即可

​				2.3、一次可以绑定多个事件，相互之间不影响，并且触发顺讯就是绑定顺序

​				2.4、事件监听处理函数的this指向挡墙调用事件的主体对象

​				2.5、取消事件监听用对应的方式，removeEventListener。

​			注意：有名函数是可以直接取消绑定的，但是匿名事件处理函数时么法取消绑定事件的。

​			**匿名事件的取消方式**：

```JavaScript
let dom = document.getElementById("content"),
    count = 0;
const MAXCOUNT=5;

dom.addEventListener("click",fucntion(e){
      	count++;
        console.log('已经点击了'+count+"次.还剩"+(MAXCOUNT-count)+"次")；
		if(count>4){
        	dom.removeEventListener(e.type,argumnents.callee,false);
            consloe.log("不能再点击了")；
        }
})
```

​		

​		3、事件添加的通用方法

```JavaScript
let EventUtil = {
    addHandle:function(el,type,handler){
        if(el.addEventListener){
            el.addEventListener(type,handler)
        }else if(el.attachEvent){
            el.attachEvent("on"+type,handler)
        }else{
            el["on"+type]=handler
        }
    },
    removeHandler:function(el,type,handler){
        if(el.removeEventListener){
            el.removeEventListener(type,handler)
        }else if(el.attachEvent){
            el.deleteEvent("on"+type,handler)
        }else{
            el["on"+type]=null
        }
    }
}
```



​			4、事件委托

​				当我们需要绑定事件的时候, 需要给事件添加绑定或者监听. 当事件触发的时候,我们会对事 件的主体进行操作. 但是如果有大量dom对象需要绑定事件,并且事件的处理函数是同一个的时 候. 这种绑定方式或者监听方式就是很蠢. 并且修改起来也会很麻烦。

​				通过监听公共父元素的形式监听事件。

```JavaScript
let lsit = document.querSelector("ul")
let ali = document.querSelctorAll("li")

functino fn(ev){
    if(ev.target.tagName.toLowerCase()==="li"){
        console.log(ev.target.innerText);
    }
}

list.addEventListener("click",fn)
```

#### 二、UI事件

​		1、 load：当页面完全加载后在window 上面触发，当所有框架都加载完毕时在框架集上面触发，当图像加载 完毕时在<img>元素上面触发，或者当嵌入的内容加载完毕时在<object>元素上面触发。 

​		2、 error：当发生JavaScript 错误时在window 上面触发，当无法加载图像时在<img>元素上面触发，当 无法加载嵌入内容时在<object>元素上面触发，或者当有一或多个框架无法加载时在框架集上面触发

​		3、 select：当用户选择文本框（<input>或<texterea>）中的一或多个字符时触发

​		4、resize：当窗口或框架的大小变化时在window 或框架上面触发

​		5、 scroll：当用户滚动带滚动条的元素中的内容时，在该元素上面触发。<body>元素中包含所加载页面的 滚动条。多数这些事件都与window 对象或表单控件相关。

#### 三、焦点/鼠标/滚轴事件

​		1、焦点事件

​				1.1、blur：在元素失去焦点时触发。这个事件不会冒泡

​				1.2、focus：在元素获得焦点时触发。这个事件不会冒泡

​				1.3、focusin：在元素获得焦点时触发。这个事件与HTML 事件focus 等价，但它冒泡

​				1.4、focusout：在元素失去焦点时触发。这个事件是HTML 事件blur 的通用版本。

​		2、鼠标事件

​				在按下鼠标时键盘上的某些键的状态也可以影响到所要采取的 操作。这些修改键就是Shift、Ctrl、Alt 和Meta（在Windows 键盘中是Windows 键，在苹果机中是Cmd 键），它们经常被用来 修改鼠标事件的行为

​				 DOM 为此规定了4 个属性，表示这些修改键的状 态：shiftKey、ctrlKey、altKey 和metaKey。这些属性中包含 的都是布尔值，如果相应的键被按下了，则值为true，否则值 为false。当某个鼠标事件发生时，通过检测这几个属性就可以确 定用户是否同时按下了其中的键

​			3、滚轴事件

​					当用户通过鼠标滚轮与页面交互、在垂直方向上滚动页面时（无 论向上还是向下, 有些特种鼠标还可以横向滑动），就会触 发mousewheel事件

​					这个事件可以在任何元素上面触发，最终会冒泡到document （IE8）或window（IE9、Opera、Chrome 及Safari）对象

​					多数时间触发的情况下，只要知道鼠标滚轮滚动的方向就 够了，而这通过检测wheelDelta 的正负号就可以确定。 -向下, +向上,  数字时滚动了多少像素(和鼠标的灵敏度 设置有关)

#### 四、键盘事件

​		用户在使用键盘时会触发键盘事件,有3 个键盘事件，简述如下

​			1、 keydown：当用户按下键盘上的任意键时触发，而且如果按住不放的话，会重复触发此事件

​			2、keypress：当用户按下键盘上的字符键时触发，而且如果按住不放的话，会重复触发此事件。 按下Esc 键也会触发这个事件。 

​			3、keyup：当用户释放键盘上的键时触发。

​			如果用户按下的是一个非字符键: 那么首先会触发keydown 事件，然后就是keyup 事件

​				

​			4、键码

​					keyCode属性: 在发生keydown 和keyup 事件 时，event 对象的keyCode 属性中会包含一个代码， 与键盘上一个特定的键对应。对数字字母字符 键，keyCode 属性的值与ASCII 码中对应小写字母或 数字的编码相同。 因此，数字键7 的keyCode 值为55，而字母A 键 的keyCode 值为65——与Shift 键的状态无关

​					code属性: 按键的英文名称

​					key属性:按下的是什么键

​				**键码表**

​					![image-20200408003725880](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200408003725880.png)



![image-20200408003743451](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200408003743451.png)



![image-20200408003804591](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200408003804591.png)