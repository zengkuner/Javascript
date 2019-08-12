### 数组
1. 数组是一种特殊的变量，它能够一次存放一个以上的值。创建数组示例：
```javascript
var car = ["Saab", "Volvo", "BMW"];
```
>空格和折行并不重要。但不要在最后一个元素之后写逗号（比如"BMV",）。
也可以使用关键字new创建数组，示例：
```javascript
var cars = new Array("Saab", "Volvo", "BMW");
```
>以上两个例子效果完全一样，第一种方法常用。
2. 访问完整数组，可通过引用数组名来访问完整数组。示例：
```javascript
var cars = ["Saab", "Volvo", "BMW"];
document.getElementById("demo").innerHTML = cars;
```
3. 数组是对象。数组是一种特殊类型的对象，在js中对数组使用typeof运算符会返回“object”。但是，js数组最好以数组来描述。
4. 关联数组：具有命名索引的数组被称为关联数组（或散列）。js中不支持命名索引的数组，数组只能使用数字索引。
5. 数组和对象的区别：
- js中，数组使用数字索引。
- js中，对象使用命名索引。
- 数组是特殊类型的对象，具有数字索引。
6. 何时使用数组，何时使用对象？
- js不支持关联数组。
- 若希望元素名为字符串（文本）则应该使用对象。
- 若希望元素名为数字则应该使用数组。
7. 如何识别数组？
- 数组属于对象，使用js运算符typeOf返回"object"。
- instanceof
### 数组方法
#### 把数组转换为字符串  toString()
1. toString()方法把数组转换为数组值（逗号分隔）的字符串。示例：
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElmentById("demo).innerHTML = fruits.toString();
//结果是Banana,Orange,Apple,Mango
```
2. join()方法也可以将数组元素结合为一个字符串。它的行为类似toString()，但是还可以规定分隔符。示例：
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElmentById("demo).innerHTML = fruits.join(" * ");
//结果为Banana * Orange * Apple * Mango
```
>空格有效。
#### 删除元素和添加新元素  Popping和Pushing
Popping和Pushing指的是：从数组弹出项目，或向数组推入项目。
1. pop()方法从数组中删除最后一个元素，该方法返回被删除的值。示例：
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
frits.pop();
document.getElementById("demo4").innerHTML = fruits;//结果为Banana,Orange,Apple
document.getElementById("demo4").innerHTML = fruits.pop();//返回值为Apple
```
2. push()方法在数组结尾处向数组添加一个新的元素，该方法返回新数组的长度。示例：
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo5").innerHTML = fruits2.push("Kiwi");//结果为5
document.getElementById("demo6").innerHTML = fruits2;
//结果为Banana,Orange,Apple,Mango,Kiwi
```
#### 位移元素
位移与弹出等同，但处理首个元素而不是最后一个。
1. shift()方法会删除首个数组元素，并把所有其他元素“位移”到更低的索引,该方法返回被位移出的字符串。示例：
```javascript
var fruits3 = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo7").innerHTML = fruits3;
document.getElementById("demo8").innerHTML = fruits3.shift();//结果为Banana
document.getElementById("demo9").innerHTML = fruits3;//结果为Orange,Apple,Mango
```
2. unshift()方法（在开头）向数组添加新元素，并“反向位移”旧元素，该方法返回新数组的长度。示例：
```javascript
var fruits3 = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo7").innerHTML = fruits3;
document.getElementById("demo8").innerHTML = fruits3.unshift("Lemon");//结果为5
document.getElementById("demo9").innerHTML = fruits3;
//结果为Lemon,Banana,Orange,Apple,Mango
```
#### 拼接数组
1. splice()方法可用于向数组添加新项，示例：
```javascript
var fruits5 = ["Banana", "Orange", "Apple", "Mango"];
fruits5.splice(2,0,"Lemon","Kiwi");
document.getElementById("demo13").innerHTML = "新数组：<br/>"+fruits5;//结果为Banana,Orange,Lemon,Kiwi,Apple,Mango
```
- 第一个参数（2）定义了应添加新元素的位置和删除的起始位置。
- 第二个参数（0）定义应删除多少元素。
- 其余参数（"Lemon","kiwi"）定义要添加的新元素。
2. splice()方法返回一个包含已删除项的数组。示例：
```javascript
var fruits6 = ["Banana", "Orange", "Apple", "Mango"];
var removed = fruits6.splice(2,2,"Lemon","Kiwi");
document.getElementById("demo15").innerHTML = "新数组：<br/>"+fruits6;//结果为Banana,Orange,Lemon,Kiwi
document.getElementById("demo16").innerHTML = "已删除项：<br/>"+removed;//结果为Apple,Mango
``` 
- 先删除后再添加。
3. 使用splice()方法来删除元素，通过聪明的设定，能够使用splice()方法在数组中不留“空洞”的情况下移除元素。示例：
```javascript
var fruits7 = ["Banana", "Orange", "Apple" ,"Mango"];
fruits7.splice(0,1);
document.getElementById("demo17").innerHTML = fruits7;
//结果为Orange,Apple,Mango
```
- 第一个参数（0）定义新元素应该被添加和被删除的起始位置。
- 第二个参数（1）定义应该删除的元素个数。
- 其余参数被省略，即表示没有新元素将被添加。
#### 合并（连接）数组
1. concat()方法通过合并（连接）现有数组来创建一个新数组。示例：
```javascript
var myGirls = ["Emma", "Isabella"];
var myBoys = ["Jacob", "Michael", "Ethan"];
var myChildren = myGirls.concat(myBoys);
document.getElementById("demo18").innerHTML = myChildren;
//结果为Emma,Isabella,Jacob,Michael,Ethan
```
- concat()方法不会更改现有数组，它总是返回一个新数组。
2. concat()方法可以使用任意数量的数组参数。示例：
```javascript
var arr1 = ["Emma", "Isabella"];
var arr2 = ["Jacob", "Michael", "Ethan"];
var arr3 = ["Joshua", "Daniel"];
var myChildren1 = arr1.concat(arr2,arr3);
document.getElementById("demo19").innerHTML = myChildren1;
//结果为Emma,Isabella,Jacob,Michael,Ethan,Joshua,Daniel
```
3. concat()方法也可以将值作为参数。示例：
```javascript
var arri = ["Emma", "Isabella"];
var myChildren2 = arr1.concat(["Jacob", "Michael", "Ethan"]);
document.getElementById("demo20").innerHTML = myChildren2;
//结果为Emma,Isabella,Jacob,Michael,Ethan
```
#### 裁剪数组
1. slice()方法用数组的某个片段切出新数组。示例：
```javascript
var fruits8 = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits8.slice(1);
document.getElementById("demo21").innerHTML = fruits8+"<br/><br/>"+citrus;
//结果为Orange,Lemon,Apple,Mango
```
- slice()方法创建新数组。它不会从原数组中删除任何元素。
2. slice()方法可接受两个参数，比如（1，3），该方法会从开始参数选取元素，直到结束参数（不包含）为止。示例：
```javascript
var fruits9 = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus1 = fruits9.slice(1,3);
document.getElementById("demo22").innerHTML = fruits9+"<br/><br/>"+citrus1;
//结果为Orange,Lemon
```
- 如果结束参数被省略，比如第一个例子，则slice()方法会切出数组的剩余部分。




