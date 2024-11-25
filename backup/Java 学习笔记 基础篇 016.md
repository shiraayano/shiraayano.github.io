# 
# 集合框架


## 1. 集合框架概述
内存层面需要针对于多个数据进行存储。此时，可以考虑的容器有:数组、集合类

数组存储多个数据方面的特点:

> 数组一旦初始化，其长度就是确定的。
>

> 数组中的多个元素是依次紧密排列的，有序的，可重复的
>

> (优点)数组一旦初始化完成，其元素的类型就是确定的。不是此类型的元素，就不能添加到此数组中
>

intllarr = new int[10];

arr[0]= 1;

arr[1]="AA";//编译报错

0bject[]arr1 = new 0bject[10];

arr1[0]= new String();

arr1[1]= new Date();

> （优点 ） 元素的类型既可以是基本数据类型，也可以是引用数据类型
>



数组存储多个数据方面的弊端：

> 数组一旦初始化，其长度就不可变了，
>

> 数组中存储数据特点的单一性。对于无序的、不可重复的场景的多个数据就无能为力了
>

> 数组可用的方法，属性极少，具体的需求都需要自己组织相关的代码逻辑
>

> 针对于数组中元素的删除，插入操作性能较差
>



Java集合框架体系(java.util包下)

java.util.Collection:存储一个-个的数据

-----子接口:List:存储有序的、可重复的数据(动态"数组")

----ArrayList、LinkedList、Vector

-----子接口:Set:存储无序的、不可重复的数据（高中学习的集合是一样的）

----HashSet、LinkedHashSet、TreeSet





List及其实现类特点

java.util.Collection:存储一个一个的数据

-----子接口:List:存储有序的、可重复的数据("动态"数组)

ArrayList:List的主要实现类;线程不安全的、效率高；底层使用 Object[] 数组存储

Vector:List的古老实现类;线程安全的、效率低:底层使用 Object[] 数组存储

LinkedList 底层使用双向链表进行存储，在对集合数据进行频繁的删除，插入操作时建议使用此类







java.util.Map:存储一对一对的数据（存储 key-value 键值对，（x1，y1）,（x2，y2）--> y=F

(x)，类似于函数）

----HashMap、LinkedHashMap、TreeMap、Hashtable、Properties

// 向列表末尾添加一个元素

void add(int index, E element) // 在指定位置插入一个元素



// 在列表末尾添加一个元素

boolean add(E element) // 在列表末尾添加一个元素，并返回true





// 在列表末尾添加多个元素

boolean addAll(Collection<? extends E> c) // 将指定集合中的所有元素添加到列表末尾，并返回true如果列表被修改



// 在列表末尾添加多个元素

boolean addAll(int index, Collection<? extends E> c) // 在指定位置插入指定集合中的所有元素，并返回true如果列表被修改



// 清除列表中的所有元素

void clear() // 移除列表中的所有元素



// 检查列表是否包含某个元素

boolean contains(Object o) // 如果列表包含指定元素，则返回true



// 检查列表是否包含指定集合中的所有元素

boolean containsAll(Collection<?> c) // 如果列表包含指定集合中的所有元素，则返回true



// 获取列表中的元素

E get(int index) // 返回列表中指定位置的元素



// 获取列表中的索引

int indexOf(Object o) // 返回指定元素在列表中第一次出现的索引，如果未找到则返回-1



// 获取列表中的最后一个元素的索引

int lastIndexOf(Object o) // 返回指定元素在列表中最后一次出现的索引，如果未找到则返回-1



// 从列表中移除一个元素

E remove(int index) // 移除列表中指定位置的元素，并返回被移除的元素



// 从列表中移除一个元素

boolean remove(Object o) // 移除列表中第一次出现的指定元素，并返回true如果元素被移除



// 从列表中移除指定集合中的所有元素

boolean removeAll(Collection<?> c) // 移除列表中所有包含在指定集合中的元素，并返回true如果列表被修改



// 保留列表中不在指定集合中的元素

boolean retainAll(Collection<?> c) // 保留列表中所有包含在指定集合中的元素，并返回true如果列表被修改



// 替换列表中的元素

E set(int index, E element) // 替换列表中指定位置的元素，并返回被替换的元素



// 获取列表的大小

int size() // 返回列表中的元素数量



// 将列表转换为数组

Object[] toArray() // 返回包含列表所有元素的数组



// 将列表转换为指定类型的数组

<T> T[] toArray(T[] a) // 返回包含列表所有元素的指定类型的数组





学习的程度把握:

层次1:针对于具体特点的多个数据，知道选择相应的适合的接口的主要实现类，会实例化，会调用常用的方法

层次2:区分接口中不同实现类的区别

层次三：1，针对于常见类，需要熟悉底层源码

