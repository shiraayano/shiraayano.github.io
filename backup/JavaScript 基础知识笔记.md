
#### 1. 基本操作
+ **alert**：浏览器弹出框，用于显示提示信息。
+ **console.log**：在控制台打印输出，用于调试。
+ **prompt**：浏览器输入框，用于获取用户输入。

#### 示例代码
HTML复制

```html
var myname = 'shiraayano';
var address = '地球村';
var age = 18;
var emial = 'shiraayano@adouzi.eu.org';
console.log(myname, address, age, emial);
```

**解释**：定义了几个变量并使用 `console.log` 打印到控制台。

HTML复制

```html
var myname = prompt("请输入你的姓名");
alert(myname + "欢迎回家");
```

**解释**：通过 `prompt` 获取用户输入的姓名，并通过 `alert` 弹出欢迎信息。

---

#### 2. 变量声明
+ **同时声明多个变量**：可以在一行中声明多个变量，用逗号分隔。
+ **未赋值的变量**：声明但未赋值的变量默认值为 `undefined`。
+ **未声明的变量**：直接使用未声明的变量会报错。
+ **不建议的赋值方式**：未声明直接赋值虽然可以使用，但不建议。

#### 示例代码
HTML复制

```html
// 同时申明多个变量
var age = 18, sex = "男", address = "北京";

var age = 18,
    sex = "男",
    address = "北京";
```

**解释**：展示了两种同时声明多个变量的方式。

HTML复制

```html
// 声明未赋值结果为undefined
var a;
console.log(a);
```

**解释**：声明了一个变量 `a`，但未赋值，打印结果为 `undefined`。

HTML复制

```html
// 不申明不赋值会报错
console.log(b);
```

**解释**：尝试打印未声明的变量 `b`，会导致错误。

HTML复制

```html
// 不声明赋值可以使用，但是不建议
c = 100;
console.log(c);
```

**解释**：未声明直接赋值给变量 `c`，虽然可以使用，但不建议。

---

#### 3. 变量命名规则
+ 变量名必须由字母、数字、下划线、`$`组成，不能以数字开头。
+ 变量名区分大小写。
+ 不能使用关键字和保留字。
+ 变量名应见名知意。
+ 建议使用驼峰命名法（首字母小写，后续单词首字母大写）。
+ 命名规范很重要，例如尽量避免使用 `name` 作为变量名，因为某些浏览器中 `name` 有特殊含义。

#### 示例代码
HTML复制

```html
// 变量命名规则
// 1.变量名必须由字母、数字、下划线、$组成，不能以数字开头
// 2.变量名区分大小写
// 3.不能是关键字和保留字
// 4.变量名要见名知意
// 5.驼峰命名法 首字母小写，后面首字母大写
// 6.命名规范
// 7.变量声明
// var 变量名 = 值;
// var age = 18;
// console.log(age);
// var name = "张三";
// console.log(name);
// 另外，我们尽量不要用name作为变量名，有些浏览器name有含义
```

---

#### 4. 变量交换
+ 通过临时变量可以实现两个变量的值交换。

#### 示例代码
HTML复制

```html
var a;
var b;
var temp;

a = 1;
b = 2;
console.log(a); // 输出 1
console.log(b); // 输出 2

temp = a;
a = b;
b = temp;

console.log(a); // 输出 2
console.log(b); // 输出 1
```

**解释**：通过临时变量 `temp` 实现了 `a` 和 `b` 的值交换。

---

#### 5. 数据类型
+ **JavaScript 是弱类型语言**：变量没有类型，值才有类型。变量的数据类型可以在运行时动态改变。
+ **基本数据类型**：包括数字、字符串、布尔值、`undefined` 和 `null`。
+ **引用数据类型**：后续会详细介绍。

#### 示例代码
HTML复制

```html
// JS中的数据类型
// JS是一种弱类型语言，变量没有类型，值才有类型。只有在运行过程中才能确定类型
// JS是动态语言，变量的数据类型是可以变化的
// 1.基本数据类型
// 2.引用数据类型

// 简单数据类型介绍
// 1.数字类型 number
// 2.字符串类型 string
// 3.布尔类型 boolean
// 4.未定义类型 undefined
// 5.空类型 null
```

---

#### 6. 简单数据类型介绍
+ **数字类型**：包括整数、小数和科学计数法。
+ **字符串类型**：用引号括起来的字符序列。
+ **布尔类型**：只有两个值，`true` 和 `false`。
+ **未定义类型**：变量声明但未赋值时的默认值。
+ **空类型**：表示空值。

#### 示例代码
HTML复制

