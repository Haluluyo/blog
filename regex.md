###### 1. ```\d，\w,\s,[a-zA-Z0-9],\b,.,*,+,?,x{3},^,$```分别是什么?
|字符|意义|
|---|---|
|```\d```|数字字符```[0-9]```|
|```\w```|单词字符```[a-zA-Z_0-9]```|
|```\s```|空白符```[\t\n\x0b\f\r]```|
|```[a-zA-Z0-9]```|匹配a-z,A-Z,0-9中的任意一个字符|
|```\b```|单词边界|
|```.```|除```\r\n```以外的所有字符```[^\r\n]```
|```*```|出现```0```次或多次(任意次)|
|```+```|出现```1```次或多次|
|```?```|出现```0```次或```1```次|
|```x{3}```|出现```3```次|
|```^```|[]内代表取反（```/[^]/```）；[]外代表以某一字符串为开头（```/^/```）|
|```&```|代表以某一字符串为结尾|

###### 2. 写一个函数trim(str)，去除字符串两边的空白字符
```
function trim(str){
    return str.replace(/^\s*|\s*$/g,'')
}
console.log(trim('  hellohello   '))
```

![进阶7-2测试.png](http://upload-images.jianshu.io/upload_images/6426975-b64ab2c2811f4658.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 3. 写一个函数isEmail(str)，判断用户输入的是不是邮箱
```
function isEmail(str){
    var reg = /^\w+@\w+\.\w+$/;
    return reg.test(str)
}
console.log(isEmail('1163172265@qq.com'));
console.log(isEmail('1163172265qq.com'))
```

![进阶7-3测试.png](http://upload-images.jianshu.io/upload_images/6426975-7919117e1c0bcf87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 4. 写一个函数isPhoneNum(str)，判断用户输入的是不是手机号
```
function isPhoneNum(str){
    var reg = /^1\d{10}$/g
    return reg.test(str)
}
console.log(isPhoneNum('1830000002433'));
console.log(isPhoneNum('18300002433'))
```

![进阶7-4测试.png](http://upload-images.jianshu.io/upload_images/6426975-eefc2cea5a817230.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 5. 写一个函数isValidUsername(str)，判断用户输入的是不是合法的用户名（长度6-20个字符，只能包括字母、数字、下划线）
```
function isValidUsername(str){
    var reg = /^\w*$/g
    if(str.length>=6&&str.length<=20){
        if(reg.test(str)){
            return '用户名'+str+'合法！'
        }else{
            return '用户名'+str+'含有非法字符，请重新输入！'
        }
    }else if(str.length>20){
         return '用户名'+str+'过长，请重新输入！'
    }else{
        return '用户名'+str+'过短，请重新输入！'
    }
}
console.log(isValidUsername('hahaha'))
console.log(isValidUsername('hahaha~'))
console.log(isValidUsername('abcdefghijklmnopqrstuvwxyz'))
console.log(isValidUsername('haha'))
```

![进阶7-5测试.png](http://upload-images.jianshu.io/upload_images/6426975-76e2d9e0cfcaac8f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 6. 写一个函数isValidPassword(str), 判断用户输入的是不是合法密码（长度6-20个字符，只包括大写字母、小写字母、数字、下划线，且至少至少包括两种）
```
function isValidPassword(str){
    if(str.length<6) return '密码'+str+'过短，请重新输入！'
    if(str.length>20) return '密码'+str+'过长，请重新输入！'
    if(!/^\w{6,20}$/.test(str)) return '密码'+str+'含有非法字符，请重新输入！'
    if(/^\d{6,20}$/.test(str)) return '密码'+str+'过于简单，请重新输入！'
    if(/^[a-z]{6,20}$/.test(str)) return '密码'+str+'过于简单，请重新输入！'
    if(/^[A-Z]{6,20}$/.test(str)) return '密码'+str+'过于简单，请重新输入！'
    if(/^_{6,20}$/.test(str)) return '密码'+str+'过于简单，请重新输入！'
    return '该密码合法！'
}
console.log(isValidPassword('abc'))
console.log(isValidPassword('abcdefghijklmnopqrstuvwxyz'))
console.log(isValidPassword('123456'))
console.log(isValidPassword('abcdefg'))
console.log(isValidPassword('ABCDEFG'))
console.log(isValidPassword('______'))
console.log(isValidPassword('123abc'))
```

![进阶7-6测试.png](http://upload-images.jianshu.io/upload_images/6426975-420ac88f6aa4a713.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 7. 写一个正则表达式，得到如下字符串里所有的颜色
```
var re = /#([0-9a-fA-F]{6}|[0-9a-fA-F]{3})(?![0-9a-fA-F])/g
//另一种写法re =/#[0-9a-fA-F]{6}(?=;)/g
var subj = "color: #121212; background-color: #AA00ef; width: 12px; bad-colors: f#fddee "
console.log( subj.match(re) )  // ['#121212', '#AA00ef']
```

![进阶7-7测试.png](http://upload-images.jianshu.io/upload_images/6426975-ded2156cfdfdc57c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 8. 下面代码输出什么? 为什么? 改写代码，让其输出[""hunger"", ""world""].
```
var str = 'hello  "hunger" , hello "world"';
var pat =  /".*"/g;
str.match(pat); //输出：[""hunger" , hello "world""]
//原因：贪婪模式会在满足条件的情况下，尽可能多的匹配，即"  hunger" , hello "world"  '

/*可以输出[""hunger"", ""world""]的写法*/
var str = 'hello  "hunger" , hello "world"';
var pat =  /".*?"/g;
str.match(pat); 
```
![进阶7-8测试.png](http://upload-images.jianshu.io/upload_images/6426975-a0edf7bf5f808e8c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
