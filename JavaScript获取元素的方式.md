# JavaScript获取元素的方式

1、ID获取

  因为一个网页上id只会出现一次，所以我们通过id所获取的元素只有一个，也就是元素本身。**即便网页有多个元素的id名称为同一个那么js也只会选中第一个id名称符合条件的元素**

​    比如 ：var content=document.getElementById（“content”）；

2、class获取

   因为一个网页上class会出现多次，所以我们通过class所获取的元素会有多个，所以此时变量wrap指向的是内存空间里面 的一个数组，数组里面存放了网页上所有的class名称为wrap的元素。 **即便网页上只有一个元素的class名称复合条件，通过js获取到的依然会是一个数组，只是该数组里面的值只有一个而已**

   比如：var wrap=document.getElemByClassName（“wrap”）；

3、标签名获取

​     因为一个网页上同一类标签会出现多次，所以我们通过TagName（标签名）所获取的元素会有多个，所以此时变量wrap指向的是内存空间里面的一个数组，数组里面存放了网页上所有标签名称为div的元素。 **即便网页上只有一个元素的标签名称符合条件，通过js获取到的依然会是一个数组，只是该数组里面的值只有一个而已。**

​    比如：var wrap=document.getElementByTagName（”div“）；

4、name获取

​    因为一个网页上拥有相同的name的值的元素会出 现多次,所以我们通过Name所获取的元素会有多个, 所以此时变量addr指向的是内存空间里面的一个数 组,数组里面存放了网页上所有name名称为指 定name值的元素。 **即便网页上只有一个元素的name名称符合条件,通过js 获取到的依然会是一个数组,只是该数组里面的值只有一 个而已**

   比如：var ip=document.getElementsByName（“addr”）；

以上四种方法呢，是已经过时方法，现在一般用以下两种方法



5、选择器获取

   document.querySelector（“选择器代码”）无论选择器实际选中的是多少，只会选中符合选择器条件的第一个元素，js代码返回的最终是单个元素。

​    比如：var content=document.querySelector（“.content”）；

   document.querySelectorAll(“选择器代码”) 选择器选择中多少就是就是多少, js代码返回的是一个数组, 即便 选择器只选择了一个元素, 返回的也是一个数组。



6、特殊元素获取

​     document.documentElement      获取整个结构文档，html架构

​    document.head      获取我们的头部标签head

​     document.body     获取body标签

​     document.title        获取标题标签

## 元素的自有属性之内容属性

 *ob.innerText=“字符串”*

   **如果元素内容原来就有一些字符内容, 那么原来的内容会被替换成js代码所设置的** 

​    **即便字符串内部有一些元素标签, 这些元素标签也会被当做字符串显示在网页上**

比如：var content=document.querySelector（“.content”）；

​           content.innerText=“一个人”



ob.innerHTML=“字符串”

​      **如果元素内容原来就有一些字符或是元素内容, 那么原来的内容会被替换成js代码所设置的** 

​      **如果innerHTML的内容是一些纯文字, 那么效果如同innerText一样** 

​       **如果innerHTML的内容中包含了一些标签元素, 那么这个标签元素会直接加入到网页中**

  比如：var content=document.querySelector（“.content”）；

​           content.innerHTML=“一个人”

### 元素的自有属性之class名称属性

1、获取class名称

​    var content=document.querySelector（“.content”）；

​     var name=content.className；

2、设置class名称

​    var content=document.querySelector（“.content”）；

​    content.className="hello"；



#### 元素的自有属性之通用获取方法

即便是同一属性,在不同的元素下同样的方式不一定能得到相 同的结果 所以ob.属性的方式并不能得到所有我们需要的元素属性的值 这时我们就要引入一个新的方法 ob.getAttribute(“属性名称”);//get获取 attribute属性

#### 元素的自有属性之通用设置方法

如上述所言, 因为ob.属性名称的方式获取元素属性的方式不一定能都奏效,那么通过该方 式设置元素属性同样也不一定就能奏效,所以我们需要一个通用的设置元素属性的方式 这时我们就要引入一个新的方法 ob.setAttribute(“属性名称”,”属性值”);//set设置 attribute属性   作用就是给ob元素设置一个属性, 属性名称为”属性名称”,属性值为”属性值” 

#### 元素的自有属性之通用删除方法

有些时候我们不再需要某个元素再有啥属性时, 我们可以用js来删除元素的属性, 比如表 单元素的默认被选中,默认禁用这样的功能就是用一个属性来实现的 
删除属性的方式是: ob.removeAttribute(“属性名称”);//删除ob元素的名称为”属性名称”的属性

