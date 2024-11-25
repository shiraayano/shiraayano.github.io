泛型



比喻 标签纸



#### 什么是泛型？
泛型就是允许在自定义类，接口时通过一个 ` 标识 ` 表示类中的某个“属性的类型”或者是某个方法的“返回值或参数的类型”。这个类型参数在使用时（eg 继承或实现这个类的接口，创建对象或调用方法时）确定（即传入实际的类型参数，也称为类型实参）



#### 在集合中使用泛型之前可能会存在的问题
1，类型不安全，因为 add()的参数时 Object 类型，意味着任何类型的对象都可以添加成功

2，需要使用强转操作，繁琐。还可能倒是 ClassCastException 异常



#### 使用说明
集合框架你在声明接口和其实现类时，使用了泛型（JDK5.0），在实例化集合对象时，如果没有泛型，则默认为 Object 类型的数据。

如果使用了泛型，则需指明泛型的具体类型。一旦指明了泛型的具体类型，则在集合相关的方法中。凡是使用类的泛型的位置，都替换为具体的泛型类型。



#### 在集合，比较器中使用泛型（重点）
```plain
class Test4{
    public static void main(String[] args) {
        //体会使用泛型的场景
        List list1 = new ArrayList();
        list1.add(34);
        list1.add(12);
        //问题1 类型不安全 因为add()的参数是Object类型 意味着任何类型的对象都录添加成功
        list1.add("AA");

        Iterator iterator = list1.iterator();
        while (iterator.hasNext()) {
            //问题2 需要使用强转 繁琐，还有可能导致ClassCastException异常
            Integer integer = (Integer) iterator.next();
            int score = integer;
            System.out.println(score);
        }
        
        /*
        34
        12
        Exception in thread "main" java.lang.ClassCastException: class java.lang.String cannot be cast to class java.lang.Integer (java.lang.String and java.lang.Integer are in module java.base of loader 'bootstrap')
        at Test4.main(CollectionsTest.java:85)*/
    }
}
```



 

```plain
class Test5{
    public static void main(String[] args) {
        List<Integer> list1 = new ArrayList<Integer>();
        list1.add(34);
        list1.add(12);
        list1.add(45);

        //list1.add("AA");
        //java: 不兼容的类型: java.lang.String无法转换为java.lang.Integer
        //编译报错 保证类型安全

        Iterator<Integer> iterator = list1.iterator();
        while (iterator.hasNext()) {
            Integer integer = (Integer) iterator.next();
            int score = integer;
            System.out.println(score);
            //因为添加的都是Intrger类型，所以避免了强转操作
        }

    }
}
```

```plain
class Test6{
    public static void main(String[] args) {
        //泛型在Map中的例子
        //HashMap<String,Integer> map = new HashMap<String,Integer>();
        HashMap<String,Integer> map = new HashMap<>();//类型推断 jdk7新特性

        map.put("Tom", 67);
        map.put("Jack", 23);
        map.put("Jill", 22);

        Set<Map.Entry<String,Integer>> entrySet = map.entrySet();
        Iterator<Map.Entry<String,Integer>> iterator = entrySet.iterator();
//       var Set = map.entrySet();
//       var Iterator = entrySet.iterator();
 //JDK10 新特性
        while (iterator.hasNext()) {
            Map.Entry<String,Integer> entry = iterator.next();
            String key = entry.getKey();
            Integer value = entry.getValue();
            System.out.println(key + "--->" +value);
        }
    }
}
```


泛型补充



### 泛型的作用
泛型（Generics）是Java语言的一项重要特性，它允许在定义类、接口和方法时使用类型参数，从而使代码更加通用和灵活。泛型的主要作用包括：

**类型安全**：

    - 泛型可以在编译时检查类型，从而避免了运行时的类型转换异常。例如，在使用集合时，泛型可以确保集合中的元素都是指定类型，避免了类型转换错误。
1. java

```plain
List<String> list = new ArrayList<>();
list.add("Hello");
// list.add(123); // 编译时会报错
```

**代码重用**：

    - 泛型使得代码更加通用，可以处理不同类型的数据，从而提高了代码的重用性。例如，泛型类和泛型方法可以适用于多种类型，而不需要为每种类型编写重复的代码。
2. java

