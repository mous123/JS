#### 一、移动端事件

​			1、移动端事件的简介

​					ios版Safari为了向开发人员传达一些特殊信息，新增了一些专有事件。因为ios设备既没有鼠标，也没有键盘，所以在为移动Safari开发交互性网页时，常规的鼠标和键盘事件根本不够用。随着Android 中的webkit的加入，很多这样的专有事件变成了事实标准，导致W3C开始制定Touch  Events规范。一下介绍的事件只针对触摸设备，触摸设备也是有鼠标事件的。

​			2、移动端的主要事件

​					2.1、touchstart：当手指触摸屏幕时触发，即使已经有一个手指放在了屏幕上也会触发。

​					2.2、touchmove ：当手指在屏幕上滑动时连续触发。这个事件发生期间，调用preventDefault（）可以阻止滚动。

​					2.3、touchend：当手指从屏幕上移开时触发

​			3、移动端事件的触发对象

​					除了常见的DOM属性外，触摸事件还包含下列三个用于跟踪触摸的属性。

​					3.1、touches：表示当前跟踪的触摸操作的Touch对象的数组。

​					3.2、targetTouches：特定事件目标的 Touch对象的数组

​					3.3、changeTouches：表示自上次触摸以来发生了什么改变的Touch对象的数组

​					**注意：移动端屏幕大多支持多点触控，所以触摸事件的触发对象可能会有多个**

​			4、移动端事件对象的位置属性

​					每个Touch对象包含下列属性

​					4.1、clientX：触摸目标在视口中的X坐标

​					4.2、clientY：触摸目标在视口中的Y坐标

​					4.3、identifier：标识触摸的唯一ID

​					4.4、pageX：触摸目标在页面中的X坐标

​					4.5、pageY：触摸目标在页面中的Y坐标

​					4.6、screenX：触摸目标在屏幕中的X坐标

​					4.7、screenY：触摸目标在屏幕中的Y坐标

​					4.8、target：触摸的DOM节点目标。

​		5、移动端事件的触发顺序

​					touchstart——touchend——mouseover——mousemover（只触发一次）——mousedown——mouseup——click。

​					**手指滑动事件一旦触发，将不会再激活鼠标事件**

#### 二、DOM变动事件

​			1、删除节点事件

​					在使用removeChild()或replaceChide()或remove()从DOM中删除某节点会触发删除节点事件。

![image-20200414123846379](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200414123846379.png)

### 三、文本事件

​			“DOM3 级事件”规范中引入了一个新事件，名叫textInput。 根据规范，当用户在可编辑区域(任意可输入区域)中输入字符时，就会触发这个事件。这个事件与keypress事件 有所不同

​				区别之一就是任何可以获得焦点的元素都可以触发keypress 事件，但只有可编辑区域才能触发textInput事 件。 

​				区别之二是textInput 事件只会在用户按下能够输入实际字符的键时才会被触发，而keypress 事件则在按下那些能够影响文本显示的键时也会触发（例如退格键）。

​				由于textInput 事件主要考虑的是字符， 因此它的event 对象中还包含一个data 属 性，这个属性的值就是用户输入的字符（而 非字符编码）。换句话说，用户在没有按上 档键的情况下按下了S 键，data 的值就 是"s"，而如果在按住上档键时按下该 键，data 的值就是"S"。

#### 四、其他事件对象

​			![image-20200414124028755](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200414124028755.png)



![image-20200414124040706](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200414124040706.png)

​			