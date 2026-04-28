
### 2.2 StringBuilder、StringBuffer的API
StringBuilder、StringBuffer的API是完全一致的，并且很多方法与String相同。

**1、常用API**

（1）StringBuffer append(xx)：提供了很多的append()方法，用于进行字符串追加的方式拼接  
（2）StringBuffer delete(int start, int end)：删除[start,end)之间字符  
（3）StringBuffer deleteCharAt(int index)：删除[index]位置字符  
（4）StringBuffer replace(int start, int end, String str)：替换[start,end)范围的字符序列为str  
（5）void setCharAt(int index, char c)：替换[index]位置字符  
（6）char charAt(int index)：查找指定index位置上的字符  
（7）StringBuffer insert(int index, xx)：在[index]位置插入xx  
（8）int length()：返回存储的字符数据的长度  
（9）StringBuffer reverse()：反转

> + 当append和insert时，如果原来value数组长度不够，可扩容。
> + 如上(1)(2)(3)(4)(9)这些方法支持`方法链操作`。原理： ![](images/image-20220405223542750.png)
>

**2、其它API**

（1）int indexOf(String str)：在当前字符序列中查询str的第一次出现下标  
（2）int indexOf(String str, int fromIndex)：在当前字符序列[fromIndex,最后]中查询str的第一次出现下标  
（3）int lastIndexOf(String str)：在当前字符序列中查询str的最后一次出现下标  
（4）int lastIndexOf(String str, int fromIndex)：在当前字符序列[fromIndex,最后]中查询str的最后一次出现下标  
（5）String substring(int start)：截取当前字符序列[start,最后]  
（6）String substring(int start, int end)：截取当前字符序列[start,end)  
（7）String toString()：返回此序列中数据的字符串表示形式  
（8）void setLength(int newLength) ：设置当前字符序列长度为newLength

```java
@Test
public void test1(){
    StringBuilder s = new StringBuilder();
    s.append("hello").append(true).append('a').append(12).append("atguigu");
    System.out.println(s);
    System.out.println(s.length());
}

@Test
public void test2(){
    StringBuilder s = new StringBuilder("helloworld");
    s.insert(5, "java");
    s.insert(5, "chailinyan");
    System.out.println(s);
}

@Test
public void test3(){
    StringBuilder s = new StringBuilder("helloworld");
    s.delete(1, 3);
    s.deleteCharAt(4);
    System.out.println(s);
}
@Test
public void test4(){
    StringBuilder s = new StringBuilder("helloworld");
    s.reverse();
    System.out.println(s);
}

@Test
public void test5(){
    StringBuilder s = new StringBuilder("helloworld");
    s.setCharAt(2, 'a');
    System.out.println(s);
}

@Test
public void test6(){
    StringBuilder s = new StringBuilder("helloworld");
    s.setLength(30);
    System.out.println(s);
}
```

### 2.3 效率测试
```java
//初始设置
long startTime = 0L;
long endTime = 0L;
String text = "";
StringBuffer buffer = new StringBuffer("");
StringBuilder builder = new StringBuilder("");

//开始对比
startTime = System.currentTimeMillis();
for (int i = 0; i < 20000; i++) {
    buffer.append(String.valueOf(i));
}
endTime = System.currentTimeMillis();
System.out.println("StringBuffer的执行时间：" + (endTime - startTime));

startTime = System.currentTimeMillis();
for (int i = 0; i < 20000; i++) {
    builder.append(String.valueOf(i));
}
endTime = System.currentTimeMillis();
System.out.println("StringBuilder的执行时间：" + (endTime - startTime));

startTime = System.currentTimeMillis();
for (int i = 0; i < 20000; i++) {
    text = text + i;
}
endTime = System.currentTimeMillis();
System.out.println("String的执行时间：" + (endTime - startTime));

```

### 2.4 练习
笔试题：程序输出：

```java
String str = null;
StringBuffer sb = new StringBuffer();
sb.append(str);

System.out.println(sb.length());//

System.out.println(sb);//

StringBuffer sb1 = new StringBuffer(str);
System.out.println(sb1);//

```

## 3. JDK8之前：日期时间API


在Java中，`Date` 类是 `java.util` 包中的一个类，用于表示特定的瞬间，精确到毫秒。这个类是抽象的，它提供了一些方法来操作日期和时间。以下是 `Date` 类的一些关键点：

1. **构造方法**<font style="color:rgb(6, 6, 7);">：</font>
    - `<font style="color:rgb(6, 6, 7);">Date()</font>`<font style="color:rgb(6, 6, 7);">：创建一个当前日期和时间的 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象。</font>
    - `<font style="color:rgb(6, 6, 7);">Date(long date)</font>`<font style="color:rgb(6, 6, 7);">：创建一个表示自1970年1月1日00:00:00 GMT以来指定毫秒数的 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象。</font>
2. **时间获取**<font style="color:rgb(6, 6, 7);">：</font>
    - `<font style="color:rgb(6, 6, 7);">long getTime()</font>`<font style="color:rgb(6, 6, 7);">：返回自1970年1月1日00:00:00 GMT以来此 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象表示的毫秒数。</font>
    - `<font style="color:rgb(6, 6, 7);">long getYear()</font>`<font style="color:rgb(6, 6, 7);">, </font>`<font style="color:rgb(6, 6, 7);">getMonth()</font>`<font style="color:rgb(6, 6, 7);">, </font>`<font style="color:rgb(6, 6, 7);">getDay()</font>`<font style="color:rgb(6, 6, 7);"> 等：这些方法返回日期的特定字段，但它们已经过时，不建议使用。</font>
3. **设置时间**<font style="color:rgb(6, 6, 7);">：</font>
    - `<font style="color:rgb(6, 6, 7);">void setTime(long time)</font>`<font style="color:rgb(6, 6, 7);">：设置此 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象来表示自1970年1月1日00:00:00 GMT以来指定毫秒数的瞬间。</font>
4. **比较日期**<font style="color:rgb(6, 6, 7);">：</font>
    - `<font style="color:rgb(6, 6, 7);">boolean before(Date when)</font>`<font style="color:rgb(6, 6, 7);">：测试此 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象是否早于指定的 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象。</font>
    - `<font style="color:rgb(6, 6, 7);">boolean after(Date when)</font>`<font style="color:rgb(6, 6, 7);">：测试此 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象是否晚于指定的 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象。</font>
    - `<font style="color:rgb(6, 6, 7);">boolean equals(Object obj)</font>`<font style="color:rgb(6, 6, 7);">：测试此 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象是否与指定的对象相等。</font>
5. **格式化和解析**<font style="color:rgb(6, 6, 7);">：</font>
    - <font style="color:rgb(6, 6, 7);">虽然 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 类本身没有提供格式化和解析日期的方法，但它可以与 </font>`<font style="color:rgb(6, 6, 7);">SimpleDateFormat</font>`<font style="color:rgb(6, 6, 7);"> 类一起使用，后者是 </font>`<font style="color:rgb(6, 6, 7);">java.text</font>`<font style="color:rgb(6, 6, 7);"> 包的一部分，用于将 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象格式化为字符串，以及将字符串解析为 </font>`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 对象。</font>
6. **时区处理**<font style="color:rgb(6, 6, 7);">：</font>
    - `<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 类本身不包含时区信息，它只表示一个特定的瞬间。时区的处理通常需要结合 </font>`<font style="color:rgb(6, 6, 7);">Calendar</font>`<font style="color:rgb(6, 6, 7);"> 类或者 </font>`<font style="color:rgb(6, 6, 7);">java.time</font>`<font style="color:rgb(6, 6, 7);"> 包中的类（Java 8 引入的新日期时间API）。</font>