```plain
public class Box<T> {
    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}

Box<String> stringBox = new Box<>();
stringBox.setValue("Hello");

Box<Integer> intBox = new Box<>();
intBox.setValue(123);
```

**减少类型转换**：

    - 泛型可以减少显式的类型转换操作，从而使代码更加简洁和易读。例如，在使用泛型集合时，不需要进行显式的类型转换。
3. java

```plain
List<String> list = new ArrayList<>();
list.add("Hello");
String str = list.get(0); // 不需要类型转换
```

**提高代码的可读性和可维护性**：

    - 泛型使得代码更加清晰，类型信息更加明确，从而提高了代码的可读性和可维护性。例如，通过泛型，可以清楚地知道集合中存储的元素类型。
4. java

```plain
Map<String, Integer> map = new HashMap<>();
map.put("one", 1);
map.put("two", 2);
```



ORM思想

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732413735596-c7540f4e-6e9c-42d6-9c97-2ed0fb0a1c79.png)



### ORM思想
#### 概念
**ORM**（Object-Relational Mapping，面向对象关系映射）是一种通过描述对象与数据库之间的映射关系，将面向对象编程语言中的对象与关系数据库中的数据进行自动转换的技术。它使得开发者可以使用面向对象的方式来操作数据库，而不需要编写大量的SQL语句。

#### 优点
1. **提高开发效率**：开发者可以专注于业务逻辑，而不需要关心底层的数据库操作。
2. **减少代码量**：通过自动生成SQL语句，减少了手写SQL的工作量。
3. **增强可维护性**：ORM框架提供了统一的接口，使得代码更易于维护和扩展。
4. **跨数据库支持**：ORM框架通常支持多种数据库，使得应用程序可以更容易地切换数据库。

#### 常见的ORM框架
1. **Hibernate**：Java领域最流行的ORM框架，提供了强大的映射功能和丰富的配置选项。
2. **Entity Framework**：微软提供的.NET平台上的ORM框架，集成在Visual Studio中，使用方便。
3. **Django ORM**：Python的Django框架自带的ORM，简洁易用，适合快速开发。

#### 工作原理
1. **映射配置**：通过配置文件或注解，将类与数据库表、类的属性与表的字段进行映射。
2. **对象操作**：开发者通过操作对象来进行数据的增删改查，ORM框架会自动生成相应的SQL语句并执行。
3. **事务管理**：ORM框架通常提供了事务管理功能，确保数据操作的原子性和一致性。

#### 示例代码（以Hibernate为例）
java

```plain
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "username")
    private String username;

    @Column(name = "password")
    private String password;

    // Getters and setters
}

// 使用Hibernate进行数据操作
Session session = sessionFactory.openSession();
Transaction transaction = session.beginTransaction();

User user = new User();
user.setUsername("john_doe");
user.setPassword("password123");

session.save(user);
transaction.commit();
session.close();
```



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732415127521-9bb56bf0-582f-44aa-8242-88870da5173b.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732415227334-3f7202f7-3288-4ebd-8331-2f737a560e06.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732415211587-afee9a48-b8e3-4853-9781-34294e8922b1.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732415694136-a3182a33-2d06-4b23-9b49-c772c2d11896.png)

想要使用可以用通配符?

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732415423560-5d64a6ba-f740-4412-9955-c1ef2a987015.png)

在通配符时无法写入数据

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732415580657-f917306f-2907-426f-aaab-7392e86b20e6.png)

除了null



有限制条件的通配符



ArrayList<?extends A>:可以将List<A>或List<B>赋值给List<?extends A>。其中B类是A类的子类,

List<?super A>:可以将List<A>或List<B>赋值给List<?extends A>。其中B类是A类的父类。



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732415843729-90ebb887-4b00-48f3-b6e0-ec26f4b4450b.png)  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732415868702-4eadc704-1ed5-40cb-97ce-2de8a7380079.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732416256999-59d7fabd-a525-4e1f-8c29-ec374eeb20cd.png)

有限制条件的统配符的读写操作(难、了解)

技巧:开发中，遇到了带限制条件的通配符，在赋值时，如果没报错，那就正常使用

如果报错了，知道不能这样写。改改!



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732416448619-cf4d479d-dc5d-4bd7-b19c-98a73f497414.png)