```html
// 简单数据类型介绍
// 1.数字类型 number
// 2.字符串类型 string
// 3.布尔类型 boolean
// 4.未定义类型 undefined
// 5.空类型 null

// 数字类型 number
// 数字类型包括整数和小数
// 整数
var num1 = 10;
console.log(num1); // 输出 10
// 小数
var num2 = 10.5;
console.log(num2); // 输出 10.5
// 科学计数法
var num3 = 1.23e3;
console.log(num3); // 输出 1230

// 在JS中 以0开头的是八进制
// 以0x开头的是十六进制
var a = 10;
var b = 010;
var c = 0x10;
console.log(a); // 输出 10
console.log(b); // 输出 8
console.log(c); // 输出 16

console.log(Number.MAX_VALUE); // 数字型的最大值
console.log(Number.MIN_VALUE); // 数字型的最小值
console.log(Number.MAX_VALUE * 2); // Infinity
console.log(-Number.MAX_VALUE * 2); // -Infinity
console.log("abc" - 10); // NaN
console.log(isNaN(10)); // false
```

HTML复制

```html
// 字符串型 加了引号都是字符串型 String
var str = "我的名字叫白绫乃";
console.log(str); // 输出 "我的名字叫白绫乃"
// 字符串拼接
var str1 = "我的名字叫";
var str2 = "白绫乃";
console.log(str1 + str2); // 输出 "我的名字叫白绫乃"
```

---

#### 7. 字符串长度
+ 使用 `length` 属性可以获取字符串的长度。

#### 示例代码
HTML复制

```html
// JS中通过length获取字符串长度
var str = "123";
var str1 = "你好";
console.log(str.length); // 输出 3
console.log(str1.length); // 输出 2
```

---

#### 8. 用户交互
+ **prompt**：获取用户输入。
+ **alert**：显示提示信息。

#### 示例代码
HTML复制

```html
var age = prompt("请输入年龄：");
alert("你" + age);
```

**解释**：通过 `prompt` 获取用户输入的年龄，并通过 `alert` 显示。

---

#### 9. 布尔类型
+ 布尔值只有两个值：`true` 和 `false`。
+ 布尔值可以参与运算。

#### 示例代码
HTML复制

```html
var flag = true;
var flag1 = false;
console.log(flag); // 输出 true
console.log(flag + 1); // 输出 2
```

---

#### 10. 类型转换
+ 使用 `typeof` 可以获取变量的类型。
+ `toString()` 和 `String()` 可以将值转换为字符串。
+ `parseInt()` 和 `parseFloat()` 可以将字符串转换为数字。
+ `Number()` 可以将值转换为数字。

#### 示例代码
HTML复制

```html
var num = 1;
console.log(typeof num); // 输出 "number"
num = "hello";
console.log(typeof num); // 输出 "string"

// 字面量
// 字面量：是源代码中一个固定值的表示法，通俗的说，就是字面量表示如何表达这个值。
// 数值字面量：8，9，10
// 字符串字面量：'hello', "world"
// 布尔字面量：true，false

// toString转化为字符串
// String强制转换
var num1 = 10;
console.log(num1.toString()); // 输出 "10"
var num2 = 10;
console.log(typeof num2.toString()); // 输出 "string"
var num3 = 10;
console.log(typeof String(num3)); // 输出 "string"

// parseInt(sring) 转化为整形
// parseFloat(sring) 转化为浮点型
// Number()转化为数值型
// - * / % 也可以将字符串转化为数值型

// 利用Number()函数
var num4 = "10";
console.log(typeof Number(num4)); // 输出 "number"

// 利用parseInt()函数
var num5 = "10.98";
console.log(parseInt(num5)); // 输出 10
var num6 = "10.98";
console.log(parseInt(num6, 10)); // 输出 10
console.log(parseInt("120px")); // 输出 120
```

---

#### 11. 计算年龄
+ 通过用户输入的出生年份计算年龄。

#### 示例代码
HTML复制

```html
var year = prompt("输入出生年份");
var age = 2025 - year; // 隐式转换
alert("您的年龄是" + age + "岁");
```

**解释**：通过 `prompt` 获取用户输入的出生年份，计算当前年龄并显示。

---

#### 12. 布尔类型转换
+ 使用 `Boolean()` 函数可以将值转换为布尔类型。
+ 一些特殊值（如 `0`、`NaN`、`null`、`undefined`、空字符串）会被转换为 `false`，其他值会被转换为 `true`。

#### 示例代码
HTML复制

```html
// 转化为布尔类型
// Boolean()函数
// 代表空、否定的值会被转化为false，如：0，NaN，null，undefined，空字符串
// 其余值都会被转化为true

console.log(Boolean(0)); // 输出 false
console.log(Boolean(NaN)); // 输出 false
console.log(Boolean(null)); // 输出 false
console.log(Boolean(undefined)); // 输出 false
console.log(Boolean(" ")); // 输出 true
console.log(Boolean("hello")); // 输出 true
```



---



#### 1. 运算符
运算符是用于执行特定操作的符号，JavaScript 中常见的运算符包括算术运算符、比较运算符、逻辑运算符和赋值运算符。