7. **过时的方法**<font style="color:rgb(6, 6, 7);">：</font>
    - `<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 类中的一些方法，如 </font>`<font style="color:rgb(6, 6, 7);">getYear()</font>`<font style="color:rgb(6, 6, 7);">, </font>`<font style="color:rgb(6, 6, 7);">getMonth()</font>`<font style="color:rgb(6, 6, 7);">, </font>`<font style="color:rgb(6, 6, 7);">getDate()</font>`<font style="color:rgb(6, 6, 7);"> 等，已经被标记为过时，因为它们不推荐使用，可能会导致混淆（例如，月份是从0开始的，0表示一月）。建议使用 </font>`<font style="color:rgb(6, 6, 7);">Calendar</font>`<font style="color:rgb(6, 6, 7);"> 类或者 Java 8 中的 </font>`<font style="color:rgb(6, 6, 7);">java.time</font>`<font style="color:rgb(6, 6, 7);"> 包。</font>

`<font style="color:rgb(6, 6, 7);">Date</font>`<font style="color:rgb(6, 6, 7);"> 类是Java早期版本中处理日期和时间的主要方式，但由于它的一些限制和不足，如线程安全问题和对时区的处理不足，Java 8 引入了新的日期时间API，即 </font>`<font style="color:rgb(6, 6, 7);">java.time</font>`<font style="color:rgb(6, 6, 7);"> 包，提供了更加全面和灵活的日期时间处理能力。在新的代码中，推荐使用 Java 8 的日期时间API。</font>

<font style="color:rgb(6, 6, 7);"></font>

+ <font style="color:rgb(6, 6, 7);">Calendar：日历类</font>
+ <font style="color:rgb(6, 6, 7);">① 实例化：由于Calendar是一个抽象类，所以我们需要创建其子类的实例。这里我们通过Calendar的静态方法getInstance()即可获取实例。</font>
+ <font style="color:rgb(6, 6, 7);">② 常用方法：</font>
    - <font style="color:rgb(6, 6, 7);">get(int field)：获取指定字段的值。</font>
    - <font style="color:rgb(6, 6, 7);">set(int field, int value)：设置指定字段的值。</font>
    - <font style="color:rgb(6, 6, 7);">add(int field, int amount)：在指定字段上增加或减少指定的量。</font>
    - <font style="color:rgb(6, 6, 7);">getTime()：返回表示Calendar时间值的Date对象。</font>
    - <font style="color:rgb(6, 6, 7);">setTime(Date date)：将Calendar的值设置为指定的Date对象</font>。

```java
import java.util.Calendar;
import java.text.SimpleDateFormat;

public class CalendarExample {
    public static void main(String[] args) {
        // 实例化Calendar对象
        Calendar calendar = Calendar.getInstance();
        
        // 设置Calendar的字段
        calendar.set(Calendar.YEAR, 2024);
        calendar.set(Calendar.MONTH, Calendar.NOVEMBER); // 注意：月份是从0开始的，所以11月是Calendar.NOVEMBER
        calendar.set(Calendar.DAY_OF_MONTH, 8);
        calendar.set(Calendar.HOUR_OF_DAY, 14);
        calendar.set(Calendar.MINUTE, 30);
        calendar.set(Calendar.SECOND, 0);
        
        // 获取并打印当前Calendar时间
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String strDate = dateFormat.format(calendar.getTime());
        System.out.println("当前设置的日期和时间: " + strDate);
        
        // 增加一天
        calendar.add(Calendar.DATE, 1);
        String strDateTomorrow = dateFormat.format(calendar.getTime());
        System.out.println("明天的日期和时间: " + strDateTomorrow);
        
        // 获取当前的年份
        int year = calendar.get(Calendar.YEAR);
        System.out.println("当前年份: " + year);
        
        // 获取当前的月份（注意：月份是从0开始的）
        int month = calendar.get(Calendar.MONTH);
        System.out.println("当前月份: " + (month + 1)); // 加1是因为Calendar月份从0开始计数
        
        // 获取当前的日期
        int day = calendar.get(Calendar.DAY_OF_MONTH);
        System.out.println("当前日期: " + day);
    }
}
```

<font style="color:rgb(6, 6, 7);">在这个例子中，我们首先导入了</font>`<font style="color:rgb(6, 6, 7);">Calendar</font>`<font style="color:rgb(6, 6, 7);">和</font>`<font style="color:rgb(6, 6, 7);">SimpleDateFormat</font>`<font style="color:rgb(6, 6, 7);">类。</font>`<font style="color:rgb(6, 6, 7);">Calendar</font>`<font style="color:rgb(6, 6, 7);">类用于操作日期和时间，而</font>`<font style="color:rgb(6, 6, 7);">SimpleDateFormat</font>`<font style="color:rgb(6, 6, 7);">类用于将日期时间格式化为易读的字符串格式。</font>

<font style="color:rgb(6, 6, 7);">我们创建了一个</font>`<font style="color:rgb(6, 6, 7);">Calendar</font>`<font style="color:rgb(6, 6, 7);">实例，并设置了年份、月份、日期、小时、分钟和秒。然后，我们使用</font>`<font style="color:rgb(6, 6, 7);">SimpleDateFormat</font>`<font style="color:rgb(6, 6, 7);">将</font>`<font style="color:rgb(6, 6, 7);">Calendar</font>`<font style="color:rgb(6, 6, 7);">的时间转换为字符串，并打印出来。接着，我们通过</font>`<font style="color:rgb(6, 6, 7);">add</font>`<font style="color:rgb(6, 6, 7);">方法给日期增加了一天，并再次打印新的日期时间。最后，我们分别获取并打印了当前的年份、月份和日期。</font>

<font style="color:rgb(6, 6, 7);"></font>

<font style="color:rgb(6, 6, 7);">//得到java.util.Date</font>

<font style="color:rgb(6, 6, 7);">Date datel= sdf.parse(pattern);</font>

<font style="color:rgb(6, 6, 7);">//转换为java.sql.Date</font>

<font style="color:rgb(6, 6, 7);">java.sql.Date date2 = new java.sql.Date(date1.getTime());</font>

<font style="color:rgb(6, 6, 7);">System.out.println(date2);</font>



一些问题

可变性:像日期和时间这样的类应该是不可变的。

编移性:Date中的年份是从1900开始的，而月份部从0开始。

格式化:格式化只对Date有用，Calendar则不行。

此外，它们也不是线程安全士，不能处理闰秒等。





### 3.1 java.lang.System类的方法
+ System类提供的public static long currentTimeMillis()：用来返回当前时间与1970年1月1日0时0分0秒之间以毫秒为单位的时间差。
    - 此方法适于计算时间差。
+ 计算世界时间的主要标准有：

> 在国际无线电通信场合，为了统一起见，使用一个统一的时间，称为通用协调时(UTC, Universal Time Coordinated)。UTC与格林尼治平均时(GMT, Greenwich Mean Time)一样，都与英国伦敦的本地时相同。这里，UTC与GMT含义完全相同。
>

    - UTC(Coordinated Universal Time)
    - GMT(Greenwich Mean Time)
    - CST(Central Standard Time)

### 3.2 java.util.Date
表示特定的瞬间，精确到毫秒。

+ 构造器：
    - Date()：使用无参构造器创建的对象可以获取本地当前时间。
    - Date(long 毫秒数)：把该毫秒值换算成日期时间对象
+ 常用方法
    - getTime(): 返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。
    - toString(): 把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)，zzz是时间标准。
    - 其它很多方法都过时了。
+ 举例：

```java
@Test
public void test1(){
    Date d = new Date();
    System.out.println(d);
}

@Test
public void test2(){
    long time = System.currentTimeMillis();
    System.out.println(time);//1559806982971
    //当前系统时间距离1970-1-1 0:0:0 0毫秒的时间差，毫秒为单位
}

@Test
public void test3(){
    Date d = new Date();
    long time = d.getTime();
    System.out.println(time);//1559807047979
}

@Test
public void test4(){
    long time = 1559807047979L;
    Date d = new Date(time);
    System.out.println(d);
}

@Test
public void test5(){
    long time = Long.MAX_VALUE;
    Date d = new Date(time);
    System.out.println(d);
}
```

### 3.3 java.text.SimpleDateFormat
+ java.text.SimpleDateFormat类是一个不与语言环境有关的方式来格式化和解析日期的具体类。
+ 可以进行格式化：日期 --> 文本
+ 可以进行解析：文本 --> 日期
+ **构造器：**
    - SimpleDateFormat() ：默认的模式和语言环境创建对象
    - public SimpleDateFormat(String pattern)：该构造方法可以用参数pattern指定的格式创建一个对象
+ **格式化：**
    - public String format(Date date)：方法格式化时间对象date
+ **解析：**
    - public Date parse(String source)：从给定字符串的开始解析文本，以生成一个日期。

![](images/1572599023197.png)

```java
//格式化
@Test
public void test1(){
    Date d = new Date();

    SimpleDateFormat sf = new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒 SSS毫秒  E Z");
    //把Date日期转成字符串，按照指定的格式转
    String str = sf.format(d);
    System.out.println(str);
}
//解析
@Test
public void test2() throws ParseException{
    String str = "2022年06月06日 16时03分14秒 545毫秒  星期四 +0800";
    SimpleDateFormat sf = new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒 SSS毫秒  E Z");
    Date d = sf.parse(str);
    System.out.println(d);
}
```

### 3.4 java.util.Calendar(日历)
+ Date类的API大部分被废弃了，替换为Calendar。
+ `Calendar` 类是一个抽象类，主用用于完成日期字段之间相互操作的功能。
+ 获取Calendar实例的方法
    - 使用`Calendar.getInstance()`方法![](images/image-20220123184906903.png)
    - 调用它的子类GregorianCalendar（公历）的构造器。![](images/image-20220405225828816.png)
+ 一个Calendar的实例是系统时间的抽象表示，可以修改或获取 YEAR、MONTH、DAY_OF_WEEK、HOUR_OF_DAY 、MINUTE、SECOND等 `日历字段`对应的时间值。
    - public int get(int field)：返回给定日历字段的值
    - public void set(int field,int value) ：将给定的日历字段设置为指定的值
    - public void add(int field,int amount)：根据日历的规则，为给定的日历字段添加或者减去指定的时间量
    - public final Date getTime()：将Calendar转成Date对象
    - public final void setTime(Date date)：使用指定的Date对象重置Calendar的时间
+ 常用字段![](images/1620277709044.png)
+ 注意：
    - 获取月份时：一月是0，二月是1，以此类推，12月是11
    - 获取星期时：周日是1，周二是2 ， 。。。。周六是7
+ 示例代码：



```java
import org.junit.Test;

