

#### 一、DOM的核心概念

​		DOM（文档对象模型）是针对HTML和XML文档的一个API（应用程序编程接口）。DOM描绘了一个层次化的节点树，允许开发人员添加，移除和修改页面的某一部分。

​				节点分为几种不同的类型，每种类型分别表示文 档中不同的信息及（或）标记。每个节点都拥有 各自的特点、数据和方法，另外也与其他节点存 在某种关系。节点之间的关系构成了层次，而所 有页面标记则表现为一个以特定节点为根节点的 树形结构

​				文档节点只有一个子节点，即<html>元素，我 们称之为文档元素。文档元素是文档的最外层 元素，文档中的其他所有元素都包含在文档元 素中。 

​				每个文档只能有一个文档元素。在HTML 页面 中，文档元素始终都是<html>元素

#### 二、DOM的NodeList

​		1、DOM元素的获取方式

​				在JavaScript的世界中，获取元素的方式很多，但是获取的结果却分为两个明显的类别NodeList和HTMLCollection。

​				这两类都属于对象数据类型的一个分支，但是继承的默认方法有所不同

​		2、DOM节点层级之父子层级

​				childNodes：获取子节点（返回的是一个新的NodeList，包含文本节点）

​				parentNode：获取父节点（返回的是父元素本身）

![image-20200330231954584](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200330231954584.png)

​		3、DOM节点层级之兄弟层级

​				Obj.nextSibling：当前节点的同一层级的下一个兄弟节点，如果当前节点已经是最后一个，那么下一个节点则返回null

​				Obj.previousSibling：当前节点的同一层级的上一个兄弟节点，如果当前节点已经是第一个，那么上一个节点则返回null。

​				同一层级只有一个节点，那么该节点的nextSibling和previousSibling都为null。

![image-20200330232353682](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200330232353682.png)

​		4、DOM节点层级之父子层级

​					Obj.firstChild：当前节点的子层级的中的第一个节点

​					Obj.lastChild：当前节点的子层级的中的最后一个节点

​					在只有一个子节点的情况下，firstChild和lastChild的值均为null。

![image-20200330232621941](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200330232621941.png)

​			

​			

​										DOM的层级关系图

![image-20200330232704882](C:\Users\HeartF\AppData\Roaming\Typora\typora-user-images\image-20200330232704882.png)

​		5、DOM的子节点判断     .hasChildNodes

​					{父}.hasChildNodes（   ）

​				如果父节点拥有子节点，返回true；否则返回false

​						比如文本节点，属性节点就没有子节点

​		6、DOM的元素子节点插入appendChild（）

​					{父}.appendChild（  子节点 ）

​					给某父元素内添加一个新的节点，添加的节点位于所有的子节点的最末，此处的子节点可以直接是一个字符串

​		7、DOM的子节点插入insertBefore

​					{父}.insertBefore（ 新增节点，原有子节点  ）

​					给父节点的某一个子节点前添加一个新的子节点，添加的节点位于原有的子节点之前，此处的子节点不可以直接是一个字符串

​		8、DOM的子节点替换replaceChild()

​					{父}.replaceChild（  新增节点，原有子节点  ）

​					给父节点的某一个子节点前添加一个新的子节点，添加的节点位于原有的子节点之前，此处的子节点不可以直接是一个字符串

#### 三、DOM的HTMlCollection

​		1、概念：HTMLCollection内没有文本节点，可以简单的理解为HTMLCollection就是没有文本节点的NodeList（当然有些方法不太一样），所以，HTMLCollection里面的元素也是可以使用NodeList方法的。

​		2、动态集合概念

​				NodeList

​				HTMLCollection

​				这两个集合是动态的，因此只要有新<div>元素被添加到页面中，这个元素也会被添加到该集合中。

#### 四、DOM的操作技术

​		1、DOM的元素遍历

​			childElementCount：返回子元素（不包括文本节点和注释）的个数。  

​			firstElementChild：指向第一个子元素；firstChild 的元素版。  

​			lastElementChild：指向最后一个子元素；lastChild 的元素版。 

​			 previousElementSibling：指向前一个同辈元素；previousSibling 的元素 版。 

​			nextElementSibling：指向后一个同辈元素；nextSibling 的元素版。

​		2、DOM的类名和标签名的获取

​				add(value)：将给定的字符串值添加到列表 中。如果值已经存在，就不添加了。 

   			 contains(value)：表示列表中是否存在给定的 值，如果存在则返回 true，否则返回 false。 

​				remove(value)：从列表中删除给定的字符 串。 		

​				toggle(value)：如果列表中已经存在给定的 值，删除它；如果列表中没有给定的值，添加它。

​		3、DOM的单元素创造

​			document.createElement（“元素的标签名称”）；

​				创走的元素默认是放在内存空间，不会放在网页上显示，如果想让它在网页上显示，那么就要通过DOM方法，把元素假如到网页上来。

​		4、DOM的元素片段创造

​				如果每次创造一个元素就把该元素添加到网页上，那么会造成非常大的网页性能损 耗。 

​				所以我们可以先在内存中建立一个元素片段区域，先把创造的元素添加到这个区域 内，再一次添加进网页中这样的性能会好的多

​				

```javascript
	let	ele=document.querSelector(".nav");
	let eleArea=document.creatDocumentFragment();
	
	for(let i=0;i<10;i++){
        let newEle=document.createElement("ul");
        eleArea.appendChild(newEle);
    }ele.appendChild(eleArea);
```

