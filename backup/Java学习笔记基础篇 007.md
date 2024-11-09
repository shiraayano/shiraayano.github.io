
## 6. 再谈同步
### 6.1 单例设计模式的线程安全问题
#### 6.1.1 饿汉式没有线程安全问题
饿汉式：在类初始化时就直接创建单例对象，而类初始化过程是没有线程安全问题的

形式一：

```java
package com.atguigu.single.hungry;

public class HungrySingle {
    private static HungrySingle INSTANCE = new HungrySingle(); //对象是否声明为final 都可以
    
    private HungrySingle(){}
    
    public static HungrySingle getInstance(){
        return INSTANCE;
    }
}
```

形式二：

```java
/*
public class HungryOne{
    public static final HungryOne INSTANCE = new HungryOne();
    private HungryOne(){}
}*/

public enum HungryOne{
    INSTANCE
}
```

测试类：

```java
package com.atguigu.single.hungry;

public class HungrySingleTest {

    static HungrySingle hs1 = null;
    static HungrySingle hs2 = null;

    //演示存在的线程安全问题
    public static void main(String[] args) {

        Thread t1 = new Thread() {
            @Override
            public void run() {
                hs1 = HungrySingle.getInstance();
            }
        };

        Thread t2 = new Thread() {
            @Override
            public void run() {
                hs2 = HungrySingle.getInstance();
            }
        };

        t1.start();
        t2.start();

        try {
            t1.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        try {
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println(hs1);
        System.out.println(hs2);
        System.out.println(hs1 == hs2);//true
    }

}
```

#### 6.1.2 懒汉式线程安全问题
懒汉式：延迟创建对象，第一次调用getInstance方法再创建对象

形式一：

```java
package com.atguigu.single.lazy;

public class LazyOne {
    private static LazyOne instance;

    private LazyOne(){}

    //方式1：
    public static synchronized LazyOne getInstance1(){
        if(instance == null){
            instance = new LazyOne();
        }
        return instance;
    }
    //方式2：
    public static LazyOne getInstance2(){
        synchronized(LazyOne.class) {
            if (instance == null) {
                instance = new LazyOne();
            }
            return instance;
        }
    }
    //方式3：
    public static LazyOne getInstance3(){
        if(instance == null){
            synchronized (LazyOne.class) {
                try {
                    Thread.sleep(10);//加这个代码，暴露问题
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                if(instance == null){
                    instance = new LazyOne();
                }
            }
        }

        return instance;
    }
    /*
    注意：上述方式3中，有指令重排问题
    mem = allocate(); 为单例对象分配内存空间
    instance = mem;   instance引用现在非空，但还未初始化
    ctorSingleton(instance); 为单例对象通过instance调用构造器
    从JDK2开始，分配空间、初始化、调用构造器会在线程的工作存储区一次性完成，然后复制到主存储区。但是需要   
    volatile关键字，避免指令重排。
    */
    
}

```

形式二：使用内部类

```java
package com.atguigu.single.lazy;

public class LazySingle {
    private LazySingle(){}
    
    public static LazySingle getInstance(){
        return Inner.INSTANCE;
    }
    
    private static class Inner{
        static final LazySingle INSTANCE = new LazySingle();
    }
    
}
```

> 内部类只有在外部类被调用才加载，产生INSTANCE实例；又不用加锁。
>
> 此模式具有之前两个模式的优点，同时屏蔽了它们的缺点，是最好的单例模式。
>
> 此时的内部类，使用enum进行定义，也是可以的。
>

测试类：

```java
package com.atguigu.single.lazy;

import org.junit.Test;

public class TestLazy {
    @Test
    public void test01(){
        LazyOne s1 = LazyOne.getInstance();
        LazyOne s2 = LazyOne.getInstance();

        System.out.println(s1);
        System.out.println(s2);
        System.out.println(s1 == s2);
    }

    //把s1和s2声明在外面，是想要在线程的匿名内部类中为s1和s2赋值
    LazyOne s1;
    LazyOne s2;
    @Test
    public void test02(){
        Thread t1 = new Thread(){
            public void run(){
                s1 = LazyOne.getInstance();
            }
        };
        Thread t2 = new Thread(){
            public void run(){
                s2 = LazyOne.getInstance();
            }
        };

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println(s1);
        System.out.println(s2);
        System.out.println(s1 == s2);
    }


    LazySingle obj1;
    LazySingle obj2;
    @Test
    public void test03(){
        Thread t1 = new Thread(){
            public void run(){
                obj1 = LazySingle.getInstance();
            }
        };
        Thread t2 = new Thread(){
            public void run(){
                obj2 = LazySingle.getInstance();
            }
        };

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println(obj1);
        System.out.println(obj2);
        System.out.println(obj1 == obj2);
    }
}

```