import java.util.Calendar;
import java.util.TimeZone;

public class TestCalendar {
    @Test
    public void test1(){
        Calendar c = Calendar.getInstance();
        System.out.println(c);

        int year = c.get(Calendar.YEAR);
        int month = c.get(Calendar.MONTH)+1;
        int day = c.get(Calendar.DATE);
        int hour = c.get(Calendar.HOUR_OF_DAY);
        int minute = c.get(Calendar.MINUTE);

        System.out.println(year + "-" + month + "-" + day + " " + hour + ":" + minute);
    }

    @Test
    public void test2(){
        TimeZone t = TimeZone.getTimeZone("America/Los_Angeles");
        Calendar c = Calendar.getInstance(t);
        int year = c.get(Calendar.YEAR);
        int month = c.get(Calendar.MONTH)+1;
        int day = c.get(Calendar.DATE);
        int hour = c.get(Calendar.HOUR_OF_DAY);
        int minute = c.get(Calendar.MINUTE);

        System.out.println(year + "-" + month + "-" + day + " " + hour + ":" + minute);
    }
    
    @Test
    public void test3(){
        Calendar calendar = Calendar.getInstance();
        // 从一个 Calendar 对象中获取 Date 对象
        Date date = calendar.getTime();
        
        // 使用给定的 Date 设置此 Calendar 的时间
        date = new Date(234234235235L);
        calendar.setTime(date);
        calendar.set(Calendar.DAY_OF_MONTH, 8);
        System.out.println("当前时间日设置为8后,时间是:" + calendar.getTime());
        
        calendar.add(Calendar.HOUR, 2);
        System.out.println("当前时间加2小时后,时间是:" + calendar.getTime());
        
        calendar.add(Calendar.MONTH, -2);
        System.out.println("当前日期减2个月后,时间是:" + calendar.getTime());  
    }
}
```

### 3.5 练习
输入年份和月份，输出该月日历。

闰年计算公式：年份可以被4整除但不能被100整除，或者可以被400整除。

## 4. JDK8：新的日期时间API
如果我们可以跟别人说：“我们在1502643933071见面，别晚了！”那么就再简单不过了。但是我们希望时间与昼夜和四季有关，于是事情就变复杂了。JDK 1.0中包含了一个java.util.Date类，但是它的大多数方法已经在JDK 1.1引入Calendar类之后被弃用了。而Calendar并不比Date好多少。它们面临的问题是：

+ 可变性：像日期和时间这样的类应该是不可变的。
+ 偏移性：Date中的年份是从1900开始的，而月份都从0开始。
+ 格式化：格式化只对Date有用，Calendar则不行。
+ 此外，它们也不是线程安全的；不能处理闰秒等。

> 闰秒，是指为保持协调世界时接近于世界时时刻，由国际计量局统一规定在年底或年中（也可能在季末）对协调世界时增加或减少1秒的调整。由于地球自转的不均匀性和长期变慢性（主要由潮汐摩擦引起的），会使世界时（民用时）和原子时之间相差超过到±0.9秒时，就把协调世界时向前拨1秒（负闰秒，最后一分钟为59秒）或向后拨1秒（正闰秒，最后一分钟为61秒）； 闰秒一般加在公历年末或公历六月末。
>
> 目前，全球已经进行了27次闰秒，均为正闰秒。
>

总结：`对日期和时间的操作一直是Java程序员最痛苦的地方之一`。

第三次引入的API是成功的，并且Java 8中引入的java.time API 已经纠正了过去的缺陷，将来很长一段时间内它都会为我们服务。

Java 8 以一个新的开始为 Java 创建优秀的 API。新的日期时间API包含：

+ `java.time` – 包含值对象的基础包
+ `java.time.chrono` – 提供对不同的日历系统的访问。
+ `java.time.format` – 格式化和解析时间和日期
+ `java.time.temporal` – 包括底层框架和扩展特性
+ `java.time.zone` – 包含时区支持的类

说明：新的 java.time 中包含了所有关于时钟（Clock），本地日期（LocalDate）、本地时间（LocalTime）、本地日期时间（LocalDateTime）、时区（ZonedDateTime）和持续时间（Duration）的类。

尽管有68个新的公开类型，但是大多数开发者只会用到基础包和format包，大概占总数的三分之一。

### 4.1 本地日期时间：LocalDate、LocalTime、LocalDateTime
| 方法 | **描述** |
| --- | --- |
| `now() `/ now(ZoneId zone) | 静态方法，根据当前时间创建对象/指定时区的对象 |
| `of(xx,xx,xx,xx,xx,xxx)` | 静态方法，根据指定日期/时间创建对象 |
| getDayOfMonth()/getDayOfYear() | 获得月份天数(1-31) /获得年份天数(1-366) |
| getDayOfWeek() | 获得星期几(返回一个 DayOfWeek 枚举值) |
| getMonth() | 获得月份, 返回一个 Month 枚举值 |
| getMonthValue() / getYear() | 获得月份(1-12) /获得年份 |
| getHours()/getMinute()/getSecond() | 获得当前对象对应的小时、分钟、秒 |
| withDayOfMonth()/withDayOfYear()/withMonth()/withYear() | 将月份天数、年份天数、月份、年份修改为指定的值并返回新的对象 |
| with(TemporalAdjuster  t) | 将当前日期时间设置为校对器指定的日期时间 |
| plusDays(), plusWeeks(), plusMonths(), plusYears(),plusHours() | 向当前对象添加几天、几周、几个月、几年、几小时 |
| minusMonths() / minusWeeks()/minusDays()/minusYears()/minusHours() | 从当前对象减去几月、几周、几天、几年、几小时 |
| plus(TemporalAmount t)/minus(TemporalAmount t) | 添加或减少一个 Duration 或 Period |
| isBefore()/isAfter() | 比较两个 LocalDate |
| isLeapYear() | 判断是否是闰年（在LocalDate类中声明） |
| format(DateTimeFormatter  t) | 格式化本地日期、时间，返回一个字符串 |
| parse(Charsequence text) | 将指定格式的字符串解析为日期、时间 |


```java
import org.junit.Test;

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;

public class TestLocalDateTime {
    @Test
    public void test01(){
        LocalDate now = LocalDate.now();
        System.out.println(now);
    }
    @Test
    public void test02(){
        LocalTime now = LocalTime.now();
        System.out.println(now);
    }
    @Test
    public void test03(){
        LocalDateTime now = LocalDateTime.now();
        System.out.println(now);
    }
    @Test
    public void test04(){
        LocalDate lai = LocalDate.of(2019, 5, 13);
        System.out.println(lai);
    }
    @Test
    public void test05(){
        LocalDate lai = LocalDate.of(2019, 5, 13);
        System.out.println(lai.getDayOfYear());
    }
    @Test
    public void test06(){
        LocalDate lai = LocalDate.of(2019, 5, 13);
        LocalDate go = lai.plusDays(160);
        System.out.println(go);//2019-10-20
    }
    @Test
    public void test7(){
        LocalDate now = LocalDate.now();
        LocalDate before = now.minusDays(100);
        System.out.println(before);//2019-02-26
    }   
}
```

### 4.2 瞬时：Instant
+ Instant：时间线上的一个瞬时点。 这可能被用来记录应用程序中的事件时间戳。
    - 时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数。
+ `java.time.Instant`表示时间线上的一点，而不需要任何上下文信息，例如，时区。概念上讲，`它只是简单的表示自1970年1月1日0时0分0秒（UTC）开始的秒数。`

| **方法** | **描述** |
| --- | --- |
| `now()` | 静态方法，返回默认UTC时区的Instant类的对象 |
| `ofEpochMilli(long epochMilli)` | 静态方法，返回在1970-01-01 00:00:00基础上加上指定毫秒数之后的Instant类的对象 |
| atOffset(ZoneOffset offset) | 结合即时的偏移来创建一个 OffsetDateTime |
| `toEpochMilli()` | 返回1970-01-01 00:00:00到当前时间的毫秒数，即为时间戳 |


> 中国大陆、中国香港、中国澳门、中国台湾、蒙古国、新加坡、马来西亚、菲律宾、西澳大利亚州的时间与UTC的时差均为+8，也就是UTC+8。
>
> instant.atOffset(ZoneOffset.ofHours(8));
>

![](images/image-20220406000442908.png)

> 整个地球分为二十四时区，每个时区都有自己的本地时间。北京时区是东八区，领先UTC八个小时，在电子邮件信头的Date域记为+0800。如果在电子邮件的信头中有这么一行： 
>
>  Date: Fri, 08 Nov 2002 09:42:22 +0800 
>
>  说明信件的发送地的地方时间是二○○二年十一月八号，星期五，早上九点四十二分（二十二秒），这个地方的本地时领先UTC八个小时(+0800， 就是东八区时间)。电子邮件信头的Date域使用二十四小时的时钟，而不使用AM和PM来标记上下午。 
>

### 4.3 日期时间格式化：DateTimeFormatter
该类提供了三种格式化方法：

+ (了解)预定义的标准格式。如：ISO_LOCAL_DATE_TIME、ISO_LOCAL_DATE、ISO_LOCAL_TIME
+ (了解)本地化相关的格式。如：ofLocalizedDate(FormatStyle.LONG)

```java
// 本地化相关的格式。如：ofLocalizedDateTime()
// FormatStyle.MEDIUM / FormatStyle.SHORT :适用于LocalDateTime
                
