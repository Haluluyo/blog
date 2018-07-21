#### Math
###### 1. 写一个函数，返回从min到max之间的 随机整数，包括min不包括max 
```
function random(min,max){
    return min+Math.floor(Math.random() * (max - min));
}
var arr=[];
for(var i=0;i<20;i++){
    arr.push(random(1,5))
}
console.log(arr);
```

![math-1测试.png](http://upload-images.jianshu.io/upload_images/6426975-f711a6fe7aa1ead7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 2. 写一个函数，返回从min都max之间的 随机整数，包括min包括max 
```
function random(min,max){
    return min+Math.floor(Math.random() * (max - min+1));
}
var arr=[];
for(var i=0;i<20;i++){
    arr.push(random(1,5))
}
console.log(arr);
```

![math-2测试.png](http://upload-images.jianshu.io/upload_images/6426975-7516ec3d065d159a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 3. 写一个函数，生成一个长度为 n 的随机字符串，字符串字符的取值范围包括0到9，a到 z，A到Z。
```
function getRandStr(len){
  //补全函数
    var dict = '0123456789abcdefghijklnmopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    var randStr = ''
    for(var i=0;i<len;i++){
        randStr+=dict[random(0,62)] //Math.floor(Math.random()*dict.length)
    }
    return randStr;
}
var str = getRandStr(10); // 0a3iJiRZap
console.log(str);
```

![math-3测试](http://upload-images.jianshu.io/upload_images/6426975-c66f686c0320e413.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 4. 写一个函数，生成一个随机 IP 地址，一个合法的 IP 地址为 0.0.0.0~255.255.255.255
```
function getRandIP(){
  //补全
    var arr = [];
    for(var i=0;i<4;i++){
        arr.push(random(0,256));
    }
    return arr.join('.');
}
var ip = getRandIP()
console.log(ip) // 10.234.121.45
```

![math-4测试.png](http://upload-images.jianshu.io/upload_images/6426975-b35b243b6dcb1089.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 5. 写一个函数，生成一个随机颜色字符串，合法的颜色为#000000~ #ffffff
```
function getRandColor(){
    var dict = '0123456789abcdef'
    var str = ''
    for(var i=0;i<6;i++){
        str+=dict[random(0,16)]//Math.floor(Math.random()*dict.length)
    }
    colorStr = '#'+str;
    return colorStr;
}
var color = getRandColor()
console.log(color)   // #3e2f1b
```
![math-5测试.png](http://upload-images.jianshu.io/upload_images/6426975-526cce790e210000.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 数组
###### 1. 数组方法里push、pop、shift、unshift、join、splice分别是什么作用？用 splice函数分别实现push、pop、shift、unshift方法
|方法|用法|作用|
|---|---|---|
|push|```Array.push(str)```|在数组尾部添加一个或多个元素|
|pop|```Array.pop()```|在数组尾部弹出一个或多个元素，并返回（对空数组则返回```undefined```）|
|shift|```Array.shift()```|将数组的第一个元素从原数组中删除，并返回被删除的元素的值（对空数组则返回```undefined```）|
|unshift|```Array.unshift(str)```|向数组的头部添加一个或更多元素，并返回新的长度|
|join|```Array.join(separator)```|将数组各个元素是通过指定的分隔符进行连接成为一个字符串|
|splice|```Array.splice(index, howmany, element1,.....,elementX)```|用于插入、删除或替换数组的元素。|
- splice函数分别实现push方法
```
var arr=new Array(1,2,3,4,5)
arr.push(100)
console.log(arr)　　      　//[1, 2, 3, 4, 5, 100]
arr.splice(6,0,'jirengu')  //灵活的写法arr.splice(arr.length,0,item)
console.log(arr)　　     　//[1, 2, 3, 4, 5, 100, "jirengu"]
```
- splice函数分别实现pop方法
```
var arr=new Array(1,2,3,4,5)
arr.pop()
console.log(arr)　　　//[1, 2, 3, 4]
arr.splice(3,1)      //灵活的写法arr.splice(arr.length-1,1)
console.log(arr)　　　//[1, 2, 3]
```
- splice函数分别实现shift方法
```
var arr=new Array(1,2,3,4,5)
arr.shift()           //1
console.log(arr)　　　//[2, 3, 4, 5]
arr.splice(0,1)
console.log(arr)　　　//[ 3, 4, 5]
```
- splice函数分别实现unshift方法
```
var arr=new Array(1,2,3,4,5)
arr.unshift(100)      //6(数组长度)
console.log(arr)　　　//[100,1, 2, 3, 4, 5]
arr.splice(0,0,'jirengu')
console.log(arr)　　　//["jirengu", 100, 1, 2, 3, 4, 5]
```

###### 2. 写一个函数，操作数组，数组中的每一项变为原来的平方，在原数组上操作
```
function squareArr(arr){
    for(var i=0;i<arr.length;i++){
        arr[i]=arr[i]*arr[i];
    }
}
var arr = [2, 4, 6]
squareArr(arr);
console.log(arr) // [4, 16, 36]
```

![数组-2测试.png](http://upload-images.jianshu.io/upload_images/6426975-f9bbe9157f8a4113.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 3. 写一个函数，操作数组，返回一个新数组，新数组中只包含正数，原数组不变
```
function filterPositive(arr){
    var newArr = [];
    for(var i=0;i<arr.length;i++){
        if(typeof arr[i] === 'number'){
            if(arr[i]>0){
                newArr.push(arr[i]);
            }
        }
    }
    return newArr
}
var arr = [3, -1,  2,  '饥人谷', true]
var newArr = filterPositive(arr)
console.log(newArr) //[3, 2]
console.log(arr) //[3, -1,  2,  '饥人谷', true]
```

![数组-3测试.png](http://upload-images.jianshu.io/upload_images/6426975-d115c7908c335ec6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
ES5数组拓展
function filterPositive(arr){
  return arr.filter(function (value) {
    return (typeof value === "number") && ( value > 0);
  });
}
var arr = [3, -1,  2,  '饥人谷', true]
var newArr = filterPositive(arr)
console.log(newArr) //[3, 2]
console.log(arr)
```


#### Date
###### 1.  写一个函数getChIntv，获取从当前时间到指定日期的间隔时间
```
function getChIntv(dateStr){
    var targetDate = new Date(dateStr);
    var curDate = new Date();
    var offset = Math.abs(targetDate-curDate);
    var totalsecond = Math.floor(offset/1000);
    var seconds = totalsecond%60;
    var totalMinutes = Math.floor((offset/1000)/60);
    var mintues = totalMinutes%60;
    var totalHours = Math.floor(((offset/1000)/60)/60);
    var hours = totalHours%24;
    var totalDays = Math.floor((((offset/1000)/60)/60)/24);
    return '距除夕还有'+totalDays+'天'+hours+'小时'+mintues+'分钟'+seconds+'秒';
}
var str = getChIntv("2018-02-15");
console.log(str);   // 距除夕还有156天9小时48分钟23秒
```
![date-1测试.png](http://upload-images.jianshu.io/upload_images/6426975-88a4d56fb2361201.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 2. 把hh-mm-dd格式数字日期改成中文日期
```
function getChsDate(date){
    var dict = ['零','一','二','三','四','五','六','七','八','九','十','十一','十二','十三','十四','十五','十六','十七','十八','十九','二十','二十一','二十二','二十三','二十四','二十五','二十六','二十七','二十八','二十九','三十','三十一'];
    var arr = [];
    var newArr = date.split('-');
    var year = newArr[0];
    for(var i = 0; i < year.length; i++){
        arr.push(dict[year[i]]);
    }
    arr.push("年");
    arr.push(dict[parseInt(newArr[1],10)]);
    arr.push("月");
    arr.push(dict[parseInt(newArr[2],10)]);
    arr.push("日");
    var newArr = arr.join('');
    return newArr
}
var str = getChsDate('2015-01-08');
console.log(str); // 二零一五年一月八日
```

![date-2测试.png](http://upload-images.jianshu.io/upload_images/6426975-ed9d8aeb616ec87b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 3. 写一个函数，参数为时间对象毫秒数的字符串格式，返回值为字符串。假设参数为时间对象毫秒数t，根据t的时间分别返回如下字符串:

刚刚（ t 距当前时间不到1分钟时间间隔）
3分钟前 (t距当前时间大于等于1分钟，小于1小时)
8小时前 (t 距离当前时间大于等于1小时，小于24小时)
3天前 (t 距离当前时间大于等于24小时，小于30天)
2个月前 (t 距离当前时间大于等于30天小于12个月)
8年前 (t 距离当前时间大于等于12个月)
```
function friendlyDate(time){
    var targetDate = time;
    var curDate = new Date().getTime();
    var offset = Math.abs(targetDate-curDate);
    if(offset < 60*1000){
        return '刚刚'
    }else if(offset < 60*1000*60){
        return '3分钟前'
    }else if(offset < 60*1000*60*24){
        return '8小时前'
    }else if(offset < 60*1000*60*24*30){
        return '3天前'
    }else if(offset < 60*1000*60*24*30*12){
        return '2个月前'
    }else if(offset >= 60*1000*60*24*30*12){
        return '8年前'
    }
}
var str1 = friendlyDate( '1494432000000' ) //  2017-5-11
 console.log(str1)
var str2 = friendlyDate('1504886400000')  //2017-9-09
console.log(str2)
```

![date-3测试.png](http://upload-images.jianshu.io/upload_images/6426975-4dadf39384f2042f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