2，熟悉常见的数据结构



数组/集合的遍历

```java
public class Collection {
    public static void main(String[] args) {
        //创建数组
        String [] arr = new String[]{"hello","world"};
        //遍历数组
        for (String s : arr) {
            System.out.println(s);
        }
    }
}

/*
 * 
 * 格式
 * 数据类型[] 数组名 = new 数据类型[]{元素1,元素2,元素3...};
 * for（数据类型 变量名 : 数组名）{ }
 * for(要遍历的集合 临时变量 ： 要遍历的集合或数组变量)
 * 说明
 * 
 */
```



例 2

```java
public class Collection {
    public static void main(String[] args) {
        // 创建数组
        String[] arr = new String[] { "hello", "world" };
        // 遍历数组
        for (String s : arr) {
            s = "MM";
            System.out.println(s);
        }

        for (int i = 0; i < arr.length; i++) {
            // arr[i] = "MM";
            System.out.println(arr[i]);
        }
    }
}

/*
 * 
 * 格式
 * 数据类型[] 数组名 = new 数据类型[]{元素1,元素2,元素3...};
 * for（数据类型 变量名 : 数组名）{ }
 * for(要遍历的集合 临时变量 ： 要遍历的集合或数组变量)
 * 
 * 输出
 * MM
 * MM
 * hello
 * world
 * 
 * 说明
 * 增强for循环遍历数组时，不能修改数组中元素的值，因为增强for循环遍历数组时，数组元素的值是拷贝的，不是数组中元素的引用
 * 
 */
```



### 1.1 生活中的容器
### 1.2 数组的特点与弊端
+ 一方面，面向对象语言对事物的体现都是以对象的形式，为了方便对多个对象的操作，就要对对象进行存储。
+ 另一方面，使用数组存储对象方面具有`一些弊端`，而Java 集合就像一种容器，可以`动态地`把多个对象的引用放入容器中。
+ 数组在内存存储方面的`特点`：
    - 数组初始化以后，长度就确定了。
    - 数组中的添加的元素是依次紧密排列的，有序的，可以重复的。
    - 数组声明的类型，就决定了进行元素初始化时的类型。不是此类型的变量，就不能添加。
    - 可以存储基本数据类型值，也可以存储引用数据类型的变量
+ 数组在存储数据方面的`弊端`：
    - 数组初始化以后，长度就不可变了，不便于扩展
    - 数组中提供的属性和方法少，不便于进行添加、删除、插入、获取元素个数等操作，且效率不高。
    - 数组存储数据的特点单一，只能存储有序的、可以重复的数据
+ Java 集合框架中的类可以用于存储多个`对象`，还可用于保存具有`映射关系`的关联数组。

### 1.3 Java集合框架体系
Java 集合可分为 Collection 和 Map 两大体系：

+ Collection接口：用于存储一个一个的数据，也称`单列数据集合`。
    - List子接口：用来存储有序的、可以重复的数据（主要用来替换数组，"动态"数组）
        * 实现类：ArrayList(主要实现类)、LinkedList、Vector
+ Set子接口：用来存储无序的、不可重复的数据（类似于高中讲的"集合"）
    - 实现类：HashSet(主要实现类)、LinkedHashSet、TreeSet
+ Map接口：用于存储具有映射关系“key-value对”的集合，即一对一对的数据，也称`双列数据集合`。(类似于高中的函数、映射。(x1,y1),(x2,y2) ---> y = f(x) )
    - HashMap(主要实现类)、LinkedHashMap、TreeMap、Hashtable、Properties
+ JDK提供的集合API位于java.util包内
+ 图示：集合框架全图

![](images/集合框架全图.png)

+ 简图1：**Collection接口继承树**
+ 简图2：**Map接口继承树**

### 1.4 集合的使用场景
![](images/image-20220407202630027.png)

![](images/第12章_集合的使用场景.png)

## 2. Collection接口及方法
+ JDK不提供此接口的任何直接实现，而是提供更具体的子接口（如：Set和List）去实现。
+ Collection 接口是 List和Set接口的父接口，该接口里定义的方法既可用于操作 Set 集合，也可用于操作 List 集合。方法如下：

### 2.1 添加
（1）add(E obj)：添加元素对象到当前集合中  
（2）addAll(Collection other)：添加other集合中的所有元素对象到当前集合中，即this = this ∪ other

注意：add和addAll的区别

