##### 1.下面的代码输出多少？修改代码让``` fnArr[i]() ```输出 i。使用 两种以上的方法
```
 var fnArr = [];
    for (var i = 0; i < 10; i ++) {
        fnArr[i] =  function(){
    	    return i;
        };
    }
    console.log( fnArr[3]() );  //
```
输出结果为 10，```fnArr[i]()```输出均为10
修改代码：
```
立即执行函数
for (var i = 0; i < 10; i ++){
  !function(j){
    fnArr[j] =  function(){
    	    return j;
        };
  }(i);
}
console.log( fnArr[3]() ); 
```
```
自执行函数
for(var i=0; i < 10; i++){
  fnArr[i] = function(i){
    return function(){
      return i;
    };
  }(i);
}
console.log( fnArr[3]() );
```
![修改函数（1）.png](https://upload-images.jianshu.io/upload_images/6426975-64ca2ff93983f045.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 2.封装一个汽车对象，可以通过如下方式获取汽车状态
```
var Car = (function(){
   var speed = 0;
   function setSpeed(s){
     return speed = s;
   }
  function getSpeed(){
     return speed;
  }
  function accelerate(){
     return speed += 10;
  }
  function decelerate(){
     return speed -= 10;
  }
  function getStatus(){
     var carStatus 
     if(speed>0){
       carStatus = 'running';
     }else if(speed===0){
       carStatus = 'stop';
     }else{
       carStatus = 'error';
     }
    return carStatus;
  }
  
   return {
      setSpeed: setSpeed,
      getSpeed: getSpeed,
      accelerate: accelerate,
      decelerate: decelerate,
      getStatus: getStatus,
   };
})();

Car.setSpeed(30);
console.log(Car.getSpeed());//30
Car.accelerate();
console.log(Car.getSpeed());//40;
Car.decelerate();
Car.decelerate();
console.log(Car.getSpeed()); //20
console.log(Car.getStatus()); // 'running';
Car.decelerate(); 
Car.decelerate();
console.log(Car.getStatus());  //'stop';
Car.decelerate();
console.log(Car.getStatus());
```
![汽车状态测试.png](https://upload-images.jianshu.io/upload_images/6426975-cac45c0123034984.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 3.下面这段代码输出结果是? 为什么?
```
var a = 1;
setTimeout(function(){
    a = 2;
    console.log(a); 
}, 0);
var a ;
console.log(a);
a = 3;
console.log(a);
```
输出结果是：1 3 2
分析：
```
var a = 1;
setTimeout(function(){
    a = 2;
    console.log('第1个a:'+a);
}, 0);
var a ;
console.log('第2个a:'+a);
a = 3;
console.log('第3个a:'+a);

变量提升：
var a ;
var a ;
a = 1;
console.log('第2个a:'+a);
a = 3;
console.log('第3个a:'+a);
//浏览器在运行代码时看到定时器setTimeout()会先放在一边不处理，
//继续执行后边的代码，完成后再执行setTimeout()
setTimeout(function(){
    a = 2;
    console.log('第1个a:'+a);
}, 0);
```

##### 4.下面这段代码输出结果是? 为什么?
```
var flag = true;
setTimeout(function(){
    flag = false;
},0)
while(flag){}
console.log(flag);
```
没有输出结果
```
分析：
     var flag;
     flag = true;
     while(flag){} //while(1){}会无限循环{}
```
##### 5.下面这段代码输出？如何输出delayer: 0, delayer:1...（使用闭包来实现）
```
for(var i=0;i<5;i++){
	setTimeout(function(){
         console.log('delayer:' + i );
	}, 0);
	console.log(i);
}
```
输出结果是：0 1 2 3 4   delay:5 delay:5 delay:5 delay:5 delay:5
```
修改代码：
for(var i=0;i<5;i++){
  !function(i){
    setTimeout(function(){
         console.log('delayer:' + i );
	}, 0);
  }(i)
  console.log(i);
}
```
![测试.png](https://upload-images.jianshu.io/upload_images/6426975-113704e6171d8af0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 6. 如何获取元素的真实宽高
getComputedStyle是一个可以获取当前元素所有最终使用的CSS属性值。
```
var style = window.getComputedStyle("元素", "伪类");
// 第一个参数为元素名，第二个为伪类，可选
```
```
var element =document.querySelector('div')
var width = window.getComputedStyle(element).width
var height = window.getComputedStyle(element).height 

//兼容低版本IE 
function trueStyle(element,pse){ return element.currentStyle ? element.currentStyle : window.getComputedStyle(element,pse) 
var width = trueStyle(element,pse).width 
var height = trueStyle(element,pse)
```
#####7.URL 如何编码解码？为什么要编码？
|编码方式|区别|解码方式|
|---|---|---|
|```encodeURI()```|不会对下列字符编码：```ASCII字母、数字、~!@#$&* ()=:/,;?+'```|```decodeURI()```|
|```encodeURIComponent()```|不会对下列字符编码：``` ASCII字母、数字、~!*()'```|```decodeURIComponent()```|
原因：url的编码格式采用的是ASCII码，而中文不是ASCII的字符，如果不先编码就传输数据，那么可能会出现问题。所以通过把中文字符编码为符合ASCII标准的字符，就可以避免这个问题
#####8.补全如下函数，判断用户的浏览器类型
```
function isAndroid(){
}
function isIphone(){
}
function isIpad(){
}
function isIOS(){
}
```
```
function isAndroid(){ 
    return /android/i.test(navigator.userAgent); 
}
function isIphone(){ 
    return /iphone/i.test(navigator.userAgent); 
} 
function isIpad(){
    return /ipad/i.test(navigator.userAgent); 
} 
function isIOS(){ 
    return /iphone|ipad|iPod/i.test(navigator.userAgent); 
}
```
