### 数据结构的逻辑关系
1. **线性结构**：一对一关系，例如数组和链表。
2. **树状结构**：一对多关系，例如树和二叉树。
3. **图结构**：多对多关系，例如图和网络。

### 数据存储的结构
1. **顺序结构**：数据按顺序存储，例如数组。
2. **链式结构**：数据通过指针链接，例如链表。
3. **索引结构**：通过索引访问数据，例如数据库索引。
4. **散列结构**：通过哈希函数访问数据，例如哈希表。

### 常见的存储结构
1. **线性表**（一对一关系）：
    - 一维数组
    - 单向链表
    - 双向链表
    - 栈
    - 队列
2. **树**（一对多关系）：
    - 各种树，例如二叉树、B+树
3. **图**（多对多关系）：
    - 图结构，例如邻接矩阵、邻接表
4. **哈希表**：
    - 例如HashMap、HashSet

### 相关的算法操作
1. **分配资源，建立结构，释放资源**
2. **插入和删除**
3. **获取和遍历**
4. **修改和排序**

### 常见存储结构
1. **数组**：顺序存储，访问速度快，但插入和删除操作效率低。
2. **链表**：链式存储，插入和删除操作效率高，但访问速度较慢。



链表的基本单位是节点 （Node）

class Node{

Object data;

Node next;



public Node(Object data){

this.data=data;

}

}



创建对象

Node node1 = new Node("AA");

Node node2 = new Node("BB");

node1.next = node2;



双向链表

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731491511928-02379174-c219-437e-9a48-a9d6eff65045.png)

class Node {

Node prev;

Object data;

Node next;



public Node(Object data){

this.data = data;

}



public Node(Node prev,Object data,Node next){

this.prev = prev;

this.data = data;

this.next = next;

}



}

创建对象

Node node1 = new Node(null,"AA",null);

Node node2 = new Node(node1,"BB",null);

Node node3 = new Node(node2,"CC",null);



node1.next = node2;

node2.next = node3;





常见存储结构 二叉树

class TreeNode{

TreeNode left;

Object data;

TreeNode right;



public TreeNode(Object data){

this.data = data;

}



public TreeNode(TreeNode left,Object data,TreeNode right){

this.left = left;

this.data = data;

this.roight = right;

}

}

创建对象 

TreeNode node1 = new TreeNode(null,"AA",null);

TreeNode leftNode = new TreeNode(null,"BB",null);

TreeNode rightNode = new TreeNode(null,"CC",null);

node1.left = leftNode;

node1.right = rightNode;







class Stack{

Object[] values;

int size;//记录存储的元素个数



public Stack(int length){

values = new Object[length];

}



//入栈

public void push(Object ele){

if(size >= values.length){

throw new RuntimeException("栈空间已满，入栈失败");

}



values[size] = ele;

size++;

}



//出栈 

public Object pop(){

if(size <= 0){

throw new RuntimeException("栈空间已空，出栈失败");

}



Object obj = values[size - 1];

values[size - 1] = null;

size--;

return obj;

}



}



常见存储结构 栈（stack，先进后出，first in last out ，FIL0 ，LIF0）



常见存储结构 队列 （queue ，先进先出 ，first in first out，FIF0）

属于抽象数据类型（ADT）

可以使用数组或链表来构建



class Queue{

Object[] values;

int size;//记录存储元素的个数



public Queue(int length){

values = new Object[length];

}



public void add(Object ele){

//添加

if(size >= values.length){

throw new RuntimeException("队列已满，添加失败");

}

values[size] = ele;

size++;

}



public Object get(){

if(size <= 0){

throw new RuntimeException("队列已空，获取失败");

}



Object obj = values[0];



//数据前移

for(int i = 0;i < size -1;i++){

values[i] = values[i + 1];

}

//最后一个元素置空

values[size - 1] = null;

size--;



return obj;

}

}



**ArrayList**

1. **ArrayList的特点**：
    - 实现了List接口，存储有序的、可以重复的数据。
    - 底层使用`Object[]`数组存储。
    - 线程不安全的。
2. **ArrayList源码解析**：

**JDK 7版本**（以JDK 1.7.0_07为例）：

    - java

```plain
// 如下代码的执行：底层会初始化数组，数组的长度为10。
Object[] elementData = new Object[10];
ArrayList<String> list = new ArrayList<>();
list.add("AA"); // elementData[0] = "AA";
list.add("BB"); // elementData[1] = "BB";
```

当要添加第11个元素的时候，底层的`elementData`数组已满，则需要扩容。默认扩容为原来长度的1.5倍，并将原有数组中的元素复制到新的数组中。

**Vector**