##### 1.1 算术运算符
算术运算符用于执行基本的数学运算。

+ `+`：加法运算，也可以用于字符串拼接。
+ `-`：减法运算。
+ `*`：乘法运算。
+ `/`：除法运算。
+ `%`：取余运算。
+ `++`：自增运算符，`++num` 是先加1再运算，`num++` 是先运算再加1。
+ `--`：自减运算符，`--num` 是先减1再运算，`num--` 是先运算再减1。

##### 示例代码
HTML复制

```html
// 算术运算符
console.log(1 + 1); // 2
console.log(5 % 3); // 2
console.log(0.1 + 0.2); // 0.30000000000000004 浮点数精度问题
```

**解释**：展示了基本的算术运算，包括加法、取余和浮点数运算。

HTML复制

```html
// 递增和递减
var num = 10;
console.log(num++); // 10，先输出再加1
console.log(++num); // 12，先加1再输出
console.log(num--); // 12，先输出再减1
console.log(--num); // 10，先减1再输出
```

**解释**：展示了自增和自减运算符的使用，注意它们在表达式中的位置会影响运算结果。

---

##### 1.2 比较运算符
比较运算符用于比较两个值的大小或是否相等。

+ `>`：大于。
+ `<`：小于。
+ `>=`：大于等于。
+ `<=`：小于等于。
+ `==`：等于（只比较值，不比较类型）。
+ `===`：严格等于（既比较值，又比较类型）。
+ `!=`：不等于（只比较值，不比较类型）。
+ `!==`：严格不等于（既比较值，又比较类型）。

##### 示例代码
HTML复制

```html
// 比较运算符
console.log(9 > 10); // false
console.log(10 == '10'); // true
console.log(10 === '10'); // false
```

**解释**：展示了比较运算符的使用，注意 `==` 和 `===` 的区别。

---

##### 1.3 逻辑运算符
逻辑运算符用于组合多个条件。

+ `&&`：逻辑与，两个条件都为真时结果才为真。
+ `||`：逻辑或，两个条件中有一个为真时结果就为真。
+ `!`：逻辑非，对条件取反。

##### 示例代码
HTML复制

```html
// 逻辑运算符
console.log(4 < 5 && 5 < 6); // true
console.log(4 < 5 && 5 > 6); // false
console.log(4 > 5 || 5 < 6); // true
console.log(!true); // false
```

**解释**：展示了逻辑运算符的使用，包括逻辑与、逻辑或和逻辑非。

---

##### 1.4 短路运算
短路运算是逻辑运算符的一个特性，用于优化代码执行。

+ `&&`：如果第一个条件为假，则不会执行第二个条件。
+ `||`：如果第一个条件为真，则不会执行第二个条件。

##### 示例代码
HTML复制

```html
// 短路运算
console.log(4 < 5 && alert("hello1")); // true，第一个为真，执行第二个
console.log(4 > 5 && alert("hello2")); // false，第一个为假，不执行第二个
console.log(4 < 5 || alert("hello3")); // true，第一个为真，不执行第二个
console.log(4 > 5 || alert("hello4")); // false，第一个为假，执行第二个
```

**解释**：展示了短路运算的特性，注意 `alert` 的执行情况。

---

##### 1.5 赋值运算符
赋值运算符用于将值赋给变量。

+ `=`：简单赋值。
+ `+=`：加法赋值。
+ `-=`：减法赋值。
+ `*=`：乘法赋值。
+ `/=`：除法赋值。
+ `%=`：取余赋值。

##### 示例代码
HTML复制

```html
// 赋值运算符
var num = 10;
num += 5; // num = num + 5
console.log(num); // 15
```

**解释**：展示了赋值运算符的使用，可以简化代码。

---

##### 1.6 运算符优先级
运算符优先级决定了表达式中运算的先后顺序。

+ 一元运算符（如 `++`、`--`）优先级最高。
+ 乘除运算优先于加减运算。
+ 括号可以改变运算顺序。
+ 逻辑运算符（如 `&&`、`||`）优先级最低。

---

#### 2. 流程控制
流程控制用于控制代码的执行顺序，包括顺序结构、分支结构和循环结构。

##### 2.1 if 语句
`if` 语句用于根据条件判断执行不同的代码块。

##### 示例代码
HTML复制

```html
// if 语句
if (10 > 5) {
    console.log("10 大于 5");
} else {
    console.log("10 不大于 5");
}
```

**解释**：展示了 `if` 语句的基本用法，根据条件的真假执行不同的代码块。

---

##### 2.2 switch 语句
`switch` 语句用于多分支选择，根据不同的条件执行不同的代码块。

##### 示例代码
HTML复制

