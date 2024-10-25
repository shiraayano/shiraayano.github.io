
---

### 1. 算术运算符

用于进行基本的数学运算，包括加法、减法、乘法、除法、取模等。不会改变数据类型。

- `+`  加法
- `-`  减法
- `*`  乘法
- `/`  除法
- `%`  取模（返回余数）
- `++` 自增运算符 (`s1++`，值自增1)
- `--` 自减运算符

**示例**：
```java
int m1 = 10;
m1 += 5;  // 等价于 m1 = m1 + 5
System.out.println(m1);  // 输出15
```

**注意**：避免使用逻辑不清的代码，尽量保持表达式简洁明了。

---

### 2. 比较运算符

用于比较两个值的大小，结果为`true`或`false`。

- `==`  等于
- `!=`  不等于
- `>`   大于
- `<`   小于
- `>=`  大于等于
- `<=`  小于等于
- `instanceof` 判断对象是否属于某个类的实例

![image (27)](https://github.com/user-attachments/assets/675207e1-d239-4d39-9f72-acd55c047458)


**注意**：`==`和`!=`也可以用于引用数据类型，比较的是内存地址是否相同。

---

### 3. 逻辑运算符

用于布尔值之间的逻辑操作。

- `&&`  逻辑与（短路与），左右两边均为`true`时返回`true`
- `||`  逻辑或（短路或），左右任一为`true`时返回`true`
- `!`   逻辑非，取反
- `^`   逻辑异或，相同返回`false`，不同返回`true`


![image (29)](https://github.com/user-attachments/assets/b5058dff-bbfd-46cd-95c8-1eac73f40e33)
![image (28)](https://github.com/user-attachments/assets/a56d1186-6c46-4688-bd06-56dc0d275694)


---

### 4. 位运算符

直接操作二进制位。

- `&`  按位与
- `|`  按位或
- `^`  按位异或
- `~`  按位取反
- `<<` 左移，左移一位等同于乘以2
- `>>` 右移，保留符号位
- `>>>` 无符号右移，空位补零

**示例**：
```java
int result = 2 << 3;  // 2*8，结果为16
```

![image (30)](https://github.com/user-attachments/assets/9ed06883-90ed-48ee-93bb-8d5bf9f074fd)


---

### 5. 条件运算符（三元运算符）

用于简化`if-else`语句 `(条件表达式) ? 表达式1 : 表达式2`

**示例**：
```java
int m = 10;
int n = 20;
int max = (m > n) ? m : n;
System.out.println("较大值为：" + max);  // 输出 "较大值为：20"
```

**应用示例**：今天是周二，10天以后是周几
```java
int week = 2;
week += 10;
week %= 7;
System.out.println((week == 0) ? "日" : week);
```

![image (31)](https://github.com/user-attachments/assets/68ef0575-a20a-4b99-8741-ebb041ee73ad)

---

### 6. 赋值运算符

将右边的值赋给左边的变量。

- `=`   赋值
- `+=`  加法赋值
- `-=`  减法赋值
- `*=`  乘法赋值
- `/=`  除法赋值
- `%=`  取模赋值

**示例**：
```java
int m1 = 10;
m1 += 5;  // 等价于 m1 = m1 + 5
```


![image (25)](https://github.com/user-attachments/assets/8bf6b4e4-0e05-4115-a7c5-be7f7aa74574)

![image (26)](https://github.com/user-attachments/assets/3cca9e78-0115-417a-adce-08b4f6bbedc7)




---

### 7. 运算符优先级

运算符有不同的优先级，优先级高的运算符在表达式中先执行。以下是优先级列表（从高到低）：

| 优先级 | 运算符说明       | Java运算符                           |
|--------|-------------------|--------------------------------------|
| 1      | 括号             | `()`、`[]`、`{}`                    |
| 2      | 正负号           | `+`、`-`                            |
| 3      | 单元运算符       | `++`、`--`、`~`、`!`                |
| 4      | 乘法、除法、求余 | `*`、`/`、`%`                       |
| 5      | 加法、减法       | `+`、`-`                            |
| 6      | 移位运算符       | `<<`、`>>`、`>>>`                   |
| 7      | 关系运算符       | `<`、`<=`、`>=`、`>`、`instanceof`  |
| 8      | 等价运算符       | `==`、`!=`                          |
| 9      | 按位与           | `&`                                 |
| 10     | 按位异或         | `^`                                 |
| 11     | 按位或           | `|`                                 |
| 12     | 条件与           | `&&`                                |
| 13     | 条件或           | `||`                                |
| 14     | 三元运算符       | `? :`                               |
| 15     | 赋值运算符       | `=`、`+=`、`-=`、`*=`、`/=`、`%=`    |
| 16     | 位赋值运算符     | `&=`、`|=`、`<<=`、`>>=`、`>>>=`     |

---

**开发建议**：

1. 尽量不要过度依赖运算符优先级，建议使用`()`来控制表达式的执行顺序，确保代码清晰。
2. 避免过于复杂的表达式，如果表达式复杂，建议分步计算以提高可读性。

---

![image (32)](https://github.com/user-attachments/assets/793e581e-d73a-400e-8f43-c2da7ecee065)



---

### Java 流程控制语句

Java 支持顺序结构、分支结构和循环结构，允许程序根据条件执行特定的代码段或重复执行代码。

#### 1. 顺序结构
顺序结构是按代码从上到下顺序执行。

#### 2. 分支结构
Java 提供 `if-else` 和 `switch-case` 来控制分支结构。

- **if-else 语句**
  - 可选 `else if` 语句用于多条件分支。
  - 注意：`if` 后面没有大括号时，仅对下一行有效。

  ```java
  if (条件) {
      // 代码块
  } else {
      // 代码块
  }
  ```

- **switch-case 语句**
  - 适合单一变量多种值的情况。
  - `break` 用于防止 “穿透” 到下一个 case。
  - `default` 处理未匹配的情况。

  ```java
  switch (变量) {
      case 值1:
          // 代码块
          break;
      case 值2:
          // 代码块
          break;
      default:
          // 默认代码块
  }
  ```

#### 3. 循环结构
Java 中有三种循环结构：`for`、`while` 和 `do-while`。

![image (53)](https://github.com/user-attachments/assets/21f04d4e-68ff-49c2-b54a-873aa2be912f)


- **for 循环**
  - 常用于已知次数的循环。

  ```java
  for (初始化; 条件; 更新) {
      // 代码块
  }
  ```

- **while 循环**
  - 条件为真时执行代码块，不满足时停止。

  ```java
  while (条件) {
      // 代码块
  }
  ```

- **do-while 循环**
  - 至少执行一次。

  ```java
  do {
      // 代码块
  } while (条件);
  ```

---

### 示例代码和注意事项

#### 示例1：判断 `if-else` 输出

```java
int x = 4;
int y = 1;
if (x > 2) {
    if (y > 2) 
        System.out.println(x + y);
    System.out.println("atguigu"); // 输出 "atguigu"
} else {
    System.out.println("x is " + x);
}
```

**说明**：`System.out.println(x + y);` 受 `if (y > 2)` 控制，而 `System.out.println("atguigu");` 不受影响。

#### 示例2：赋值和比较的差别

```java
boolean b = true;
if(b = false) // 赋值表达式，不是条件比较
    System.out.println("a");
else if(b)
    System.out.println("b"); // 输出 "b"
```

#### `if-else` 示例：判断输入的正负数

```java
Scanner input = new Scanner(System.in);
int num = input.nextInt();
if (num > 0) {
    System.out.println(num + "是正整数");
} else if (num < 0) {
    System.out.println(num + "是负整数");
} else {
    System.out.println(num + "是零");
}
input.close();
```

#### `switch-case` 示例：星期的英文单词

```java
Scanner input = new Scanner(System.in);
int weekday = input.nextInt();
switch(weekday) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    // ...
    default: System.out.println("输入有误！");
}
input.close();
```

#### 转换字符为大写

```java
char word = 'c';
switch (word) {
    case 'a': System.out.println("A"); break;
    case 'b': System.out.println("B"); break;
    case 'c': System.out.println("C"); break;
    // ...
    default: System.out.println("other");
}
```

---

### 其他小技巧

- **随机数生成**  
  使用 `Math.random()` 生成 0-1 的小数。

  ```java
  int randomNum = (int)(Math.random() * (b - a + 1)) + a;
  ```

- **`break` 和 `continue`**  
  在循环中，`break` 终止循环，`continue` 跳过当前循环。

- **九九乘法表**

  ```java
  for (int i = 1; i <= 9; i++) {
      for (int j = 1; j <= i; j++) {
          System.out.print(j + "*" + i + "=" + i * j + "\t");
      }
      System.out.println();
  }
  ```

- **ATM 菜单**

  ```java
  Scanner scanner = new Scanner(System.in);
  int choice = scanner.nextInt();
  switch (choice) {
      case 1: System.out.println("查询余额"); break;
      case 2: System.out.println("存款"); break;
      case 3: System.out.println("取款"); break;
      case 4: System.out.println("退出"); break;
      default: System.out.println("输入错误，请重新输入");
  }
  scanner.close();
  ```

- **水仙花数**  
  一个水仙花数是三位数，各位数字的立方和等于该数本身。

  ```java
  for (int i = 100; i < 1000; i++) {
      int a = i / 100;
      int b = i / 10 % 10;
      int c = i % 10;
      if (i == a * a * a + b * b * b + c * c * c) {
          System.out.println(i);
      }
  }
  ```

- **寻找 100 以内的素数**

  ```java
  for (int i = 2; i <= 100; i++) {
      boolean isPrime = true;
      for (int j = 2; j <= Math.sqrt(i); j++) {
          if (i % j == 0) {
              isPrime = false;
              break;
          }
      }
      if (isPrime) {
          System.out.println(i);
      }
  }
  ```

---

### Java 流程控制补充说明

#### 1. 分支结构的注意事项

- **赋值与条件判断的区别**  
  `=` 是赋值运算符，`==` 是条件判断，容易混淆。

- **推荐使用 `!` 符号进行布尔值检查**  
  `if (b == false)` 等同于 `if (!b)`，用 `!` 会更简洁。

#### 2. `switch-case` 语句的补充

- **`switch-case` 的变量类型**  
  `switch` 的变量可以是 `int`、`char`、`String` 等类型，不支持 `boolean`。
  
![image (37)](https://github.com/user-attachments/assets/1d50f438-1516-4c98-9b90-80e4ae34a26b)
![image (40)](https://github.com/user-attachments/assets/c4b1aa5f-6231-414a-a47f-7a3f2554ed49)


- **case穿透现象**  
  如果 `case` 语句块中缺少 `break`，程序会继续执行下一个 `case` 语句。

![image (41)](https://github.com/user-attachments/assets/17d463b1-6241-4c68-abdf-6f81d1e7ab13)


![image (38)](https://github.com/user-attachments/assets/8896135e-97cb-4913-bc78-c0f060b16e20)



#### 3. 循环结构的补充

- **`do-while` 循环至少执行一次**  
  因为条件在循环末尾判断，所以循环体在第一次会被执行。

- **`while(true)` 模式**  
  通过 `break` 退出无限循环。

#### 4. 运算符与数据类型

- **运算符**  
  - `==` 用于判断值相等，而 `equals()` 比较引用类型的数据内容相等。

![image (34)](https://github.com/user-attachments/assets/ffccf540-05f0-465d-9841-b6a1a94e8a72)


#### 5. 特殊字符转义

- `\\` 用于反斜杠，`\"` 用于双引号，在字符串中要用 `\` 转义符。

![image (35)](https://github.com/user-attachments/assets/61843f7f-8f25-4142-b780-184e16355776)


#### 6.如何获取一个随机数
1.可以使用java提供的api:Math random();
double d1 = Math.random();
调用后会返回一个0.0-1.0的值


#### 7. (int)(Math.random()*101);
//注意括号 如果int运算random会一直输出0
![image (36)](https://github.com/user-attachments/assets/02132ff5-5f74-426b-86ce-13b58025d1a3)

#### 8.布尔类型不能与其它类型做运算

#### 9.`break` 和 `continue` 

- **`break`**：直接跳出当前整个循环，无论循环条件是否仍为真。常用于条件满足时提前结束循环。
  
  ```java
  for (int i = 0; i < 10; i++) {
      if (i == 5) {
          break; // 当 i == 5 时，跳出循环
      }
      System.out.println(i);
  }
  // 输出：0, 1, 2, 3, 4
  ```

- **`continue`**：跳过当前循环的剩余部分，直接进入下一次循环判断，不终止整个循环。常用于跳过某些不满足条件的情况。

  ```java
  for (int i = 0; i < 10; i++) {
      if (i == 5) {
          continue; // 当 i == 5 时，跳过此循环
      }
      System.out.println(i);
  }
  // 输出：0, 1, 2, 3, 4, 6, 7, 8, 9
  ```

- **`break`** 适合需要在满足某条件时直接结束整个循环的情况。
- **`continue`** 适合在满足某条件时跳过当前循环的执行，继续下一次循环。


![image (42)](https://github.com/user-attachments/assets/6af425a1-9e4f-437a-97fe-af8d065c3542)


在 Java 中，可以使用 `label` 标签配合 `break` 和 `continue` 控制多层嵌套循环的跳出或继续。通过标签指定，可以控制跳出指定的循环层，或继续执行外层的循环。



#### 10.使用 `label` 和 `break`
`break label;` 直接跳出指定标签的循环。

```java
outerLoop: // 定义标签
for (int i = 0; i < 5; i++) {
    for (int j = 0; j < 5; j++) {
        if (i == 2 && j == 2) {
            break outerLoop; // 跳出outerLoop标签的循环
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
// 输出到 i=2, j=1 为止
```

### 使用 `label` 和 `continue`
`continue label;` 直接跳过指定标签的当前循环，继续下一次循环。

```java
outerLoop:
for (int i = 0; i < 5; i++) {
    for (int j = 0; j < 5; j++) {
        if (j == 2) {
            continue outerLoop; // 跳过 outerLoop 循环的当前迭代
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
// 输出会跳过每一行中 j=2 的情况
```

- 标签仅在代码逻辑清晰时使用，否则可能影响代码可读性。
- 使用时，确保标签与循环的层次和逻辑对应。

![image (43)](https://github.com/user-attachments/assets/c65d9e88-b7b4-4a77-bd07-1eb4e9180031)





### Java 数组相关概念

![image (44)](https://github.com/user-attachments/assets/3b4e42cc-2c38-49ff-b3cc-aaca97da92a4)


#### 1. 基本概念
- **数组名**：数组的引用，用于访问数组中的元素。
- **数组元素**：数组中存储的每个数据项。
- **数组下标（角标、索引、index）**：表示元素在数组中的位置，通常从 0 开始。
- **数组长度**：数组中元素的总个数，用 `length` 属性表示。

#### 2. 数组特点
- **数据类型**：数组是引用数据类型，元素可以是基本数据类型，也可以是引用类型。
- **分类**：
  - 按元素类型：基本数据类型的数组、引用数据类型的数组。
  - 按维数：一维数组、二维数组（Java 中没有真正的多维数组，二维数组是数组的数组）。

![image (45)](https://github.com/user-attachments/assets/24fb038b-940c-462c-8a0b-0db14278992f)

![image (46)](https://github.com/user-attachments/assets/6e74f6cf-e5f1-48a3-bf11-9ff967d82429)


#### 3. 一维数组的使用
- **声明与初始化**：
  - 静态初始化：数组声明和元素赋值同时进行。
    ```java
    double[] prices = new double[]{20.32, 111};
    ```
  - 动态初始化：先声明数组，再指定长度。
    ```java
    String[] foods = new String[4];
    ```
- **数组长度不可变**：数组一旦初始化，长度无法修改。
- **内存紧密排列**：数组在内存中连续存储。

![image (47)](https://github.com/user-attachments/assets/5244c1ef-3b70-4edd-9bae-21663726d669)


- **错误示例**：
  - 初始化语法不正确：
    ```java
    int[] arr2 = new int[3]{1, 2, 3}; // 错误
    int[3] arr3 = new int[]; // 错误
    ```

#### 4. 数组越界问题
- 数组下标从 0 开始，到 `length - 1` 结束。
- 数组索引表示相对于起始位置的“偏移量”，第一个元素偏移量为 0。

#### 5. 数组的长度
- 用 `length` 属性表示数组元素的数量。
  ```java
  System.out.println(foods.length);
  ```

#### 6. 数组遍历
- 使用 `for` 循环遍历数组：
  ```java
  for (int i = 0; i < prices.length; i++) {
      System.out.println(prices[i]);
  }
  ```

#### 7. 数组元素的默认值
- 整型：`0`
- 浮点型：`0.0`
- 字符型：`'\u0000'`
- 布尔型：`false`
- 引用类型：`null`

#### 8. 二维数组
- 二维数组可以理解为“一维数组的数组”。
- 二维数组的外层元素存储的是一维数组的地址。
  ```java
  int[][] arr2 = new int[][]{{0, 1}, {1, 2}, {2, 3}};
  ```
![image (49)](https://github.com/user-attachments/assets/95374a6e-1ad0-4ffa-8928-77d1d0b77a92)



![image (48)](https://github.com/user-attachments/assets/abbf4b6c-f5be-488f-9a8b-4a5632a51be5)


#### 9. 数组赋值
- 要求维数相同，类型相同的数组之间可以相互赋值。
![image (50)](https://github.com/user-attachments/assets/793ed5fb-86e2-4bc5-92fa-382f55376e7a)



#### 10. 数组常用算法

- **元素求和**：将所有元素相加。
- **最大值**：
  ```java
  int max = arr[0];
  for (int i = 1; i < arr.length; i++) {
      if (arr[i] > max) {
          max = arr[i];
      }
  }
  ```
- **平均值**：总和除以元素个数。

#### 11. 常见操作

- **数组反转**：将数组元素的顺序倒置。
- **扩容和缩容**：增加或减少数组容量。
- **元素查找**：
  - 顺序查找：遍历数组查找，时间复杂度为 `O(N)`。
  - 二分查找：适用于已排序数组，时间复杂度为 `O(log N)`。

#### 12. 排序算法分类
- **内部排序**：在内存中完成排序。
- **外部排序**：需要将数据暂存到外部存储设备的排序。

### 继续深入 Java 数组的使用与相关算法

#### 13. 数组的反转
数组反转是将数组中元素的顺序进行颠倒的过程，常用的方法是使用一个临时变量来交换元素。以下是实现数组反转的示例代码：

```java
public class ArrayReverse {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        reverseArray(arr);
        
        // 输出反转后的数组
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }

    public static void reverseArray(int[] array) {
        int left = 0;
        int right = array.length - 1;
        while (left < right) {
            // 交换元素
            int temp = array[left];
            array[left] = array[right];
            array[right] = temp;

            left++;
            right--;
        }
    }
}
```

#### 14. 数组的扩容与缩容
在 Java 中，数组的大小一旦定义后就不能改变。如果需要改变数组的大小，通常的方法是创建一个新的数组，并将原数组的元素复制到新数组中。以下是扩容的示例：

```java
public class ArrayResize {
    public static void main(String[] args) {
        int[] originalArray = {1, 2, 3};
        int[] newArray = resizeArray(originalArray, 5);

        // 输出扩容后的数组
        for (int num : newArray) {
            System.out.print(num + " ");
        }
    }

    public static int[] resizeArray(int[] oldArray, int newSize) {
        int[] newArray = new int[newSize];
        for (int i = 0; i < oldArray.length && i < newArray.length; i++) {
            newArray[i] = oldArray[i];
        }
        return newArray;
    }
}
```

#### 15. 数组元素的查找
- **顺序查找**：
  顺序查找是从数组的第一个元素开始，逐个比较，直到找到目标元素或到达数组末尾。

```java
public class SequentialSearch {
    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40, 50};
        int target = 30;
        int index = sequentialSearch(arr, target);

        if (index != -1) {
            System.out.println("Element found at index: " + index);
        } else {
            System.out.println("Element not found.");
        }
    }

    public static int sequentialSearch(int[] array, int target) {
        for (int i = 0; i < array.length; i++) {
            if (array[i] == target) {
                return i; // 返回找到的下标
            }
        }
        return -1; // 返回 -1 表示未找到
    }
}
```

- **二分查找**：
  二分查找适用于已排序的数组，它通过不断将查找区间缩小一半来寻找目标元素，效率较高。

```java
public class BinarySearch {
    public static void main(String[] args) {
        int[] sortedArray = {10, 20, 30, 40, 50};
        int target = 30;
        int index = binarySearch(sortedArray, target);

        if (index != -1) {
            System.out.println("Element found at index: " + index);
        } else {
            System.out.println("Element not found.");
        }
    }

    public static int binarySearch(int[] array, int target) {
        int left = 0;
        int right = array.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2; // 防止溢出
            if (array[mid] == target) {
                return mid; // 找到目标元素
            } else if (array[mid] < target) {
                left = mid + 1; // 目标在右半边
            } else {
                right = mid - 1; // 目标在左半边
            }
        }
        return -1; // 返回 -1 表示未找到
    }
}
```

#### 16. 数组的排序算法
- **冒泡排序**：每次比较相邻的元素，将较大的元素“冒泡”到数组的末尾。

```java
public class BubbleSort {
    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2};
        bubbleSort(arr);

        // 输出排序后的数组
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }

    public static void bubbleSort(int[] array) {
        int n = array.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (array[j] > array[j + 1]) {
                    // 交换
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                }
            }
        }
    }
}
```

- **选择排序**：每一轮选择最小（或最大）的元素放到已排序的序列中。

```java
public class SelectionSort {
    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2};
        selectionSort(arr);

        // 输出排序后的数组
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }

    public static void selectionSort(int[] array) {
        int n = array.length;
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (array[j] < array[minIndex]) {
                    minIndex = j; // 找到最小元素的索引
                }
            }
            // 交换
            int temp = array[minIndex];
            array[minIndex] = array[i];
            array[i] = temp;
        }
    }
}
```

#### 17. 衡量算法优劣
- **时间复杂度**：描述算法执行所需时间的数量级，常用符号表示法（如 O(N)、O(log N)、O(N^2) 等）。
- **空间复杂度**：描述算法在执行过程中所需存储空间的数量级。
- **稳定性**：对于相等的元素，排序算法是否保持它们的原始顺序。

![image (51)](https://github.com/user-attachments/assets/031542a1-2328-47c1-910c-73a9b1b9359b)
![image (52)](https://github.com/user-attachments/assets/8abaf9d8-b9a0-41ca-8c9f-e867ba5bff68)

### Java 数组的常见异常

在 Java 中，操作数组时可能会遇到各种异常。以下是一些常见的数组异常及其描述：

1. **`ArrayIndexOutOfBoundsException`**：
   - **描述**：当尝试访问数组的索引超出其有效范围时，抛出此异常。例如，访问一个长度为 5 的数组的第 6 个元素（索引为 5）。
   - **示例**：
   ```java
   int[] array = new int[5];
   System.out.println(array[5]); // 会抛出 ArrayIndexOutOfBoundsException
   ```

2. **`NullPointerException`**：
   - **描述**：当尝试在未初始化的数组上执行操作时，抛出此异常。例如，尝试访问或修改一个尚未被分配内存空间的数组的元素。
   - **示例**：
   ```java
   int[] array = null;
   System.out.println(array[0]); // 会抛出 NullPointerException
   ```

3. **`NegativeArraySizeException`**：
   - **描述**：当创建数组时，如果指定的数组大小为负数，会抛出此异常。
   - **示例**：
   ```java
   int[] array = new int[-1]; // 会抛出 NegativeArraySizeException
   ```

4. **`ArrayStoreException`**：
   - **描述**：当尝试将不兼容类型的元素赋值给数组时，会抛出此异常。例如，尝试将一个 `String` 对象赋值给一个 `Integer` 类型的数组。
   - **示例**：
   ```java
   Integer[] array = new Integer[10];
   array[0] = "Hello"; // 会抛出 ArrayStoreException
   ```

5. **`ClassCastException`**：
   - **描述**：当尝试将一个对象强制转换为不兼容的类型时，抛出此异常。虽然这通常不是数组特有的，但在处理多维数组或数组的数组时可能会遇到。
   - **示例**：
   ```java
   Object[] objects = new Object[10];
   objects[0] = new Integer(1);
   String str = (String) objects[0]; // 会抛出 ClassCastException
   ```

6. **`IllegalArgumentException`**：
   - **描述**：当传递给方法的参数不合法时，可能会抛出此异常。虽然不是专门针对数组的，但在使用数组作为参数的方法中可能会遇到。
   - **示例**：
   ```java
   public void processArray(int[] array) {
       if (array == null) {
           throw new IllegalArgumentException("Array cannot be null");
       }
   }
   ```

### 数组的概念与使用

数组可以理解为多个数据的组合，是程序中的一种容器，用于存储同一类型的数据。

#### 1. 一维数组的使用（重要）

- **数组的声明和初始化**：
  ```java
  int[] arr = new int[10]; // 声明一个长度为10的整型数组
  String[] arr1 = new String[]{"tom", "jerry"}; // 初始化一个字符串数组
  ```

- **调用数组的指定元素**：
  - 使用角标（索引）访问元素，索引从 0 开始。
  ```java
  System.out.println(arr[0]); // 访问数组的第一个元素
  ```

- **数组的属性**：
  - `length` 属性：表示数组的长度。
  ```java
  System.out.println(arr.length); // 输出数组的长度
  ```

- **数组的遍历**：
  ```java
  for (int i = 0; i < arr.length; i++) {
      System.out.println(arr[i]); // 遍历输出数组的每个元素
  }
  ```

- **数组元素的默认初始化值**：
  - 整型数组的默认值为 0，浮点数组为 0.0，字符数组为 `'\u0000'`，布尔数组为 `false`，引用数据类型数组为 `null`。

#### 2. 一维数组的内存解析（难点）

- **内存结构**：
  - 在 `main()` 方法中声明变量：`int[] arr = new int[]{1, 2, 3};`
  - **虚拟机栈**：`main()` 作为一个栈帧，压入栈空间中。在 `main()` 栈帧中，存储着 `arr` 变量，`arr` 记录着数组实体的首地址值。
  - **堆**：数组的元素存储在堆空间中。

#### 3. 二维数组的使用（难点）

- **声明与初始化**：
  - 二维数组可以看作是数组的数组。以下是二维数组的声明和初始化：
  ```java
  int[][] arr2 = new int[3][4]; // 声明一个3行4列的二维数组
  int[][] arr3 = {{1, 2}, {3, 4}}; // 静态初始化
  ```

- **访问元素**：
  - 通过两个索引访问二维数组的元素，第一个索引表示行，第二个索引表示列。
  ```java
  System.out.println(arr3[1][0]); // 输出第二行第一列的元素
  ```

- **遍历二维数组**：
  ```java
  for (int i = 0; i < arr2.length; i++) { // 遍历行
      for (int j = 0; j < arr2[i].length; j++) { // 遍历列
          System.out.print(arr2[i][j] + " "); // 输出每个元素
      }
      System.out.println(); // 换行
  }
  ```

- **内存结构**：
  - 二维数组在内存中并不一定是连续存储的。每一行的数组可能存储在不同的内存位置。