```java
package com.atguigu.collection;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;

public class TestCollectionAdd {
    @Test
    public void testAdd(){
        //ArrayList是Collection的子接口List的实现类之一。
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        System.out.println(coll);
    }

    @Test
    public void testAddAll(){
        Collection c1 = new ArrayList();
        c1.add(1);
        c1.add(2);
        System.out.println("c1集合元素的个数：" + c1.size());//2
        System.out.println("c1 = " + c1);

        Collection c2 = new ArrayList();
        c2.add(1);
        c2.add(2);
        System.out.println("c2集合元素的个数：" + c2.size());//2
        System.out.println("c2 = " + c2);

        Collection other = new ArrayList();
        other.add(1);
        other.add(2);
        other.add(3);
        System.out.println("other集合元素的个数：" + other.size());//3
        System.out.println("other = " + other);
        System.out.println();

        c1.addAll(other);
        System.out.println("c1集合元素的个数：" + c1.size());//5
        System.out.println("c1.addAll(other) = " + c1);

        c2.add(other);
        System.out.println("c2集合元素的个数：" + c2.size());//3
        System.out.println("c2.add(other) = " + c2);
    }
}
```

> 注意：coll.addAll(other);与coll.add(other);
>

![](images/1563548078274.png)

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class ListTest {
    @SuppressWarnings("unchecked")
    public static void main(String[] args) {

        // List<String> list = new ArrayList<>();


        List list = new ArrayList<>();
        list.add("Hello");
        list.add("World");
        list.add(111);//自动装箱
        list.add(222);
        System.out.println(list);
        // [Hello, World, 111, 222]

        list.remove(1);
        System.out.println(list);
        // [Hello, 111, 222]

        List<Integer> list2 = new ArrayList<>(Arrays.asList(1, 2, 3));
        System.out.println(list2);
        // [1, 2, 3]

        list.addAll(list2);
        //将list2中的所有元素添加到list中

        System.out.println(list);
        // [Hello, 111, 222, 1, 2, 3]

        list.addAll(1, list2);
        //将list2中的所有元素添加到list的索引1的位置

        System.out.println(list);
        //[Hello, 1, 2, 3, 111, 222, 1, 2, 3]

        list.remove(1);
        System.out.println(list);
        //[Hello, 2, 3, 111, 222, 1, 2, 3]

        list.add(new Person("Tom", 18));
        System.out.println(list);
        //[Hello, 2, 3, 111, 222, 1, 2, 3, Person@5caf905d]

        //删除list中所有的Person对象
        list.removeAll(Arrays.asList(new Person("Tom", 18)));
        System.out.println(list);
        //[Hello, 2, 3, 111, 222, 1, 2, 3]
    }
}
class Person{
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

### 2.2 判断
（3）int size()：获取当前集合中实际存储的元素个数  
（4）boolean isEmpty()：判断当前集合是否为空集合  
（5）boolean contains(Object obj)：判断当前集合中是否存在一个与obj对象equals返回true的元素  
（6）boolean containsAll(Collection coll)：判断coll集合中的元素是否在当前集合中都存在。即coll集合是否是当前集合的“子集”  
（7）boolean equals(Object obj)：判断当前集合与obj是否相等

```java
package com.atguigu.collection;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;

public class TestCollectionContains {
    @Test
    public void test01() {
        Collection coll = new ArrayList();
        System.out.println("coll在添加元素之前，isEmpty = " + coll.isEmpty());
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        coll.add("佛地魔");
        System.out.println("coll的元素个数" + coll.size());

        System.out.println("coll在添加元素之后，isEmpty = " + coll.isEmpty());
    }

    @Test
    public void test02() {
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        coll.add("佛地魔");
        System.out.println("coll = " + coll);
        System.out.println("coll是否包含“小李广” = " + coll.contains("小李广"));
        System.out.println("coll是否包含“宋红康” = " + coll.contains("宋红康"));

        Collection other = new ArrayList();
        other.add("小李广");
        other.add("扫地僧");
        other.add("尚硅谷");
        System.out.println("other = " + other);

        System.out.println("coll.containsAll(other) = " + coll.containsAll(other));
    }

    @Test
    public void test03(){
        Collection c1 = new ArrayList();
        c1.add(1);
        c1.add(2);
        System.out.println("c1集合元素的个数：" + c1.size());//2
        System.out.println("c1 = " + c1);

        Collection c2 = new ArrayList();
        c2.add(1);
        c2.add(2);
        System.out.println("c2集合元素的个数：" + c2.size());//2
        System.out.println("c2 = " + c2);

        Collection other = new ArrayList();
        other.add(1);
        other.add(2);
        other.add(3);
        System.out.println("other集合元素的个数：" + other.size());//3
        System.out.println("other = " + other);
        System.out.println();

        c1.addAll(other);
        System.out.println("c1集合元素的个数：" + c1.size());//5
        System.out.println("c1.addAll(other) = " + c1);
        System.out.println("c1.contains(other) = " + c1.contains(other));
        System.out.println("c1.containsAll(other) = " + c1.containsAll(other));
        System.out.println();

        c2.add(other);
        System.out.println("c2集合元素的个数：" + c2.size());
        System.out.println("c2.add(other) = " + c2);
        System.out.println("c2.contains(other) = " + c2.contains(other));
        System.out.println("c2.containsAll(other) = " + c2.containsAll(other));
    }

}
```

### 2.3 删除
（8）void clear()：清空集合元素  
（9） boolean remove(Object obj) ：从当前集合中删除第一个找到的与obj对象equals返回true的元素。  
（10）boolean removeAll(Collection coll)：从当前集合中删除所有与coll集合中相同的元素。即this = this - this ∩ coll  
（11）boolean retainAll(Collection coll)：从当前集合中删除两个集合中不同的元素，使得当前集合仅保留与coll集合中的元素相同的元素，即当前集合中仅保留两个集合的交集，即this  = this ∩ coll；

注意几种删除方法的区别

```java
package com.atguigu.collection;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;
import java.util.function.Predicate;

public class TestCollectionRemove {
    @Test
    public void test01(){
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        coll.add("佛地魔");
        System.out.println("coll = " + coll);

        coll.remove("小李广");
        System.out.println("删除元素\"小李广\"之后coll = " + coll);
        
        coll.clear();
        System.out.println("coll清空之后，coll = " + coll);
    }

    @Test
    public void test02() {
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        coll.add("佛地魔");
        System.out.println("coll = " + coll);

        Collection other = new ArrayList();
        other.add("小李广");
        other.add("扫地僧");
        other.add("尚硅谷");
        System.out.println("other = " + other);

        coll.removeAll(other);
        System.out.println("coll.removeAll(other)之后，coll = " + coll);
        System.out.println("coll.removeAll(other)之后，other = " + other);
    }

    @Test
    public void test03() {
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        coll.add("佛地魔");
        System.out.println("coll = " + coll);

        Collection other = new ArrayList();
        other.add("小李广");
        other.add("扫地僧");
        other.add("尚硅谷");
        System.out.println("other = " + other);

        coll.retainAll(other);
        System.out.println("coll.retainAll(other)之后，coll = " + coll);
        System.out.println("coll.retainAll(other)之后，other = " + other);
    }

}
```

### 2.4 其它
（12）Object[] toArray()：返回包含当前集合中所有元素的数组  
（13）hashCode()：获取集合对象的哈希值  
（14）iterator()：返回迭代器对象，用于集合遍历

```java
public class TestCollectionContains {
    @Test
    public void test01() {
        Collection coll = new ArrayList();

        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        coll.add("佛地魔");
        //集合转换为数组：集合的toArray()方法
        Object[] objects = coll.toArray();
        System.out.println("用数组返回coll中所有元素：" + Arrays.toString(objects));
        
        //对应的，数组转换为集合：调用Arrays的asList(Object ...objs)
        Object[] arr1 = new Object[]{123,"AA","CC"};
        Collection list = Arrays.asList(arr1);
        System.out.println(list);
    }
}
```



```java
// 亲例:键盘录入学生信息，保存到集合List中。
// 1)定义学生类，属性为姓名、年龄，提供必要的getter、setter方法，构造器，toString()，equals()方法
// 使用ArrayList集合，保存录入的多个学生对象。
// 2)
// 0，结束录入。
// 3)循环录入的方式，1:继续录入，
// 4)录入结束后，用foreach遍历集合

import java.util.ArrayList;
import java.util.Scanner;

public class Student {
    private String name;
    private int age;

    public Student() {

    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        
    }
    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Student student = (Student) o;

        if (age != student.age) return false;
        return name.equals(student.name);
    }
    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';

    }

    public static void main(String[] args) {
        ArrayList<Student> list = new ArrayList<>();
        Scanner sc = new Scanner(System.in);
        while (true) {
            System.out.println("请输入学生姓名");
            String name = sc.next();
            System.out.println("请输入学生年龄");
            int age = sc.nextInt();

            Student s = new Student(name,age);
            list.add(s);

            System.out.println("是否继续录入？1/0");
            if (sc.nextInt() == 0) {
                //输出成绩
                for (Student student : list) {
                    System.out.println(student);
                }
                break;
                
            }
    }
    
}
}
```



```java
//音乐菜单
import java.util.ArrayList;
import java.util.Scanner;

public class Music {
    private String name;
    private String singer;

    public Music(String name, String singer) {
        this.name = name;
        this.singer = singer;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
    
    public String getSinger() {
        return singer;
    }

    public void setSinger(String singer) {
        this.singer = singer;
    }

    @Override
    public String toString() {
        return "歌曲名:" + name + ",歌手:" + singer;
    }

    public static void main(String[] args) {
        ArrayList<Music> list = new ArrayList<>();
        Scanner sc = new Scanner(System.in);
        while (true) {
            // 输出歌曲
            for (int i = 0; i < list.size(); i++) {
                System.out.println((i + 1) + "." + list.get(i).toString());
            }
            System.out.println("-欢迎来到点歌系统--");
            System.out.println("1.添加歌曲至列表");
            System.out.println("2.将歌曲置顶");
            System.out.println("3.将歌曲前移一位");
            System.out.println("4.退出");

            int choice = sc.nextInt();
            sc.nextLine(); // 清除输入缓冲区中的换行符

            switch (choice) {
                case 1:
                    System.out.println("请输入歌曲名:");
                    String name = sc.nextLine();
                    System.out.println("请输入歌手名:");
                    String singer = sc.nextLine();
                    Music music = new Music(name, singer);
                    list.add(music);
                    break;
                case 2:
                    if (list.isEmpty()) {
                        System.out.println("歌曲列表为空");
                    } else {
                        System.out.println("请输入要置顶的歌曲名:");
                        String songName = sc.nextLine();
                        for (int i = 0; i < list.size(); i++) {
                            if (list.get(i).getName().equals(songName)) {
                                Music temp = list.remove(i);
                                list.add(0, temp);
                                break;
                            }
                        }
                    }
                    break;
                case 3:
                    if (list.isEmpty()) {
                        System.out.println("歌曲列表为空");
                    } else {
                        System.out.println("请输入要前移的歌曲名:");
                        String songName = sc.nextLine();
                        for (int i = 0; i < list.size(); i++) {
                            if (list.get(i).getName().equals(songName)) {
                                if (i > 0) {
                                    Music temp = list.remove(i);
                                    list.add(i - 1, temp);
                                } else {
                                    System.out.println("该歌曲已经在列表最前面");
                                }
                                break;
                            }
                        }
                    }
                    break;
                case 4:
                    System.out.println("退出点歌系统");
                    sc.close();
                    return;
                default:
                    System.out.println("无效的指令，请重新输入");
            }
        }
    }
}
```

## 3. Iterator(迭代器)接口
### 3.1 Iterator接口
+ 在程序开发中，经常需要遍历集合中的所有元素。针对这种需求，JDK专门提供了一个接口`java.util.Iterator`。`Iterator`接口也是Java集合中的一员，但它与`Collection`、`Map`接口有所不同。
    - Collection接口与Map接口主要用于`存储`元素
    - `Iterator`，被称为迭代器接口，本身并不提供存储对象的能力，主要用于`遍历`Collection中的元素
+ Collection接口继承了java.lang.Iterable接口，该接口有一个iterator()方法，那么所有实现了Collection接口的集合类都有一个iterator()方法，用以返回一个实现了Iterator接口的对象。
    - `public Iterator iterator()`: 获取集合对应的迭代器，用来遍历集合中的元素的。
    - 集合对象每次调用iterator()方法都得到一个全新的迭代器对象，默认游标都在集合的第一个元素之前。
+ Iterator接口的常用方法如下：
    - `public E next()`:返回迭代的下一个元素。
    - `public boolean hasNext()`:如果仍有元素可以迭代，则返回 true。
+ 注意：在调用it.next()方法之前必须要调用it.hasNext()进行检测。若不调用，且下一条记录无效，直接调用it.next()会抛出`NoSuchElementException异常`。



举例：

```java
package com.atguigu.iterator;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class TestIterator {
    @Test
    public void test01(){
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");

        Iterator iterator = coll.iterator();
        System.out.println(iterator.next());
        System.out.println(iterator.next());
        System.out.println(iterator.next());
        System.out.println(iterator.next()); //报NoSuchElementException异常
    }

    @Test
    public void test02(){
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");

        Iterator iterator = coll.iterator();//获取迭代器对象
        while(iterator.hasNext()) {//判断是否还有元素可迭代
            System.out.println(iterator.next());//取出下一个元素
        }
    }
}

```

### 3.2 迭代器的执行原理
Iterator迭代器对象在遍历集合时，内部采用指针的方式来跟踪集合中的元素，接下来通过一个图例来演示Iterator对象迭代元素的过程：

![](images/image-20220407235130988.png)

使用Iterator迭代器删除元素：java.util.Iterator迭代器中有一个方法：void remove() ;

```java
Iterator iter = coll.iterator();//回到起点
while(iter.hasNext()){
    Object obj = iter.next();
    if(obj.equals("Tom")){
        iter.remove();
    }
}
```

注意：

+ Iterator可以删除集合的元素，但是遍历过程中通过迭代器对象的remove方法，不是集合对象的remove方法。
+ 如果还未调用next()或在上一次调用 next() 方法之后已经调用了 remove() 方法，再调用remove()都会报IllegalStateException。
+ Collection已经有remove(xx)方法了，为什么Iterator迭代器还要提供删除方法呢？因为迭代器的remove()可以按指定的条件进行删除。



例如：要删除以下集合元素中的偶数

```java
package com.atguigu.iterator;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class TestIteratorRemove {
    @Test
    public void test01(){
        Collection coll = new ArrayList();
        coll.add(1);
        coll.add(2);
        coll.add(3);
        coll.add(4);
        coll.add(5);
        coll.add(6);

        Iterator iterator = coll.iterator();
        while(iterator.hasNext()){
            Integer element = (Integer) iterator.next();
            if(element % 2 == 0){
                iterator.remove();
            }
        }
        System.out.println(coll);
    }
}

```

在JDK8.0时，Collection接口有了removeIf 方法，即可以根据条件删除。（第18章中再讲）

```java
package com.atguigu.collection;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;
import java.util.function.Predicate;

public class TestCollectionRemoveIf {
    @Test
    public void test01(){
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        coll.add("佛地魔");
        System.out.println("coll = " + coll);

        coll.removeIf(new Predicate() {
            @Override
            public boolean test(Object o) {
                String str = (String) o;
                return str.contains("地");
            }
        });
        System.out.println("删除包含\"地\"字的元素之后coll = " + coll);
    }
}
```

### 3.3 foreach循环
+ foreach循环（也称增强for循环）是 JDK5.0 中定义的一个高级for循环，专门用来`遍历数组和集合`的。
+ foreach循环的语法格式：



```java
for(元素的数据类型 局部变量 : Collection集合或数组){ 
      //操作局部变量的输出操作
}
//这里局部变量就是一个临时变量，自己命名就可以
```

+ 举例：



```java
package com.atguigu.iterator;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;

public class TestForeach {
    @Test
    public void test01(){
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        //foreach循环其实就是使用Iterator迭代器来完成元素的遍历的。
        for (Object o : coll) {
            System.out.println(o);
        }
    }
    @Test
    public void test02(){
        int[] nums = {1,2,3,4,5};
        for (int num : nums) {
            System.out.println(num);
        }
        System.out.println("-----------------");
        String[] names = {"张三","李四","王五"};
        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

+ 对于集合的遍历，增强for的内部原理其实是个Iterator迭代器。如下图。

![](images/image-20220128010114124.png)

+ 它用于遍历Collection和数组。通常只进行遍历元素，不要在遍历的过程中对集合元素进行增删操作。
    - 练习：判断输出结果为何？

```java
public class ForTest {
    public static void main(String[] args) {
        String[] str = new String[5];
        for (String myStr : str) {
            myStr = "atguigu";
            System.out.println(myStr);
        }
        for (int i = 0; i < str.length; i++) {
            System.out.println(str[i]);
        }
    }
}

```

## 4. Collection子接口1：List
### 4.1 List接口特点
+ 鉴于Java中数组用来存储数据的局限性，我们通常使用`java.util.List`替代数组
+ List集合类中`元素有序`、且`可重复`，集合中的每个元素都有其对应的顺序索引。
    - 举例：List集合存储数据，就像银行门口客服，给每一个来办理业务的客户分配序号：第一个来的是“张三”，客服给他分配的是0；第二个来的是“李四”，客服给他分配的1；以此类推，最后一个序号应该是“总人数-1”。

![](images/1563549818689.png)

+ JDK API中List接口的实现类常用的有：`ArrayList`、`LinkedList`和`Vector`。

### 4.2 List接口方法
List除了从Collection集合继承的方法外，List 集合里添加了一些`根据索引`来操作集合元素的方法。

+ 插入元素
    - `void add(int index, Object ele)`:在index位置插入ele元素
    - boolean addAll(int index, Collection eles):从index位置开始将eles中的所有元素添加进来
+ 获取元素
    - `Object get(int index)`:获取指定index位置的元素
    - List subList(int fromIndex, int toIndex):返回从fromIndex到toIndex位置的子集合
+ 获取元素索引
    - int indexOf(Object obj):返回obj在集合中首次出现的位置
    - int lastIndexOf(Object obj):返回obj在当前集合中末次出现的位置
+ 删除和替换元素
    - `Object remove(int index)`:移除指定index位置的元素，并返回此元素
    - `Object set(int index, Object ele)`:设置指定index位置的元素为ele



举例：

```java
package com.atguigu.list;

import java.util.ArrayList;
import java.util.List;

public class TestListMethod {
    public static void main(String[] args) {
        // 创建List集合对象
        List<String> list = new ArrayList<String>();

        // 往 尾部添加 指定元素
        list.add("图图");
        list.add("小美");
        list.add("不高兴");

        System.out.println(list);
        // add(int index,String s) 往指定位置添加
        list.add(1,"没头脑");

        System.out.println(list);
        // String remove(int index) 删除指定位置元素  返回被删除元素
        // 删除索引位置为2的元素
        System.out.println("删除索引位置为2的元素");
        System.out.println(list.remove(2));

        System.out.println(list);

        // String set(int index,String s)
        // 在指定位置 进行 元素替代（改）
        // 修改指定位置元素
        list.set(0, "三毛");
        System.out.println(list);

        // String get(int index)  获取指定位置元素
        // 跟size() 方法一起用  来 遍历的
        for(int i = 0;i<list.size();i++){
            System.out.println(list.get(i));
        }
        //还可以使用增强for
        for (String string : list) {
            System.out.println(string);
        }
    }
}
```

> 注意：在JavaSE中List名称的类型有两个，一个是java.util.List集合接口，一个是java.awt.List图形界面的组件，别导错包了。
>

### 4.3 List接口主要实现类：ArrayList
+ ArrayList 是 List 接口的`主要实现类`
+ 本质上，ArrayList是对象引用的一个”变长”数组
+ Arrays.asList(…) 方法返回的 List 集合，既不是 ArrayList 实例，也不是 Vector 实例。 Arrays.asList(…) 返回值是一个固定长度的 List 集合![](images/image-20220408210743342.png)

### 4.4 List的实现类之二：LinkedList
+ 对于频繁的插入或删除元素的操作，建议使用LinkedList类，效率较高。这是由底层采用链表（双向链表）结构存储数据决定的。

![](images/image-20220408225615829.png)

+ 特有方法：
    - void addFirst(Object obj)
    - void addLast(Object obj)	
    - Object getFirst()
    - Object getLast()
    - Object removeFirst()
    - Object removeLast()

### 4.5 List的实现类之三：Vector
+ Vector 是一个`古老`的集合，JDK1.0就有了。大多数操作与ArrayList相同，区别之处在于Vector是`线程安全`的。
+ 在各种List中，最好把`ArrayList作为默认选择`。当插入、删除频繁时，使用LinkedList；Vector总是比ArrayList慢，所以尽量避免使用。
+ 特有方法：
    - void addElement(Object obj)
    - void insertElementAt(Object obj,int index)
    - void setElementAt(Object obj,int index)
    - void removeElement(Object obj)
    - void removeAllElements()

### 4.6 练习
**面试题：**

```java
@Test
public void testListRemove() {
    List list = new ArrayList();
    list.add(1);
    list.add(2);
    list.add(3);
    updateList(list);
    System.out.println(list);//[1,2]
}

private static void updateList(List list) {
    list.remove(2);  
}

```

**练习1：**

+ 定义学生类，属性为姓名、年龄，提供必要的getter、setter方法，构造器，toString()，equals()方法。
+ 使用ArrayList集合，保存录入的多个学生对象。
+ 循环录入的方式，1：继续录入，0：结束录入。
+ 录入结束后，用foreach遍历集合。
+ 代码实现，效果如图所示：![](images/1559890098509.png)

```java
package com.atguigu.test01;

import java.util.ArrayList;
import java.util.Scanner;

public class StudentTest {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        ArrayList stuList = new ArrayList();