```html
// switch 语句
var day = 3;
switch (day) {
    case 1:
        console.log("星期一");
        break;
    case 2:
        console.log("星期二");
        break;
    case 3:
        console.log("星期三");
        break;
    case 4:
        console.log("星期四");
        break;
    case 5:
        console.log("星期五");
        break;
    case 6:
        console.log("星期六");
        break;
    case 7:
        console.log("星期日");
        break;
    default:
        console.log("输入有误");
}
```

**解释**：展示了 `switch` 语句的用法，根据变量的值选择执行不同的代码块。

---

#### 3. 实例应用
##### 3.1 闰年判断
判断一个年份是否为闰年。

##### 示例代码
HTML复制

```html
// 闰年判断
var year = prompt("请输入年份");
if (year % 4 == 0 && year % 100 !== 0 || year % 400 == 0) {
    alert(year + " 是闰年");
} else {
    alert(year + " 不是闰年");
}
```

**解释**：根据闰年的定义（能被4整除但不能被100整除，或者能被400整除），使用 `if` 语句进行判断。

---

##### 3.2 三元表达式
三元表达式是一种简化的条件表达式，格式为 `条件 ? 表达式1 : 表达式2`。

##### 示例代码
HTML复制

```html
// 三元表达式
var age = 18;
var result = age >= 18 ? "成年" : "未成年";
console.log(result);
```

**解释**：根据年龄是否大于等于18，使用三元表达式输出“成年”或“未成年”。

---

好的，我会按照你的要求整理笔记，将代码块拆开，并在代码块外部添加一些解释，同时保持代码和注释的原样，不改变内容顺序。以下是整理后的笔记：

---

### 
#### 1. 循环
循环用于重复执行一段代码，直到满足某个条件为止。JavaScript 中有多种循环结构。

##### 1.1 for 循环
`for` 循环是最常用的循环结构，适用于已知循环次数的情况。

HTML复制

```html
// for循环
// for(初始化变量;条件表达式;操作表达式){
//     循环体
// }
for (var i = 0; i < 5; i++) {
    console.log(i);
}
```

**解释**：`for` 循环初始化一个变量 `i`，在每次循环开始时检查条件 `i < 5`，如果条件为真，则执行循环体，然后执行操作表达式 `i++`。

---

##### 1.2 while 循环
`while` 循环在每次循环开始时检查条件，只有条件为真时才会执行循环体。

HTML复制

