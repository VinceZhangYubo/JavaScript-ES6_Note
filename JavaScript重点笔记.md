

# JavaScript重点笔记

## JS数据类型与运算

### 变量数据类型

- 基本数据类型（值类型）：String 字符串、Number 数值、Boolean 布尔值、Null 空值、Undefined 未定义。

- 引用数据类型（对象类型）：Object 对象、Date日期、Array数组。
  注意：内置对象 Function、Array、Date、RegExp、Error等都是属于 Object 类型。也就是说，除了那五种基本数据类型之外，其他的，都称之为 Object类型。

数据类型之间最大的区别：

- 基本数据类型：参数赋值的时候，传数值

- 引用数据类型：参数赋值的时候，**传地址**（修改的同一片内存空间）

注意：

-  NaN 的数据类型是数值，NaN 属于 JavaScript 保留词，指示某个数不是合法数

- JS中的数值类型始终是64位浮点数，整数（不使用指数或科学计数法）会被精确到 15 位

- JavaScript 从左向右进行编译，计算遵循依左计算。String+Number转换为String，+是连字符，Number+String转换为Number，+是加号，而- * /运算都能隐式转换为Number进行计算
- 对象不能用==进行判断，即使结构都相同但是不同对象
- 如果符号两侧的值都是字符串时，不会将其转换为数字进行比较。比较两个字符串时，比较的是字符串的Unicode编码。比较字符编码时，是一位一位进行比较。如果两位一样，则比较下一位。

### 栈内存和堆运存

JS中，所有的变量都是保存在栈内存中的。

基本数据类型：基本数据类型的值，直接保存在栈内存中。值与值之间是独立存在，修改一个变量不会影响其他的变量。字符串里面的值不可被改变。虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间。

引用数据类型：对象是保存到堆内存中的。每创建一个新的对象，就会在堆内存中开辟出一个新的空间；而变量保存了对象的内存地址（对象的引用），保存在栈内存当中。如果两个变量保存了同一个对象的引用，当一个通过一个变量修改属性时，另一个也会受到影响。

### Null和Undefined

null 虽然是一个单独的数据类型，但null 相当于是一个 object， 只不过地址为空（空指针）而已。null 和 undefined 有很大的相似性。 `null == undefined` 的结果为 `true` ，但是 `null === undefined` 的结果是 false。它们虽然相似，但还是有区别，和数字运算时，10 + null 结果为 10，10 + undefined 结果为 NaN。

- null 的typeof数据类型是对象 
- 未定义变量和尚未赋值的变量的数据类型是 **undefined** 
-  任何数据类型和 undefined 运算都是 NaN; 任何值和 null 运算，null 可看做 0 运算。 

### 变量类型转换

**显式类型转换** 

sth.toString()     String(sth)     Number(sth)     parseInt(string, n)：将string看成n进制并转换为整数     parseFloat(string)     Boolean() 

- Number()尽量转，parseInt()只看第一位是否数字，无四舍五入，转不了NaN
- `val = Bolean(sth)  sth === '0', {}, [];  val === true;` `sth = 0, NaN, '', null, undefined; val === false;`

**隐式类型转换** 

isNaN ()     自增/自减运算符： `++` 、 `--`     正号/负号： `+a` 、` -a`     加号： `+`      运算符： `- 、 * 、 /`

### 运算符

**连加**：`b = ++a`:先加加再赋值；`b = a++`:先赋值再加加

**非Bull值的与或运算**：为了做容错和兜底处理

```javascript
//用变量a来接收result里面的图片，能拿到result.data.imgUrl就用，拿不到用兜底图片
if (result.resultCode == 0) {
	var a = result && result.data && result.data.imgUrl ||'http://img.smyhvae.com/20160401_01.jpg';
}
```

### 基本包装类型

new String()    new Number()    new Boolean()

Boolean包装类型对象判断都是不相等，因为都是对象；且不能当作判断条件，都存在对象所以判断都是ture。

基本包装类型的作用：

当我们对一些基本数据类型的值去调用属性和方法时，浏览器会临时使用包装类将基本数据类型转换为引用数据类型，这样的话，基本数据类型就有了属性和方法，然后再调用对象的属性和方法；调用完以后，再将其转换为基本数据类型。例如在底层，字符串是以字符数组的形式保存的。

## JS方法

### 原生输出方法

`alert('输出')`：警告

`result = confirm('请确认')`：确认框

`getValue = prompt('请输入....')`：弹出输入框

### 数字方法

`toFixed()`：小数，返回的是**字符串