// 本地化相关的格式。如：ofLocalizedDate()
// FormatStyle.FULL / FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT : 适用于LocalDate
```

+ 自定义的格式。如：ofPattern(“yyyy-MM-dd hh:mm:ss”)

| **方**   **法** | **描**   **述** |
| --- | --- |
| **ofPattern(String**  **pattern)** | 静态方法，返回一个指定字符串格式的DateTimeFormatter |
| **format(TemporalAccessor** **t)** | 格式化一个日期、时间，返回字符串 |
| **parse(CharSequence**  **text)** | 将指定格式的字符序列解析为一个日期、时间 |


举例：

```java
import org.junit.Test;

import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;

public class TestDatetimeFormatter {
    @Test
    public void test1(){
        // 方式一：预定义的标准格式。如：ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;ISO_LOCAL_TIME
        DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
        // 格式化:日期-->字符串
        LocalDateTime localDateTime = LocalDateTime.now();
        String str1 = formatter.format(localDateTime);
        System.out.println(localDateTime);
        System.out.println(str1);//2022-12-04T21:02:14.808

        // 解析：字符串 -->日期
        TemporalAccessor parse = formatter.parse("2022-12-04T21:02:14.808");
        LocalDateTime dateTime = LocalDateTime.from(parse);
        System.out.println(dateTime);
    }

    @Test
    public void test2(){
        LocalDateTime localDateTime = LocalDateTime.now();
        // 方式二：
        // 本地化相关的格式。如：ofLocalizedDateTime()
        // FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT :适用于LocalDateTime
        DateTimeFormatter formatter1 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.LONG);
        
        // 格式化
        String str2 = formatter1.format(localDateTime);
        System.out.println(str2);// 2022年12月4日 下午09时03分55秒

        // 本地化相关的格式。如：ofLocalizedDate()
        // FormatStyle.FULL / FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT : 适用于LocalDate
        DateTimeFormatter formatter2 = DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL);
        // 格式化
        String str3 = formatter2.format(LocalDate.now());
        System.out.println(str3);// 2022年12月4日 星期日
    }

    @Test
    public void test3(){
        //方式三：自定义的方式（关注、重点）
        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
        //格式化
        String strDateTime = dateTimeFormatter.format(LocalDateTime.now());
        System.out.println(strDateTime); //2022/12/04 21:05:42
        //解析
        TemporalAccessor accessor = dateTimeFormatter.parse("2022/12/04 21:05:42");
        LocalDateTime localDateTime = LocalDateTime.from(accessor);
        System.out.println(localDateTime); //2022-12-04T21:05:42
    }
}
```

### 4.4 其它API
**1、指定时区日期时间：ZondId和ZonedDateTime**

+ ZoneId：该类中包含了所有的时区信息，一个时区的ID，如 Europe/Paris
+ ZonedDateTime：一个在ISO-8601日历系统时区的日期时间，如 2007-12-03T10:15:30+01:00 Europe/Paris。
    - 其中每个时区都对应着ID，地区ID都为“{区域}/{城市}”的格式，例如：Asia/Shanghai等
+ 常见时区ID：



```java
Asia/Shanghai
UTC
America/New_York
```

+ 可以通过ZondId获取所有可用的时区ID：



```java
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.util.Set;

public class TestZone {
    @Test
    public void test01() {
        //需要知道一些时区的id
        //Set<String>是一个集合，容器
        Set<String> availableZoneIds = ZoneId.getAvailableZoneIds();
        //快捷模板iter
        for (String availableZoneId : availableZoneIds) {
            System.out.println(availableZoneId);
        }
    }

    @Test
    public void test02(){
        ZonedDateTime t1 = ZonedDateTime.now();
        System.out.println(t1);

        ZonedDateTime t2 = ZonedDateTime.now(ZoneId.of("America/New_York"));
        System.out.println(t2);
    }
}

```

**2、持续日期/时间：Period和Duration**

+ 持续时间：Duration，用于计算两个“时间”间隔
+ 日期间隔：Period，用于计算两个“日期”间隔

```java
import org.junit.Test;

import java.time.Duration;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.Period;

public class TestPeriodDuration {
    @Test
    public void test01(){
        LocalDate t1 = LocalDate.now();
        LocalDate t2 = LocalDate.of(2018, 12, 31);
        Period between = Period.between(t1, t2);
        System.out.println(between);

        System.out.println("相差的年数："+between.getYears());
        System.out.println("相差的月数："+between.getMonths());
        System.out.println("相差的天数："+between.getDays());
        System.out.println("相差的总数："+between.toTotalMonths());
    }

    @Test
    public void test02(){
        LocalDateTime t1 = LocalDateTime.now();
        LocalDateTime t2 = LocalDateTime.of(2017, 8, 29, 0, 0, 0, 0);
        Duration between = Duration.between(t1, t2);
        System.out.println(between);

        System.out.println("相差的总天数："+between.toDays());
        System.out.println("相差的总小时数："+between.toHours());
        System.out.println("相差的总分钟数："+between.toMinutes());
        System.out.println("相差的总秒数："+between.getSeconds());
        System.out.println("相差的总毫秒数："+between.toMillis());
        System.out.println("相差的总纳秒数："+between.toNanos());
        System.out.println("不够一秒的纳秒数："+between.getNano());
    }
    @Test
    public void test03(){
        //Duration:用于计算两个“时间”间隔，以秒和纳秒为基准
        LocalTime localTime = LocalTime.now();
        LocalTime localTime1 = LocalTime.of(15, 23, 32);
        //between():静态方法，返回Duration对象，表示两个时间的间隔
        Duration duration = Duration.between(localTime1, localTime);
        System.out.println(duration);

        System.out.println(duration.getSeconds());
        System.out.println(duration.getNano());

        LocalDateTime localDateTime = LocalDateTime.of(2016, 6, 12, 15, 23, 32);
        LocalDateTime localDateTime1 = LocalDateTime.of(2017, 6, 12, 15, 23, 32);

        Duration duration1 = Duration.between(localDateTime1, localDateTime);
        System.out.println(duration1.toDays());
    }
    
    @Test
    public void test4(){
        //Period:用于计算两个“日期”间隔，以年、月、日衡量
        LocalDate localDate = LocalDate.now();
        LocalDate localDate1 = LocalDate.of(2028, 3, 18);

        Period period = Period.between(localDate, localDate1);
        System.out.println(period);

        System.out.println(period.getYears());
        System.out.println(period.getMonths());
        System.out.println(period.getDays());

        Period period1 = period.withYears(2);
        System.out.println(period1);

    }
}

