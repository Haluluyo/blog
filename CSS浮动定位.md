##### 浮动元素有什么特征？对父容器、其他浮动元素、普通元素、文字分别有什么影响?
- 特征：
 * 浮动元素会脱离正常的文档流，元素将不在页面占用空间，按照其外边距指定的位置相对于它的上一个块级元素（或父元素）显示；
 * 浮动元素后面的块级元素的内容会向此浮动元素的外边距靠齐，但文档普通流中的块框感知不到浮动框的存在；
 * 浮动元素后面的内联元素会向此浮动元素的外边距靠齐。
- 影响：
 * 对于父容器：元素浮动之后，它脱离当前正常的文档流，因而无法撑开其父元素，造成父元素的塌陷。
 * 对于其它浮动元素：
同一个方向的浮动元素，像行内元素的样式一样水平排列，空间不够时会自动转到下一行，但如果高度设置存在问题，那么多个浮动元素水平排列会存在“卡住”的情况；
反方向的浮动元素，互不影响，位于同一条水平线上，当空间不够时会被挤下。
 * 对于普通元素：若为块级元素，该元素会忽视浮动元素的而占据它的位置，且元素会处在浮动元素的下层（无法通过z-index属性改变他们的层叠位置），但它的内部文字和其他行内元素都会环绕浮动元素。
 * 对于文字：环绕浮动元素排列。


##### 清除浮动指什么? 如何清除浮动? 两种以上方法
- What
解决父容器高度塌陷问题（CSS背景不能显示、边框不能随内容而被撑开）；解决margin padding设置值不能正确显示问题（特别是margin-top、margin-bottom、padding-top、padding-bottom）
- How
 1.  **clear**  