| 方法              | 描述                                       |
| :---------------- | :----------------------------------------- |
| Math.PI           | 圆周率                                     |
| Math.abs()        | **返回绝对值**                             |
| Math.random()     | 生成0-1之间的**随机浮点数**                |
| Math.floor()      | **向下取整**（往小取值）                   |
| Math.ceil()       | **向上取整**（往大取值）                   |
| Math.round()      | 四舍五入取整（正数四舍五入，负数五舍六入） |
| Math.max(x, y, z) | 返回多个数中的最大值                       |
| Math.min(x, y, z) | 返回多个数中的最小值                       |
| Math.pow(x,y)     | 乘方：返回 x 的 y 次幂                     |
| Math.sqrt()       | 开方：对一个数进行开方运算                 |

`num.toString(param)`：param参数可以指定几进制

```javascript
Math.floor(Math.random()*(max-min) + min)   //生成[min,max)之间的随机数
Math.floor(Math.random()*(max-min+1))+min   //生成[min,max]之间的随机数
```

### 字符串方法

**字符串的所有方法都不会改变原字符串，只会返回一个新的字符串。**

```javascript
//查
resultIndex = IndexOf('String', 开始索引位置)
resultIndex = lastIndexOf('String', 开始索引位置) //从后向前查
search('String') or search(Regexp) //查位置，返回索引位置，不存在-1
isExist = String.includes('a',开始索引位置) //String中是否存在字符串‘a’，返回boolean
startsWith()
endsWith()
str[index]  = chartAt(index)
chartCodeAt(index)：返回Unicode编码（0-127英文）
fromCharCode(Unicode)：返回字符

slice(startIndex, endIndex)//截取片段，原字符串不变，包左不包右[s,e)
substring(startIndex, endIndex)//截取，参数不为负
substr(startIndex, length)//截取长度为length的字符
array1.concat(array2)//拼接,= array1+array2

split(分隔符): 字符串划分为数组

replace(被替换字符串，新字符串)：只替换第一个匹配，全替换用正则

str.repeat(2) //strstr
trim()//去掉两侧空白
toUpperCase()
toLowerCase()

//用UTF-8替换无效或不可识别的字符
encodeURIComponent();   //把字符串作为 URI 组件进行编码，让浏览器可以理解
decodeURIComponent();   //把字符串作为 URI 组件进行解码
```

### Date方法

| 方法名        | 含义                                    |
| ------------- | --------------------------------------- |
| new Date()    | 没参数获取当前时间                      |
| getFullYear() | 获取年份                                |
| getMonth()    | 获取月： 0-11，**0代表1月**             |
| getDate()     | 获取日：1-31                            |
| getDay()      | 获取星期：0-6，**0代表周日，1代表周一** |
| getHours()    | 获取小时：0-23                          |
| getMinutes()  | 获取分钟：0-59                          |
| getSeconds()  | 获取秒：0-59获取毫秒                    |

格式化年月日

```javascript
/*
方法：日期格式化。
格式要求：今年是：2020年02月02日 08:57:09 星期日
*/
function formatDate() {
	var date = new Date();
	var year = date.getFullYear(); // 年
	var month = date.getMonth() + 1; // 月
	var day = date.getDate(); // 日
	var week = date.getDay(); // 星期几
	var weekArr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
	var hour = date.getHours(); // 时
	hour = hour < 10 ? '0' + hour : hour; // 如果只有一位，则前面补零
	var minute = date.getMinutes(); // 分
	minute = minute < 10 ? '0' + minute : minute; // 如果只有一位，则前面补零
	var second = date.getSeconds(); // 秒
	second = second < 10 ? '0' + second : second; // 如果只有一位，则前面补零
	var result = '今天是：' + year + '年' + month + '月' + day + '日 ' + hour + ':'
	+ minute + ':' + second + ' ' + weekArr[week];
	return result;
}

//获取时间戳
const timeStamp = new Date().getTime()     
const timeStamp = +new Date()

time.format('yyyy-mm-dd')

moment.js
```

### 数组方法

**数组增删**

| 方法                           | 描述                                                         | 备注               |
| ------------------------------ | ------------------------------------------------------------ | ------------------ |
| new Array(参数)                | 参数为空，创建一个空数组；参数一个数值，表示数组的长度；有多个参数，表示数组中的元素 |                    |
| push()                         | 向数组的最后面插入一个或多个元素，返回结果为**新数组的长度** | 会改变原数组       |
| pop()                          | 删除数组中的最后一个元素，返回结果为**被删除的元素**         | 会改变原数组       |
| unshift()                      | 在数组最前面插入一个或多个元素，返回结果为新数组的长度       | 会改变原数组       |
| shift()                        | 删除数组中的第一个元素，返回结果为被删除的元素               | 会改变原数组       |
| slice(startIndex,endIndex)     | 从数组中提取指定的一个或多个元素，返回结果为新的数组，包前不包后[start, end) | **不会改变原数组** |
| splice(index, number, array[]) | 从数组中删除指定index位置的number个元素并在后面添加array，返回结果为组成的新数组 | 会改变原数组       |
| fill()                         | 填充数组：用固定的值填充数组，返回结果为新的数组             | 会改变原数组       |

