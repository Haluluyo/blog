### form的简介
表单是可以搜集不同类型的用户输入，并通过浏览器将这些数据传送到服务器端，实现网站与用户之间的信息交互。
###form的属性
- action：指定表单数据提交到哪个地址进行处理
- method：指明提交表单的HTTP方法，取值为get或post
- target：在何处打开action，与`<a>`标签的target属性用法类似。
- enctype（编码方式）：
 1. application/x-www-form-urlencoded：在发送前编码所有字符（默认）
 2. text/plain：空格转换为 "+" 加号，但不对特殊字符编码
 3. multipart/form-data：使用包含文件上传控件的表单时，必须使用该值

eg.`<form action="xxxx" method="post/get">.....</form>`

### 常用标签
|input标签|作用|
|---|---|
|`<input type="text" >` |文本输入框，单行，默认宽度为20个字符 |
|`<input type="password" >` |密码输入框，输入内容自动转变成圆点|
|`<input type="radio" >` |单选框，用name分组要一致，一定要加value值|
|`<input type="checkbox" >` |复选框，用name分组要一致，一定要加value值|
|`<input type="file" >` |文件上传，accept属性值可限制上传文件类型 |
|`<input type="hidden" >` |隐藏字段，后台可根据name、value值判断用户提交的表单数据是否安全|
|`<input type="button" >` |定义按钮|
|`<input type="submit" >` |定义提交表单数据至表单处理程序的按钮|
|`<input type="reset" >` |定义重置按钮|
|`<input type="image" >` |定义图像形式的提交按钮|
eg.
```
<form  method="post" action="save.php">
  <div class="username">
    <label> 账户: </label>
    <input type="text" name="myname" >
  </div>
  <div class="password">
    <label> 密码: </label>
    <input type="password" name="pass">
  </div> 
  <div>
    <input class="submit" type="submit"  value="提交">
    <input class="reset" type="reset"  value="重置">
  </div>
  <div class="sex">
    <label> 性别: </label>
    <input type="radio" name="sex" value="boy">男
    <input type="radio" name="sex" value="girl">女
  </div>
  <div class="hobby">
    <label> 爱好: </label>
    <input type="checkbox" name="hobby" value="read">读书
    <input type="checkbox" name="hobby" value="run">跑步
    <input type="checkbox" name="hobby" value="sing">唱歌
    <input type="checkbox" name="hobby" value="dance">跳舞
  </div>
  <div class="file">
    <label> 设置头像: </label>
    <input type="file" name="myfile" accept="image/png">
    <!--accept属性限制上传文件的类型-->
  </div>
</form> 
```
显示效果：

![input.png](http://upload-images.jianshu.io/upload_images/6426975-3d04d202b908a3fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- textarea标签：多行文本输入
 ```
<div class="textarea">
     <textarea name="article" rows="10" cols="40">在这里输入内容...
     </textarea>
     <!--cols：多行输入域的列数；rows：多行输入域的行数-->
 </div>
```
显示效果：
![textarea.png](http://upload-images.jianshu.io/upload_images/6426975-b4b2b7189331f666.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- select标签：下拉菜单
```
<div class="select">
  职业：
   <select>
      <option value="老师">老师</option>
      <option value="医生">医生</option>
      <option value="律师">律师</option>
      <option value="学生">学生</option>
      <option value="程序猿" selected>程序猿</option>
      <!--selected属性表示默认初始值-->
   </select>
</div>
```
显示效果：
![select.png](http://upload-images.jianshu.io/upload_images/6426975-685fc6f60238d993.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- label标签&placeholder属性：
```
 <div class="username"> 
    <label for="username">姓名：</label> 
    <input id="username" type="text" name="username" value=""> 
    <!--label标签的 for 属性中的值一定要与相关控件的 id 属性值相同-->
 </div>
 <div class="password">
   <label for="password">密码：</label>
   <input id="password" type="password" name="password" placeholder="请输入密码...">
  </div>
```
显示效果：
![label&placeholder.png](http://upload-images.jianshu.io/upload_images/6426975-be9169b097cb865d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 说明：
  1.  如果在 label 标签内点击文本，就会触发此控件。就是说，当用户单击选中该label标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。
==大白话：点击“密码”或输入框均可输入密码==
 2. placeholder是提示文字，当用户在文本框里输入了什么信息，提示信息就会隐藏
