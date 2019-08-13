### Timing事件
windows对象允许以指定的时间间隔执行代码，这些时间间隔称为定时事件。
通过js使用的有两个关键的方法：
- setTimeout(function,milliseconds)：在等待指定的毫秒数后执行函数。
- setInterval(function,milliseconds)：等同于setTimeout()h，但持续重复执行该函数。
>setTimeout()和setInterval()都属于HTML DOM Window对象的方法。
#### setTimeout()方法
window.setTimeout(function,miiliseconds);
1. 可以不带window前缀来编写，第一个参数是要执行的函数，第二个参数指示执行前的毫秒数。示例：
```javascript
<button onclick="setTimeout(myFunction,3000);">试一试</button>
<script>
    function myFunction(){
        alert("Hello!");
    }
</script>
```
2. 如何停止执行？
- clearTimeout()方法停止执行setTimeout()规定的函数。
```javascript
window.clearTimeout(timeoutVarible);
```
window.clearTimeout()方法可以不带window前缀来写。
- clearTimeout()使用从setTimeout()返回的变量：
```javascript
myVar = setTimeout(function,milliseconds);
clearTimeout(myVar);
```
示例（类似上例，但是添加了“停止”按钮）：
```javascript
<button onclick="myVar=setTimeout(myFunction,3000);">试一试</button>
<button onclick="clearTimeout(myVar)">停止</button>
```
#### setInterval()方法
1. 该方法在每个给定的时间间隔重复给定的函数，同样也可以不带window前缀来写。
```javascript
window.setInterval(function,milliseconds);
```
- 第一个参数是要执行的函数。
- 第二个参数每个执行之间的时间间隔的长度。
示例（本例每秒执行一次函数“myTimer”）：
```javascript
var myVar = setInterval(myTimer, 1000);
function myTimer() {
    var d = new Date();
    document.getElementById("demo").innerHTML = d.toLocaleTimeString();
}
```
2. 如何停止执行？
- clearInterval()方法停止setInterval()方法中指定的函数的执行。
```javascript
window.clearInterval(timeVarible)
```
- 该方法同样可以不带window前缀来写。
- clearInterval()方法使用从setInterval()返回的变量：
```javascript
myVar = setInterval(function,milliseconds);
clearInterval(myVar);
```
示例（类似上例，只是添加了一个“停止时间按钮”）：
```javascript
<p id="demo"></p>

<button onclick="clearInterval(myVar)">停止时间</button>

<script>
var myVar = setInterval(myTimer, 1000);
 function myTimer() {
    var d = new Date();
    document.getElementById("demo").innerHTML = d.toLocaleTimeString();
}
</script>
```