三种方案实现线程安全

### 1. 同步整个方法
这种方法简单直接，通过将`getInstance`方法声明为`synchronized`来保证线程安全。但是这样做会降低程序的性能，因为每次调用`getInstance`时都会锁住整个方法，即使`instance`已经被初始化了。

```java
public class BankTest {
    //static Bank bank = new Bank();
    //static Bank bank2 = new Bank();

    public static void main(String[] args) {
        Thread t1 = new Thread() {
            @Override
            public void run() {
                System.out.println(Bank.getInstance());
            }
        };

        Thread t2 = new Thread() {
            @Override
            public void run() {
                System.out.println(Bank.getInstance());
            }
        };

        t1.start();
        t2.start();
    }
}

class Bank {
    private Bank() {}

    private static Bank instance = null;

    public static synchronized Bank getInstance() {
        if (instance == null) {
            instance = new Bank();
        }
        return instance;
    }
}
```

### 2. 双重检查锁定（Double-Check Locking）
这是更高效的实现方式，它只在`instance`未被初始化时进行同步操作。这样可以避免每次调用`getInstance`时都进行同步，提高了性能。

```java
public class BankTest {
    //static Bank bank = new Bank();
    //static Bank bank2 = new Bank();

    public static void main(String[] args) {
        Thread t1 = new Thread() {
            @Override
            public void run() {
                System.out.println(Bank.getInstance());
            }
        };

        Thread t2 = new Thread() {
            @Override
            public void run() {
                System.out.println(Bank.getInstance());
            }
        };

        t1.start();
        t2.start();
    }
}

class Bank {
    private Bank() {}

    private static volatile Bank instance = null;

    public static Bank getInstance() {
        if (instance == null) { // 第一次检查
            synchronized (Bank.class) {
                if (instance == null) { // 第二次检查
                    instance = new Bank();
                }
            }
        }
        return instance;
    }
}
```

### 3. 静态内部类
这是最推荐的方式，因为它既保证了线程安全，又避免了同步带来的性能损失。静态内部类在第一次被加载时才会初始化，因此是延迟加载的。

```java
public class BankTest {
    //static Bank bank = new Bank();
    //static Bank bank2 = new Bank();

    public static void main(String[] args) {
        Thread t1 = new Thread() {
            @Override
            public void run() {
                System.out.println(Bank.getInstance());
            }
        };

        Thread t2 = new Thread() {
            @Override
            public void run() {
                System.out.println(Bank.getInstance());
            }
        };

        t1.start();
        t2.start();
    }
}

class Bank {
    private Bank() {}

    private static class BankHolder {
        private static final Bank INSTANCE = new Bank();
    }

    public static Bank getInstance() {
        return BankHolder.INSTANCE;
    }
}
```

### 总结
+ **同步整个方法**：简单但性能较差，每次调用`getInstance`都会加锁。
+ **双重检查锁定**：性能较好，只在`instance`未被初始化时进行同步。
+ **静态内部类**：推荐使用，既线程安全又延迟加载，性能最好。

你可以根据具体需求选择适合的实现方式。希望这些示例对你有所帮助！



### 6.2 死锁
不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步资源，就形成了线程的死锁。

![](images/thread-lock.png)

> 【小故事】
>
> 面试官：你能解释清楚什么是死锁，我就录取你！  
面试者：你录取我，我就告诉你什么是死锁！  
….  
恭喜你，面试通过了
>



1.如何看待死锁?

不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步资源，就形成了线程的死锁。

我们编写程序时，要避免出现死锁。

2.诱发死锁的原因?

互斥条件

占用且等待

不可抢夺(或不可抢占)

循环等待

以上4个条件，同时出现就会触发死锁。

3.如何避免死锁?

针对条件1:互斥条件基本上无法被破坏。因为线程需要通过互斥解决安全问题。

针对条件2:可以考虑一次性申请所有所需的资源，这样就不存在等待的问题。

针对条件3:占用部分资源的线程在进一步申请其他资源时，如果申请不到，就主动释放掉已经占用的资源。

针对条件4:可以将资源改为线性顺序。申请资源时，先申请序号较小的，这样避免循环等待问题。





1.步骤:

步骤1.创建Lock的实例，需要确保多个线程共用同一个Lock实例!需要考虑将此对象声明为static final

步骤2.执行lock()方法，锁定对共享资源的调用

