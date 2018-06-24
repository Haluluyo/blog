### class 和 id 的使用场景
 **class：**（.class）一个标签可以有多个类且同一个类可以用到不同的标签上，适用于多个元素有共同的样式。
**id：**（#id）一个标签只能有一个id且每个id只能使用一次，能够快速获取标签对象，适用于页面上唯一的元素。
### 常用的CSS选择器
- 基础选择器

|选择器|含义|
|---|---|
|*|通配符选择器，匹配页面任何元素|
|#id|id选择器，匹配特定id的元素|
|.class|类选择器，匹配class包含(不是等于)特定类的元素|
|element|标签选择器|
- 组合选择器

|选择器|含义|
|---|---|
|E,F|多元素选择器，用,分隔，同时匹配元素E或元素F|
|E F|后代选择器，用空格分隔，匹配E元素所有的后代（不只是子元素、子元素向下递归）元素F|
|E>F|子元素选择器，用>分隔，匹配E元素的所有**直接**子元素|
|E+F|直接相邻选择器，匹配E元素**之后**的**相邻**的同级元素F|
|E~F|普通相邻选择器（弟弟选择器），匹配E元素**之后**的同级元素F（无论直接相邻与否）|
|.class1.class2|id和class选择器和选择器连写的时候中间没有分隔符，**.**和 # 本身充当分隔符的元素|
|element#id|id 、class选择器和选择器连写的时候中间没有分隔符，**.**和 #本身充当分隔符的元素|
- 属性选择器

|选择器|含义|
|---|---|
|E[attr]|匹配所有具有属性为attr的元素（div[id]能选择所有具有id属性的div）|
|E[attr=value]|匹配所有属性为value的元素（div[type=text]匹配id=text的div）|
|E[attr~=value]|匹配所有属性attr具有多个空格分隔，其中一个值等于value的元素|
|E[attr ^=value]|匹配属性attr的值以value开头的元素|
|E[attr $=value]|匹配属性attr的值以value结尾的元素|
|E[attr *=value]|匹配属性attr的值包含value的元素|
- 伪类选择器

|选择器|含义|
|---|---|
|a:link |匹配素有未被点击的链接|
|a:visited|匹配所有已经被点击的链接|
|a:hover|匹配鼠标悬停其上的E元素|
|a:active|匹配鼠标点击与释放之间的E元素（对于无href属性的a无作用）|
|E:focus|匹配获得当前焦点的E元素|
|E:enabled|匹配表单中可用的元素|
|Edisabled|匹配表单中禁用的元素|
|E:checked|匹配表单中被选中的radio或checkbox元素|
|E:selection|匹配用户当前选中的元素|
|E:nth-child(n)|匹配其父元素的第n个子元素|
|E:first-child|匹配作为第一个子元素的元素E|
|E:nth-last-child|匹配其父元素的倒数第n个子元素|
|E:last-child|匹配父元素的最后一个子元素，即：nth-last-child(1)|
|E:only-child|匹配其父元素下仅有的一个子元素，即：first-child:last-child或 nth-child(1):nth-last-child(1)|
|E:nth-of-type(n)|匹配其父元素下使用同种标签的第n个子元素|
|E:first-of-type|匹配其父元素下使用同种标签的第一个子元素，即：E:nth-of-type(1)|
|E:nth-last-of-type(n)|匹配其父元素下使用同种标签的倒数第n个子元素|
|E:last-of-type	|匹配父元素下使用同种标签的最后一个子元素，即：E:nth-last-of-type(1)|
|E:only-of-type|匹配父元素下使用同种标签的唯一一个子元素|
|E:root|匹配文档的根元素，对于HTML文档，就是HTML元素|
- 伪元素选择器

|选择器|含义|
|---|---|
|E::before|在E元素之前插入生成的内容|
|E::after|在E元素之后插入生成的内容|
|E::first-line|匹配E元素内容的第一行|
|E::first-letter|匹配E元素内容的第一个字母|

### 选择器的优先级
优先级由**高**到**低**：(注：继承的权值最低)
1. `!important`：在属性后面使用，会覆盖页面内任何位置定义的元素样式
2. 内联样式：作为style属性写在标签上的
3. id选择器
4. class选择器
5. 伪类选择器
6. 属性选择器
7. 标签选择器
8. 通用元素选择器
9. 浏览器自定义

(注：继承的权值最低)