```

3、Clock：使用时区提供对当前即时、日期和时间的访问的时钟。

4、

TemporalAdjuster : 时间校正器。有时我们可能需要获取例如：将日期调整到“下一个工作日”等操作。  
TemporalAdjusters : 该类通过静态方法(firstDayOfXxx()/lastDayOfXxx()/nextXxx())提供了大量的常用 TemporalAdjuster 的实现。

```java
@Test
public void test1(){
    // TemporalAdjuster:时间校正器
    // 获取当前日期的下一个周日是哪天？
    TemporalAdjuster temporalAdjuster = TemporalAdjusters.next(DayOfWeek.SUNDAY);
    LocalDateTime localDateTime = LocalDateTime.now().with(temporalAdjuster);
    System.out.println(localDateTime);
    // 获取下一个工作日是哪天？
    LocalDate localDate = LocalDate.now().with(new TemporalAdjuster() {
        	@Override
        	public Temporal adjustInto(Temporal temporal) {
            LocalDate date = (LocalDate) temporal;
           	if (date.getDayOfWeek().equals(DayOfWeek.FRIDAY)) {
                   return date.plusDays(3);
            } else if (date.getDayOfWeek().equals(DayOfWeek.SATURDAY)) {
                return date.plusDays(2);
            } else {
                return date.plusDays(1);
            }
        }
    });
    System.out.println("下一个工作日是：" + localDate);

}
```

### 4.5 与传统日期处理的转换
| **类** | **To** **遗留类** | **From** **遗留类** |
| --- | --- | --- |
| **java.time.Instant与java.util.Date** | Date.from(instant) | date.toInstant() |
| **java.time.Instant与java.sql.Timestamp** | Timestamp.from(instant) | timestamp.toInstant() |
| **java.time.ZonedDateTime与java.util.GregorianCalendar** | GregorianCalendar.from(zonedDateTime) | cal.toZonedDateTime() |
| **java.time.LocalDate与java.sql.Time** | Date.valueOf(localDate) | date.toLocalDate() |
| **java.time.LocalTime与java.sql.Time** | Date.valueOf(localDate) | date.toLocalTime() |
| **java.time.LocalDateTime与java.sql.Timestamp** | Timestamp.valueOf(localDateTime) | timestamp.toLocalDateTime() |
| **java.time.ZoneId与java.util.TimeZone** | Timezone.getTimeZone(id) | timeZone.toZoneId() |
| **java.time.format.DateTimeFormatter与java.text.DateFormat** | formatter.toFormat() | 无 |


## 5. Java比较器
我们知道基本数据类型的数据（除boolean类型外）需要比较大小的话，之间使用比较运算符即可，但是引用数据类型是不能直接使用比较运算符来比较大小的。那么，如何解决这个问题呢？

![](images/image-20220406001726285.png)

+ 在Java中经常会涉及到对象数组的排序问题，那么就涉及到对象之间的比较问题。
+ Java实现对象排序的方式有两种：
    - 自然排序：java.lang.Comparable
    - 定制排序：java.util.Comparator

### 5.1 自然排序：java.lang.Comparable
+ Comparable接口强行对实现它的每个类的对象进行整体排序。这种排序被称为类的自然排序。
+ 实现 Comparable 的类必须实现 `compareTo(Object obj) `方法，两个对象即通过 compareTo(Object obj) 方法的返回值来比较大小。如果当前对象this大于形参对象obj，则返回正整数，如果当前对象this小于形参对象obj，则返回负整数，如果当前对象this等于形参对象obj，则返回零。

```java
package java.lang;

public interface Comparable{
    int compareTo(Object obj);
}
```

+ 实现Comparable接口的对象列表（和数组）可以通过 Collections.sort 或 Arrays.sort进行自动排序。实现此接口的对象可以用作有序映射中的键或有序集合中的元素，无需指定比较器。
+ 对于类 C 的每一个 e1 和 e2 来说，当且仅当 e1.compareTo(e2) == 0 与 e1.equals(e2) 具有相同的 boolean 值时，类 C 的自然排序才叫做与 equals 一致。建议（虽然不是必需的）`最好使自然排序与 equals 一致`。
+ Comparable 的典型实现：(`默认都是从小到大排列的`)
    - String：按照字符串中字符的Unicode值进行比较
    - Character：按照字符的Unicode值来进行比较
    - 数值类型对应的包装类以及BigInteger、BigDecimal：按照它们对应的数值大小进行比较
    - Boolean：true 对应的包装类实例大于 false 对应的包装类实例
    - Date、Time等：后面的日期时间比前面的日期时间大



方式一:实现Comparable接口的方式

实现步骤:

① 具体的类A实现Comparable接口

② 重写Comparable接口中的compareTo(0bject obj)方法，在此方法中指明比较类A的对象的大小的标准

③ 创建类A的多个实例，进行大小的比较或排序。



方式二:实现Comparator接口的方式

实现步骤:

 1， 创建一个实现了cGmparator接口的实现类A

2 ， 实现类A要求重写comparator接口中的抽象方法compare(0bjecto1,0bject o2)，在此方法中 3，  指明比较大小的对象的大小关系。(比如，String类、Product类)

创建此实现类A的对象，并将此对象传入到相关方法的参数位置即可。(比如:Arrays.sort(..,类A的实例))



对比两种方式:

角度一:

自然排序:单一的，唯一的

定制排序:灵活的，多样的

角度二:

自然排序:一劳永逸的

定制排序:临时的



角度三:细节

自然排序:对应的接口是Comparable，对应的抽象方法compareTo(0bject obj)

定制排序:对应的接口是Comparator，对应的抽象方法compare(0bject obj1,0bject obj2)



使用`Comparable`接口对商品菜单列表进行排序。在这个例子中，我们将创建一个`Product`类，它实现了`Comparable`接口，并根据商品的价格进行排序。

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

// 商品类，实现Comparable接口
class Product implements Comparable<Product> {
    private String name; // 商品名称
    private double price; // 商品价格

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    // 获取商品名称
    public String getName() {
        return name;
    }

    // 获取商品价格
    public double getPrice() {
        return price;
    }

    // 实现Comparable接口的compareTo方法，根据价格排序
    @Override
    public int compareTo(Product other) {
        return Double.compare(this.price, other.price);
    }

    @Override
    public String toString() {
        return "Product{name='" + name + '\'' + ", price=" + price + '}';
    }
}

public class ProductMenuExample {
    public static void main(String[] args) {
        // 创建商品列表
        List<Product> products = new ArrayList<>();
        products.add(new Product("苹果", 3.5));
        products.add(new Product("香蕉", 2.0));
        products.add(new Product("橙子", 4.0));
        products.add(new Product("西瓜", 1.5));

        // 使用Collections.sort()方法对商品列表进行排序
        Collections.sort(products);

        // 打印排序后的商品列表
        for (Product product : products) {
            System.out.println(product);
        }
    }
}
```

在这个例子中，`Product`类有两个属性：`name`（商品名称）和`price`（商品价格）。`Product`类实现了`Comparable`接口，并重写了`compareTo`方法，该方法接受另一个`Product`对象作为参数，并根据商品的价格进行比较。这里使用了`Double.compare`方法来比较两个商品的价格。

在`ProductMenuExample`类的`main`方法中，我们创建了一个`ArrayList`来存储`Product`对象，并添加了一些商品。然后，我们使用`Collections.sort`方法对商品列表进行排序。由于`Product`类实现了`Comparable`接口，`Collections.sort`方法可以自动根据商品的价格进行排序。

最后，我们遍历并打印排序后的商品列表。在这个例子中，商品将按照价格升序排序。

+ 代码示例：



```java
package com.atguigu.api;

public class Student implements Comparable {
    private int id;
    private String name;
    private int score;
    private int age;

    public Student(int id, String name, int score, int age) {
        this.id = id;
        this.name = name;
        this.score = score;
        this.age = age;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getScore() {
        return score;
    }

    public void setScore(int score) {
        this.score = score;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", score=" + score +
                ", age=" + age +
                '}';
    }

    @Override
    public int compareTo(Object o) {
        //这些需要强制，将o对象向下转型为Student类型的变量，才能调用Student类中的属性
        //默认按照学号比较大小
        Student stu = (Student) o;
        return this.id - stu.id;
    }
}
```

测试类

```java
package com.atguigu.api;

public class TestStudent {
    public static void main(String[] args) {
        Student[] arr = new Student[5];
        arr[0] = new Student(3,"张三",90,23);
        arr[1] = new Student(1,"熊大",100,22);
        arr[2] = new Student(5,"王五",75,25);
        arr[3] = new Student(4,"李四",85,24);
        arr[4] = new Student(2,"熊二",85,18);

        //单独比较两个对象
        System.out.println(arr[0].compareTo(arr[1]));
        System.out.println(arr[1].compareTo(arr[2]));
        System.out.println(arr[2].compareTo(arr[2]));

        System.out.println("所有学生：");
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
        System.out.println("按照学号排序：");
        for (int i = 1; i < arr.length; i++) {
            for (int j = 0; j < arr.length-i; j++) {
                if(arr[j].compareTo(arr[j+1])>0){
                    Student temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}

```

再举例：

```java

public class Student implements Comparable {
    private String name;
    private int score;

    public Student(String name, int score) {
        this.name = name;
        this.score = score;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getScore() {
        return score;
    }

    public void setScore(int score) {
        this.score = score;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", score=" + score +
                '}';
    }

    @Override
    public int compareTo(Object o) {
        return this.score - ((Student)o).score;
    }
}
```

测试：

```java
@Test
public void test02() {
    Student[] students = new Student[3];
    students[0] = new Student("张三", 96);
    students[1] = new Student("李四", 85);
    students[2] = new Student("王五", 98);

    System.out.println(Arrays.toString(students));
    Arrays.sort(students);
    System.out.println(Arrays.toString(students));
}
```

再举例：

