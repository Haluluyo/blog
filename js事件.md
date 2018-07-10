###### 1.  DOM0事件和DOM2级在事件监听使用方式上有什么区别？
- 添加方式：DOM0级事件是通过内联方式```<div onclick="console.log()"></div>```,或是在JS中写```onlicke=function(){}```函数；DOM2级事件通过```addEventListener```来填加事件监听,接受三个参数,事件类型,事件处理方法,布尔值(true表示事件捕获阶段响应，false表示事件冒泡阶段响应,默认false)```btn.addEventListener("click",function(){}，false)```。
- 删除事件：删除DOM0事件处理程序是将对应事件属性置为null，```btnClick.onclick = null```；DOM2级事件通过```removeEventListener```删除事件的监听，```btn.removeEventListener('click', function(){}, false);```，但不能移除匿名函数。
- 多个事件处理程序：DOM0事件不支持，会出现后面的覆盖前面的这种情况，只能一个事件处理程序对应一个处理函数；DOM2级事件处理程序可以添加多个事件处理程序。
- ```this```：DOM0级事件中```this```对象指向全局对象；DOM2级事件```this```指向Element节点
- DOM0级事件只能在冒泡阶段进行监听器触发；DOM2级事件可以选择在捕获阶段还是冒泡阶段进行监听器触发。
- 兼容性：DOM0级事件兼容所有浏览器；DOM2级事件要求浏览器为IE8以上
```
<!DOCTTYPE HTML>
<html>
  <head>
    <title>test</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>
    <div class="container">
      <button id="btn01" type="button">点我1 我是DOM0级</button>
      <button id="btn02" type="button" onclick="console.log(btn02Click)">点我2 我是DOM0级(内联式)</button>
      <button id="btn2" type="button">点我 我是DOM2级</button>
    </div>
    <script>
      var btn01Click = document.querySelector("#btn01")
      var btn02Click = document.querySelector("#btn02")  
      var btn2Click = document.querySelector("#btn2")
      btn01Click.onclick = function(){
        console.log(btn01Click)
      }
      btn2Click.addEventListener('click',function(){
        console.log(btn2Click)
      },false);
    </script>
  </body>
</html
```
![进阶8-1测试.jpg](http://upload-images.jianshu.io/upload_images/6426975-5f478e1c57ddd95a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 2. attachEvent与addEventListener的区别？
- 参数：attachEvent有2个参数(事件名称和方法),```btn.attachEvent("onclick",function(){})```，attachEvent添加的事件处理程序只能发生在冒泡阶段；addEventListener有3个参数(事件名称、方法和布尔值),```btn.addEventListener("click",function(){},false)```，布尔值默认false,false指冒泡阶段触发事件，ture指捕获阶段触发函数。
- this：作用域不相同，attachEvent事件处理程序会在全局变量内运行，this指window；而addEventListener的作用域是元素本身，this是指的触发元素。
- 执行顺序：为一个事件添加多个事件处理程序时，执行顺序不同，attachEvent添加多个事件处理程序时顺序无规律(添加的方法少的时候大多是按添加顺序的反顺序执行的，但是添加的多了就无规律了)；addEventListener添加会按照添加顺序执行。
```
<!DOCTTYPE HTML>
<html>
  <head>
    <title>test</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>
    <div class="container">
      <button id="btn1" type="button">点我 attachEvent</button>  
      <button id="btn2" type="button">点我 addEventListener</button>
    </div>
    <script type="text/javascript">
      var btn1Click = document.querySelector("#btn1")
      var btn2Click = document.querySelector("#btn2")
      var handler = function(){
        console.log(btn1Click)
        console.log(this.id);
      }
      btn1Click.attachEvent('click',handler)    //只有IE6-10支持
      btn2Click.addEventListener('click',function(){
        console.log(btn2Click)
        console.log(this.id);
      },false);
    </script>
  </body>
</html>
```
###### 3. 解释IE事件冒泡和DOM2事件传播机制？
- IE事件冒泡：传播顺序是由里到外，即事件开始时由最具体的元素，文档中嵌套最深的那个节点接收，然后逐级向上传播到window（document）
![事件冒泡.png](http://upload-images.jianshu.io/upload_images/6426975-d3d7765b774abe40.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- DOM2事件传播机制分为三个阶段：
  - 事件捕获阶段，即由最顶层元素（一般是从window元素开始，有的浏览器是从document开始，至于其中的差别我稍后会更新）开始，逐次进入dom内部，最后到达目标元素，依次执行绑定在其上的事件
  - 处于目标阶段，检测机制到达目标元素，按事件注册顺序执行绑定在目标元素上的事件。
  - 事件冒泡阶段，从目标元素出发，向外层元素冒泡，最后到达顶层（window或document），依次执行绑定再其上的事件。
![DOM2级事件.png](http://upload-images.jianshu.io/upload_images/6426975-bd2ef70111526d09.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 4. 如何阻止事件冒泡？ 如何阻止默认事件？
- 阻止事件冒泡:
  - DOM：```e.stopPropagation();```
  - IE：```e.cancelBubble = true```
```
function stopPropagation(e) {
  if (e.stopPropagation)
      e.stopPropagation();
  else
      e.cancelBubble = true;
}
```
- 阻止默认事件:
  - DOM：```event.preventDefault();```
  - IE： ```event.returnValue = false;```（该属性默认为true）
```
function preventDefault(e) {
  if (e.preventDefault)
      e.preventDefault();
  else
      e.returnValue = false;
}
```
###### 5. 有如下代码，要求当点击每一个元素li时控制台展示该元素的文本内容。不考虑兼容
```
<ul class="ct">
    <li>这里是</li>
    <li>饥人谷</li>
    <li>前端6班</li>
</ul>
<script>
//todo ...
  var liNode = document.querySelector(".ct");
  liNode.addEventListener("click",function(e){
    console.log(e.target.innerText);
  },false);
</script>
```
![进阶9-5测试.png](http://upload-images.jianshu.io/upload_images/6426975-bec07636eefb8a4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 6. 补全代码，要求：

当点击按钮开头添加时在<li>这里是</li>元素前添加一个新元素，内容为用户输入的非空字符串；当点击结尾添加时在最后一个 li 元素后添加用户输入的非空字符串.
当点击每一个元素li时控制台展示该元素的文本内容。
```
<ul class="ct">
    <li>这里是</li>
    <li>饥人谷</li>
    <li>任务班</li>
</ul>
<input class="ipt-add-content" placeholder="添加内容"/>
<button id="btn-add-start">开头添加</button>
<button id="btn-add-end">结尾添加</button>
<script>
//你的代码
  function $(id){
    return document.querySelector(id);
  }
  $(".ct").addEventListener("click",function(e){
    if(e.target.tagName.toLowerCase()==="li"){
      console.log(e.target.innerText);
    }
  },false);
  $("#btn-add-start").addEventListener("click",function(){ 
    var newNode = document.createElement("li");
    var newLi = $(".ipt-add-content").value;
    if(newLi!==""){
      newNode.innerText = newLi;
      $(".ct").insertBefore(newNode,$(".ct").firstChild);
    }else{
      console.log('所输入内容不能为空！')
    }
  },false)
  $("#btn-add-end").addEventListener("click",function(){
    var newNode = document.createElement("li");
    var newLi = $(".ipt-add-content").value;
    if(newLi!==""){
      newNode.innerText = newLi;
      $(".ct").appendChild(newNode)
    }else{
      console.log('所输入内容不能为空！')
    }
  },false)
</script>
```
![进阶9-6测试.png](http://upload-images.jianshu.io/upload_images/6426975-335ff21bc1fd2a53.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 7. 补全代码，要求：当鼠标放置在li元素上，会在img-preview里展示当前li元素的data-img对应的图片。
```
<ul class="ct">
    <li data-img="http://upload-images.jianshu.io/upload_images/6426975-9e2ffa119078ee9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240">鼠标放置查看图片1</li>
    <li data-img="http://upload-images.jianshu.io/upload_images/6426975-6696359c8995ac03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240">鼠标放置查看图片2</li>
    <li data-img="http://upload-images.jianshu.io/upload_images/6426975-a6f6d9e2f8e6e123.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240">鼠标放置查看图片3</li>
</ul>
<div class="img-preview"></div>
<script>
//你的代码
  function $(cls){
    return document.querySelector(cls);
  }
  var newImg=document.createElement("img")
  $(".ct").addEventListener("mouseover",function(e){
    if(e.target.tagName.toLowerCase()==="li"){
      newImg.src = e.target.getAttribute('data-img');
      $(".img-preview").appendChild(newImg)
    }
  },false)
  $(".ct").addEventListener("mouseout",function(){
    $(".img-preview").removeChild(newImg);
  },false);
</script>
```
![进阶9-7测试.png](http://upload-images.jianshu.io/upload_images/6426975-c13c0c47c7a416f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 8. 写一篇博客，讲解事件相关知识点，如事件冒泡、捕获、代理、兼容写法等(选做题目)
