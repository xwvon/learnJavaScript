## 一、禁止移动端浏览器页面滚动
1. HTML实现
```html
<body ontouchmove="event.preventDefault()"></body>
```
2. JavaScript实现
```js
document.addEventListener('touchmove', function (event) {
    event.preventDefault();
});
```
## 二、阻止默认行为
```js
//原生JavaScript实现
document.getElementById('btn').addEventListener('click', function (event) {
    event = event || window.event;
    if (event.preventDefault) {
        event.preventDefault();
    } else {
        //IE浏览器
        event.returnValue = false;
    }
}, false);
//jquery实现
$('#btn').on('click', function (event) {
    event.preventDefault();
});
```
## 三、阻止冒泡
```js
//javascript原生实现
document.getElementById('btn').addEventListener('click', function (event) {
    event = event || window.event;
    if (event.stopPropagation) {
        event.stopPropagation();
    } else {
        //IE浏览器
        event.cancleBubble = true;
    }
}, false);
//jquery实现
$('#btn').on('click', function (event) {
    event.stopPropagation();
});
```
## 四、检测浏览器是否支持svg
```js
function isSupportSvg() {
    const SVG_NS = 'http://www.w3.org/2000/svg';
    return !!document.createElementNS && !!document.createElementNS(SVG_NS, 'svg').createSVGRect;
    console.log(isSupportSvg());
}
```
## 五、检测浏览器是否支持Canvas
```js
function isSupportCanvas() {
    if (document.createElement('canvas').getContext) {
        return true;
    } else {
        return false;
    }
}
console.log(isSupportCanvas());
```
## 六、检测是否是微信浏览器
```js
function isWeiXinClient() {
    const ua = navigator.userAgent.toLowerCase();
    if (ua.match(/MicroMessenger/i) === "micromessenger") {
        return true;
    } else {
        return false;
    }
}
alert(isWeiXinClient());
```
## 七、检测是否移动端及浏览器内核
```js
var browser = { 
    versions: function() { 
        var u = navigator.userAgent; 
        return { 
            trident: u.indexOf('Trident') > -1, //IE内核 
            presto: u.indexOf('Presto') > -1, //opera内核 
            webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核 
            gecko: u.indexOf('Firefox') > -1, //火狐内核Gecko 
            mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否移动终端 
            ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios 
            android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android 
            iPhone: u.indexOf('iPhone') > -1 , //iPhone 
            iPad: u.indexOf('iPad') > -1, //iPad 
            webApp: u.indexOf('Safari') > -1 //Safari 
        }; 
    }
} 

if (browser.versions.mobile() || browser.versions.ios() || browser.versions.android() || browser.versions.iPhone() || browser.versions.iPad()) { 
    alert('移动端'); 
}
```
## 八、强制移动端横屏
```js
$( window ).on( "orientationchange", function( event ) {
    if (event.orientation=='portrait') {
        $('body').css('transform', 'rotate(90deg)');
    } else {
        $('body').css('transform', 'rotate(0deg)');
    }
});
$( window ).orientationchange();
```
## 九、检测浏览器内核
```js
function getNavigatorKernel(){    
    if(navigator.userAgent.indexOf("MSIE")>0) {    
      return "MSIE";       //IE浏览器  
    }  

    if(isFirefox=navigator.userAgent.indexOf("Firefox")>0){    
      return "Firefox";     //Firefox浏览器  
    }  

    if(isSafari=navigator.userAgent.indexOf("Safari")>0) {    
      return "Safari";      //Safan浏览器  
    }  

    if(isCamino=navigator.userAgent.indexOf("Camino")>0){    
      return "Camino";   //Camino浏览器  
    }  
    if(isMozilla=navigator.userAgent.indexOf("Gecko/")>0){    
      return "Gecko";    //Gecko浏览器  
    }    
}
```
## 十、电脑端页面全屏显示
```js
function fullscreen(element) {
    if (element.requestFullscreen) {
        element.requestFullscreen();
    } else if (element.mozRequestFullScreen) {
        element.mozRequestFullScreen();
    } else if (element.webkitRequestFullscreen) {
        element.webkitRequestFullscreen();
    } else if (element.msRequestFullscreen) {
        element.msRequestFullscreen();
    }
}

fullscreen(document.documentElement);
```
## 十一、获得/失去焦点
```html
<input id="i_input" type="text" value="会员卡号/手机号">
```
```js
window.onload = function(){
    var oIpt = document.getElementById("i_input");

    if(oIpt.value == "会员卡号/手机号"){
        oIpt.style.color = "#888";
    }else{
        oIpt.style.color = "#000";
    };

    oIpt.onfocus = function(){
        if(this.value == "会员卡号/手机号"){
            this.value="";
            this.style.color = "#000";
            this.type = "password";
        }else{
            this.style.color = "#000";
        }
    };
    
    oIpt.onblur = function(){
        if(this.value == ""){
            this.value="会员卡号/手机号";
            this.style.color = "#888";
            this.type = "text";
        }
    };
}
```
## 十二、获取上传文件大小
```html
<input type="file" id="filePath" onchange="getFileSize(this)"/>
```
```js
function getFileSize(obj){
    var filesize;
    
    if(obj.files){
        filesize = obj.files[0].size;
    }else{
        try{
            var path,fso; 
            path = document.getElementById('filePath').value;
            fso = new ActiveXObject("Scripting.FileSystemObject"); 
            filesize = fso.GetFile(path).size; 
        }
        catch(e){
            // 在IE9及低版本浏览器，如果不容许ActiveX控件与页面交互，点击了否，就无法获取size
            console.log(e.message); // Automation 服务器不能创建对象
            filesize = 'error'; // 无法获取
        }
    }
    return filesize;
}
```
## 十三、常用正则表达式
```js
//验证邮箱 
/^\w+@([0-9a-zA-Z]+[.])+[a-z]{2,4}$/ 

//验证手机号 
/^1[3|5|8|7]\d{9}$/ 

//验证URL 
/^http:\/\/.+\./

//验证身份证号码 
/(^\d{15}$)|(^\d{17}([0-9]|X|x)$)/ 

//匹配字母、数字、中文字符 
/^([A-Za-z0-9]|[\u4e00-\u9fa5])*$/ 

//匹配中文字符
/[\u4e00-\u9fa5]/ 

//匹配双字节字符(包括汉字) 
/[^\x00-\xff]/
```
## 十四、倒计时
```html
<p id="lefttime"></p>
```
```js
function countdown() {

    var endtime = new Date("May 4, 2018 11:05:09");
    var nowtime = new Date();

    if (nowtime >= endtime) {
        document.getElementById("_lefttime").innerHTML = "倒计时间结束";
        return;
    }

    var leftsecond = parseInt((endtime.getTime() - nowtime.getTime()) / 1000);
    if (leftsecond < 0) {
        leftsecond = 0;
    }

    __d = parseInt(leftsecond / 3600 / 24);
    __h = parseInt((leftsecond / 3600) % 24);
    __m = parseInt((leftsecond / 60) % 60); 
    __s = parseInt(leftsecond % 60);

    document.getElementById("lefttime").innerHTML = __d + "天" + __h + "小时" + __m + "分" + __s + "秒";
}

countdown();

setInterval(countdown, 1000);
```
## 十五、倒计时跳转
```html
<div id="showtimes"></div>
```
```js
//设置倒计时
var t = 10

function showtime() {
    t -= 1;
    document.getElementById('showtimes').innerHtml = t;
    if (t === 0) {
        location.href = 'error404.php';
    }
    setTimeout(function () {
        showtime();
    }, 1000);
}
```
## 十六、时间戳格式化
```js
function formatDate(now) { 
    var y = now.getFullYear();
    var m = now.getMonth() + 1; // 注意 JavaScript 月份+1 
    var d = now.getDate();
    var h = now.getHours(); 
    var m = now.getMinutes(); 
    var s = now.getSeconds();
    
    return y + "-" + m + "-" + d + " " + h + ":" + m + ":" + s; 
} 

var nowDate = new Date(1442978789184);

alert(formatDate(nowDate));
```
## 十八、当前日期
```js
var calculateDate = function(){

    var date = new Date();
    var weeks = ["日","一","二","三","四","五","六"];

    return date.getFullYear()+"年"+(date.getMonth()+1)+"月"+
    date.getDate()+"日 星期"+weeks[date.getDay()];
}

$(function(){
    $("#dateSpan").html(calculateDate());
});
```
## 十九、判断周六/日
```html
<p id="text"></p>
```
```js
function time(y,m){
    var tempTime = new Date(y,m,0);
    var time = new Date();
    var saturday = new Array();
    var sunday = new Array();
    
    for(var i=1;i<=tempTime.getDate();i++){
        time.setFullYear(y,m-1,i);
        
        var day = time.getDay();
        
        if(day == 6){
            saturday.push(i);
        }else if(day == 0){
            sunday.push(i);
        }
    }
    
    var text = y+"年"+m+"月份"+"<br />"
                +"周六："+saturday.toString()+"<br />"
                +"周日："+sunday.toString();
                
    document.getElementById("text").innerHTML = text;
}
 
time(2018,5);
```