```java
class Goods implements Comparable {
    private String name;
    private double price;

    //按照价格，比较商品的大小
    @Override
    public int compareTo(Object o) {
        if(o instanceof Goods) {
            Goods other = (Goods) o;
            if (this.price > other.price) {
                return 1;
            } else if (this.price < other.price) {
                return -1;
            }
            return 0;
        }
        throw new RuntimeException("输入的数据类型不一致");
    }
    //构造器、getter、setter、toString()方法略
}


```

测试：

```java
public class ComparableTest{
    public static void main(String[] args) {

        Goods[] all = new Goods[4];
        all[0] = new Goods("《红楼梦》", 100);
        all[1] = new Goods("《西游记》", 80);
        all[2] = new Goods("《三国演义》", 140);
        all[3] = new Goods("《水浒传》", 120);

        Arrays.sort(all);

        System.out.println(Arrays.toString(all));

    }

}

```

### 5.2 定制排序：java.util.Comparator
+ 思考
    - 当元素的类型没有实现java.lang.Comparable接口而又不方便修改代码（例如：一些第三方的类，你只有.class文件，没有源文件）
    - 如果一个类，实现了Comparable接口，也指定了两个对象的比较大小的规则，但是此时此刻我不想按照它预定义的方法比较大小，但是我又不能随意修改，因为会影响其他地方的使用，怎么办？
+ JDK在设计类库之初，也考虑到这种情况，所以又增加了一个java.util.Comparator接口。强行对多个对象进行整体排序的比较。
    - 重写compare(Object o1,Object o2)方法，比较o1和o2的大小：如果方法返回正整数，则表示o1大于o2；如果返回0，表示相等；返回负整数，表示o1小于o2。
    - 可以将 Comparator 传递给 sort 方法（如 Collections.sort 或 Arrays.sort），从而允许在排序顺序上实现精确控制。

```java
package java.util;

public interface Comparator{
    int compare(Object o1,Object o2);
}
```

举例：

```java
package com.atguigu.api;

import java.util.Comparator;
//定义定制比较器类
public class StudentScoreComparator implements Comparator { 
    @Override
    public int compare(Object o1, Object o2) {
        Student s1 = (Student) o1;
        Student s2 = (Student) o2;
        int result = s1.getScore() - s2.getScore();
        return result != 0 ? result : s1.getId() - s2.getId();
    }
}
```

测试类

```java
package com.atguigu.api;

public class TestStudent {
    public static void main(String[] args) {
        Student[] arr = new Student[5];
        arr[0] = new Student(3, "张三", 90, 23);
        arr[1] = new Student(1, "熊大", 100, 22);
        arr[2] = new Student(5, "王五", 75, 25);
        arr[3] = new Student(4, "李四", 85, 24);
        arr[4] = new Student(2, "熊二", 85, 18);


        System.out.println("所有学生：");
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }

        System.out.println("按照成绩排序");
        StudentScoreComparator sc = new StudentScoreComparator();
        for (int i = 1; i < arr.length; i++) {
            for (int j = 0; j < arr.length - i; j++) {
                if (sc.compare(arr[j], arr[j + 1]) > 0) {
                    Student temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```

再举例：

```java
@Test
public void test01() {
    Student[] students = new Student[5];
    students[0] = new Student(3, "张三", 90, 23);
    students[1] = new Student(1, "熊大", 100, 22);
    students[2] = new Student(5, "王五", 75, 25);
    students[3] = new Student(4, "李四", 85, 24);
    students[4] = new Student(2, "熊二", 85, 18);

    System.out.println(Arrays.toString(students));
    //定制排序
    StudentScoreComparator sc = new StudentScoreComparator();
    Arrays.sort(students, sc);
    System.out.println("排序之后：");
    System.out.println(Arrays.toString(students));
}
```

再举例：

```java
Goods[] all = new Goods[4];
all[0] = new Goods("War and Peace", 100);
all[1] = new Goods("Childhood", 80);
all[2] = new Goods("Scarlet and Black", 140);
all[3] = new Goods("Notre Dame de Paris", 120);

Arrays.sort(all, new Comparator() {

    @Override
    public int compare(Object o1, Object o2) {
        Goods g1 = (Goods) o1;
        Goods g2 = (Goods) o2;

        return g1.getName().compareTo(g2.getName());
    }
});

System.out.println(Arrays.toString(all));

```



三个类的对比 String StringBuffer StringBuilder

String 不可变的字符序列 （jdk8 以前使用 char[] jdk9 以后使用 byte[]）

StringBuffer 可变的字符序列 线程安全 效率低（jdk8 以前使用 char[] jdk9 以后使用 byte[]）

StringBuilder 可变的字符序列 线程不安全 效率高（jdk8 以前使用 char[] jdk9 以后使用 byte[]）



<font style="color:rgb(6, 6, 7);">针对于StringBuilder来说： 内部的属性有： char[] value; // 存储字符序列 int count; // 实际存储的字符的个数</font>

<font style="color:rgb(6, 6, 7);">StringBuilder sBuffer1 = new StringBuilder(); // char[] value = new char[16]; StringBuilder sBuffer1 = new StringBuilder("abc"); // char[] value = new char[16 + "abc".length]; sBuffer1.append("ac"); // value[0] = 'a'; value[1] = 'c'; sBuffer1.append("b"); // value[2] = 'b';</font>

<font style="color:rgb(6, 6, 7);">...不断的添加，一旦count要超过value.length时，就需要扩容：默认扩容为原有容量的2倍+2。 并将原有value数组中的元素复制到新的数组中。</font>

<font style="color:rgb(6, 6, 7);"></font>

<font style="color:rgb(6, 6, 7);">源码启示：</font>

<font style="color:rgb(6, 6, 7);">如果在开发中需要频繁地对字符串进行增、删、改等操作，建议使用</font>`StringBuffer`<font style="color:rgb(6, 6, 7);">或</font>`StringBuilder`<font style="color:rgb(6, 6, 7);">替换</font>`String`<font style="color:rgb(6, 6, 7);">。因为使用</font>`String`<font style="color:rgb(6, 6, 7);">效率低。</font>

<font style="color:rgb(6, 6, 7);">如果在开发中不涉及到线程安全问题，建议使用</font>`StringBuilder`<font style="color:rgb(6, 6, 7);">替换</font>`StringBuffer`<font style="color:rgb(6, 6, 7);">。因为使用</font>`StringBuilder`<font style="color:rgb(6, 6, 7);">效率高。</font>

<font style="color:rgb(6, 6, 7);">如果在开发中大体确定要操作的字符的个数，建议使用带</font>`int capacity`<font style="color:rgb(6, 6, 7);">参数的构造器。因为这样可以避免底层多次扩容操作，性能更好。</font>

<font style="color:rgb(6, 6, 7);">这些建议是基于</font>`String`<font style="color:rgb(6, 6, 7);">、</font>`StringBuffer`<font style="color:rgb(6, 6, 7);">和</font>`StringBuilder`<font style="color:rgb(6, 6, 7);">的内部实现机制。</font>`String`<font style="color:rgb(6, 6, 7);">对象是不可变的，每次对字符串的修改都会生成一个新的</font>`String`<font style="color:rgb(6, 6, 7);">对象，这会导致频繁的内存分配和垃圾回收，影响性能。而</font>`StringBuffer`<font style="color:rgb(6, 6, 7);">和</font>`StringBuilder`<font style="color:rgb(6, 6, 7);">都是可变的，它们内部使用字符数组来存储字符串，当字符数组容量不足以容纳新的字符时，会进行扩容操作。</font>`StringBuffer`<font style="color:rgb(6, 6, 7);">是线程安全的，而</font>`StringBuilder`<font style="color:rgb(6, 6, 7);">不是，因此在不需要线程安全的情况下，使用</font>`StringBuilder`<font style="color:rgb(6, 6, 7);">可以获得更好的性能。如果能够预估将要处理的字符串的大小，通过指定初始容量可以减少扩容的次数，从而提高性能。</font>

<font style="color:rgb(6, 6, 7);"></font>

<font style="color:rgb(6, 6, 7);">StringBuffer和StringBuilder中的常用方法</font>

<font style="color:rgb(6, 6, 7);">增:</font>

<font style="color:rgb(6, 6, 7);">append(xx)</font>

<font style="color:rgb(6, 6, 7);">删:</font>

<font style="color:rgb(6, 6, 7);">delete(int start, int end)</font>

<font style="color:rgb(6, 6, 7);">deleteCharAt(int index)</font>

<font style="color:rgb(6, 6, 7);">改:</font>

<font style="color:rgb(6, 6, 7);">replace(int start, int end, string str)</font>

<font style="color:rgb(6, 6, 7);">setCharAt(int index,char c)</font>

<font style="color:rgb(6, 6, 7);">查:</font>

<font style="color:rgb(6, 6, 7);">charAt(int index)</font>

<font style="color:rgb(6, 6, 7);">插:</font>

<font style="color:rgb(6, 6, 7);">insert(int index,xx)</font>

<font style="color:rgb(6, 6, 7);">长度:</font>

