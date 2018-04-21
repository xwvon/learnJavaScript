![logo](./logo.png)
30 seconds of code
===================

>收集自[justjavac的github](https://github.com/justjavac/30-seconds-of-code-zh-CN/)

目录
---
+ [字符串换位组合](#字符串换位组合)
+ [Average of array of numbers](#average-of-array-of-numbers)
+ [Capitalize first letter of every word](#capitalize-first-letter-of-every-word)
+ [Capitalize first letter](#capitalize-first-letter)
+ [Count occurrentences of a value in array](#count-occurrentences-of-a-value-in-array)
+ [Current URL](#current-URL)
+ [Curry](#curry)
+ [Difference between arrays](#difference-between-arrays)
+ [Distance between two points](#distance-between-two-points)
+ [Escape regular expression](#escape-regular-expression)
+ [Even or odd number](#even-or-odd-number)
+ [Factorial](#factorial)
+ [Fibonacci array generator](#fibonacci-array-generator)
+ [Filter out non-unique values in an array](#filter-out-non-unique-values-in-an-array)
+ [Flatten array](#flatten-array)
+ [et scroll position](#et-scroll-position)
+ [Greatest common divisor](#greatest-common-divisor)
+ [Initialize array with range](#initialize-array-with-range)
+ [Initialize array with value](#initialize-array-with-value)
+ [Object from key-value pairs](#object-from-key-value-pairs)
+ [Powerset](#powerset)
+ [Randomize order of array](#randomize-order-of-array)
+ [Redirect to URL](#redirect-to-URL)
+ [Reverse a string](#reverse-a-string)
+ [RGB to hexadecimal](#rGB-to-hexadecimal)
+ [Scroll to top](#scroll-to-top)
+ [Similarity between arrays](#similarity-between-arrays)
+ [Sort characters in string](#sort-characters-in-string)
+ [Unique values of array](#unique-values-of-array)
+ [Validate number](#validate-number)
+ [ary](#ary)
+ [call](#call)
## 字符串换位组合
```js
const anagrams = s => {
    if(s.length <= 2) return s.length === 2 ? [s, s[1] + s[0]] : [s];
    return s.split('').reduce( (a, l, i) => {
        anagrams(s.slice(0, i) + s.slice(i+1)).map( v => a.push(l+v));
        return a;
    }, []);
}
```
## Average of array of numbers
Use reduce() to add each value to an accumulator, initialized with a value of 0, divide by the length of array
> 利用数组的归并方法求得数组的和，再除以数组的长度
```js
const average = array => array.reduce( (a, b) => a + b, 0) / array.length;
```
## Capitalize first letter of every word
Use replace() to match the first character of each word and toUpperCase() to capitalize it
> 使得字符串中的每个单词的第一个字母变成大写
```js
const capitalizeEveryWord = str => str.replace(/\b[a-z]/g, char => char.toUpperCase());
```
## Capitalize first letter
Use slice(0,1) and toUpeprease() to capitalize first letter, slice(1) to get the rest of the string. Omit the lowerRest parameter to keep the rest of the string intact, or set it to true convert to lower case
> 把传入的字符串转化成首字母大写的形式
```js
const capitalize = (str, lowerRest=false) => str.substring(0,1).toUpperCase() + (lowerRest ? str.substring(1).toLowerCase() : str.substring(1));
```
## Count occurrentences of a value in array
Use reduce() to increment a counter each time you encounter the specific value inside the array
> 利用数组的归并方法统计给定数值在数组中的个数
```js
const countValueArray = (arr, value) => arr.reduce((i, item) => item === value ? i+1 : i+0, 0);
```
## Current URL
Use Window.location.href to get current URL
> 获得当前网页的URL
```js
const currentUrl = _ => window.location.href;
```
## Curry
> 柯里化一个函数
```js
const curry = f => (...args) => args.length >= f.length ? f(...args) : (...othArgs) => curry(f)(...args, ...othArgs);
```
## Diffence between arrays
Use filter() to remove values that are part of values, determined using includes()
> 过滤出两个数组之间不相同的元素
```js
const diffence = (arr, values) => arr.filter( (v) => !values.includes(v));
```
## Distance between two points
Use Math.hypot() to calculate the Euclidean distance between two points
> 利用Math.hypot()方法计算出两个点之间的距离
```js
const disance = (x1, y1, x2, y2) => Math.hypot(x2 - x1, y2 - y1);
```
## Escape regular expression
Use replace() to escape special characters
> 利用正则表达式替换特殊字符
```js
const escapeRegExp = s => s.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
```
## Even or odd
Use Math.abs() to extend logic to negative numbers, check using the modulo(%) operator. Return true if the number is even, false if the number is odd
> 判断一个数字的寄偶
```js
const isEven = num => Math.abs(num) % 2 === 0;
```
## Factorial
Use recursion. If n is less than or equal to 1, return 1. Otherwise, return the product of n and the factorial of n - 1.
> 利用递归求一个整数的阶乘
```js
const factorial = n => n <= 1 ? 1 : n * factorial(n - 1);
```
## Fibonacci array generator
Create an empty array of the specific length, initialzing the first and two values (0 and 1). Use reduce() to add value into the array, using the sum of the last two values, expect for the first two.
> 利用数组的归并方法创建一个斐波那契数列生成器
```js
const fibonacci = n => Array.apply(null, [1,2]concat(Array(n-2))).reduce((acc, val, i) => {
    acc.push( i > 1 ? acc[i-1] + acc[i-2] : val);
    return acc;
}, []);
```
## Filter out non-unique values in an array
Use Array.filter() for an array containing only the unique values.
> 利用数组的filter()方法过滤出数组中不止出现过一次的数
```js
const unique = arr => arr.filter(i => arr.indexOf(i) === arr.lastIndexOf(i));
```
## Flatten array
Use recursion. Use reduce() to get all elements that are not arrays, flatten each element that is an arrry.
> 使用递归将多维数组变成一维数组
```js
const flatten = arr => arr.reduce((a, v) => a.concat(Array.isArray(v) ? flattene(v) : v), []);
```
## et scroll position
Use pageXOffset and pageYOffset if they are defined, otherwise scrollLeft and scrollTop. Omit el to use default value of window.
```js
const getScrollPos = (el=window) => {
    ({ x: (el.pageXOffset !== undefined) ? el.pageXOffset : el.scrollLeft,
    y: (el.pageYOffset !== undefined) ? el.pageYOffset : el.scrollTop });
}
```
## Greatest common divisor
Use recursion. Base case is when y equals 0. In this case, return x. Otherwise, return the GCD of y and the remainder of the divison x/y.
> 使用递归的方法求两个数字的最大公约数
```js
const gcd = (x, y) => y % x === 0 ? x : gcd(y%x, x);
```
## Initialize array with range
使用Array(end-start)来创建给定长度的空数组,并用数组的map()方法来填充数组范围内的值,开始值默认为0
```js
const initiallizeArrayRange = (end, start = 0) => Array.apply(null, Array(end-start)).map((v, i) => i + start);
```
## Initialize array with value
用Array(n)来创建给定长度为n的数组，并用fill()方法填充数组给定的值，默认以0填充
```js
const initializeArray = (n, v) => Array(n).fill(v);
```
## Object from key-value pairs
用数组的map()方法把参数数组里的每个元素变成相应的对象，并用Object.assign()把每一个对象结合起来
```js
const objectFromPairs = arr => 
    Object.assign(...arr.map(v => {return {[v[0]]: v[1]};}));
```
## Random number in range
用Math.random()方法生成指定范围内的随机数
```js
const randomInRange = (min, max) => Math.random() * (max - min) + min;
```
## Randomize order of array
随机化一个数组
```js
const randomizeOfArray = arr => arr.sort((a, b) => Math.random() >= 0.5 ? -1 : 1);
```
## Redirect to URL
URL重定向
```js
const redirect = (url, aslink = true) => aslink ? window.location.href = url : window.location.replace(url);
```
## Reverse a string
反转一个字符串
```js
const reverseString = str => [...str].reverse().join('');
```
## RGB to hexadecimal
把以RGB颜色的表示转换为16进制字符串的表示法
```js
const rgbToHex = (r, g, b) => [r, g, b].map(val => (val).toString(16).padStart(2, '0')).join('');
```
## Scroll to top
```js
const scrollToTop = _ => {
    const c = document.documentElement.scrollTop || document.body.scrollTop;
    if (c > 0) {
        window.requestAnimationFrame(scrollToTop);
        window.scrollTo(0, c - c / 8);
    }
}
```
## Similarity between arrays
```js
const diffence = (arr, value) => arr.filter(v => value.includes(v));
```
## Sort characters in string
```js
const sortCharactersInString = str => str.split('').sort((a, b) => a.localeCompare(b)).join('');
```
## Unique vlaues of array
快速数组去重
```js
const uniqueArray = arr => [...new Set(arr)];
```
## Validate number
```js
const validateNumber = n => !isNaN(parseFloat(n)) && isFinite(n);
```
## ary
将传入的fn函数作用于前n个参数，忽略其他的参数
```js
const ary = (fn, n) => (...args) => fn(...args.slice(0, n));

```
Example
```js
const firstTwoMax = ary(Math.max, 2);
[[2,6,,'a'], [8,4,6], [10]].map(arr => firstTwoMax(...arr));
```
## call
```js
const call = (key, ...args) => context => context[key](...args);
```
Example
```js
Promise.reslove([1,2,3]).then(call('map', x => 2 * x)).then(console.log); //[2,4,6]
const map = call.bind(null, 'map');
Promise.resolve([1,2,3]).then(map(x => 2 * x)).then(console.log); //[2,4,6]
```
