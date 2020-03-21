### JavaScript对象原型
1. 示例：
```javascript
function Person(first, last, age, eye){
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eye;
}
Person.nationality = "English";
var myFriend = new Person("Bill","Gates",62,"blue");
var myBrother = new Person("Steve","Jobs",56,"green");
document.getElementById("demo").innerHTML = "My friend is " + myFriend.age + ". My brother is " + myBrother.age;
document.getElementById("demo1").innerHTML = "The nationality of my friend is " + myFriend.nationality.
//结果为My friend is 62. My brother is 56
//The nationality of my friend is undefined
```
>此时已经无法为已有的对象构造器添加新属性了。
2. 如需向构造器添加一个新属性，则必须把它添加到构造器函数。示例：
```javascript
function Person(first,last,age,eye){
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eye;
    this.nationality = "English";
}
var myFriend = new Person("Bill","Gates",62,"blue");
var myBrother = new Person("Steve","Jobs",56,"green");
document.getElementById("demo2").innerHTML = "The nationality of my friend is " + myFriend.nationality + ". The nationality of my friend is " + myBrother.nationality;
//结果为The nationality of my friend is English. The nationality of my friend is English
```
#### 原型继承
所有JavaScript对象都从原型继承属性和方法。
- 日期对象继承自Date.prototype。
- 数组对象继承自Array.prototye。
- Person对象继承自Person.prototype.
- 日期对象、数组对象和Person对象都继承自Object.prototype。
#### 向对象添加属性和方法
1. 使用prototype属性可以为对象构造器添加新属性和新方法。示例：
```javascript
function Person2(first,last,age,eye){
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eye;
}
Person2.prototype.name = function(){
    return this.firstName + " " + this.lastName;
}
Person2.prototype.nationality = "English";
var myFriend2 = new Person2("Bill", "Gates",62, "blue");
document.getElementById("demo3").innerHTML = "The nationality of my friend2 is " + myFriend2.nationality;
document.getElementById("demo4").innerHTML = "My friend2 is " + myFriend2.name();
//结果为The nationality of my friend2 is English
//My firend2 is Bill Gates
```
