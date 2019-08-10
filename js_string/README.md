### 字符串
1. javascript字符串是引号中的零个或多个字符，可以使用单引号或双引号：
```javascript
var carname = "Porsche 911";
var carname = 'Porsche 911';
```
也可以在字符串中使用引号，只要不匹配围绕字符串的引号即可。示例：
```javascript
var answer = "It's good to see you again!";
var answer = "He is called 'Bill";
var answer = 'He is called "Bill"';
```
2. 转义字符（\）<br/>
由于字符串必须由引号包围，js会误解这段字符串：
```javascript
var y = "中国是瓷器的故乡，因此china与"China(中国)"同名。"
```
该字符串将被解析为"中国是瓷器的故乡，因此china与"。<br/>
可用转义字符改为：
```javascript
var y = "中国是瓷器的故乡，因此china与\"China(中国)\"同名。"
```
- 如果字符串中含有\，并要输出，则用\ \ 转义：
```javascript
var x = "字符\\被称为反斜杠。";
```
- 其余情况类似。

3. 字符串换行。
4. 字符串可以是对象
- 通常，js字符串是原始值，通过字面方式创建：
```javascript
var firstName = "Bill";
```
- 但是字符串也可以通过关键词new定义为对象:
```javascript
var firstName = new String("Bill");
```
>不要把字符串创建为对象。它会拖慢执行速度。
- 示例：
```javascript
var x = "Bill"; //typeof x将返回string
var y = new String("Bill");//typeof y 将返回object
```
当使用 == 相等运算符时，相等字符串是相等的（上例中x == y为true）。当使用 === 运算符时，相等字符串是不相等的，因为 === 运算符需要类型和值同时相等（上例中x===y为false，因为x和y的类型不同，x类型是字符串，y类型是对象）。
- 示例:
```javascript
var x = new String("Bill");
var y = new String("Bill");
```
此例中(x===y)为false，因为x和y是不同的对象。
>js对象无法进行对比，比较两个js对象将始终返回false。
### 字符串方法
#### 查找字符串中的字符串。
1. indexOf()方法返回字符串中指定文本首次出现的索引（下标）。示例：
```javascript
var str = "The full name of China is the People's Republic of China.";
var pos = str.indexOf("China");
//pos的值为17。
```
>注意空格也占一个位置。
2. lastIndexOf()方法返回指定文本在字符串中最后一次出现的索引。示例：
```javascript
var str = "The full name of China is the People's Republic of China.";
var pos = str.lastIndexOf("China");
//pos的值为51.
```
- 如果未找到文本，indexOf()和lastIndexOf()均返回-1.
- 两种方法都接受作为检索起始位置的第二个参数。示例：
```javascript
var str = "The full name of China is the People's Republic of China.";
var pos = str.indexOf("China",18);
//pos的值为51
```
>设置第二个参数虽然改变了检索的起始位置，但是计数点没有清0，依然从字符串起点开始计数。
- lastIndexOf()方法向后进行检索（从尾到头），这意味着：假如第二个参数是50，则从位置50开始检索，直到字符串的起点。示例：
```javascript
var str = "The full name of China is the People's Republic of China.";
var pos = str.lastIndexOf("China",50);
//pos返回值为17.
```
>注意检索到之后，依旧从字符串头部开始计数。
#### 检索字符串中的字符串
1. search()方法搜索特定值的字符串，并返回匹配的位置。示例：
```javascript
var str = "The full name of China is the People's Republic of China.";
var pos = str.search("China");
//pos的值为17
```
>注意：search()方法和indexOf()方法是不相等的。
>- 区别一：search()方法无法设置第二个开始位置参数。
>- 区别二：indexOf()方法无法设置更强大的搜索值（正则表达式）。
#### 提取部分字符串
有三种提取部分字符串的方法：
- slice(start,end)
- substring(start,end)
- substr(start,length)
1. slice()方法提取字符串的某个部分并在新字符串中返回被提取的部分。该方法设置两个参数：起始索引（开始位置），终止索引（结束位置）。示例：
```javascript
var str = "Apple,Banana,Mango";
var res = str.slice(7,13);
//res的结果是Banana
```
>注意结束位置13处是逗号，所以结束位置不会被截取到。
- 如果某个参数为负数，则从字符串的结尾开始计数。示例：
```javascript
var str = "Apple, Banana, Mango";
var res = str.slice(-13,-7);
//res的结果是Banana
```
>注意-13的位置处是空格，第一个参数是负值情况下也不会被截取到(计数都从0开始)。
- 如果省略第二个参数，第一个参数为正时则该方法将裁剪字符串的剩余部分。第一个参数为负就从结尾计数。示例：
```javascript
var res = str.slice(7);
var res1 = str.slice(-13);
//res的结果是Banana, Mango
//res1的结果是Banana, Mango
```
>负值位置不适用IE8及其更早版本。
2. substring()方法
- substring()类似于slice()。不同之处在于substring()无法接受负的索引。
3. substr()方法类似于slice().不同之处在于第二个参数规定被提取部分的长度。示例：
```javascript
var str = "Apple, Banana, Mango";
var res = str.substr(7,6);
//res的结果是Banana
```
- 如果省略第二个参数，则该substr()将裁剪字符串的剩余部分（与slice()方法相同）。
- 如果首个参数为负数，则从字符串的结尾计算位置（与slice()方法相同）。
- 第二个参数不能为负，因为它定义的是长度。
#### 替换字符串的内容
replace()方法用于另一个值替换在字符串中指定的值。示例：
```javascript
str = "Please visit Micosoft!";
var n = str.replace("Micosoft","W3School");
```
>replace方法不会改变调用它的字符串。它返回的是新字符串。默认地，replace()只替换首个匹配，并且对大小写敏感。
#### 转换为大写和小写
1. 通过toUpperCase()把字符串转换为大写。示例：
```javascript
var text1 = "Hello World!"; //字符串
var text2 = text1.toUpperCase();
//text1的值不变，text2的值为HELLO WORLD!
```
2. toLowerCase()把字符串转换为小写。
#### concat()方法
concat()连接两个或多个字符串。示例：
```javascript
var text1 = "Hello";
var text2 = "World";
text3 = text1.concat(" ",text2);
//text3的值为Hello World
```
>所有字符串方法都会返回新字符串。它们不会修改原始字符串。正式的说：字符串是不可变的：字符串不能更改，只能替换。
#### String.trim()
trim()方法删除字符串两端的空白符。示例：
#### 提取字符串字符
有两个方法：
- charAt(position)
- charCodeAt(position)
#### 属性访问（Property Access）
#### 把字符串转换为数组