在浮动元素末尾加新的空标签，给其设置属性**clear：both**
```
html:
<div class="ct">
   <div class="box" id="box1"></div>
   <div class="box" id="box2"></div>
   <div class="box" id="box3"></div>
   <div class="empty"></div>
 </div>
```
```
css:
.ct {
      border: 3px solid #000;
      width: 300px;
}
.box {
  width: 100px;
  height: 100px;
  float: left;
}
#box1 {
  background: red;
}
#box2 {
  background: green;
}
#box3 {
  background: blue;
}
.empty {
  clear: both;
}
```
![clear示例](http://upload-images.jianshu.io/upload_images/6426975-e45df1c085870242.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. **BFC**(块级格式化上下文)
后面详细说~
 3. **：after**
作用于浮动元素的父容器，加**class="clearfix"**，目前通用的清理浮动的方法
```
方法1：
.clearfix {
        *zoom: 1;/*页面缩放为1，可触发IE6 7 的layout特性，实现类似BFC的作用*/
}
.clearfix:after {
        content: " ";
        display: block;
        clear: left;
}
```
```
方法2：
.clearfix {
       *zoom: 1;
}
.clearfix:after {
       content: " ";
       display: table;
       clear: both;
}
```

##### 有几种定位方式，分别是如何实现定位的，参考点是什么，使用场景是什么？
|属性值|描述|
|---|---|
|static|默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。|
|relative|生成相对定位的元素，相对于其正常位置进行定位。|
|absolute|生成绝对定位的元素，相对于 **static 定位以外的第一个父元素**进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。|
|fixed|生成绝对定位的元素，相对于**浏览器窗口**进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。|
-  **static**：文档默认的定位方式，即在文档的普通流中。
```
html:
<div class="ct">
   <div class="box" id="box1"></div>
   <div class="box" id="box2"></div>
   <div class="box" id="box3"></div>
   <div class="empty"></div>
 </div>
```
```
css:
.ct {
    border: 3px solid #000;
    width: 200px;
}
.box {
  width: 100px;
  height: 100px;
}
#box1 {
  background: red;
}
#box2 {
  background: green;
}
#box3 {
  background: blue;
}
.empty {
  clear: both;
}
```
![普通流](http://upload-images.jianshu.io/upload_images/6426975-0fa2dabf3fd625a5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-  **relative**：相对定位，以其自身作为定位的基准，做一定量的偏移，但是会保留偏移前所占用的文档流。**参考点**：元素本身
```
css:
.ct {
    border: 3px solid #000;
    width: 200px;
}
.box {
  width: 100px;
  height: 100px;
}
#box1 {
  background: red;
}
#box2 {
  background: green;
  position: relative;
  top: 20px;
  left: 20px;
}
#box3 {
  background: blue;
}
.empty {
  clear: both;
}
```
![相对定位](http://upload-images.jianshu.io/upload_images/6426975-d83b4093fdbb5761.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-  **absolute**：绝对定位，这种定位方式会使被定位的元素脱离文档流。**参考点**：相对于距离最近的非static祖先元素位置决定，若没有则相对于包含块html来定位。
```
css:
.ct {
    border: 3px solid #000;
    width: 200px;
}
.box {
  width: 100px;
  height: 100px;
}
#box1 {
  background: red;
}
#box2 {
  background: green;
  position: absolute;
  top: 20px; 
  left: 20px;
}
#box3 {
  background: blue;
}
.empty {
  clear: both;
}
```
![绝对定位](http://upload-images.jianshu.io/upload_images/6426975-cde8a906029bd707.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
-  **fixed**：固定定位，这种定位方式也让元素脱离文档流。**参考点**：浏览器窗口
```
css:
.ct {
    border: 3px solid #000;
    width: 200px;
   margin: 100px;/*区别position：absolute*/
}
.box {
  width: 100px;
  height: 100px;
}
#box1 {
  background: red;
}
#box2 {
  background: green;
  position: fixed;/*位置不随滚动条的改变而变*/
  top: 20px; 
  left: 20px;
}
#box3 {
  background: blue;
}
.empty {
  clear: both;
}
```
![固定定位](http://upload-images.jianshu.io/upload_images/6426975-5938a15396c8b391.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### z-index 有什么作用? 如何使用?
- 作用
z-index属性的作用是设置元素的堆叠顺序。它决定了一个HTML元素的层叠级别。z-index值较大的元素将叠加在z-index值较小的元素之上。对于未指定此属性的定位对象，z-index 值为正数的对象会在其之上，而 z-index 值为负数的对象在其之下。
- 使用
z-index仅在设置了position非static属性的元素生效，且z-index的值只能在兄弟元素之间比较。z-index默认值为auto,则不建立层叠上下文。设置为0则会建立层叠上下文。

##### position:relative和负margin都可以使元素位置发生偏移?二者有什么区别
- position:relative：可以使元素位置发生偏移，在文档流中仍然占据着原来的位置，所以**其他元素的位置不会发生变化**
- margin：可以使元素位置发生偏移，放弃偏移前占据的空间，连同后面的元素一起偏移，所以**其他元素的位置发生了变化**
```
<div class="ct ct1">
   <div class="box" id="box1">position:relative</div>
   <div class="box" id="box2">position:relative</div>
   <div class="box" id="box3">position:relative</div>
   <div class="empty"></div>
 </div>
 <div class="ct ct2">
   <div class="box" id="box4">margin</div>
   <div class="box" id="box5">margin</div>
   <div class="box" id="box6">margin</div>
   <div class="empty"></div>
</div>
```
```
.ct {
    border: 3px solid #000;
    width: 200px;
    float: left;
}
.box {
  width: 100px;
  height: 100px;
}
#box1 {
  background: red;
}
#box2 {
  background: green;
  position: relative;
  top: 20px; 
  left: 20px;
}
#box3 {
  background: blue;
}
#box4 {
  background: red;
}
#box5 {
  background: green;
  margin-top: 20px;
}
#box6 {
  background: blue;
}
```
![relative和margin对比](http://upload-images.jianshu.io/upload_images/6426975-0004a9970584f88c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### BFC 是什么？如何生成 BFC？BFC 有什么作用？举例说明
- What
Block formatting context，块级格式化上下文。是一种布局方式，它决定了元素如何对其内容进行定位，以及与其他元素的关系和相互作用。
- How
 * 设置```position: absolute或fixed```(局限性：会改变元素的定位方式) 
 * 设置```float: left或right``` (局限性：虽然解决了父容器塌陷问题，但爷爷容器就该塌了=.=)
 * 设置```display: inline-block或table-cell或table-caption```(局限性：浏览器兼容问题，低版本IE不支持inline-block)
 * 设置 ```overflow: auto或hidden或scroll ```(局限性：影响绝对定位的元素和滚动条)
- Why
 * 阻止外边距折叠 （下一个问题详细说）
 * 不会被浮动元素重叠：div浮动兄弟遮盖问题：由于左侧块级元素发生了浮动，所以和右侧未发生浮动的块级元素不在同一层内，所以会发生div遮挡问题。（2栏布局）
```
HTML
<body>
 <div class="ct">
  <div class="aside">
     <h4>举例：浮动元素覆盖</h4>
     <p>我是左边栏的内容</p>
  </div>
  <div class="content">
    <h4>举例：浮动元素覆盖</h4>
    <p>我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容我是右边栏的内容</p>
  </div>
 </div>
</body>
```
```
CSS
.ct {
  border: 1px solid;
}
.aside {
  width: 160px;
  height: 100px;
  border: 1px solid;
  background: red;
  float:left;
}
.content {
  margin-left: 180px;//文字不会围绕浮动元素
}
```
![未加BFC.png](http://upload-images.jianshu.io/upload_images/6426975-df1f5347d7fc716e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![加BFC](http://upload-images.jianshu.io/upload_images/6426975-61415618382ad2aa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 * 包含浮动元素：解决高度塌陷问题
```
HTML
<body>
 <div class="ct">
   <div class="box1">
     举例：包含浮动元素
   </div>
   <div class="box2">
     举例：包含浮动元素
   </div>
 </div>
</body>
```
```
CSS
.ct {
  background: red;
  float: left; //包含浮动元素
}
.box1,.box2 {
  width: 150px;
  height: 150px;
  border: 1px solid;
  float: left;
}
```
![未给父元素加BFC.png](http://upload-images.jianshu.io/upload_images/6426975-4de6209ab204ea4f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![给父元素加BFC.png](http://upload-images.jianshu.io/upload_images/6426975-e655bbaab91ef399.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 在什么场景下会出现外边距合并？如何合并？如何不让相邻元素外边距合并？给个父子外边距合并的范例
- What
同属一个BFC中的元素（包括相邻元素和嵌套元素），若它们之间没有阻挡（例如边框、非空内容、padding等）会发生垂直margin重叠（文档流中块级标签之间竖直方向的margin会以大的为准）。
- How
让发生margin重叠的元素不在同一个BFC内即可清除浮动，嵌套元素适用，将父元素设置为BFC，则子元素的margin不与父元素的重叠。
**合并规则**：
 1.  两个margin都是正值的时候，取两者的最大值；
 2. 当 margin 都是负值的时候，取的是其中绝对值较大的，然后，从0位置，负向位移；
 3. 当有正有负的时候，先取出负 margin 中绝对值中最大的，然后，和正 margin 值中最大的 margin 相加。
 4. 所有毗邻的margin要一起参与运算，不能分步进行。
- Example 
```
HTML
<body>
 <div class="box">
   <div class="content">
     举例：垂直外边距折叠
   </div>
 </div>
</body>
```
```
CSS
.box {
  width: 150px;
  height: 140px;
  border: 1pxsolid;
  background: red;
  overflow: hidden;//清除浮动
}
.content {
  background: yellow;
  margin: 40px;
}
```

![未加overflow，margin无效](http://upload-images.jianshu.io/upload_images/6426975-19e9cbbc2a82b22a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![加overflow.png](http://upload-images.jianshu.io/upload_images/6426975-a3da06c606e29328.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


[alert效果](http://js.jirengu.com/gejuvuduju/1/edit?html,css,output)
[表单效果](http://js.jirengu.com/daritenola/1/edit?html,css,output)
[模态框效果](http://js.jirengu.com/fonukevazu/1/edit?html,css,output)
[导航栏效果](http://js.jirengu.com/gidutopexe/1/edit?html,css,output)
- **收获**：
 1. 组合选择器： .box input[type=text]

 2. 删除表单文本输入框的边框和轮廓
```
.box input[type=text],
.box textarea {
      border: none;
      display: block;
      border-bottom: 1px solid #808080;
}
.box input[type=text]:focus,
.box textarea:focus {
      outline: none;
}
```

###### 参考资料
[浅析BFC及其作用](http://blog.csdn.net/riddle1981/article/details/52126522)
[BFC神奇背后的原理](http://blog.sina.com.cn/s/blog_a034e55f0102ww4q.html)
[CSS中zoom:1的作用 ，小标签大作用](http://blog.sina.com.cn/s/blog_a034e55f0102wvib.html)
