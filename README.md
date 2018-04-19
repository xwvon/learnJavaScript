<<<<<<< HEAD
# JavaScript学习记录
## 冒泡排序
```js
function sortArr(arr) {
    for (i = 0; i < arr.length - 1; i++) {
        for (j = 0; j < arr.length - 1 - i; j++) {
            if (arr[j] > arr[j+1]) {
                var tmp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = tmp;
            }
        }
    }
    return arr;
}
```
## 三个number比较
```
1 < 2 < 3 //->true
```
::: tip
1 < 2 -> true -> Number(true) === 1 -> 1 < 3 ->true
:::
## 隐式转换
```js
const a = {};
var b = {key: 'b'}, c = {key: 'c'};
a[b] = 123;
a[c] = 456;
console.log(a) // ->456 ->b和c都被转化为'[object object]'
```
## JSONP实现跨域
```js
<script>
    var script = document.createElement('script');
    script.type = 'text/plain';
    script.src = 'http://www.......:8080/login?use=admin&callback=onBack';
    document.head.appendChild(script);
    function onBack() {
        alert(JSON.stringify(res));
    }
</script>
```
## 二分查找
```js
function search(key, arr){
    let l = 0, h = arr.length - 1;
    while(l <= h) {
        let mid = l + (h - l) / 2;
        if (key === arr[mid]) {
            return mid;
        }else if (key < arr[mid]) {
            h = mid - 1;
        }else if (key > arr[mid]) {
            l = mid + 1;
        }else {
            return -1;
        }
    }
}
```
## leetcode第一题两数之和
```js
function twoSum(nums, targe) {
    var obj = {};
    for (var i = 0; i < nums.length; i++) {
        var x = nums[i]
        if(obj.hasOwnProperty(target - x)) {
            return [obj[target-x], i];
        } else {
            obj[x] = i;
        }
    }

}
```
## leetcode之反转整数
```js
function reverseNum(num) {
    var x1 = num > 0 ? 1 : -1;
    var num2str = Math.abs(num) + '';
    var resultStr = num2str.split('').reverse().join('');
    if (+resultStr > 2147483647) {
        return 0;
    }
    return resultStr * x1;
}
```
## leetcode之回文数
```js
function isPalindrome(num) {
    return num === parseInt(String(num).split('').reverse().join(''));
}
```
## leetcode之罗马数字转整数
```js
function roman2num(s){
    var romanObj = {
        M: 1000,
        C: 500,
        D: 100,
        L: 50,
        X: 10,
        V: 5,
        I: 1
    };
    var result = 0
    for (var i = 0; i < s.length; i++) {
        var current = s.charAt(i)
        if (i === 0) {
            result += romanObj[current];
        } else {
            var prev = s.charAt(i - 1);
            if (romanObj[current] > romanObj[prev]) {
                result += romanObj[current];
                result -= romanObj[prev] * 2;
            } else {
                result += romanObj[current];
            }
        }
    }
    return result;
}
```
## leetcode之最长公共前缀
```js
function longestCommonPrefix(strs) {
    if (strs.length) <= 1 {
        return String(strs);
    }
    return strs.reduce((s1, s2) => {
        var result = '';
        for (var i = 0; i < s1.length; i++) {
            if (s1.charAt(i) === s2.charAt(i)) {
                result += s1.charAt(i);
            }else {
                break;
            }
        }
        return result;
    });
}
```
## 有效的括号
Given a string containing just the characters '(',')','{','}','[' and ']', determine if the input string is valid.
The brackets must close in correct order, '()' and '(){}[]' are all valid but '(]' and '([)]' are not.
```js
function isValid(s) {
    if (!s) return true;
    var map = {
        '(': ')',
        '[': ']',
        '{': '}'
    },
    stack = [];
    for (var i = 0; i < s.length; i++) {
        if (map[s[i]]) {
            stack.push(map[s[i]]);
        } else {
            if (s[i] !== stack.pop()) {
                return false;
            }
        }
    }
    return stack.length === 0;
}
```
## leetcode之删除排序数组中的重复项
```js
function removeDuplicates = function (nums) {
    if (nums.lenght === 0) return 0;
    var i = 0;
    for (var j = 1; j < nums.length; j++) {
        if (nums[j] !== nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i+1;
}
```