步骤了.unlock(的调用，释放对共享数据的锁定

2.面试题:

synchronized同步的方式与Lock的对比?

synchronized不管是同步代码块还是同步方法，都需要在结束一对{}之后，释放对同步监视器的调用

-ock是通过两个方法控制需要被同步的代码，更灵活一些。

Lock作为接口，提供了多种实现类，适合更多更复杂的场景，效率更高。





一旦出现死锁，整个程序既不会发生异常，也不会给出任何提示，只是所有线程处于阻塞状态，无法继续。

举例1：

```java
public class DeadLockTest {
    public static void main(String[] args) {

        StringBuilder s1 = new StringBuilder();
        StringBuilder s2 = new StringBuilder();

        new Thread() {
            public void run() {
                synchronized (s1) {
                    s1.append("a");
                    s2.append("1");
                    
                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                    synchronized (s2) {
                        s1.append("b");
                        s2.append("2");

                        System.out.println(s1);
                        System.out.println(s2);

                    }
                }
            }
        }.start();

        new Thread() {
            public void run() {
                synchronized (s2) {
                    s1.append("c");
                    s2.append("3");

                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    
                    synchronized (s1) {
                        s1.append("d");
                        s2.append("4");

                        System.out.println(s1);
                        System.out.println(s2);

                    }

                }
            }
        }.start();

    }
}
```

举例2：

```java

class A {
    public synchronized void foo(B b) {
        System.out.println("当前线程名: " + Thread.currentThread().getName()
                + " 进入了A实例的foo方法"); // ①
        try {
            Thread.sleep(200);
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        }
        System.out.println("当前线程名: " + Thread.currentThread().getName()
                + " 企图调用B实例的last方法"); // ③
        b.last();
    }

    public synchronized void last() {
        System.out.println("进入了A类的last方法内部");
    }
}

class B {
    public synchronized void bar(A a) {
        System.out.println("当前线程名: " + Thread.currentThread().getName()
                + " 进入了B实例的bar方法"); // ②
        try {
            Thread.sleep(200);
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        }
        System.out.println("当前线程名: " + Thread.currentThread().getName()
                + " 企图调用A实例的last方法"); // ④
        a.last();
    }

    public synchronized void last() {
        System.out.println("进入了B类的last方法内部");
    }
}

public class DeadLock implements Runnable {
    A a = new A();
    B b = new B();

    public void init() {
        Thread.currentThread().setName("主线程");
        // 调用a对象的foo方法
        a.foo(b);
        System.out.println("进入了主线程之后");
    }

    public void run() {
        Thread.currentThread().setName("副线程");
        // 调用b对象的bar方法
        b.bar(a);
        System.out.println("进入了副线程之后");
    }

    public static void main(String[] args) {
        DeadLock dl = new DeadLock();
        new Thread(dl).start();
        dl.init();
    }
}
```

举例3：

```java
public class TestDeadLock {
    public static void main(String[] args) {
        Object g = new Object();
        Object m = new Object();
        Owner s = new Owner(g,m);
        Customer c = new Customer(g,m);
        new Thread(s).start();
        new Thread(c).start();
    }
}
class Owner implements Runnable{
    private Object goods;
    private Object money;

    public Owner(Object goods, Object money) {
        super();
        this.goods = goods;
        this.money = money;
    }

    @Override
    public void run() {
        synchronized (goods) {
            System.out.println("先给钱");
            synchronized (money) {
                System.out.println("发货");
            }
        }
    }
}
class Customer implements Runnable{
    private Object goods;
    private Object money;

    public Customer(Object goods, Object money) {
        super();
        this.goods = goods;
        this.money = money;
    }

    @Override
    public void run() {
        synchronized (money) {
            System.out.println("先发货");
            synchronized (goods) {
                System.out.println("再给钱");
            }
        }
    }
}
```

**诱发死锁的原因：**

+ 互斥条件
+ 占用且等待
+ 不可抢夺（或不可抢占）
+ 循环等待

以上4个条件，同时出现就会触发死锁。

**解决死锁：**

死锁一旦出现，基本很难人为干预，只能尽量规避。可以考虑打破上面的诱发条件。

针对条件1：互斥条件基本上无法被破坏。因为线程需要通过互斥解决安全问题。

针对条件2：可以考虑一次性申请所有所需的资源，这样就不存在等待的问题。

针对条件3：占用部分资源的线程在进一步申请其他资源时，如果申请不到，就主动释放掉已经占用的资源。

针对条件4：可以将资源改为线性顺序。申请资源时，先申请序号较小的，这样避免循环等待问题。

### 6.3 JDK5.0新特性：Lock(锁)
+ JDK5.0的新增功能，保证线程的安全。与采用synchronized相比，Lock可提供多种锁方案，更灵活、更强大。Lock通过显式定义同步锁对象来实现同步。同步锁使用Lock对象充当。
+ java.util.concurrent.locks.Lock接口是控制多个线程对共享资源进行访问的工具。锁提供了对共享资源的独占访问，每次只能有一个线程对Lock对象加锁，线程开始访问共享资源之前应先获得Lock对象。
+ 在实现线程安全的控制中，比较常用的是`ReentrantLock`，可以显式加锁、释放锁。
    - ReentrantLock类实现了 Lock 接口，它拥有与 synchronized 相同的并发性和内存语义，但是添加了类似锁投票、定时锁等候和可中断锁等候的一些特性。此外，它还提供了在激烈争用情况下更佳的性能。
+ Lock锁也称同步锁，加锁与释放锁方法，如下：
    - public void lock() :加同步锁。
    - public void unlock() :释放同步锁。
+ 代码结构

```java
class A{
    //1. 创建Lock的实例，必须确保多个线程共享同一个Lock实例
    private final ReentrantLock lock = new ReenTrantLock();
    public void m(){
        //2. 调动lock()，实现需共享的代码的锁定
        lock.lock();
        try{
            //保证线程安全的代码;
        }
        finally{
            //3. 调用unlock()，释放共享代码的锁定
            lock.unlock();  
        }
    }
}

```

> 注意：如果同步代码有异常，要将unlock()写入finally语句块。
>

举例：

```java
import java.util.concurrent.locks.ReentrantLock;

class Window implements Runnable{
    int ticket = 100;
    //1. 创建Lock的实例，必须确保多个线程共享同一个Lock实例
    private final ReentrantLock lock = new ReentrantLock();
    public void run(){
        
        while(true){
            try{
                //2. 调动lock()，实现需共享的代码的锁定
                lock.lock();
                if(ticket > 0){
                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(ticket--);
                }else{
                    break;
                }
            }finally{
                //3. 调用unlock()，释放共享代码的锁定
                lock.unlock();
            }
        }
    }
}

public class ThreadLock {
    public static void main(String[] args) {
        Window t = new Window();
        Thread t1 = new Thread(t);
        Thread t2 = new Thread(t);
        
        t1.start();
        t2.start();
    }
}
```

**synchronized与Lock的对比**

1. Lock是显式锁（手动开启和关闭锁，别忘记关闭锁），synchronized是隐式锁，出了作用域、遇到异常等自动解锁
2. Lock只有代码块锁，synchronized有代码块锁和方法锁
3. 使用Lock锁，JVM将花费较少的时间来调度线程，性能更好。并且具有更好的扩展性（提供更多的子类），更体现面向对象。
4. （了解）Lock锁可以对读不加锁，对写加锁，synchronized不可以
5. （了解）Lock锁可以有多种获取锁的方式，可以从sleep的线程中抢到锁，synchronized不可以

> 说明：开发建议中处理线程安全问题优先使用顺序为：
>
> •    Lock ----> 同步代码块 ----> 同步方法
>

## 7. 线程的通信
### 7.1 线程间通信
**为什么要处理线程间通信：**

当我们`需要多个线程`来共同完成一件任务，并且我们希望他们`有规律的执行`，那么多线程之间需要一些通信机制，可以协调它们的工作，以此实现多线程共同操作一份数据。

比如：线程A用来生产包子的，线程B用来吃包子的，包子可以理解为同一资源，线程A与线程B处理的动作，一个是生产，一个是消费，此时B线程必须等到A线程完成后才能执行，那么线程A与线程B之间就需要线程通信，即—— **等待唤醒机制。**

### 7.2 等待唤醒机制
这是多个线程间的一种`协作机制`。谈到线程我们经常想到的是线程间的`竞争（race）`，比如去争夺锁，但这并不是故事的全部，线程间也会有协作机制。

在一个线程满足某个条件时，就进入等待状态（`wait() / wait(time)`）， 等待其他线程执行完他们的指定代码过后再将其唤醒（`notify()`）;或可以指定wait的时间，等时间到了自动唤醒；在有多个线程进行等待时，如果需要，可以使用 `notifyAll()`来唤醒所有的等待线程。wait/notify 就是线程间的一种协作机制。

1. wait：线程不再活动，不再参与调度，进入 `wait set` 中，因此不会浪费 CPU 资源，也不会去竞争锁了，这时的线程状态是 WAITING 或 TIMED_WAITING。它还要等着别的线程执行一个`特别的动作`，也即“`通知（notify）`”或者等待时间到，在这个对象上等待的线程从wait set 中释放出来，重新进入到调度队列（`ready queue`）中
2. notify：则选取所通知对象的 wait set 中的一个线程释放；
3. notifyAll：则释放所通知对象的 wait set 上的全部线程。

> 注意：
>
> 被通知的线程被唤醒后也不一定能立即恢复执行，因为它当初中断的地方是在同步块内，而此刻它已经不持有锁，所以它需要再次尝试去获取锁（很可能面临其它线程的竞争），成功后才能在当初调用 wait 方法之后的地方恢复执行。
>
> 总结如下：
>
> + 如果能获取锁，线程就从 WAITING 状态变成 RUNNABLE（可运行） 状态；
> + 否则，线程就从 WAITING 状态又变成 BLOCKED（等待锁） 状态
>

### 7.3 举例
例题：使用两个线程打印 1-100。线程1, 线程2 交替打印

```java
class Communication implements Runnable {
    int i = 1;
    public void run() {
        while (true) {
            synchronized (this) {
                notify();
                if (i <= 100) {
                    System.out.println(Thread.currentThread().getName() + ":" + i++);
                } else
                    break;
                try {
                    wait();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

```java
public class PrintNumber {
    // 定义一个锁对象
    private static final Object lock = new Object();
    // 定义一个计数器
    private static int count = 1;

    public static void main(String[] args) {
        // 创建两个线程，一个打印奇数，一个打印偶数
        Thread t1 = new Thread(new PrintTask(true), "Thread-1");
        Thread t2 = new Thread(new PrintTask(false), "Thread-2");

        // 启动线程
        t1.start();
        t2.start();
    }

    // 定义一个打印任务的内部类
    static class PrintTask implements Runnable {
        // 定义一个布尔变量，用于判断是打印奇数还是偶数
        private boolean isOdd;

        // 构造方法，传入布尔变量
        public PrintTask(boolean isOdd) {
            this.isOdd = isOdd;
        }

        @Override
        // 实现Runnable接口的run方法
        public void run() {
            // 循环打印数字
            while (count <= 100) {
                // 加锁
                synchronized (lock) {
                    // 判断是否打印奇数或偶数
                    if ((count % 2 == 1 && isOdd) || (count % 2 == 0 && !isOdd)) {
                        // 打印数字
                        System.out.println(Thread.currentThread().getName() + ": " + count++);
                        // 唤醒其他线程
                        lock.notify();
                    } else {
                        // 如果不是当前线程应该打印的数字，则等待
                        try {
                            lock.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        }
    }
}
```

sleep 和 wait 的区别 sleep 不会释放同步监视器





### 7.4 调用wait和notify需注意的细节
1. wait方法与notify方法必须要由`同一个锁对象调用`。因为：对应的锁对象可以通过notify唤醒使用同一个锁对象调用的wait方法后的线程。
2. wait方法与notify方法是属于Object类的方法的。因为：锁对象可以是任意对象，而任意对象的所属类都是继承了Object类的。
3. wait方法与notify方法必须要在`同步代码块`或者是`同步函数`中使用。因为：必须要`通过锁对象`调用这2个方法。否则会报java.lang.IllegalMonitorStateException异常。



涉及到三个方法的使用:

wait():线程一旦执行此方法，就进入等待状态。同时，会释放对同步监视器的调用

notify():一旦执行此方法，就会唤醒被wait()的线程中优先级最高的那一个线程。(如果被wait()的多个线程的优先级相同

随机唤醒一个)。被唤醒的线程从当初被wait的位置继续执行。

notifyALl():一旦执行此方法，就会唤醒所有被wait的线程。



注意点:

此三个方法的使用，必须是在同步代码块或同步方法中，

(超纲:Lock需要配合Condition实现线程间的通信)

此三个方法的调用者，必须是同步监视器。否则，会报IllegalMonitorStateException异常

此三个方法声明在0bject类中。



1. **此三个方法的使用必须是在同步代码块或同步方法中**：
    - 这是因为 `wait()`, `notify()`, 和 `notifyAll()` 方法需要在同步上下文中调用，以确保线程安全。如果尝试在非同步上下文中调用这些方法，将抛出 `IllegalMonitorStateException` 异常。
2. **此三个方法的调用者必须是同步监视器**：
    - 同步监视器通常是指当前执行线程所持有的对象锁。如果一个线程没有持有对象的锁，那么它就不能调用这些方法，否则会抛出 `IllegalMonitorStateException` 异常。
3. **此三个方法声明在Object类中**：
    - 这意味着所有的 Java 对象都可以使用这些方法，因为它们继承自 Object 类。

下面是使用这些方法的代码示例：

```java
public class Example {
    public synchronized void doSomething() {
        while (conditionNotMet) {
            try {
                wait(); // 调用 wait() 方法，释放锁并等待
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        // 执行一些操作
    }

    public synchronized void changeCondition() {
        // 改变条件
        conditionNotMet = false;
        notifyAll(); // 唤醒所有等待的线程
    }
}
```

在这个例子中，`doSomething()` 方法是一个同步方法，它在条件不满足时调用 `wait()` 方法，使得当前线程等待，并且释放锁。`changeCondition()` 方法也是一个同步方法，它在条件改变时调用 `notifyAll()` 方法，唤醒所有等待的线程。

请注意，`wait()` 方法会释放锁，允许其他线程进入同步块或方法，而 `notify()` 和 `notifyAll()` 方法则用于唤醒一个或所有等待的线程。



对比

1. **<font style="color:rgb(6, 6, 7);">声明的位置</font>**<font style="color:rgb(6, 6, 7);">：</font>
    - `wait()`<font style="color:rgb(6, 6, 7);">：声明在</font>`Object`<font style="color:rgb(6, 6, 7);">类中。</font>
    - `sleep()`<font style="color:rgb(6, 6, 7);">：声明在</font>`Thread`<font style="color:rgb(6, 6, 7);">类中，是静态的。</font>
2. **<font style="color:rgb(6, 6, 7);">使用的场景不同</font>**<font style="color:rgb(6, 6, 7);">：</font>
    - `wait()`<font style="color:rgb(6, 6, 7);">：只能在同步代码块或同步方法中使用。</font>
    - `sleep()`<font style="color:rgb(6, 6, 7);">：可以在任何需要使用的场景中使用。</font>
3. **<font style="color:rgb(6, 6, 7);">使用在同步代码块或同步方法中</font>**<font style="color:rgb(6, 6, 7);">：</font>
    - `wait()`<font style="color:rgb(6, 6, 7);">：一旦执行，会释放同步监视器（即当前线程持有的对象锁）。</font>
    - `sleep()`<font style="color:rgb(6, 6, 7);">：一旦执行，不会释放同步监视器。</font>
4. **<font style="color:rgb(6, 6, 7);">结束阻塞的方式</font>**<font style="color:rgb(6, 6, 7);">：</font>
    - `wait()`<font style="color:rgb(6, 6, 7);">：到达指定时间自动结束阻塞，或者通过被</font>`notify()`<font style="color:rgb(6, 6, 7);">或</font>`notifyAll()`<font style="color:rgb(6, 6, 7);">唤醒，结束阻塞。</font>
    - `sleep()`<font style="color:rgb(6, 6, 7);">：到达指定时间自动结束阻塞。</font>





### 7.5 生产者与消费者问题
等待唤醒机制可以解决经典的“生产者与消费者”的问题。生产者与消费者问题（英语：Producer-consumer problem），也称有限缓冲问题（英语：Bounded-buffer problem），是一个多线程同步问题的经典案例。该问题描述了两个（多个）`共享固定大小缓冲区的线程`——即所谓的“生产者”和“消费者”——在实际运行时会发生的问题。

生产者的主要作用是生成一定量的数据放到缓冲区中，然后重复此过程。与此同时，消费者也在缓冲区消耗这些数据。**该问题的关键就是要保证生产者不会在缓冲区满时加入数据，消费者也不会在缓冲区中空时消耗数据。**

**举例：**

生产者(Productor)将产品交给店员(Clerk)，而消费者(Customer)从店员处取走产品，店员一次只能持有固定数量的产品(比如:20），如果生产者试图生产更多的产品，店员会叫生产者停一下，如果店中有空位放产品了再通知生产者继续生产；如果店中没有产品了，店员会告诉消费者等一下，如果店中有产品了再通知消费者来取走产品。

类似的场景，比如厨师和服务员等。

**生产者与消费者问题中其实隐含了两个问题：**

+ 线程安全问题：因为生产者与消费者共享数据缓冲区，产生安全问题。不过这个问题可以使用同步解决。
+ 线程的协调工作问题：
    - 要解决该问题，就必须让生产者线程在缓冲区满时等待(wait)，暂停进入阻塞状态，等到下次消费者消耗了缓冲区中的数据的时候，通知(notify)正在等待的线程恢复到就绪状态，重新开始往缓冲区添加数据。同样，也可以让消费者线程在缓冲区空时进入等待(wait)，暂停进入阻塞状态，等到生产者往缓冲区添加数据之后，再通知(notify)正在等待的线程恢复到就绪状态。通过这样的通信机制来解决此类问题。

**代码实现：**

```java
public class ConsumerProducerTest {
    public static void main(String[] args) {
        Clerk clerk = new Clerk();
        Producer p1 = new Producer(clerk);
        
        Consumer c1 = new Consumer(clerk);
        Consumer c2 = new Consumer(clerk);
        
        p1.setName("生产者1");
        c1.setName("消费者1");
        c2.setName("消费者2");
        
        p1.start();
        c1.start();
        c2.start();
    }
}

//生产者
class Producer extends Thread{
    private Clerk clerk;
    
    public Producer(Clerk clerk){
        this.clerk = clerk;
    }
    
    @Override
    public void run() {
        
        System.out.println("=========生产者开始生产产品========");
        while(true){
            
            try {
                Thread.sleep(40);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            
            //要求clerk去增加产品
            clerk.addProduct();
        }
    }
}

//消费者
class Consumer extends Thread{
    private Clerk clerk;
    
    public Consumer(Clerk clerk){
        this.clerk = clerk;
    }
    @Override
    public void run() {
        System.out.println("=========消费者开始消费产品========");
        while(true){
            
            try {
                Thread.sleep(90);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            
            //要求clerk去减少产品
            clerk.minusProduct();
        }
    }
}

//资源类
class Clerk {
    private int productNum = 0;//产品数量
    private static final int MAX_PRODUCT = 20;
    private static final int MIN_PRODUCT = 1;
    
    //增加产品
    public synchronized void addProduct() {
        if(productNum < MAX_PRODUCT){
            productNum++;
            System.out.println(Thread.currentThread().getName() + 
                    "生产了第" + productNum + "个产品");
            //唤醒消费者
            this.notifyAll();
        }else{
            
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    //减少产品
    public synchronized void minusProduct() {
        if(productNum >= MIN_PRODUCT){
            System.out.println(Thread.currentThread().getName() + 
                    "消费了第" + productNum + "个产品");
            productNum--;
            
            //唤醒生产者
            this.notifyAll();
        }else{
            
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    
}
```



### 7.6 面试题：区分sleep()和wait()
相同点：一旦执行，都会使得当前线程结束执行状态，进入阻塞状态。

不同点：

 ① 定义方法所属的类：sleep():Thread中定义。  wait():Object中定义

② 使用范围的不同：sleep()可以在任何需要使用的位置被调用； wait():必须使用在同步代码块或同步方法中

③ 都在同步结构中使用的时候，是否释放同步监视器的操作不同：sleep():不会释放同步监视器 ;wait():会释放同步监视器

④ 结束等待的方式不同：sleep()：指定时间一到就结束阻塞。 wait():可以指定时间也可以无限等待直到notify或notifyAll。



sleep 在哪个线程里调用的就在哪里执行，与前面的对象无关

### 7.7 是否释放锁的操作
任何线程进入同步代码块、同步方法之前，必须先获得对同步监视器的锁定，那么何时会释放对同步监视器的锁定呢？

#### 7.7.1 释放锁的操作
当前线程的同步方法、同步代码块执行结束。

当前线程在同步代码块、同步方法中遇到break、return终止了该代码块、该方法的继续执行。

当前线程在同步代码块、同步方法中出现了未处理的Error或Exception，导致当前线程异常结束。

当前线程在同步代码块、同步方法中执行了锁对象的wait()方法，当前线程被挂起，并释放锁。

#### 7.7.2 不会释放锁的操作
线程执行同步代码块或同步方法时，程序调用Thread.sleep()、Thread.yield()方法暂停当前线程的执行。

线程执行同步代码块时，其他线程调用了该线程的suspend()方法将该该线程挂起，该线程不会释放锁（同步监视器）。

+ 应尽量避免使用suspend()和resume()这样的过时来控制线程。

## 8. JDK5.0新增线程创建方式
创建多线程的方式三:实现callable(jdk5.0新增的)  
1， 与之前的方式的对比:与Runnable方式的对比的好处

> call()可以有返回值，更灵活  
call()可以使用throws的方式处理异常，更灵活  
Callable使用了泛型参数，可以指明具体的call()的返回值类型，更灵活  
有缺点吗?如果在主线程中需要获取分线程call()的返回值，则此时的主线程是阻塞状态的。
>

2.创建多线程的方式四:使用线程池

此方式的好处:

提高了程序执行的效率。(因为线程已经提前创建好了)

提高了资源的复用率。(因为执行完的线程并未销毁，而是可以继续执行其他的任务)

可以设置相关的参数，对线程池中的线程的使用进行管理



## 8.1 新增方式一：实现Callable接口
+ 与使用Runnable相比， Callable功能更强大些
    - 相比run()方法，可以有返回值
    - 方法可以抛出异常
    - 支持泛型的返回值（需要借助FutureTask类，获取返回结果）
+ Future接口（了解）
    - 可以对具体Runnable、Callable任务的执行结果进行取消、查询是否完成、获取结果等。
    - FutureTask是Futrue接口的唯一的实现类
    - FutureTask 同时实现了Runnable, Future接口。它既可以作为Runnable被线程执行，又可以作为Future得到Callable的返回值
+ 缺点：在获取分线程执行结果的时候，当前线程（或是主线程）受阻塞，效率较低。
+ 代码举例

```java
/*
 * 创建多线程的方式三：实现Callable （jdk5.0新增的）
 */
//1.创建一个实现Callable的实现类
class NumThread implements Callable {
    //2.实现call方法，将此线程需要执行的操作声明在call()中
    @Override
    public Object call() throws Exception {
        int sum = 0;
        for (int i = 1; i <= 100; i++) {
            if (i % 2 == 0) {
                System.out.println(i);
                sum += i;
            }
        }
        return sum;
    }
}


public class CallableTest {
    public static void main(String[] args) {
        //3.创建Callable接口实现类的对象
        NumThread numThread = new NumThread();

        //4.将此Callable接口实现类的对象作为传递到FutureTask构造器中，创建FutureTask的对象
        FutureTask futureTask = new FutureTask(numThread);
        //5.将FutureTask的对象作为参数传递到Thread类的构造器中，创建Thread对象，并调用start()
        new Thread(futureTask).start();


//      接收返回值
        try {
            //6.获取Callable中call方法的返回值
            //get()返回值即为FutureTask构造器参数Callable实现类重写的call()的返回值。
            Object sum = futureTask.get();
            System.out.println("总和为：" + sum);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (ExecutionException e) {
            e.printStackTrace();
        }
    }

}
```

### 8.2 新增方式二：使用线程池
**现有问题：**

如果并发的线程数量很多，并且每个线程都是执行一个时间很短的任务就结束了，这样频繁创建线程就会大大降低系统的效率，因为频繁创建线程和销毁线程需要时间。

那么有没有一种办法使得线程可以复用，即执行完一个任务，并不被销毁，而是可以继续执行其他的任务？

**思路：**提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中。可以避免频繁创建销毁、实现重复利用。类似生活中的公共交通工具。

![](images/线程池的理解.jpg)

**好处：**

+ 提高响应速度（减少了创建新线程的时间）
+ 降低资源消耗（重复利用线程池中线程，不需要每次都创建）
+ 便于线程管理
    - corePoolSize：核心池的大小
    - maximumPoolSize：最大线程数
    - keepAliveTime：线程没有任务时最多保持多长时间后会终止
    - …

**线程池相关API**

+ JDK5.0之前，我们必须手动自定义线程池。从JDK5.0开始，Java内置线程池相关的API。在java.util.concurrent包下提供了线程池相关API：`ExecutorService` 和 `Executors`。
+ `ExecutorService`：真正的线程池接口。常见子类ThreadPoolExecutor
    - `void execute(Runnable command)` ：执行任务/命令，没有返回值，一般用来执行Runnable
    - `<T> Future<T> submit(Callable<T> task)`：执行任务，有返回值，一般又来执行Callable
    - `void shutdown()` ：关闭连接池
+ `Executors`：一个线程池的工厂类，通过此类的静态工厂方法可以创建多种类型的线程池对象。
    - `Executors.newCachedThreadPool()`：创建一个可根据需要创建新线程的线程池
    - `Executors.newFixedThreadPool(int nThreads)`; 创建一个可重用固定线程数的线程池
    - `Executors.newSingleThreadExecutor()` ：创建一个只有一个线程的线程池
    - `Executors.newScheduledThreadPool(int corePoolSize)`：创建一个线程池，它可安排在给定延迟后运行命令或者定期地执行。

**代码举例：**

```java
class NumberThread implements Runnable{

    @Override
    public void run() {
        for(int i = 0;i <= 100;i++){
            if(i % 2 == 0){
                System.out.println(Thread.currentThread().getName() + ": " + i);
            }
        }
    }
}

class NumberThread1 implements Runnable{

    @Override
    public void run() {
        for(int i = 0;i <= 100;i++){
            if(i % 2 != 0){
                System.out.println(Thread.currentThread().getName() + ": " + i);
            }
        }
    }
}

class NumberThread2 implements Callable {
    @Override
    public Object call() throws Exception {
        int evenSum = 0;//记录偶数的和
        for(int i = 0;i <= 100;i++){
            if(i % 2 == 0){
                evenSum += i;
            }
        }
        return evenSum;
    }

}

public class ThreadPoolTest {

    public static void main(String[] args) {
        //1. 提供指定线程数量的线程池
        ExecutorService service = Executors.newFixedThreadPool(10);
        ThreadPoolExecutor service1 = (ThreadPoolExecutor) service;
//        //设置线程池的属性
//        System.out.println(service.getClass());//ThreadPoolExecutor
        service1.setMaximumPoolSize(50); //设置线程池中线程数的上限

        //2.执行指定的线程的操作。需要提供实现Runnable接口或Callable接口实现类的对象
        service.execute(new NumberThread());//适合适用于Runnable
        service.execute(new NumberThread1());//适合适用于Runnable

        try {
            Future future = service.submit(new NumberThread2());//适合使用于Callable
            System.out.println("总和为：" + future.get());
        } catch (Exception e) {
            e.printStackTrace();
        }
        //3.关闭连接池
        service.shutdown();
    }

}
```