```html
// while循环
// while(条件表达式){
//     循环体
// }
var i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

**解释**：`while` 循环在每次循环开始时检查条件 `i < 5`，如果条件为真，则执行循环体并更新变量 `i`。

---

##### 1.3 do...while 循环
`do...while` 循环至少执行一次循环体，然后检查条件，如果条件为真，则继续执行循环。

HTML复制

```html
// do while循环
// do {
//    循环体
// } while(条件表达式)
var i = 1;
do {
    console.log(i);
    i++;
} while (i < 99);
```

**解释**：`do...while` 循环先执行一次循环体，然后检查条件 `i < 99`，如果条件为真，则继续执行循环。

---

#### 2. break 和 continue
+ `**break**`：跳出整个循环。
+ `**continue**`：跳过当前循环的剩余部分，直接进入下一次循环。

---

#### 3. 循环的应用
循环常用于处理数组、计算累加值等场景。

##### 3.1 累加和
HTML复制

```html
// 递加
var sum = 0;
for (var i = 1; i < 10; i++) {
    sum = sum + i;
}
console.log(sum);
```

**解释**：计算从 1 到 9 的累加和。

---

##### 3.2 平均数
HTML复制

```html
// 平均数
sum = 0;
for (var i = 1; i <= 100; i++) {
    sum = sum + i;
}
arg = sum / 100;
console.log(arg);
```

**解释**：计算从 1 到 100 的平均数。

---

##### 3.3 奇偶数和
HTML复制

```html
// 奇偶数和
var sum1 = 0;
var sum2 = 0;
for (var i = 1; i <= 100; i++) {
    if (i % 2 == 0) {
        // 偶数
        sum1 = sum1 + i;
    } else {
        // 奇数
        sum2 = sum2 + i;
    }
}
console.log(sum1); // 偶数和
console.log(sum2); // 奇数和
console.log(sum1 + sum2); // 总和
```

**解释**：分别计算从 1 到 100 的奇数和与偶数和。

---

##### 3.4 被 3 整除的数的和
HTML复制

```html
// 1-100能被3整除的数的和
sum = 0;
for (var i = 1; i <= 100; i++) {
    if (i % 3 == 0) {
        sum = sum + i;
    }
}
console.log(sum);
```

**解释**：计算从 1 到 100 中能被 3 整除的数的和。

---

##### 3.5 九九乘法表
HTML复制

```html
// 九九乘法表
for (var i = 1; i <= 9; i++) {
    for (var j = 1; j <= i; j++) {
        document.write(j + '*' + i + '=' + i * j + ' ');
    }
    document.write('<br>');
}
```

**解释**：使用嵌套循环输出九九乘法表。

---

##### 3.6 心形图案
HTML复制

```html
// 心形图案
var str = '';
for (var i = 1; i <= 9; i++) {
    str = str + '❤';
    console.log(str);
}
```

**解释**：逐行打印心形图案。

---

##### 3.7 倒三角图案
HTML复制

```html
// 倒三角图案
for (var i = 10; i >= 0; i--) {
    var str = '';
    for (var j = i; j >= 0; j--) {
        str = str + '❤';
    }
    console.log(str);
}
```

**解释**：逐行打印倒三角图案。

---

##### 3.8 嵌套循环
HTML复制

```html
// 嵌套循环
for (var i = 1; i <= 9; i++) {
    for (j = 1; j <= i; j++) {
        document.write(j + '*' + i + '=' + i * j + ' ');
    }
    document.write('<br>');
}
```

**解释**：使用嵌套循环输出九九乘法表。

---

#### 4. while 和 do...while 的应用
HTML复制

```html
// while循环
var i = 1;
while (i <= 100) {
    console.log(i);
    i++;
}
```

**解释**：使用 `while` 循环打印从 1 到 100 的数字。

---

HTML复制

```html
// do...while循环
var i = 1;
do {
    console.log(i + '岁了');
    i++;
    if (i == 2) {
        break;
    }
} while (i <= 99);
```

**解释**：使用 `do...while` 循环打印从 1 到 99 的数字，当 `i` 等于 2 时跳出循环。

---

HTML复制

```html
// do...while循环
var i = 1;
do {
    console.log(i + '岁了');
    i++;
    if (i == 2) {
        continue;
    }
} while (i <= 99);
```

**解释**：使用 `do...while` 循环打印从 1 到 99 的数字，当 `i` 等于 2 时跳过当前循环。

---

#### 5. 数组
数组是一种用于存储一组数据的集合。

##### 5.1 创建数组
HTML复制

```html
// 两种创建方式
new Array(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
console.log(arr[0]);
```

**解释**：展示了两种创建数组的方式，并访问数组的第一个元素。

---

##### 5.2 遍历数组
HTML复制

```html
// 遍历数组
for (let index = 0; index < arr.length; index++) {
    const element = arr[index];
    console.log(element);
}
```

**解释**：使用 `for` 循环遍历数组并打印每个元素。

---

HTML复制

```html
// 遍历数组
for (var i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

**解释**：另一种方式使用 `for` 循环遍历数组并打印每个元素。

---

##### 5.3 数组最大值和最小值
HTML复制

```html
// 数组最大值和最小值
var arr = [11, 2, 33, 44, 5, 66, 77];
var max = 0;
for (var i = 0; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
console.log(max);

var min = 999;
for (var i = 0; i < arr.length; i++) {
    if (arr[i] < min) {
        min = arr[i];
    }
}
console.log(min);
```

**解释**：遍历数组，找到最大值和最小值。

---

##### 5.4 数组过滤
HTML复制

```html
// 数组过滤
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var arr1 = [];
for (var i = 0; i < arr.length; i++) {
    if (arr[i] > 10) {
        arr1[arr1.length] = arr[i];
    }
}
console.log(arr1);
```

**解释**：过滤数组中大于 10 的元素。

---

##### 5.5 数组倒序
HTML复制

```html
// 数组倒序
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var arr1 = [];
for (var i = 0; i < arr.length; i++) {
    arr1[arr1.length] = arr[arr.length - i - 1];
}
console.log(arr1);
```

**解释**：将数组倒序存储到另一个数组中。

---

##### 5.6 倒序输出字符串
HTML复制

```html
// 倒序输出字符串
var a = 'index';
for (var i = a.length - 1; i >= 0; i--) {
    console.log(a[i]);
}
```

**解释**：倒序输出字符串的每个字符。

---

##### 5.7 数组去重
HTML复制

```html
// 数组去重
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var arr1 = [];
for (var i = 0; i < arr.length; i++) {
    if (arr1.indexOf(arr[i]) == -1) {
        arr1[arr1.length] = arr[i];
    }
}
console.log(arr1);
```

**解释**：去除数组中的重复元素。

---

##### 5.8 修改数组长度
HTML复制

```html
// 修改数组长度
// JS中数组长度是可变的
arr.length = 10;
// 修改索引号
arr['你好'] = '666';
console.log(arr['你好']);
```

**解释**：修改数组的长度和索引。

---

##### 5.9 冒泡排序
HTML复制

```html
// 冒泡排序
arr = [44, 66, 11, 22, 33];
for (var i = 0; i < arr.length - 1; i++) {
    for (var j = 0; j < arr.length - 1 - i; j++) {
        if (arr[j] > arr[j + 1]) {
            var temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}
```

**解释**：使用冒泡排序对数组进行排序。

---

#### 6. 函数
函数是封装可重复使用的代码块。

##### 6.1 声明函数
HTML复制

```html
// 函数：封装一段可重复使用的代码块
function fn() {
    console.log('hello world');
}
fn();
```

**解释**：声明一个简单的函数并调用它。

---

##### 6.2 函数参数
HTML复制

```html
// 函数接收的实参小于形参 时，形参的值为undefined
function fn(a, b) {
    console.log(a, b);
}
fn(1);
```

**解释**：如果传入的参数少于函数定义的参数，未传入的参数值为 `undefined`。

---

##### 6.3 函数返回值
HTML复制

```html
// 函数没有return 返回值时，返回值为undefined
// return 不仅可以退出循环，还可以返回结果，结束当前函数
```

**解释**：函数如果没有 `return` 语句，默认返回 `undefined`。

---



好的，我会按照你的要求整理笔记，将代码块拆开，并在代码块外部添加一些解释，同时保持代码和注释的原样，不改变内容顺序。以下是整理后的笔记：

---



#### 1. `arguments` 对象
`arguments` 是一个类数组对象，存储了函数调用时传入的所有参数。

HTML复制

```html
// arguments存储了所有实参
// 它是伪数组的形式
function f() {
    console.log(arguments); // 打印所有参数
    console.log(arguments.length); // 打印参数个数
}
f(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
```

**解释**：`arguments` 对象可以用来访问函数调用时传入的所有参数。

---

#### 2. 获取最大值
通过 `arguments` 对象获取传入参数中的最大值。

HTML复制

```html
// 获取最大数
function getMax() {
    var max = arguments[0]; // 先取第一个数
    for (var i = 0; i < arguments.length; i++) {
        if (arguments[i] > max) {
            max = arguments[i];
        }
    }
    return max;
}
console.log(getMax(22, 44, 66, 11)); // 输出 66
```

**解释**：通过遍历 `arguments` 对象，找到最大值并返回。

---

#### 3. 倒序输出字符串
将字符串倒序输出。

HTML复制

```html
// 倒序输出
function fun1() {
    var str = arguments[0];
    var str1 = [];
    for (var i = 0; i < str.length; i++) {
        str1[i] = str[str.length - 1 - i];
    }
    return str1;
}
console.log(fun1("hello")); // 输出 ["o", "l", "l", "e", "h"]
```

**解释**：将字符串的每个字符倒序存储到数组中。

---

#### 4. 冒泡排序
对数组进行冒泡排序。

HTML复制

```html
// 冒泡排序
function fun2() {
    var arr = arguments[0];
    for (var i = 0; i < arr.length; i++) {
        for (var j = 0; j < arr.length - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                var temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}
console.log(fun2([1, 3, 2, 5, 4])); // 输出 [1, 2, 3, 4, 5]
```

**解释**：通过嵌套循环实现冒泡排序，将数组从小到大排序。

---

#### 5. 闰年判断
判断一个年份是否为闰年。

HTML复制

```html
function isRunYear() {
    var year = arguments[0];
    if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
        return true;
    } else {
        return false;
    }
}
console.log(isRunYear(2000)); // 输出 true
```

**解释**：根据闰年的条件（能被4整除但不能被100整除，或者能被400整除）判断一个年份是否为闰年。

---

#### 6. 函数的声明方式
JavaScript 中有两种声明函数的方式。

HTML复制

```html
// 函数的两种声明方式
// 1. function关键字声明
function fn() {
    console.log("hello");
}
fn(); // 正常调用

// 2. 函数表达式声明
var f = function() {
    console.log("hello");
}
f(); // 调用方式 f();
```

**解释**：函数可以通过 `function` 关键字声明，也可以通过函数表达式声明。

---

#### 7. 作用域
作用域决定了变量的可访问范围。

HTML复制

```html
// 全局变量
var num = 10;
console.log(num); // 输出 10

function fun() {
    console.log(num); // 输出 10
}
fun();
```

**解释**：全局变量在全局范围内都可以访问。

HTML复制

```html
// 局部变量
function fun1() {
    var num1 = 20;
    console.log(num1); // 输出 20
}
fun1();
// console.log(num1); // 报错
```

**解释**：局部变量只在函数内部有效，函数外部无法访问。

---

#### 8. 作用域链
在函数内部查找变量时，会先在当前函数作用域中查找，如果找不到，则向上查找，直到全局作用域。

HTML复制

```html
// 作用域链
function fun2() {
    var num2 = 20;
    function fun3() {
        var num3 = 30;
        console.log(num3); // 输出 30
        console.log(num2); // 输出 20
        console.log(num); // 输出 10
    }
    fun3();
}
fun2();
```

**解释**：展示了作用域链的工作方式。

---

#### 9. 预解析
JavaScript 在执行代码之前会进行预解析。

HTML复制

```html
// 预解析
console.log(num1); // 输出 undefined
num1 = 10;
```

**解释**：变量声明会被提升到当前作用域的顶部，但赋值操作不会提升。

HTML复制

```html
// 函数提升
fn(); // 正常调用
function fn() {
    console.log('fn');
}
```

**解释**：函数声明会被提升到当前作用域的顶部，可以直接调用。

---

#### 10. 变量提升和函数提升
JavaScript 中的变量提升和函数提升。

HTML复制

```html
// 变量提升
console.log(num1); // 输出 undefined
var num1;
num1 = 10;
```

**解释**：变量声明会被提升到当前作用域的顶部，但赋值操作不会提升。

HTML复制

```html
// 函数提升
fn(); // 正常调用
function fn() {
    console.log('fn');
}
```

**解释**：函数声明会被提升到当前作用域的顶部，可以直接调用。

---

#### 11. 函数表达式调用
函数表达式调用必须写在函数赋值之后。

HTML复制

```html
// 函数表达式调用
// fn1(); // 报错，fn1 is not a function
var fn1 = function() {
    console.log('fn1');
}
fn1(); // 正常调用
```

**解释**：函数表达式调用必须写在函数赋值之后，否则会报错。

---

1. 变量作用域
变量的作用域决定了变量的可访问范围。
HTML复制
function fun1() {
    var a = b = c = 9; // a 是局部变量，b 和 c 是全局变量
    console.log(a, b, c); // 输出 9 9 9
}
fun1(); // 要执行才会有 b 和 c
// console.log(a); // 报错
console.log(b); // 输出 9
console.log(c); // 输出 9
解释：在函数内部声明的变量 a 是局部变量，而 b 和 c 由于没有使用 var 声明，因此成为全局变量。
2. 对象
对象是一个具体的事物，由属性和方法组成。
2.1 创建对象
JavaScript 提供了多种方式来创建对象。
2.1.1 字面量创建对象
HTML复制
var obj1 = {}; // 创建了一个空的对象
var obj1 = {
    name: 'shiraayano',
    age: 3,
    sex: 'Ta',
    sayHi: function() {
        console.log('hi');
    }
};
console.log(obj1.name); // 输出 shiraayano
console.log(obj1['age']); // 输出 3
obj1.sayHi(); // 调用方法，输出 hi
解释：使用对象字面量方式创建对象，并访问其属性和方法。
2.1.2 使用 new Object 创建对象
HTML复制
var obj2 = new Object();
obj2.name = 'shiraayano';
obj2.age = 6;
obj2.sex = 'Ta';
obj2.sayHi = function() {
    console.log('hi');
};
解释：通过 new Object 创建对象，属性和方法的写法与字面量方式相同。
2.1.3 使用构造函数创建对象
HTML复制
function User(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.sayHi = function() {
        console.log('hi');
    };
}
var u1 = new User('shiraayano', 3, 'Ta');
var u2 = new User('adouzi', 3, 'Ta');
console.log(u1.name); // 输出 shiraayano
解释：通过构造函数创建对象，称为实例化。构造函数中使用 this 指代新创建的对象。
2.2 new 的执行过程
new 关键字在执行时会做以下四件事：
在内存中开辟一块空间。
把 this 指向这块空间。
执行构造函数，给对象添加属性和方法。
返回这个对象（所以构造函数里面不需要 return）。
2.3 遍历对象
使用 for...in 语句遍历对象的属性。
HTML复制
for (var k in u1) {
    console.log(k); // 输出属性名
    console.log(u1[k]); // 输出属性值
}
解释：for...in 语句可以遍历对象的所有可枚举属性。
3. 内置对象
JavaScript 提供了一些内置对象，如 Math、Date、Array、String 等。
3.1 Math 对象
Math 对象提供了数学相关的属性和方法。
HTML复制
console.log(Math.PI); // 输出圆周率
console.log(Math.abs(-1)); // 输出绝对值 1
console.log(Math.max(1, 2, 3, 4, 5)); // 输出最大值 5
console.log(Math.floor(1.9)); // 向下取整，输出 1
console.log(Math.ceil(1.1)); // 向上取整，输出 2
console.log(Math.round(-1.5)); // 四舍五入，输出 -1
console.log(Math.random()); // 输出随机数
解释：Math 对象提供了常用的数学功能，如绝对值、最大值、取整和随机数等。
3.2 Date 对象
Date 对象用于处理日期和时间。
HTML复制
var d = new Date();
console.log(d); // 输出当前日期和时间
console.log(d.getFullYear()); // 输出年份
console.log(d.getMonth()); // 输出月份（0-11）
console.log(d.getDate()); // 输出日期
console.log(d.getDay()); // 输出星期几（0-6）
console.log(d.getHours()); // 输出小时
console.log(d.getMinutes()); // 输出分钟
console.log(d.getSeconds()); // 输出秒数
console.log(d.getTime()); // 输出时间戳
console.log(d.toLocaleDateString()); // 输出本地日期
console.log(d.toLocaleTimeString()); // 输出本地时间
解释：Date 对象提供了获取和设置日期和时间的方法。
3.3 自定义 Math 对象
可以自定义一个对象来封装常用的数学方法。
HTML复制
var mMath = {
    PI: Math.PI,
    max: function() {
        return Math.max.apply(null, arguments);
    },
    min: function() {
        return Math.min.apply(null, arguments);
    },
    pai: function() {
        var arg = Array.prototype.slice.call(arguments);
        for (var i = 0; i < arguments.length; i++) {
            for (var j = 0; j < arguments.length - 1 - i; j++) {
                if (arg[j] > arg[j + 1]) {
                    var temp = arg[j];
                    arg[j] = arg[j + 1];
                    arg[j + 1] = temp;
                }
            }
        }
        return arg;
    }
};
console.log(mMath.pai(66, 1, 2, 3, 4, 5)); // 输出 [1, 2, 3, 4, 5, 66]
解释：自定义了一个 mMath 对象，封装了常用的数学方法。
4. 数组
数组用于存储一组数据。
4.1 创建数组
HTML复制
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var arr1 = new Array(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
var arr2 = new Array(10); // 创建一个长度为10的数组
解释：展示了三种创建数组的方式。
4.2 数组操作
HTML复制
arr.push(11); // 在数组末尾添加元素
console.log(arr); // 输出 [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
arr.unshift(0); // 在数组开头添加元素
console.log(arr); // 输出 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
解释：使用 push 和 unshift 方法向数组中添加元素。
4.3 数组排序
HTML复制
// 升序排序
arr.sort(function(a, b) {
    return a - b;
});
console.log(arr); // 输出 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]

// 降序排序
arr.sort(function(a, b) {
    return b - a;
});
console.log(arr); // 输出 [11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
解释：使用 sort 方法对数组进行升序或降序排序。
4.4 数组去重
HTML复制
var arr1 = [];
for (var i = 0; i < arr.length; i++) {
    if (arr.indexOf(arr[i]) == i) {
        arr1[arr1.length] = arr[i];
    }
}
console.log(arr1); // 输出去重后的数组
解释：通过 indexOf 方法去除数组中的重复项。
5. 字符串
字符串用于存储文本数据。
5.1 字符串不可变
HTML复制
var str = 'andy';
str = 'red';
console.log(str); // 输出 red
解释：字符串是不可变的，每次修改字符串时，实际上是在创建一个新的字符串。
5.2 字符串方法
HTML复制
var str = 'andy';
console.log(str.length); // 输出 4
console.log(str.toUpperCase()); // 输出 ANDY
console.log(str.toLowerCase()); // 输出 andy
解释：字符串提供了多种方法，如获取长度、转换大小写等。
5.3 字符串拼接
HTML复制
var str = 'andy';
console.log(str + 'red'); // 输出 andyred
解释：使用 + 运算符可以拼接字符串。
5.4 字符串查找
HTML复制
var str = '改革春风吹满地,春风吹满地';
console.log(str.indexOf('春', 3)); // 输出 5
解释：使用 indexOf 方法查找字符串中指定内容的位置。
5.5 字符串截取
HTML复制
var str = '改革春风吹满地';
console.log(str.slice(2, 4)); // 输出 春风
console.log(str.substring(2, 4)); // 输出 春风
console.log(str.substr(2, 4)); // 输出 春风地
解释：使用 slice、substring 和 substr 方法截取字符串。
5.6 字符串替换
HTML复制
var str = 'andy';
console.log(str.replace('a', 'A')); // 输出 Andy
解释：使用 replace 方法替换字符串中的指定内容。
5.7 字符串分割
HTML复制
var str = 'red,blue,green';
console.log(str.split(',')); // 输出 ["red", "blue", "green"]
解释：使用 split 方法将字符串分割成数组。
6. 数据类型
JavaScript 中的数据类型分为简单数据类型和复杂数据类型。
6.1 简单数据类型
简单数据类型包括数字、字符串、布尔值等。
HTML复制
var temp = null;
console.log(typeof temp); // 输出 object
解释：null 是一个特殊的简单数据类型，表示空值。
6.2 复杂数据类型
复杂数据类型包括对象、数组等。
HTML复制
var arr = [1, 2, 3];
console.log(arr instanceof Array); // 输出 true
console.log(Array.isArray(arr)); // 输出 true
解释：使用 instanceof 和 Array.isArray 方法检测变量是否为数组。
7. 内存存储
简单数据类型存储在栈中，复杂数据类型存储在堆中。
HTML复制
var str = 'andy';
var obj = { name: 'andy' };
解释：简单数据类型直接存储值，复杂数据类型存储的是地址。