### 如何计算复杂场景的优先级
- id选择器默认优先级最高，其权值为100
- class选择器、属性选择器和伪类选择器的权值为10
- 标签选择器的优先级较低，其权值为1

在比较样式的优先级时，统计选择符中的id、class、标签名个数，然后把对应的权值相加即可。根据结果便可得出优先级高低。
  -  结果较大的优先级较高
  - 结果相同，则后定义的样式优先级较高
  - 如果样式值中含有`!important`，则该值优先级最高

###  a标签的伪类选择器的定义顺序及原因
- 定义的顺序：`a:link{}->a:visited{}->a:hover{}}->a:active{}`
(记忆口诀：LV哈！小仙女们，为了我们的LV；大兄弟们，为了你们老婆的LV，好好学习前端吧~.~)

- 原因：
 *  样式覆盖：优先级相同的选择器，写在后面的会覆盖前面的。
 * 当链接未被点击时，正常状态只有`a:link`有效。
 * 当使用过程中，即鼠标经过链接时，`a:link`和`a:visited`生效，我们需要显示hover，所以`a:hover`在`a:link`后。
 * 当鼠标处于点击与释放链接之间，且链接之前被点击过，`a:visited`，`a:hover`和`a:active`生效，我们需要显示active，所以`a:active`在`a:hover`。
 * visited是已访问过的，如果写在最后，当鼠标悬停在a标签上时，也会有visited属性，所以`a:visited`需要在`a:hover`和`a:active`之前。

### 说明下列选择器的含义
|选择器|含义|
|---|---|
|`#header{}`|id选择器，匹配id="header"的元素|
|`.header{}`|类选择器，匹配class="header"的元素|
|`.header .logo{}`|后代选择器，匹配class="header"的后代元素中class="logo"的元素|
|`.header.mobile{}`|类选择器，匹配class="header mobile"的元素|
|`.header p, .header h3{}`|多元素选择器，匹配class="header"的后代元素中标签为p和h3的元素|
|`#header .nav>li{}`|匹配id="header"的后代元素中class="nav"的直接后代元素中标签为li的元素|
|`#header a:hover{}`|匹配id=''header"的后代元素中的A标签，且事件状态为悬停的样式|
|`#header .logo~p{}`|匹配id="header"的后代元素中，class="logo"的元素之后的标签为p的元素|
|`#header input[type="text"]{}`|匹配id="header"的后代元素中，以type命名属性值为tex的input标签下的元素|

### 简析div:first-child和div:first-of-type

|选择器|作用|举例
|---|---|---|
|`div:first-child`|匹配 div 的父元素下第一个子元素|例1|
|`div:first-of-type`|匹配 div 的父元素下使用同种标签的第一个子元素|例2|
|`div :first-child`|后代选择器，匹配div标签下的所有第一个子元素|例3|
|`div :first-of-type`|后代选择器，匹配div标签下的所有使用同种标签的第一个子元素|例4|

例1：
```
<div><!--整个div都选中--> 
<span>This span is limed!</span> 
<span>This span is not. :(</span> 
</div>```
例2：
```
<div><!--整个div都选中-->
<span>This span is first!</span>
<span>This span is not. :(</span>
<span>what about this <em>nested element</em>?</span>
<strike>This is another type</strike>
<span>Sadly, this one is not...</span>
</div>```
例3：
```
<div>
 <span>This span is limed!</span><!--选中-->
 <span>This span is not. :(</span>
</div>
```
例4：
```
<div>
 <span>This span is first!</span><!--选中-->
 <span>This span is not. :(</span>
 <span>what about this
 <em>nested element</em><!--选中-->
 </span>
 <strike>This is another type</strike><!--选中-->
<span>Sadly, this one is not...</span>
</div>
```

### 运行代码 解析原因

![代码](http://upload-images.jianshu.io/upload_images/6426975-af28cdcdcb562ddb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![输出样式](http://upload-images.jianshu.io/upload_images/6426975-7b6ba18d20beba13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**分析：**
1. `.item1:first-child{}`：匹配 id="item1 "的父元素（即`<div class="ct">`）下第一个子元素，即`<p class="item1">aa</p>`，所以aa显示为红色字体。
2. `.item1:first-of-type{}`：匹配 id="item1 "的父元素（即`<div class="ct">`）下使用同种标签的第一个子元素，即p标签和h3标签各自对应的第一个子元素` <p class="item1">aa</p>`和 ` <h3 class="item1">bb</h3>`，所以aa和bb的背景颜色为蓝色。


