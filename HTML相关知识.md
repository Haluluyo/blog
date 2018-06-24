##  HTML、XML、XHTML 的区别
- html：超文本标记语言（Hyper Text Markup Language），是最早写网页的语言，但是由于时间早，规范不是很好，大小写混写且编码不规范；
- xhtml：升级版的html（Extensible Hyper Text Markup Language），对html进行了规范，编码更加严谨纯洁，也是一种过渡语言，html向xml过渡的语言；
- xml：可扩展标记语言（Extensible Markup Language），是一种跨平台语言，编码更自由，其标签没有被预定义，可以根据自己需求自由创建标签。主要用于存储数据和结构[参考](http://w3school.com.cn/xml/xml_intro.asp)，而非显示数据。
######  总结：XHTML是HTML向XML 过度的一个桥梁。而xml是web发展的趋势。

##  HTML 语义化
- #### what
语义化的含义就是用正确的标签做正确的事情，html语义化就是根据内容的结构化（内容语义化），选择合适的标签（代码语义化），它是Web网页标准化的重要一环，也是标准制定时重要的设计原则。便于对浏览器、搜索引擎解析；在没有样式CCS情况下也以一种文档格式显示，并且是容易阅读的。
- #### how
举例说明
HTML标签语义化HTML5中新增加的很多标签（如：<article>、<nav>、<header>和<footer>等）就是基于这样的设计原则。
![html5-layout](http://upload-images.jianshu.io/upload_images/6426975-7ff90de42a92bbca.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- #### why
1.有利于SEO，有利于搜索引擎爬虫更好的理解我们的网页，从而获取更多的有效信息，提升网页的权重。
2.在没有CSS的时候能够清晰的看出网页的结构，增强可读性。
3.便于团队开发和维护，语义化的HTML可以让开发者更容易的看明白，从而提高团队的效率和协调能力。
4.支持多终端设备的浏览器渲染

## 内容与样式分离的原则
- #### what 
由HTML来管理内容和网页结构 , 文本样式由 CSS来管理，行为操作交给JavaScript来控制。即HTML+CSS+Javascript
- #### how
在实现分离时候保持两个原则即可：
1.html只管结构，不要太复杂，写html时不要管css和js的事儿，只管语义化，简洁化，不要涉及表现的标签、不要把样式写在行内。
2.css表现层和js行为层分别用独自的.css和.js文件来写。写js行为控制样式的时候尽量不要去直接控制css样式，而是通过在结构层html上添加class和id，在css中定义class来是实现。
- #### why
1.使页面载入得更快
2.修改设计时更有效率,方便修改维护和改版重构。
3.有利于搜索优化，更好的被搜索引擎收录

## 常见的meta标签
meta的属性

|属性|值|描述|
|---|---|---|
|content(必需)|some_text|定义与 http-equiv 或 name 属性相关的元信息|
|http-equiv|content-type；expires；refresh；set-cookie|把 content 属性关联到 HTTP 头部。|
|name|author；description；keywords；generator； revised；others|把 content 属性关联到一个名称。|
|scheme|some_text|定义用于翻译 content 属性值的格式|
常见meta举例

|标签|含义|
|---|---|
|<meta charset="utf-8">|声明文档使用的字符编码|
| <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1"/>|声明文档兼容模式，指示IE以目前可用的最高模式显示内容 |
|<meta name="keywords" content="your tags"> |定义针对搜索引擎的关键词 |
|<meta name="description" content="不超过850个字符"> |页面描述，告诉搜索引擎你的站点的主要内容 |
|<meta name="author" content="你的姓名"> |定义网页作者 |
|<meta name="revised" content="David, 2008/8/8/" /> > |定义页面的最新版本 |
|<meta http-equiv="refresh" content="5"/> |5秒刷新一次页面 |
|<meta http-equiv="expires" content="Mon,12 May 2001 00:20:00 GMT"> |用于设定网页的到期时间，一旦过期则必须到服务器上重新调用。需要注意的是必须使用GMT时间格式 |
|<meta http-equiv="pragma" content="no-cache"> |禁用缓存 |
|<meta http-equiv="set-cookie" content="Mon, 12 May 2001 00:20:00 GMT"> |cookie设定，如果网页过期，存盘的cookie将被删除。需要注意的也必须使用GMT时间格式。 |
|<meta name="robots" content="index,follow" /> |搜索引擎索引方式 |
<meta name="robots" content="index,follow" />
all：文件将被检索，且页面上的链接可以被查询；
none：文件将不被检索，且页面上的链接不可以被查询；
index：文件将被检索；
follow：页面上的链接可以被查询；
noindex：文件将不被检索；
nofollow：页面上的链接不可以被查询。

## 文档声明的作用?严格模式和混杂模式指什么?<!doctype html> 的作用?
文档声明是用于告诉浏览器用什么文档类型来解析页面。
严格模式指在文档开头明确申明了文档类型，整个页面只有这一种文档类型。
混杂模式指文档开头不明确申明，由浏览器来自行判断页面的文档类型，可以兼容各类型。
<!doctype html> 的作用是告知浏览器页面是用html5编写的。

## 浏览器乱码的原因及如何解决
- 乱码产生的根本原因
1.保存的编码格式和浏览器解析时的解码格式不匹配导致
2.乱码一般是英文以外的字符才会出现
- 解决办法
1.设置<meta charset>标签声明文档使用的字符编码
2.设置正确的字符编码
3.设置浏览器显示正确的编码
如果浏览器浏览时候出现网页乱码，在浏览器中找到转换编码的菜单调整。
 IE9浏览器：在需要转码的网页空白出右键鼠标，选择“编码”。
 傲游浏览器：在需要转码的网页时，菜单“查看”-->“编码”即可选择转换编码。
谷歌浏览器：在需要转码的网页时，点击右上角“三横”图标选择“工具”-->“编码”即可选择切换网页编码。

## 常见的浏览器有哪些？什么内核？
chrome、Safari、360极速浏览器以及搜狗浏览器高速模式使用WebKit内核
IE、猎豹、360、搜狗、傲游、世界之窗、Avant、腾讯TT使用Trident内核，又称为IE内核。
Firefox、Netscape6至9使用Gecko内核。
Chrome（28及往后版本）、Opera（15及往后版本）和Yandex浏览器中使用Blink内核。

## HTML常见的标签及应用
|标签 |应用 |
|---|---|
|`<html>`...`</html>`|根标签，描述网页|
|`<head>`...`</head>`|文档的头部，描述了文档的各种属性和信息，包括文档的标题等|
|`<title>`...`</title>` |标签之间的文字内容是网页的标题信息，它会出现在浏览器的标题栏中 |
|`<meta />`|提供有关页面的元信息，其属性定义了与文档相关联的名称/值对|
|`<body>`...`</body>` |定义文档的主体，包含文档的所有内容(如文本、超链接、图像、表格和列表等) |
|`<h1>`-`<h6>`|文章的标题，一共有6个并且依据重要性递减。`<h1>`是最高的等级|
|`<p>`..`.</p>` |文章的段落 |
| `<div>`...`</div>` |定义 HTML 文档中的一个分隔区块或者一个区域部分，常用于组合块级元素，以便通过 CSS 来对这些元素进行格式化 |
|`<a>`...`</a>` |定义超链接 ，`<a href="#">`|
|`<img />` (xhtml1.0 )|给网页插入图片，src属性为图片地址，alt属性是当图片未加载成功时的文字提示|
|`<span>`...`</span>` |行内分区元素，最简单的inline元素；常用于为元素分组、页面布局 |
|`<br />`(xhtml1.0 ) |换行 |
|`<ul>`...`</ul>`  |定义无序列表， 每项前都自带一个圆点，与li标签配合使用|
|`<ol>`...`</ol>`  |定义有序列表.，列表排序以数字来显示，与li标签配合使用  |
|`<li>`...`</li>`  |定义列表项目 |
|`<table>`...`</table>`  |定义 HTML 表格 |
| `<tr>`...`</tr>` |定义表格行，有几对tr 表格就有几行 |
| `<th>`...`</th>` |定义表格的头部的一个单元格，表格表 |
| `<td>`...`</td>` |定义表格单元，一行中包含几对td就说明一行中就有几列。 |
| `<form>`...`</form>` |用于创建供用户输入的 HTML 表单 |
| `<label>`...`</label>` |为 input 元素定义标注（标记）,当用户单击选中该label标签时，浏览器就会自动将焦点转到和标签相关的表单控件上 |
| `<input />` (xhtml1.0) |规定用户可以在其中输入数据的输入字段，用来声明允许用户输入数据的 input 控件|
| `<hr />`(xhtml1.0) | 水平分隔横线，默认样式线条比较粗，颜色为灰色|
|`&nbsp`|空格|
|`<!--xxx-->`|代码注释,代码的用途、程序的功能的说明，不显示在网页上|




##### 参考资料：
 [前端基础知识](http://www.jianshu.com/p/71be45c9e8f8)
[HTML 5的革新——语义化标签](http://www.html5jscss.com/html5-semantics-section.html)
[HTML知识点](http://www.jianshu.com/p/48259c04d0f7)