        for (;;) {

            System.out.println("选择（录入 1 ；结束 0）");
            int x = scanner.nextInt();//根据x的值，判断是否需要继续循环

            if (x == 1) {
                System.out.println("姓名");
                String name = scanner.next();
                System.out.println("年龄");
                int age = scanner.nextInt();
                Student stu = new Student(age, name);
                stuList.add(stu);

            } else if (x == 0) {
                break;

            } else {

                System.out.println("输入有误，请重新输入");
            }
        }

        for (Object stu : stuList) {
            System.out.println(stu);
        }
    }
}

public class Student {

    private int age;
    private String name;

    public Student() {
    }

    
    public Student(int age, String name) {
        super();
        this.age = age;
        this.name = name;
    }


    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;

    }

    @Override
    public String toString() {
        return "Student [age=" + age + ", name=" + name + "]";
    }

}
```

**练习2：**

	1、请定义方法public static int listTest(Collection list,String s)统计集合中指定元素出现的次数

	2、创建集合，集合存放随机生成的30个小写字母

	3、用listTest统计，a、b、c、x元素的出现次数

	4、效果如下

![](images/1559896150606.png)

```java
package com.atguigu.test02;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Random;

public class Test02 {
    public static void main(String[] args) {
        Collection list = new ArrayList();
        Random rand = new Random();
        for (int i = 0; i < 30; i++) {
            list.add((char)(rand.nextInt(26)+97)+"");
        }
        System.out.println(list);
        System.out.println("a:"+listTest(list, "a"));	
        System.out.println("b:"+listTest(list, "b"));	
        System.out.println("c:"+listTest(list, "c"));
        System.out.println("x:"+listTest(list, "x"));	
    }