<font style="color:rgb(6, 6, 7);">length()</font>

<font style="color:rgb(6, 6, 7);"></font>

<font style="color:rgb(6, 6, 7);">效率从高到低排列:</font>

<font style="color:rgb(6, 6, 7);">StringBuilder >StringBuffer > String</font>

<font style="color:rgb(6, 6, 7);"></font>

1. **<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">不可变性</font>**<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：</font>
    - `<font style="background-color:#FBDE28;">String</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：字符串是不可变的，这意味着一旦创建，它的值就不能被改变。任何修改都会生成一个新的字符串对象。</font>
    - `<font style="background-color:#FBDE28;">StringBuffer</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;"> </font><font style="color:rgb(6, 6, 7);background-color:#FBDE28;">和</font><font style="color:rgb(6, 6, 7);background-color:#FBDE28;"> </font>`<font style="background-color:#FBDE28;">StringBuilder</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：字符串是可变的，可以在不创建新对象的情况下修改字符串的内容。</font>
2. **<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">线程安全</font>**<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：</font>
    - `<font style="background-color:#FBDE28;">String</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：线程安全的，因为它的不可变性意味着不需要额外的同步。</font>
    - `<font style="background-color:#FBDE28;">StringBuffer</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：线程安全的，因为它的方法是同步的，可以被多个线程安全地使用。</font>
    - `<font style="background-color:#FBDE28;">StringBuilder</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：非线程安全的，因为它的方法不是同步的，但在单线程环境下性能更好。</font>
3. **<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">性能</font>**<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：</font>
    - `<font style="background-color:#FBDE28;">String</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：由于不可变性，每次修改都会创建新的字符串对象，所以频繁的修改操作会导致性能问题。</font>
    - `<font style="background-color:#FBDE28;">StringBuffer</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：由于同步机制，性能比</font>`<font style="background-color:#FBDE28;">StringBuilder</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">稍差，但在多线程环境下是安全的。</font>
    - `<font style="background-color:#FBDE28;">StringBuilder</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：性能最好，因为它是非线程安全的，没有同步开销。</font>
4. **<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">使用场景</font>**<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：</font>
    - `<font style="background-color:#FBDE28;">String</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：适用于字符串内容一旦创建后不需要修改的场景。</font>
    - `<font style="background-color:#FBDE28;">StringBuffer</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：适用于多线程环境下需要频繁修改字符串的场景。</font>
    - `<font style="background-color:#FBDE28;">StringBuilder</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：适用于单线程环境下需要频繁修改字符串的场景。</font>
5. **<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">方法</font>**<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：</font>
    - `<font style="background-color:#FBDE28;">String</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：提供基本的字符串操作，如</font>`<font style="background-color:#FBDE28;">substring</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">、</font>`<font style="background-color:#FBDE28;">concat</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">、</font>`<font style="background-color:#FBDE28;">replace</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">等。</font>
    - `<font style="background-color:#FBDE28;">StringBuffer</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;"> </font><font style="color:rgb(6, 6, 7);background-color:#FBDE28;">和</font><font style="color:rgb(6, 6, 7);background-color:#FBDE28;"> </font>`<font style="background-color:#FBDE28;">StringBuilder</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：除了</font>`<font style="background-color:#FBDE28;">String</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">提供的方法外，还提供了</font>`<font style="background-color:#FBDE28;">append</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">、</font>`<font style="background-color:#FBDE28;">insert</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">、</font>`<font style="background-color:#FBDE28;">delete</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">、</font>`<font style="background-color:#FBDE28;">reverse</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">等方法，用于修改字符串。</font>
6. **<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">内部实现</font>**<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：</font>
    - `<font style="background-color:#FBDE28;">String</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：使用字符数组（</font>`<font style="background-color:#FBDE28;">char[]</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">）存储字符串。</font>
    - `<font style="background-color:#FBDE28;">StringBuffer</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;"> </font><font style="color:rgb(6, 6, 7);background-color:#FBDE28;">和</font><font style="color:rgb(6, 6, 7);background-color:#FBDE28;"> </font>`<font style="background-color:#FBDE28;">StringBuilder</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：使用可扩展的字节数组（</font>`<font style="background-color:#FBDE28;">byte[]</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">）存储字符串，这意味着它们可以在不创建新数组的情况下增长。</font>
7. **<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">API</font>**<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">：</font>
    - `<font style="background-color:#FBDE28;">StringBuffer</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;"> 和 </font>`<font style="background-color:#FBDE28;">StringBuilder</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;"> 提供了类似的API，但</font>`<font style="background-color:#FBDE28;">StringBuffer</font>`<font style="color:rgb(6, 6, 7);background-color:#FBDE28;">的每个方法都是同步的。</font>

<font style="color:rgb(6, 6, 7);"></font>



## 6. 系统相关类
### 6.1 java.lang.System类
+ System类代表系统，系统级的很多属性和控制方法都放置在该类的内部。该类位于`java.lang包`。
+ 由于该类的构造器是private的，所以无法创建该类的对象。其内部的成员变量和成员方法都是`static的`，所以也可以很方便的进行调用。
+ 成员变量   Scanner scan = new Scanner(System.in);
    - System类内部包含`in`、`out`和`err`三个成员变量，分别代表标准输入流(键盘输入)，标准输出流(显示器)和标准错误输出流(显示器)。
+ 成员方法
    - `native long currentTimeMillis()`：  
该方法的作用是返回当前的计算机时间，时间的表达格式为当前计算机时间和GMT时间(格林威治时间)1970年1月1号0时0分0秒所差的毫秒数。
    - `void exit(int status)`：  
该方法的作用是退出程序。其中status的值为0代表正常退出，非零代表异常退出。使用该方法可以在图形界面编程中实现程序的退出功能等。
    - `void gc()`：  
该方法的作用是请求系统进行垃圾回收。至于系统是否立刻回收，则取决于系统中垃圾回收算法的实现以及系统执行时的情况。
    - `String getProperty(String key)`：  
该方法的作用是获得系统中属性名为key的属性对应的值。系统中常见的属性名以及属性的作用如下表所示：![](images/image-20220406003340258.png)
+ 举例

```java
import org.junit.Test;

public class TestSystem {
    @Test
    public void test01(){
        long time = System.currentTimeMillis();
        System.out.println("现在的系统时间距离1970年1月1日凌晨：" + time + "毫秒");

        System.exit(0);

        System.out.println("over");//不会执行
    }

    @Test
    public void test02(){
        String javaVersion = System.getProperty("java.version");
        System.out.println("java的version:" + javaVersion);

        String javaHome = System.getProperty("java.home");
        System.out.println("java的home:" + javaHome);

        String osName = System.getProperty("os.name");
        System.out.println("os的name:" + osName);

        String osVersion = System.getProperty("os.version");
        System.out.println("os的version:" + osVersion);

        String userName = System.getProperty("user.name");
        System.out.println("user的name:" + userName);

        String userHome = System.getProperty("user.home");
        System.out.println("user的home:" + userHome);

        String userDir = System.getProperty("user.dir");
        System.out.println("user的dir:" + userDir);
    }

    @Test
    public void test03() throws InterruptedException {
        for (int i=1; i <=10; i++){
            MyDemo my = new MyDemo(i);
            //每一次循环my就会指向新的对象，那么上次的对象就没有变量引用它了，就成垃圾对象
        }

        //为了看到垃圾回收器工作，我要加下面的代码，让main方法不那么快结束，因为main结束就会导致JVM退出，GC也会跟着结束。
        System.gc();//如果不调用这句代码，GC可能不工作，因为当前内存很充足，GC就觉得不着急回收垃圾对象。
                    //调用这句代码，会让GC尽快来工作。
        Thread.sleep(5000);
    }
}

class MyDemo{
    private int value;

    public MyDemo(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "MyDemo{" + "value=" + value + '}';
    }

    //重写finalize方法，让大家看一下它的调用效果
    @Override
    protected void finalize() throws Throwable {
//        正常重写，这里是编写清理系统内存的代码
//        这里写输出语句是为了看到finalize()方法被调用的效果
        System.out.println(this+ "轻轻的我走了，不带走一段代码....");
    }
}
```

+ `static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)`： 从指定源数组中复制一个数组，复制从指定的位置开始，到目标数组的指定位置结束。常用于数组的插入和删除

```java
import org.junit.Test;

import java.util.Arrays;

public class TestSystemArrayCopy {
    @Test
    public void test01(){
        int[] arr1 = {1,2,3,4,5};
        int[] arr2 = new int[10];
        System.arraycopy(arr1,0,arr2,3,arr1.length);
        System.out.println(Arrays.toString(arr1));
        System.out.println(Arrays.toString(arr2));
    }

    @Test
    public void test02(){
        int[] arr = {1,2,3,4,5};
        System.arraycopy(arr,0,arr,1,arr.length-1);
        System.out.println(Arrays.toString(arr));
    }

    @Test
    public void test03(){
        int[] arr = {1,2,3,4,5};
        System.arraycopy(arr,1,arr,0,arr.length-1);
        System.out.println(Arrays.toString(arr));
    }
}
```

