# 个人收集的一些简单jQuery技巧
## 使用`noConflict()`来解除`$`别名
在文档开始处使用`noConflict()`方法就可以通过`jQuery`变量名来代替`$`引用jQuery对象（例如：jQuery('div p').hide()）
```js
jQuery.noConflict();
```
## 检查jQuery是否加载
```js
if (typeof jQuery === 'undefined') {
    console.log('jQuery 还没有加载！');
} else {
    console.log('jQuery 已经加载...');
}
```
## 使用`.on()`绑定来替代`.click()`
使用`.on()`比使用`.click()`更有优势，比如能添加多个事件绑定
```js
.on('click tap hover')
```
并且能给绑定的事件添加命名，这样就可以给具体的事件解除绑定
```js
.on('click.menuOpening');
.off('click.menuOpening');
```
## 返回顶部
通过使用jQuery的`animate`和`scrollTop`方法就可以实现一个简单返回顶部动画
```html
<div class="container">
    <a href="#" class="back-to-top">返回顶部</a>
</div>
<script>
    $('.container').on('click', '.back-to-top', function (e) {
        e.preventDefault();
        $('html, body').animate({scrollTop: 0}, 800);
    });
</script>
```
## 图片预加载
```js
$.preloadImages = function () {
    for (var i = 0; i < arguments; i++) {
        $('<img>').attr('src', arguments[i]);
    }
};
$.preloadImages('img/hover-on.png', 'img/hover-off.png');
```
## 自动修复错误图片
```js
$('img').on('error', function () {
    if(!$(this).hasClass('broken-image')) {
        $(this).attr('src', 'img/broken.png').addClass('broken-image);
    }
});
```
你也通过可以隐藏错误图片
```js
$('img').on('error', function () {
    $(this).hide();
});
```
## 用Ajax提交表单
```js
$.post('sign_up.php', {
    user_name: $('input[name=user_name]').val(),
    email: $('input[name=email]').val(),
    password: $('input[name=password]').val();
});
```
更好的方法是用`serialize()`方法来序列化用户输入
```js
$.post('sign_up.php', $('#form').serialize());
```
## 切换样式
```js
$('#btn').on('hover', function () {
    $(this).toggleClass('hover');
});
```
## 禁用元素
```js
$('input[type="submit"]').prop('disabled', true);
```
## 切换淡入/淡出或者滑入滑出效果
```js
$('.btn').on('click', function () {
    $('.element').fadeToggle('slow');
});
$('.btn').on('click', function () {
    $('.element').slideToggle('slow');
});
```
## 简单折叠
```js
//close all panels
$('#accordion').find('.content').hide();
//accordion
$('#accordion').find('.accordion-header').on('click', function () {
    var next = $(this).next();
    next.slideToggle('fast');
    $('.content').not(next).slideUp('fast');
});
```
## 设置两个div具有相同的高度
```js
$('#div1').css('min-height', $('#div2').height());
```
## 通过文本找到元素
```js
var search = $('#search').val();
$('div:not(:contains("' + search + '"))').hide();
```
## 按字母顺序排列
```js
var ul = $('#list'),
    lis = $('li', ul).get();
lis.sort(function (a, b) {
    return ($(a).text().toUpperCase() < $(b).text().toUpperCase()) ? 1 : -1;
});
ul.append(lis);
```
## 禁用鼠标右键
```js
$(document).ready(function () {
    $(document).bind('contextmenu', function (e) {
        return false;
    });
});
```