    public static int listTest(Collection list, String string) {
        int count = 0;
        for (Object object : list) {
            if(string.equals(object)){
                count++;
            }
        }
        return count;
    }
}

```

**练习3：KTV点歌系统**

**描述**

分别使用ArrayList和LinkedList集合，编写一个**`KTV点歌系统`**的程序。在程序中：

+ 指令1代表添加歌曲
+ 指令2代表将所选歌曲置顶
+ 指令3代表将所选歌曲提前一位
+ 指令4代表退出该系统

要求根据用户输入的指令和歌曲名展现歌曲列表。例如输入指令1，输入歌曲名"爱你一万年"，则输出“当前歌曲列表：[爱你一万年]”。

**提示**

+ 为了指引用户操作，首先要将各个指令所表示的含义打印到控制台

```java
System.out.println("-------------欢迎来到点歌系统------------");
System.out.println("1.添加歌曲至列表");
System.out.println("2.将歌曲置顶");
System.out.println("3.将歌曲前移一位");
System.out.println("4.退出");
```

+ 程序中需要创建一个集合作为歌曲列表，并向其添加一部分歌曲
+ 通过ArrayList或LinkedList集合定义的方法操作歌曲列表

**代码**

+ 使用ArrayList集合模拟点歌系统的实现代码，如下所示：

```java
/**
 * @author 尚硅谷-宋红康
 * @create 20:26
 */