### 6.2 java.lang.Runtime类
每个 Java 应用程序都有一个 `Runtime` 类实例，使应用程序能够与其运行的环境相连接。

`public static Runtime getRuntime()`： 返回与当前 Java 应用程序相关的运行时对象。应用程序不能创建自己的 Runtime 类实例。

`public long totalMemory()`：返回 Java 虚拟机中初始化时的内存总量。此方法返回的值可能随时间的推移而变化，这取决于主机环境。默认为物理电脑内存的1/64。

`public long maxMemory()`：返回 Java 虚拟机中最大程度能使用的内存总量。默认为物理电脑内存的1/4。

`public long freeMemory()`：回 Java 虚拟机中的空闲内存量。调用 gc 方法可能导致 freeMemory 返回值的增加。

```java
package com.atguigu.system;

public class TestRuntime {
    public static void main(String[] args) {
        Runtime runtime = Runtime.getRuntime();
        long initialMemory = runtime.totalMemory(); //获取虚拟机初始化时堆内存总量
        long maxMemory = runtime.maxMemory(); //获取虚拟机最大堆内存总量
        String str = "";
        //模拟占用内存
        for (int i = 0; i < 10000; i++) {
            str += i;
        }
        long freeMemory = runtime.freeMemory(); //获取空闲堆内存总量
        System.out.println("总内存：" + initialMemory / 1024 / 1024 * 64 + "MB");
        System.out.println("总内存：" + maxMemory / 1024 / 1024 * 4 + "MB");
        System.out.println("空闲内存：" + freeMemory / 1024 / 1024 + "MB") ;
        System.out.println("已用内存：" + (initialMemory-freeMemory) / 1024 / 1024 + "MB");
    }
}
```

## 7. 和数学相关的类
### 7.1 java.lang.Math
`java.lang.Math` 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。类似这样的工具类，其所有方法均为静态方法，并且不会创建对象，调用起来非常简单。

+ `public static double abs(double a) ` ：返回 double 值的绝对值。

```java
double d1 = Math.abs(-5); //d1的值为5
double d2 = Math.abs(5); //d2的值为5
```

+ `public static double ceil(double a)` ：返回大于等于参数的最小的整数。

```java
double d1 = Math.ceil(3.3); //d1的值为 4.0
double d2 = Math.ceil(-3.3); //d2的值为 -3.0
double d3 = Math.ceil(5.1); //d3的值为 6.0
```

+ `public static double floor(double a) ` ：返回小于等于参数最大的整数。

```java
double d1 = Math.floor(3.3); //d1的值为3.0
double d2 = Math.floor(-3.3); //d2的值为-4.0
double d3 = Math.floor(5.1); //d3的值为 5.0
```

+ `public static long round(double a)` ：返回最接近参数的 long。(相当于四舍五入方法)

技巧 x + 0.5 再向下取整

```java
long d1 = Math.round(5.5); //d1的值为6
long d2 = Math.round(5.4); //d2的值为5
long d3 = Math.round(-3.3); //d3的值为-3
long d4 = Math.round(-3.8); //d4的值为-4
```

+ public static double pow(double a,double b)：返回a的b幂次方法
+ public static double sqrt(double a)：返回a的平方根
+ `public static double random()`：返回[0,1)的随机值
+ public static final double PI：返回圆周率
+ public static double max(double x, double y)：返回x,y中的最大值
+ public static double min(double x, double y)：返回x,y中的最小值
+ 其它：acos,asin,atan,cos,sin,tan 三角函数

```java
double result = Math.pow(2,31);
double sqrt = Math.sqrt(256);
double rand = Math.random();
double pi = Math.PI;
```

### 7.2 java.math包
#### 7.2.1 BigInteger
+ Integer类作为int的包装类，能存储的最大整型值为2<sup>31-1，Long类也是有限的，最大为2</sup>63-1。如果要表示再大的整数，不管是基本数据类型还是他们的包装类都无能为力，更不用说进行运算了。
+ java.math包的BigInteger可以表示`不可变的任意精度的整数`。BigInteger 提供所有 Java 的基本整数操作符的对应物，并提供 java.lang.Math 的所有相关方法。另外，BigInteger 还提供以下运算：模算术、GCD 计算、质数测试、素数生成、位操作以及一些其他操作。 
+ 构造器
    - BigInteger(String val)：根据字符串构建BigInteger对象
+ 方法
    - public BigInteger `abs`()：返回此 BigInteger 的绝对值的 BigInteger。
    - BigInteger `add`(BigInteger val) ：返回其值为 (this + val) 的 BigInteger
    - BigInteger `subtract`(BigInteger val) ：返回其值为 (this - val) 的 BigInteger
    - BigInteger `multiply`(BigInteger val) ：返回其值为 (this * val) 的 BigInteger
    - BigInteger `divide`(BigInteger val) ：返回其值为 (this / val) 的 BigInteger。整数相除只保留整数部分。
    - BigInteger `remainder`(BigInteger val) ：返回其值为 (this % val) 的 BigInteger。
    - BigInteger[] `divideAndRemainder`(BigInteger val)：返回包含 (this / val) 后跟 (this % val) 的两个 BigInteger 的数组。
    - BigInteger `pow`(int exponent) ：返回其值为 (this^exponent) 的 BigInteger。

```java
@Test
public void test01(){
    //long bigNum = 123456789123456789123456789L;

    BigInteger b1 = new BigInteger("12345678912345678912345678");
    BigInteger b2 = new BigInteger("78923456789123456789123456789");

    //System.out.println("和：" + (b1+b2));//错误的，无法直接使用+进行求和

    System.out.println("和：" + b1.add(b2));
    System.out.println("减：" + b1.subtract(b2));
    System.out.println("乘：" + b1.multiply(b2));
    System.out.println("除：" + b2.divide(b1));
    System.out.println("余：" + b2.remainder(b1));
}
```

#### 7.2.2 BigDecimal
+ 一般的Float类和Double类可以用来做科学计算或工程计算，但在**商业计算中，要求数字精度比较高，故用到java.math.BigDecimal类。**
+ BigDecimal类支持不可变的、任意精度的有符号十进制定点数。
+ 构造器
    - public BigDecimal(double val)
    - public BigDecimal(String val) --> 推荐
+ 常用方法
    - public BigDecimal `add`(BigDecimal augend)
    - public BigDecimal `subtract`(BigDecimal subtrahend)
    - public BigDecimal `multiply`(BigDecimal multiplicand)
    - public BigDecimal `divide`(BigDecimal divisor, int scale, int roundingMode)：divisor是除数，scale指明保留几位小数，roundingMode指明舍入模式（ROUND_UP :向上加1、ROUND_DOWN :直接舍去、ROUND_HALF_UP:四舍五入）
+ 举例

```java
@Test
public void test03(){
    BigInteger bi = new BigInteger("12433241123");
    BigDecimal bd = new BigDecimal("12435.351");
    BigDecimal bd2 = new BigDecimal("11");
    System.out.println(bi);
    // System.out.println(bd.divide(bd2));
    System.out.println(bd.divide(bd2, BigDecimal.ROUND_HALF_UP));
    System.out.println(bd.divide(bd2, 15, BigDecimal.ROUND_HALF_UP));
}

```

### 7.3 java.util.Random
用于产生随机数

+ `boolean nextBoolean()`:返回下一个伪随机数，它是取自此随机数生成器序列的均匀分布的 boolean 值。 
+ `void nextBytes(byte[] bytes)`:生成随机字节并将其置于用户提供的 byte 数组中。 
+ `double nextDouble()`:返回下一个伪随机数，它是取自此随机数生成器序列的、在 0.0 和 1.0 之间均匀分布的 double 值。 
+ `float nextFloat()`:返回下一个伪随机数，它是取自此随机数生成器序列的、在 0.0 和 1.0 之间均匀分布的 float 值。 
+ `double nextGaussian()`:返回下一个伪随机数，它是取自此随机数生成器序列的、呈高斯（“正态”）分布的 double 值，其平均值是 0.0，标准差是 1.0。 
+ `int nextInt()`:返回下一个伪随机数，它是此随机数生成器的序列中均匀分布的 int 值。 
+ `int nextInt(int n)`:返回一个伪随机数，它是取自此随机数生成器序列的、在 0（包括）和指定值（不包括）之间均匀分布的 int 值。 
+ `long nextLong()`:返回下一个伪随机数，它是取自此随机数生成器序列的均匀分布的 long 值。

```java
@Test
public void test04(){
    Random r = new Random();
    System.out.println("随机整数：" + r.nextInt());
    System.out.println("随机小数：" + r.nextDouble());
    System.out.println("随机布尔值：" + r.nextBoolean());
}
```

# 