1. **Vector的特点**：
    - 实现了List接口，存储有序的、可以重复的数据。
    - 底层使用`Object[]`数组存储。
    - 线程安全的。

**Vector源码解析**（以JDK 1.8.0_271为例）：

2. java

```plain
Vector v = new Vector(); // 底层初始化数组，长度为10。
Object[] elementData = new Object[10];
v.add("AA"); // elementData[0] = "AA";
v.add("BB"); // elementData[1] = "BB";
```



三、LinkedList

1. **LinkedList的特点**：
    - 实现了List接口，存储有序的、可以重复的数据。
    - 底层使用双向链表存储。
    - 线程不安全的。

**LinkedList在JDK 8中的源码解析**：

2. java

```plain
LinkedList<String> list = new LinkedList<>(); // 底层没做啥
list.add("AA"); // 将 AA 封装到一个 Node 对象 1 中，last 对象的属性 first，last 都指向此 Node 对象 1
list.add("BB"); // 将 BB 封装到一个 Node 对象 2 中 对象 1 和对象 2 构成一个双向链表，同时 last 指向此 Node 对象 2
```



1. LinkedList是否存在扩容问题？No，LinkedList不涉及扩容问题，因为它使用的是链表结构，而不是数组。

四、启示与开发建议：

1. Vector基本不使用了。
2. ArrayList底层使用数组结构，查找和添加（尾部添加）操作效率高，时间复杂度为O(1)。删除和插入操作效率低，时间复杂度为O(n)。
3. LinkedList底层使用双向链表结构，删除和插入操作效率高，时间复杂度为O(1)。（有可能添加操作是O(1)）

在选择了ArrayList的前提下：

+ `new ArrayList()`：底层创建长度为10的数组。
+ `new ArrayList(int capacity)`：底层创建指定capacity长度的数组。

如果在开发中，大体确认数组的长度，则推荐使用`ArrayList(int capacity)`这个构造器，避免了底层的扩容，复制数组的效率会更高一些。



+ **HashMap中的所有的key彼此之间是不可重复的、无序的。所有的key就构成一个Set集合。**
+ key所在的类要重写`hashCode()`和`equals()`方法，以确保key的唯一性和正确的比较。
+ **HashMap中的所有的value彼此之间是可重复的、无序的。所有的value就构成一个Collection集合。**
+ value所在的类不需要重写`hashCode()`和`equals()`方法，因为HashMap对value的唯一性没有要求。
+ **HashMap中的一个key-value，就构成了一个entry。**
+ 这是正确的，一个entry表示一个键值对。
+ **HashMap中的所有的entry彼此之间是不可重复的、无序的。所有的entry就构成了一个Set集合。**
+ HashMap中的entry集合是通过`entrySet()`方法返回的，这个集合是一个Set，表示所有的键值对。  



### HashMap源码解析
#### 2.1 JDK 7中创建对象和添加数据过程（以JDK 1.7.0_07为例说明）：
java

```plain
// 创建对象的过程中，底层会初始化数组Entry[] table = new Entry[16];
HashMap<String, Integer> map = new HashMap<>();
map.put("AA", 78); // "AA"和78封装到一个Entry对象中，考虑将此对象添加到table数组中。
```

**添加/修改的过程**：

1. 将(key1, value1)添加到当前的map中：
    - 首先，需要调用key1所在类的`hashCode()`方法，计算key1对应的哈希值1，此哈希值1经过某种算法(`hash()`)之后，得到哈希值2。
    - 哈希值2再经过某种算法(`indexFor()`)之后，就确定了(key1, value1)在数组table中的索引位置i。
2. 如果此索引位置i的数组上没有元素，则(key1, value1)添加成功。
3. 如果此索引位置i的数组上有元素(key2, value2)，则需要继续比较key1和key2的哈希值2：
    - 如果key1的哈希值2与key2的哈希值2不相同，则(key1, value1)添加成功。
    - 如果key1的哈希值2与key2的哈希值2相同，则需要继续比较key1和key2的`equals()`，要调用key1所在类的`equals()`，将key2作为参数传递进去：
        * 调用`equals()`，返回false：则(key1, value1)添加成功。
        * 调用`equals()`，返回true：则认为key1和key2是相同的。默认情况下，value1替换原有的value2。

**说明**：

+ 情况1：将(key1, value1)存放到数组的索引i的位置。
+ 情况2、情况3：(key1, value1)元素与现有的(key2, value2)构成单向链表结构，(key1, value1)指向(key2, value2)。

**扩容**：

+ 随着不断的添加元素，在满足如下条件的情况下，会考虑扩容：
    - `(size >= threshold) && (null != table[i])`