**排序合拆**

| 方法名                | 含义                                      |
| --------------------- | ----------------------------------------- |
| array1.concat(array2) | 合并数组，不改变原数组                    |
| join(连字符)          | 将数组转化为字符串                        |
| reverse()             | 翻转数组，返回翻转后的数组，会改变数组    |
| sort()                | 按照Unicode编码从小到大排序，会改变原数组 |

合并数组也可以用展开语法，例：

```javascript
const arr1 = [1, 2, 3]
const result = [a, b, c, ...arr1]     //result = [a, b, c, 1, 2, 3] 
```

数字排序：

```javascript
let result = arr.sort((a,b)=>{return a-b}) //升序排序，基础实现方法为冒泡排序
```

**查找数组**

| 方法                                                      | 描述                                                         | 备注         |
| :-------------------------------------------------------- | :----------------------------------------------------------- | :----------- |
| indexOf(value)                                            | 从前往后索引，检索一个数组中是否含有指定的元素               |              |
| lastIndexOf(value)                                        | 从后往前索引，检索一个数组中是否含有指定的元素               |              |
| includes(item)                                            | 数组中是否包含指定的内容，返回boolean类型                    |              |
| find((item,index)=>{... ...return true})                  | 找出**第一个**满足「指定条件返回 true」的元素                |              |
| findIndex((item,index)=>{... ... return true})            | 找出**第一个**满足「指定条件返回 true」的元素的 index        |              |
| every((item,index)=>{if(...){return false}  return true}) | 确保数组中的每个元素都满足「指定条件返回 true」，则停止遍历，此方法才返回 true | 全真才为true |
| some()                                                    | 数组中只要有一个元素满足「指定条件返回 true」，则停止遍历，此方法就返回 true | 一真即true   |

**遍历数组**

| 方法                 | 描述                                                         | 备注                                                     |
| :------------------- | :----------------------------------------------------------- | :------------------------------------------------------- |
| for (index in array) | for in，循环的是Index，主要用来遍历对象属性                  | for key in Object                                        |
| for(item of array)   | for of，循环的是item                                         |                                                          |
| forEach()            | 和 for 循环类似，但需要兼容 IE8 以上                         | forEach() 没有返回值。也就是说，它的返回值是 undefined   |
| map()                | 对原数组中的每一项进行加工，将组成新的数组                   | **不会改变原数组**，如果修改对象数组的属性也会修改原数组 |
| filter()             | 过滤数组：返回结果是 true 的项，将组成新的数组，返回结果为**新的数组** | 不会改变原数组                                           |
| reduce()             | 接收一个函数作为累加器，返回值是回调函数累计处理的结果       |                                                          |

**forEach()不能修改数组元素是基本数据类型的数组，可以修改对象数组里面的属性。如果在遍历数组的同时想修改数组最好使用map()**

```javascript
//preV和item必填,initV可替代初始的preV，item为arr里的值
arr.reduce((previousValue,item, index, arr)=>{
	//进行处理
    return value //在下次循环作为preV使用
}, initialValue)
```

函数中的`arguments`代表实参，是一个伪数组，`arguments.callee`返回正在执行的函数，返回的是这个函数对象。

## 作用域、this和闭包

JS只提升声明，不提升赋值。一切声明的全局变量都是windows的属性。let和const不能提升。

### this

JavaScript **this** 关键词指的是它所属的对象。

- 单独的情况下，this 指的是全局对象。
- 在函数中，this 指的是全局对象。严格模式下，this 是 undefined。
- 在对象的方法中，this 指的是所有者对象。
- 在事件中，this 指的是接收事件的元素。
- 像 call() 和 apply() 这样的方法可以将 this 引用到任何对象
- 箭头函数会继承外层函数调用的this绑定（无论this绑定到什么）
- 构造函数形式调用时，this是新创建的实例对象

箭头函数没有自己的 this。它们不适合定义对象方法。

箭头函数未被提升。它们必须在使用前进行定义。

**改变函数this指向函数**

- function1.call(想要this指向的地方, 函数实参1, 函数实参2)    //将this指向改变，传参1和2到function1并调用执行，可实现继承
- function2.apply(想要this指向的地方, [])
- newFun = function3.bind(想要绑定的this指向,实参1...)    //用的最多，bind不会调用function3，但返回修改this指向和指定实参的新函数

### 闭包

闭包：有权访问另一个函数作用域中变量的函数。作用就是延伸变量的作用范围。

```javascript
function fn1() {
	let a = 20;
	return function() {
		console.log(a)
	}
}
const foo = fn1();
foo();
```

