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