+ 当元素的个数达到临界值（数组的长度 * 加载因子）时，就考虑扩容。默认的临界值 = 16 * 0.75 = 12。
+ 默认扩容为原来的2倍。

#### 2.2 JDK 8与JDK 7的不同之处（以JDK 1.8.0_271为例）：
+ JDK 8中引入了红黑树来优化链表的性能，当链表长度超过一定阈值（默认是8）时，链表会转换为红黑树，以提高查找和插入的效率。

#### 2.3 属性/字段：
+ `table`：存储元素的数组。
+ `size`：HashMap中存储的键值对的数量。
+ `threshold`：扩容的临界值。
+ `loadFactor`



### JDK 8与JDK 7的不同之处（以JDK 1.8.0_271为例）
1. **初始化数组**：
    - 在JDK 8中，当我们创建了HashMap实例以后，底层并没有初始化`table`数组。当首次添加(key, value)时，如果发现`table`尚未初始化，则对数组进行初始化。
    - 在JDK 7中，创建HashMap实例时，底层会立即初始化`table`数组。
2. **内部类**：
    - 在JDK 8中，HashMap底层定义了`Node`内部类，替换了JDK 7中的`Entry`内部类。意味着，我们创建的数组是`Node[]`。
    - 在JDK 7中，数组类型是`Entry[]`。
3. **元素添加方式**：
    - 在JDK 8中，如果当前的(key, value)经过一系列判断之后，可以添加到当前的数组索引i中。如果此时索引i位置上有元素，在JDK 8中是旧的元素指向新的(key, value)元素（尾插法）。
    - 在JDK 7中，是将新的(key, value)指向已有的旧的元素（头插法）。
4. **数据结构**：
    - JDK 7：数组 + 单向链表。
    - JDK 8：数组 + 单向链表 + 红黑树。
5. **红黑树的使用**：
    - 在JDK 8中，如果数组索引i位置上的元素的个数达到8，并且数组的长度达到64时，我们就将此索引i位置上的多个元素改为使用红黑树的结构进行存储。红黑树进行`put()`/`get()`/`remove()`操作的时间复杂度为O(logn)，比单向链表的时间复杂度O(n)更高效。

什么时候会使用红黑树变为单向链表：当使用红黑树的索引 i 上的元素个数少于 6 的时候，就会将红黑树结构退化为单向链表



### 2.3 属性/字段
java

```plain
int DEFAULT_INITIAL_CAPACITY = 1 << 4; // 默认的初始容量 16
static final int MAXIMUM_CAPACITY = 1 << 30; // 最大容量 1 << 30
static final float DEFAULT_LOAD_FACTOR = 0.75f; // 默认加载因子
static final int TREEIFY_THRESHOLD = 8; // 默认树化阈值8，当链表的长度达到这个值后，要考虑树化
static final int UNTREEIFY_THRESHOLD = 6; // 默认反树化阈值6，当树中结点的个数达到此阈值后，要考虑变为链表
static final int MIN_TREEIFY_CAPACITY = 64; // 最小树化容量64
transient Node<K, V>[] table; // 数组
transient int size; // 记录有效映射关系的对数，也是Entry对象的个数
int threshold; // 阈值，当size达到值时，考虑扩容
final float loadFactor; // 加载因子，影响扩容的频率
```

**说明**：

+ 当单个链表的结点个数达到8，并且`table`的长度达到64时，才会树化。
+ 当单个链表的结点个数达到8，但是



### LinkedHashMap
**LinkedHashMap**在HashMap使用的数组+单向链表+红黑树的基础上，又增加了一对双向链表，记录添加的(key, value)先后顺序，便于我们遍历所有的key-value。

**LinkedHashMap重写了HashMap的如下方法**：

java

```plain
Node<K, V> newNode(int hash, K key, V value, Node<K, V> e) {
    LinkedHashMap.Entry<K, V> p = new LinkedHashMap.Entry<K, V>(hash, key, value, e);
    linkNodeLast(p);
    return p;
}
```

**底层结构**： LinkedHashMap内部定义了一个Entry：

java

```plain
static class Entry<K, V> extends HashMap.Node<K, V> {
    Entry<K, V> before, after; // 增加的一对双向链表
    Entry(int hash, K key, V value, Node<K, V> next) {
        super(hash, key, value, next);
    }
}
```

### HashSet和LinkedHashSet的源码分析
**HashSet**：

+ HashSet基于HashMap实现，底层使用HashMap来存储元素。
+ HashSet不允许重复元素，且不保证元素的顺序。

**LinkedHashSet**：

+ LinkedHashSet继承自HashSet，底层使用LinkedHashMap来存储元素。