foo 代表的就是整个 fn1里return的函数。当执行了 foo() 语句之后，fn1 函数内就产生了闭包。 一般来说，在 fn1 函数执行完毕后，它里面的变量 a 会立即销毁。但此时由于产生了闭包，所以 fn1 函 数中的变量 a 不会立即销毁，因为 fn2 函数还要继续调用变量 a。只有等所有函数把变量 a 调用完了， 变量 a 才会销毁。 而且，可以看出， 在执行 foo() 语句之后，竟然能够打印出 20 ，这就完美通过闭包实现了：全局作用域成功访问到了局部作用域中的变量 a。

### 对象的深拷贝和浅拷贝

- 浅拷贝：只拷贝引用，拷贝传址而非传值
- 深拷贝：会把对象里所有的数据重新复制到新的内存空间，是最彻底的拷贝。

**浅拷贝1：for in**

```javascript
let obj1 = {
	name: 'name1',
	desc: {
		descId: 6,
		descDetail: 'acccccccccc'
	}
}
const obj2 = {}
for (let key in obj1){
    obj2[key] = obj1[key]
}
```

obj1的name是基础属性，所以赋值给obj2时存放到新的堆内存地址中，修改obj1的name，obj2的name不会受影响；但obj1的desc传给obj2时传的是属性desc的地址，修改obj1的desc里的属性，obj2会受到影响一同改变。

**浅拷贝2： Object.assgin()   常用**

```javascript
// 语法1
obj2 = Object.assgin({}, obj1);
obj2 = Object.assgin(obj2, obj1); //obj2中如果有属性和obj1同名，则会被obj1覆盖
// 语法2
Object.assign(obj2, obj1,obj3); //将obj1和obj3合并赋值给obj2
```

**深拷贝：for in递归**

```javascript
let obj1 = {
    name: 'qianguyihao',
    age: 28,
    info: {
    	desc: 'hello',
    },
    color: ['red', 'blue', 'green'],
};
let obj2 = {};
deepCopy(obj2, obj1);
console.log(obj2);
obj1.info.desc = 'github';
console.log(obj2);
// 方法：深拷贝
function deepCopy(newObj, oldObj) {
    for (let key in oldObj) {
        // 获取属性值 oldObj[key]
        let item = oldObj[key];
        // 判断这个值是否是数组
        if (item instanceof Array) {
            newObj[key] = [];
            deepCopy(newObj[key], item);
        } else if (item instanceof Object) {
            // 判断这个值是否是对象
            newObj[key] = {};
            deepCopy(newObj[key], item);
        } else {
            // 简单数据类型，直接赋值
            newObj[key] = item;
        }
    }
}

```

### 原型链和原型继承



### 类和构造继承



## 其他

### JSON

JSON：JavaScript Object Notation（JavaScript 对象表示形式）。 JSON 和对象字面量的区别：JSON 的属性必须用双引号引号引起来，对象字面量可以省略。json里一般放常量、数组、对象等，但很少放 function。另外，对象和 json 没有长度，json.length 的打印结果是 undefined。于是乎，自然也就不能直接用 for 循环遍历（因为遍历时需要获取长度 length）。 json 遍历的方法： json 采用 for key in JSON 进行遍历。

### 正则表达式

```javascript
//写法1
var reg = new RegExp("正则表达式", "匹配模式"); // 注意，两个参数都是字符串，匹配模式可不传
//写法2
var reg = /正则表达式/匹配模式
reg.test(str) //判断str是否符合reg的正则表达式规则	

//匹配模式：i(不区分大小写), g(全局匹配)，全局匹配不用test()，返回的lastIndex置为找到的位置，继续test往下找
```

**正则表达式符号**

```xml
/[ab]/：等于/a|b/，a或b
/[a-z]/ ：检查一个字符串那种是否包含任意小写字母
/[A-Z]/ ：任意大写字母
/[A-z]/ ：任意字母
/[0-9]/ ：任意数字
/a[bde]c/ ：检查一个字符串中是否包含 abc 或 adc 或 aec
/[^]/：除了
/[^ab]/：除了ab是否还有其他
/[^0-9]/：除了数字是否还有其他
/^1/：以1开头
```

```javascript
//去掉字符串开头和结尾空格
str = str.replace(/^\s*|\s*$/g,"")
//判断是否为电子邮箱
var emailReg = /^\w{3,}(\.\w+)*@[A-z0-9]+(\.[A-z]{2,5}){1,2}$/;
```

### DOM API

### Ajax



## ES6



### JavaScript性能——加速网页加载



[JavaScript 性能 (w3school.com.cn)](https://www.w3school.com.cn/js/js_performance.asp)



- 减少循环中的活动

- 减少DOM访问

- 缩减DOM规模

- 避免不必要的不打算储存的变量

- 延迟JavaScript加载，把脚本放在页面底部

- 避免使用with