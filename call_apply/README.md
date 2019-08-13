### call()和apply()
#### call()
使用call()方法可以编写能够在不同对象上使用的方法。
1. 如果一个函数不是JS对象的方法，那么它就是全局对象的函数，示例：
```javascript
var myObject = {
    firstName:"Bill",
    lastName:"Gates",
    fullName:function(){
        return this.firstName + " " + this.lastName;
    }
}
x = myObject.fullName();
document.getElementById("demo").innerHTML = x;
//结果为Bill Gates
```
- fullName属性是一个方法，person对象是该方法的拥有者。
- fullName属性属于person对象的方法。
2. call()方法是预定义的js方法，它可以用来调用所有者对象作为参数的方法，通过call可以使用属于另一个对象的方法。示例：
```javascript
var person = {
    fullName: function(){
        return this.firstName + " " + this.lastName;
    }
}
var person1 = {
    firstName:"Bill",
    lastName:"Gates"
}
var person2 = {
    firstName:"Steve",
    lastName:"Jobs"
}
var x = person.fullName.call(person1);
document.getElementById("demo1").innerHTML = x;
//结果为Bill Gates
```
上例中调用person的fullName方法，并用于person1。
3. 带参数的call()方法，示例：
```javascript
var person = {
    fullName:function(city,country){
        return this.firstName+ " " + this.lastName + "," + city + "," + country;
    }
}
var person1 = {
    firstName:"Bill",
    lastName:"Gates"
}
var person2 = {
    firstName:"Steve",
    lastName:"Jobs"
}
var x = person.fullName.call(person1,"Seatle","USA");
document.getElementById("demo2").innerHTML = x;
//结果为Bill Gates,Seatle,USA
```
#### apply()方法  能够编写用于不同对象的方法
1. apply()方法与call()方法非常相似，person的fullName方法被应用到person1。示例：
```javascript
var person = {
    fullName: function(){
        return this.firstName + " " + this.lastName;
    }
}
var person1 = {
    firstName:"Bill",
    lastName:"Gates"
}
var x = person.fullName.apply(person1);
document.getElementById("demo3").innerHTML = x;
//结果为Bill Gates
```
2. call()和apply()之间的区别
不同之处是：
- call()方法分别接受参数。
- apply()方法接受数组形式的参数。
如果要使用数组而不是参数列表，则apply()方法非常方便。
3. 带参数的apply()方法，apply()方法接受数组中的参数。示例：
```javascript
var person = {
    fullName: function(city,country){
        return this.firstName + " " + this.lastName + "," +city  + "," + country;
    }
}
var person1 = {
    firstName:"Bill",
    lastName:"Gates"
}
var x = person.fullName.apply(person1,["Seatle","USA"]);
document.getElementById("demo4").innerHTML = x;
//结果为Bill Gates,Seatle,USA
```