public class KTVByArrayList {
    private static ArrayList musicList = new ArrayList();// 创建歌曲列表
    private static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        addMusicList();// 添加一部分歌曲至歌曲列表
        boolean flag = true;
        while (flag) {
            System.out.println("当前歌曲列表：" + musicList);
            System.out.println("-------------欢迎来到点歌系统------------");
            System.out.println("1.添加歌曲至列表");
            System.out.println("2.将歌曲置顶");
            System.out.println("3.将歌曲前移一位");
            System.out.println("4.退出");
            System.out.print("请输入操作序号：");
            int key = sc.nextInt();// //接收键盘输入的功能选项序号
            // 执行序号对应的功能
            switch (key) {
                case 1:// 添加歌曲至列表
                    addMusic();
                    break;
                case 2:// 将歌曲置顶
                    setTop();
                    break;
                case 3:// 将歌曲前移一位
                    setBefore();
                    break;
                case 4:// 退出
                    System.out.println("----------------退出---------------");
                    System.out.println("您已退出系统");
                    flag = false;
                    break;
                default:
                    System.out.println("----------------------------------");
                    System.out.println("功能选择有误，请输入正确的功能序号!");
                    break;
            }

        }
    }

    // 初始时添加歌曲名称
    private static void addMusicList() {
        musicList.add("本草纲目");
        musicList.add("你是我的眼");
        musicList.add("老男孩");
        musicList.add("白月光与朱砂痣");
        musicList.add("不谓侠");
        musicList.add("爱你");
    }

    // 执行添加歌曲
    private static void addMusic() {
        System.out.print("请输入要添加的歌曲名称：");
        String musicName = sc.next();// 获取键盘输入内容
        musicList.add(musicName);// 添加歌曲到列表的最后
        System.out.println("已添加歌曲：" + musicName);
    }

    // 执行将歌曲置顶
    private static void setTop() {
        System.out.print("请输入要置顶的歌曲名称：");
        String musicName = sc.next();// 获取键盘输入内容
        int musicIndex = musicList.indexOf(musicName);// 查找指定歌曲位置
        if (musicIndex < 0) {// 判断输入歌曲是否存在
            System.out.println("当前列表中没有输入的歌曲！");
        }else if(musicIndex == 0){
            System.out.println("当前歌曲默认已置顶！");
        }else {
            musicList.remove(musicName);// 移除指定的歌曲
            musicList.add(0, musicName);// 将指定的歌曲放到第一位
            System.out.println("已将歌曲《" + musicName + "》置顶");
        }
    }

    // 执行将歌曲置前一位
    private static void setBefore() {
        System.out.print("请输入要置前的歌曲名称：");
        String musicName = sc.next();// 获取键盘输入内容
        int musicIndex = musicList.indexOf(musicName);// 查找指定歌曲位置
        if (musicIndex < 0) {// 判断输入歌曲是否存在
            System.out.println("当前列表中没有输入的歌曲！");
        } else if (musicIndex == 0) {// 判断歌曲是否已在第一位
            System.out.println("当前歌曲已在最顶部！");
        } else {
            musicList.remove(musicName);// 移除指定的歌曲
            musicList.add(musicIndex - 1, musicName);// 将指定的歌曲放到前一位
            System.out.println("已将歌曲《" + musicName + "》置前一位");
        }
    }
}
```
