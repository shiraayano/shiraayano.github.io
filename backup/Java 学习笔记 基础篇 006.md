# 第10章_多线程

线程的创建方式一:继承Thread类

步骤:

创建一个继承于Thread类的子类

重写Thread类的run()--->将此线程要执行的操作，声明在此方法体中

创建当前Thread的子类的对象

通过对象调用start()


我们之前学习的程序在没有跳转语句的情况下，都是由上至下沿着一条路径依次执行。现在想要设计一个程序，可以同时有多条执行路径同时执行。比如，`一边游戏，一边qq聊天，一边听歌`，怎么设计？

要解决上述问题，需要使用`多进程`或者`多线程`来解决。

## 1. 相关概念
### 1.1 程序、进程与线程
+ **程序（program）**：为完成特定任务，用某种语言编写的`一组指令的集合`。即指`一段静态的代码`，静态对象。
+ **进程（process）**：程序的一次执行过程，或是正在内存中运行的应用程序。如：运行中的QQ，运行中的网易音乐播放器。
    - 每个进程都有一个独立的内存空间，系统运行一个程序即是一个进程从创建、运行到消亡的过程。（生命周期）
    - 程序是静态的，进程是动态的
    - 进程作为`操作系统调度和分配资源的最小单位`（亦是系统运行程序的基本单位），系统在运行时会为每个进程分配不同的内存区域。
    - 现代的操作系统，大都是支持多进程的，支持同时运行多个程序。比如：现在我们上课一边使用编辑器，一边使用录屏软件，同时还开着画图板，dos窗口等软件。
+ **线程（thread）**：进程可进一步细化为线程，是程序内部的`一条执行路径`。一个进程中至少有一个线程。

> 注意：
>
> 不同的进程之间是不共享内存的。
>
> 进程之间的数据交换和通信的成本很高。
>

    - 一个进程同一时间若`并行`执行多个线程，就是支持多线程的。
    - 线程作为`CPU调度和执行的最小单位`。
    - 一个进程中的多个线程共享相同的内存单元，它们从同一个堆中分配对象，可以访问相同的变量和对象。这就使得线程间通信更简便、高效。但多个线程操作共享的系统资源可能就会带来`安全的隐患`。
    - 下图中，红框的蓝色区域为线程独享，黄色区域为线程共享。

### 1.2 查看进程和线程
我们可以在电脑底部任务栏，右键----->打开任务管理器，可以查看当前任务的进程：

1、每个应用程序的运行都是一个进程

2、一个应用程序的多次运行，就是多个进程

3、一个进程中包含多个线程

### 1.3 线程调度
+ **分时调度**所有线程`轮流使用` CPU 的使用权，并且平均分配每个线程占用 CPU 的时间。
+ **抢占式调度**让`优先级高`的线程以`较大的概率`优先使用 CPU。如果线程的优先级相同，那么会随机选择一个(线程随机性)，Java使用的为抢占式调度。![](images/抢占式调度.bmp)

### 1.4 多线程程序的优点
**背景：**以单核CPU为例，只使用单个线程先后完成多个任务（调用多个方法），肯定比用多个线程来完成用的时间更短，为何仍需多线程呢？

**多线程程序的优点：**

1. 提高应用程序的响应。对图形化界面更有意义，可增强用户体验。
2. 提高计算机系统CPU的利用率
3. 改善程序结构。将既长又复杂的进程分为多个线程，独立运行，利于理解和修改

### 1.5 补充概念
#### 1.5.1 单核CPU和多核CPU
单核CPU，在一个时间单元内，只能执行一个线程的任务。例如，可以把CPU看成是医院的医生诊室，在一定时间内只能给一个病人诊断治疗。所以单核CPU就是，代码经过前面一系列的前导操作（类似于医院挂号，比如有10个窗口挂号），然后到cpu处执行时发现，就只有一个CPU（对应一个医生），大家排队执行。

这时候想要提升系统性能，只有两个办法，要么提升CPU性能（让医生看病快点），要么多加几个CPU（多整几个医生），即为多核的CPU。

`问题：多核的效率是单核的倍数吗？`譬如4核A53的cpu，性能是单核A53的4倍吗？理论上是，但是实际不可能，至少有两方面的损耗。

+ `一个是多个核心的其他共用资源限制`。譬如，4核CPU对应的内存、cache、寄存器并没有同步扩充4倍。这就好像医院一样，1个医生换4个医生，但是做B超检查的还是一台机器，性能瓶颈就从医生转到B超检查了。
+ `另一个是多核CPU之间的协调管理损耗`。譬如多个核心同时运行两个相关的任务，需要考虑任务同步，这也需要消耗额外性能。好比公司工作，一个人的时候至少不用开会浪费时间，自己跟自己商量就行了。两个人就要开会同步工作，协调分配，所以工作效率绝对不可能达到2倍。

#### 1.5.2 并行与并发
+ **并行（parallel）**：指两个或多个事件在`同一时刻`发生（同时发生）。指在同一时刻，有`多条指令`在`多个CPU`上`同时`执行。比如：多个人同时做不同的事。![](images/image-20220401000804242.png)
+ **并发（concurrency）**：指两个或多个事件在`同一个时间段内`发生。即在一段时间内，有`多条指令`在`单个CPU`上`快速轮换、交替`执行，使得在宏观上具有多个进程同时执行的效果。![](images/image-20220401000515678.png)



在操作系统中，启动了多个程序，`并发`指的是在一段时间内宏观上有多个程序同时运行，这在单核 CPU 系统中，每一时刻只能有一个程序执行，即微观上这些程序是分时的交替运行，只不过是给人的感觉是同时运行，那是因为分时交替运行的时间是非常短的。

而在多核 CPU 系统中，则这些可以`并发`执行的程序便可以分配到多个CPU上，实现多任务并行执行，即利用每个处理器来处理一个可以并发执行的程序，这样多个程序便可以同时执行。目前电脑市场上说的多核 CPU，便是多核处理器，核越多，`并行`处理的程序越多，能大大的提高电脑运行的效率。

## 2.创建和启动线程
### 2.1 概述
+ Java语言的JVM允许程序运行多个线程，使用`java.lang.Thread`类代表**线程**，所有的线程对象都必须是Thread类或其子类的实例。
+ Thread类的特性
    - 每个线程都是通过某个特定Thread对象的run()方法来完成操作的，因此把run()方法体称为`线程执行体`。
    - 通过该Thread对象的start()方法来启动这个线程，而非直接调用run()
    - 要想实现多线程，必须在主线程中创建新的线程对象。

### 2.2 方式1：继承Thread类
Java通过继承Thread类来**创建**并**启动多线程**的步骤如下：

1. 定义Thread类的子类，并重写该类的run()方法，该run()方法的方法体就代表了线程需要完成的任务
2. 创建Thread子类的实例，即创建了线程对象
3. 调用线程对象的start()方法来启动该线程

代码如下：

```java
package com.atguigu.thread;
//自定义线程类
public class MyThread extends Thread {
    //定义指定线程名称的构造方法
    public MyThread(String name) {
        //调用父类的String参数的构造方法，指定线程的名称
        super(name);
    }
    /**
     * 重写run方法，完成该线程执行的逻辑
     */
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName()+"：正在执行！"+i);
        }
    }
}
```

测试类：

```java
package com.atguigu.thread;

public class TestMyThread {
    public static void main(String[] args) {
        //创建自定义线程对象1
        MyThread mt1 = new MyThread("子线程1");
        //开启子线程1
        mt1.start();
        
        //创建自定义线程对象2
        MyThread mt2 = new MyThread("子线程2");
        //开启子线程2
        mt2.start();
        
        //在主方法中执行for循环
        for (int i = 0; i < 10; i++) {
            System.out.println("main线程！"+i);
        }
    }
}

```

> 注意：
>
> 1. 如果自己手动调用run()方法，那么就只是普通方法，没有启动多线程模式。
> 2. run()方法由JVM调用，什么时候调用，执行的过程控制都有操作系统的CPU调度决定。
> 3. 想要启动多线程，必须调用start方法。
> 4. 一个线程对象只能调用一次start()方法启动，如果重复调用了，则将抛出以上的异常“`IllegalThreadStateException`”。
>

### 2.3 方式2：实现Runnable接口
Java有单继承的限制，当我们无法继承Thread类时，那么该如何做呢？在核心类库中提供了Runnable接口，我们可以实现Runnable接口，重写run()方法，然后再通过Thread类的对象代理启动和执行我们的线程体run()方法

步骤如下：

1. 定义Runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程执行体。
2. 创建Runnable实现类的实例，并以此实例作为Thread的target参数来创建Thread对象，该Thread对象才是真正  
的线程对象。
3. 调用线程对象的start()方法，启动线程。调用Runnable接口实现类的run方法。

代码如下：

```java
package com.atguigu.thread;

public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println(Thread.currentThread().getName() + " " + i);
        }
    }
}
```

测试类：

```java
package com.atguigu.thread;

public class TestMyRunnable {
    public static void main(String[] args) {
        //创建自定义类对象  线程任务对象
        MyRunnable mr = new MyRunnable();
        //创建线程对象
        Thread t = new Thread(mr, "长江");
        t.start();
        for (int i = 0; i < 20; i++) {
            System.out.println("黄河 " + i);
        }
    }
}
```

 通过实现Runnable接口，使得该类有了多线程类的特征。所有的分线程要执行的代码都在run方法里面。

在启动的多线程的时候，需要先通过Thread类的构造方法Thread(Runnable target) 构造出对象，然后调用Thread对象的start()方法来运行多线程代码。

实际上，所有的多线程代码都是通过运行Thread的start()方法来运行的。因此，不管是继承Thread类还是实现  
Runnable接口来实现多线程，最终还是通过Thread的对象的API来控制线程的，熟悉Thread类的API是进行多线程编程的基础。

说明：Runnable对象仅仅作为Thread对象的target，Runnable实现类里包含的run()方法仅作为线程执行体。  
而实际的线程对象依然是Thread实例，只是该Thread线程负责执行其target的run()方法。

### 2.4 变形写法
**使用匿名内部类对象来实现线程的创建和启动**

```java
new Thread("新的线程！"){
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName()+"：正在执行！"+i);
        }
    }
}.start();
```

```java
new Thread(new Runnable(){
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName()+"：" + i);
        }
    }
}).start();
```

### 2.5 对比两种方式
**联系**

Thread类实际上也是实现了Runnable接口的类。即：

```java
public class Thread extends Object implements Runnable
```

**区别**

+ 继承Thread：线程代码存放Thread子类run方法中。
+ 实现Runnable：线程代码存在接口的子类的run方法。

**实现Runnable接口比继承Thread类所具有的优势**

+ 避免了单继承的局限性
+ 多个线程可以共享同一个接口实现类的对象，非常适合多个相同线程来处理同一份资源。
+ 增加程序的健壮性，实现解耦操作，代码可以被多个线程共享，代码和线程独立。



### 2.6 练习
 例题:创建一个分线程1，用于遍历10以内的偶数

```java
public class EvenNumberTest {
    public static void main(String[] args) {
        //第三步 创建Thread的子类对象
        EvenNumber en = new EvenNumber();
        //第四步 调用start方法
        en.start();

    }
}
//第一步 创建一个继承于Thread类的子类
class EvenNumber extends Thread{
    //第二步 重写run方法
    @Override
    public void run() {
        for (int i = 0; i < 100; i+=2) {
            System.out.println(i);
        }
    }
}
```

【拓展】 再创建一个分线程2，用于遍历100以内的偶数

创建两个分线程，让其中一个线程输出1-100之间的偶数，另一个线程输出1-100之间的奇数。



1. 创建一个继承于Thread类的子类，并重写run()方法。

```java
// 线程1：遍历10以内的偶数
class EvenThread1 extends Thread {
    @Override
    public void run() {
        for (int i = 2; i <= 10; i += 2) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
        }
    }
}

// 线程2：遍历100以内的偶数
class EvenThread2 extends Thread {
    @Override
    public void run() {
        for (int i = 2; i <= 100; i += 2) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
        }
    }
}
```

1.2 例题：创建并启动线程。

```java
public class ThreadExample {
    public static void main(String[] args) {
        // 创建线程1的对象
        EvenThread1 thread1 = new EvenThread1();
        // 设置线程1的名字
        thread1.setName("Thread-1");
        // 启动线程1
        thread1.start();

        // 创建线程2的对象
        EvenThread2 thread2 = new EvenThread2();
        // 设置线程2的名字
        thread2.setName("Thread-2");
        // 启动线程2
        thread2.start();
    }
}
```

在上述代码中，我们创建了两个线程类`EvenThread1`和`EvenThread2`，它们都继承自`Thread`类，并重写了`run()`方法，分别用于遍历10以内和100以内的偶数。在`main`方法中，我们分别创建了这两个线程的实例，并设置了线程名称，然后通过调用`start()`方法来启动线程。这样，两个线程就会并行执行，分别输出它们各自的偶数序列。

## 3. Thread类的常用结构
### 3.1 构造器
+ public Thread() :分配一个新的线程对象。
+ public Thread(String name) :分配一个指定名字的新的线程对象。
+ public Thread(Runnable target) :指定创建线程的目标对象，它实现了Runnable接口中的run方法
+ public Thread(Runnable target,String name) :分配一个带有指定目标新的线程对象并指定名字。

### 3.2 常用方法系列1
+ public void run() :此线程要执行的任务在此处定义代码。
+ public void start() :导致此线程开始执行; Java虚拟机调用此线程的run方法。
+ public String getName() :获取当前线程名称。
+ public void setName(String name)：设置该线程名称。
+ public static Thread currentThread() :返回对当前正在执行的线程对象的引用。在Thread子类中就是this，通常用于主线程和Runnable实现类
+ public static void sleep(long millis) :使当前正在执行的线程以指定的毫秒数暂停（暂时停止执行）。
+ public static void yield()：yield只是让当前线程暂停一下，让系统的线程调度器重新调度一次，希望优先级与当前线程相同或更高的其他线程能够获得执行机会，但是这个不能保证，完全有可能的情况是，当某个线程调用了yield方法暂停之后，线程调度器又将其调度出来重新执行。

### 3.3 常用方法系列2
+ public final boolean isAlive()：测试线程是否处于活动状态。如果线程已经启动且尚未终止，则为活动状态。 
+ void join() ：等待该线程终止。 void join(long millis) ：等待该线程终止的时间最长为 millis 毫秒。如果millis时间到，将不再等待。 void join(long millis, int nanos) ：等待该线程终止的时间最长为 millis 毫秒 + nanos 纳秒。 
+ public final void stop()：`已过时`，不建议使用。强行结束一个线程的执行，直接进入死亡状态。run()即刻停止，可能会导致一些清理性的工作得不到完成，如文件，数据库等的关闭。同时，会立即释放该线程所持有的所有的锁，导致数据得不到同步的处理，出现数据不一致的问题。
+ void suspend() / void resume() : 这两个操作就好比播放器的暂停和恢复。二者必须成对出现，否则非常容易发生死锁。suspend()调用会导致线程暂停，但不会释放任何锁资源，导致其它线程都无法访问被它占用的锁，直到调用resume()。`已过时`，不建议使用。

### 3.4 常用方法系列3
每个线程都有一定的优先级，同优先级线程组成先进先出队列（先到先服务），使用分时调度策略。优先级高的线程采用抢占式策略，获得较多的执行机会。每个线程默认的优先级都与创建它的父线程具有相同的优先级。

+ Thread类的三个优先级常量：
    - MAX_PRIORITY（10）：最高优先级 
    - MIN _PRIORITY （1）：最低优先级
    - NORM_PRIORITY （5）：普通优先级，默认情况下main线程具有普通优先级。
+ public final int getPriority() ：返回线程优先级 
+ public final void setPriority(int newPriority) ：改变线程的优先级，范围在[1,10]之间。

```java
public class EvenNumberTest {
    public static void main(String[] args) {
        //第三步 创建Thread的子类对象
        EvenNumber en = new EvenNumber();
        //第四步 调用start方法
        en.start();
        for (int i = 0; i < 100; i++) {
            System.out.println(Thread.currentThread().getName() + "***");
            
            try {
                Thread.sleep(1);
            }
            catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }
}
//第一步 创建一个继承于Thread类的子类
class EvenNumber extends Thread{
    //第二步 重写run方法
    @Override
    public void run() {
        for (int i = 0; i < 100; i+=2) {
            //System.out.println(i);
            System.out.println(Thread.currentThread().getName() + i +"***");
            

        }
    }
}
```

练习：获取main线程对象的名称和优先级。

声明一个匿名内部类继承Thread类，重写run方法，在run方法中获取线程名称和优先级。设置该线程优先级为最高优先级并启动该线程。

```java
    public static void main(String[] args) {
        Thread t = new Thread(){
            public void run(){
                System.out.println(getName() + "的优先级：" + getPriority());
            }
        };
        t.setPriority(Thread.MAX_PRIORITY);
        t.start();
        
        System.out.println(Thread.currentThread().getName() +"的优先级：" + 		                                          Thread.currentThread().getPriority());
    }
```

案例：

+ 声明一个匿名内部类继承Thread类，重写run方法，实现打印[1,100]之间的偶数，要求每隔1秒打印1个偶数。
+ 声明一个匿名内部类继承Thread类，重写run方法，实现打印[1,100]之间的奇数，
    - 当打印到5时，让奇数线程暂停一下，再继续。
    - 当打印到5时，让奇数线程停下来，让偶数线程执行完再打印。



```java
package com.atguigu.api;

public class TestThreadStateChange {
    public static void main(String[] args) {
        Thread te = new Thread() {
            @Override
            public void run() {
                for (int i = 2; i <= 100; i += 2) {
                    System.out.println("偶数线程：" + i);
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        };
        te.start();

        Thread to = new Thread() {
            @Override
            public void run() {
                for (int i = 1; i <= 100; i += 2) {
                    System.out.println("奇数线程：" + i);
                    if (i == 5) {
//                        Thread.yield();
                        try {
                            te.join();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }

                }
            }
        };
        to.start();
    }
}
```

以下是改正后的文本：

线程的创建方式二：实现Runnable接口  
步骤：  
① 创建一个实现Runnable接口的类  
实现接口中的run()方法 --> 将此线程要执行的操作，声明在此方法体中  
② 创建当前实现类的对象  
③ 将此对象作为参数传递到Thread类的构造器中，创建Thread类的实例  
④ Thread类的实例调用start()方法



<font style="color:rgb(6, 6, 7);">对比两种线程创建方式的共同点和不同点，以及建议使用实现Runnable接口方式的好处：</font>

**<font style="color:rgb(6, 6, 7);">共同点：</font>**

1. <font style="color:rgb(6, 6, 7);">启动线程时，使用的都是Thread类中定义的</font>`start()`<font style="color:rgb(6, 6, 7);">方法。</font>
2. <font style="color:rgb(6, 6, 7);">创建的线程对象，都是Thread类或其子类的实例。</font>

**<font style="color:rgb(6, 6, 7);">不同点：</font>**

1. **<font style="color:rgb(6, 6, 7);">继承Thread类</font>**<font style="color:rgb(6, 6, 7);">：这种方式是通过创建Thread类的子类来创建线程。在这种方式中，线程的执行代码需要在子类中重写Thread类的</font>`run()`<font style="color:rgb(6, 6, 7);">方法。</font>
2. **<font style="color:rgb(6, 6, 7);">实现Runnable接口</font>**<font style="color:rgb(6, 6, 7);">：这种方式是通过创建一个实现了Runnable接口的类，并实现其</font>`run()`<font style="color:rgb(6, 6, 7);">方法来定义线程执行的代码。然后，将这个实现了Runnable接口的类的实例作为参数传递给Thread类的构造器，从而创建一个Thread对象。</font>

**<font style="color:rgb(6, 6, 7);">建议使用实现Runnable接口的方式的好处：</font>**

1. **<font style="color:rgb(6, 6, 7);">避免多继承问题</font>**<font style="color:rgb(6, 6, 7);">：在Java中，一个类只能继承一个父类，如果这个类已经继承了另一个类，就不能再继承Thread类。使用Runnable接口可以实现多重继承的效果，因为一个类可以实现多个接口。</font>
2. **<font style="color:rgb(6, 6, 7);">代码重用</font>**<font style="color:rgb(6, 6, 7);">：实现了Runnable接口的类可以被多个Thread对象共享，这样可以提高代码的重用性。</font>
3. **<font style="color:rgb(6, 6, 7);">类结构更清晰</font>**<font style="color:rgb(6, 6, 7);">：将线程执行的代码和线程的创建和管理代码分离，使得代码结构更加清晰，更易于维护。</font>
4. **<font style="color:rgb(6, 6, 7);">资源管理</font>**<font style="color:rgb(6, 6, 7);">：实现了Runnable接口的类可以更容易地被用作资源，因为它可以被传递给不同的Thread对象，而不需要关心Thread对象的具体实现。</font>
5. **<font style="color:rgb(6, 6, 7);">灵活性</font>**<font style="color:rgb(6, 6, 7);">：实现了Runnable接口的类可以更容易地与其他对象和类集成，提高了代码的灵活性和可扩展性。</font>



`Runnable`接口创建线程例子：

```java
// 定义一个实现了Runnable接口的类
class MyRunnable implements Runnable {
    @Override
    public void run() {
        // 这里是线程执行的代码
        System.out.println("线程运行中...");
        for (int i = 0; i < 5; i++) {
            System.out.println("线程执行步骤 " + (i + 1));
            try {
                // 模拟耗时操作
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("线程结束");
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        // 创建MyRunnable的实例
        MyRunnable myRunnable = new MyRunnable();

        // 将MyRunnable的实例作为参数传递给Thread类的构造器
        Thread thread = new Thread(myRunnable);

        // 启动线程
        thread.start();

        // 主线程继续执行其他任务...
        System.out.println("主线程继续执行...");
    }
}
```

在这个例子中，我们定义了一个名为`MyRunnable`的类，它实现了`Runnable`接口，并覆盖了`run()`方法，其中包含了线程将要执行的代码。在`main`方法中，我们创建了`MyRunnable`的一个实例，并将其传递给`Thread`类的构造器来创建一个新的线程对象。最后，我们通过调用`start()`方法来启动线程。



![](images/这是要闹哪样.jpg)<font style="background-color:#FBDE28;">Java代理模式（Proxy Pattern）是设计模式中的一种结构型模式，它为其他对象提供一个代理以控制对这个对象的访问。代理模式在不直接访问实际对象的情况下，提供了对目标对象的间接访问。代理模式的主要优点包括：</font>

1. **<font style="background-color:#FBDE28;">访问控制</font>**<font style="background-color:#FBDE28;">：代理可以控制对实际对象的访问，根据不同的需求提供不同的访问策略。</font>
2. **<font style="background-color:#FBDE28;">延迟初始化</font>**<font style="background-color:#FBDE28;">：代理可以在需要时才创建实际对象，从而节省资源。</font>
3. **<font style="background-color:#FBDE28;">日志记录</font>**<font style="background-color:#FBDE28;">：代理可以在访问实际对象前后添加日志记录功能。</font>
4. **<font style="background-color:#FBDE28;">安全控制</font>**<font style="background-color:#FBDE28;">：代理可以添加权限检查，以确保只有授权用户才能访问实际对象。</font>
5. **<font style="background-color:#FBDE28;">智能引用</font>**<font style="background-color:#FBDE28;">：代理可以提供额外的功能，比如引用计数，以管理对象的生命周期。</font>

<font style="background-color:#FBDE28;">代理模式通常分为几种类型：</font>

1. **<font style="background-color:#FBDE28;">静态代理</font>**<font style="background-color:#FBDE28;">：在代码编译时就已经确定代理类和目标类的映射关系。代理类和目标类实现相同的接口，代理类在内部持有目标类的引用，并在调用目标对象的方法前后进行额外的操作。</font>
2. **<font style="background-color:#FBDE28;">动态代理</font>**<font style="background-color:#FBDE28;">（Java反射）：在运行时使用Java的反射机制动态创建代理类。Java提供了</font>`<font style="background-color:#FBDE28;">java.lang.reflect.Proxy</font>`<font style="background-color:#FBDE28;">类和</font>`<font style="background-color:#FBDE28;">java.lang.reflect.InvocationHandler</font>`<font style="background-color:#FBDE28;">接口来实现动态代理。动态代理不需要在编译时就知道所有的目标类，可以在运行时动态地为一组类创建代理。</font>

<font style="background-color:#FBDE28;">下面是一个简单的静态代理模式的例子：</font>

```java
// 定义一个接口
public interface Subject {
    void request();
}

// 实现接口的目标类
public class RealSubject implements Subject {
    @Override
    public void request() {
        System.out.println("RealSubject: Handling request.");
    }
}

// 代理类
public class Proxy implements Subject {
    private RealSubject realSubject;

    public Proxy() {
        this.realSubject = new RealSubject();
    }

    @Override
    public void request() {
        System.out.println("Proxy: Logging request.");
        realSubject.request();
        System.out.println("Proxy: Logging after request.");
    }
}

// 客户端代码
public class Client {
    public static void main(String[] args) {
        Subject proxy = new Proxy();
        proxy.request();
    }
}
```

<font style="background-color:#FBDE28;">在这个例子中，</font>`<font style="background-color:#FBDE28;">Proxy</font>`<font style="background-color:#FBDE28;">类是</font>`<font style="background-color:#FBDE28;">RealSubject</font>`<font style="background-color:#FBDE28;">类的代理，它实现了与</font>`<font style="background-color:#FBDE28;">RealSubject</font>`<font style="background-color:#FBDE28;">相同的接口。在</font>`<font style="background-color:#FBDE28;">Proxy</font>`<font style="background-color:#FBDE28;">类的</font>`<font style="background-color:#FBDE28;">request</font>`<font style="background-color:#FBDE28;">方法中，我们可以在调用</font>`<font style="background-color:#FBDE28;">RealSubject</font>`<font style="background-color:#FBDE28;">的</font>`<font style="background-color:#FBDE28;">request</font>`<font style="background-color:#FBDE28;">方法前后添加额外的操作，比如日志记录。</font>

<font style="background-color:#FBDE28;">动态代理的例子需要使用Java的反射API，这里就不展开了，但基本思想是创建一个实现了</font>`<font style="background-color:#FBDE28;">InvocationHandler</font>`<font style="background-color:#FBDE28;">接口的类，并在其中定义</font>`<font style="background-color:#FBDE28;">invoke</font>`<font style="background-color:#FBDE28;">方法，该方法负责处理对代理对象的所有方法调用。然后使用</font>`<font style="background-color:#FBDE28;">Proxy.newProxyInstance</font>`<font style="background-color:#FBDE28;">方法动态创建代理对象。动态代理通常用于需要在运行时动态地为多个类创建代理的场景。</font>

### 3.5 守护线程（了解）
有一种线程，它是在后台运行的，它的任务是为其他线程提供服务的，这种线程被称为“守护线程”。JVM的垃圾回收线程就是典型的守护线程。

守护线程有个特点，就是如果所有非守护线程都死亡，那么守护线程自动死亡。形象理解：`兔死狗烹`，`鸟尽弓藏`

调用setDaemon(true)方法可将指定线程设置为守护线程。必须在线程启动之前设置，否则会报IllegalThreadStateException异常。

调用isDaemon()可以判断线程是否是守护线程。



<font style="color:rgb(6, 6, 7);">线程的常用结构 线程中的构造器</font>

1. <font style="color:rgb(6, 6, 7);">public Thread(): 分配一个新的线程对象。</font>
2. <font style="color:rgb(6, 6, 7);">public Thread(String name): 分配一个指定名字的新的线程对象。</font>
3. <font style="color:rgb(6, 6, 7);">public Thread(Runnable target): 指定创建线程的目标对象，它实现了Runnable接口中的run方法。</font>
4. <font style="color:rgb(6, 6, 7);">public Thread(Runnable target, String name): 分配一个带有指定目标和名字的新的线程对象。</font>
5. <font style="color:rgb(6, 6, 7);">线程中的常用方法：</font>
+ <font style="color:rgb(6, 6, 7);">start(): ① 启动线程 ② 调用线程的run()方法。</font>
+ <font style="color:rgb(6, 6, 7);">run(): 将线程要执行的操作，声明在run()方法中。</font>
+ <font style="color:rgb(6, 6, 7);">currentThread(): 获取当前执行代码对应的线程。</font>
+ <font style="color:rgb(6, 6, 7);">getName(): 获取线程名。</font>
+ <font style="color:rgb(6, 6, 7);">setName(String name): 设置线程名。</font>
+ <font style="color:rgb(6, 6, 7);">sleep(long millis) 睡眠 毫秒级</font>
+ <font style="color:rgb(6, 6, 7);">yield() 主动释放 cpu 的执行权</font>
+ <font style="color:rgb(6, 6, 7);">join()  线程 a 调用此方法时会进入阻塞状态，直到 b 线程结束 a 的阻塞状态才会结束，继续运行</font>
+ <font style="color:rgb(6, 6, 7);">isAlive() 判断当前线程是否存活，返回布尔值</font>

<font style="color:rgb(6, 6, 7);">过时的方法</font>

+ stop() 强行停止
+ void suspend() / void resume()



<font style="color:rgb(6, 6, 7);">线程的优先级：</font>

+ `getPriority()`<font style="color:rgb(6, 6, 7);">：获取线程的优先级。</font>
+ `setPriority()`<font style="color:rgb(6, 6, 7);">：设置线程的优先级。范围[1,10]。</font>

`Thread`<font style="color:rgb(6, 6, 7);">类内部声明的三个常量：</font>

+ `MAX_PRIORITY`<font style="color:rgb(6, 6, 7);">（10）：最高优先级。</font>
+ `MIN_PRIORITY`<font style="color:rgb(6, 6, 7);">（1）：最低优先级。</font>
+ `NORM_PRIORITY`<font style="color:rgb(6, 6, 7);">（5）：普通优先级，默认情况下main线程具有普通优先级。</font>

<font style="color:rgb(6, 6, 7);"></font>

<font style="color:rgb(6, 6, 7);">线程的生命周期</font>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1730967964777-6b498c81-189b-42bb-b359-2ab7d5915b1e.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1730968182796-39d6548c-ab29-4c59-aa15-4eeb25f21299.png)

<font style="color:rgb(6, 6, 7);"></font>

<font style="color:rgb(6, 6, 7);"></font>



```java
public class TestThread {
    public static void main(String[] args) {
        MyDaemon m = new MyDaemon();
        m.setDaemon(true);
        m.start();

        for (int i = 1; i <= 100; i++) {
            System.out.println("main:" + i);
        }
    }
}

class MyDaemon extends Thread {
    public void run() {
        while (true) {
            System.out.println("我一直守护者你...");
            try {
                Thread.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## 4. 多线程的生命周期
Java语言使用Thread类及其子类的对象来表示线程，在它的一个完整的生命周期中通常要经历如下一些状态：

### 4.1 JDK1.5之前：5种状态
线程的生命周期有五种状态：新建（New）、就绪（Runnable）、运行（Running）、阻塞（Blocked）、死亡（Dead）。CPU需要在多条线程之间切换，于是线程状态会多次在运行、阻塞、就绪之间切换。

**1.新建**

当一个Thread类或其子类的对象被声明并创建时，新生的线程对象处于新建状态。此时它和其他Java对象一样，仅仅由JVM为其分配了内存，并初始化了实例变量的值。此时的线程对象并没有任何线程的动态特征，程序也不会执行它的线程体run()。

**2.就绪**

但是当线程对象调用了start()方法之后，就不一样了，线程就从新建状态转为就绪状态。JVM会为其创建方法调用栈和程序计数器，当然，处于这个状态中的线程并没有开始运行，只是表示已具备了运行的条件，随时可以被调度。至于什么时候被调度，取决于JVM里线程调度器的调度。

> 注意：
>
> 程序只能对新建状态的线程调用start()，并且只能调用一次，如果对非新建状态的线程，如已启动的线程或已死亡的线程调用start()都会报错IllegalThreadStateException异常。
>

**3.运行**

如果处于就绪状态的线程获得了CPU资源时，开始执行run()方法的线程体代码，则该线程处于运行状态。如果计算机只有一个CPU核心，在任何时刻只有一个线程处于运行状态，如果计算机有多个核心，将会有多个线程并行(Parallel)执行。

当然，美好的时光总是短暂的，而且CPU讲究雨露均沾。对于抢占式策略的系统而言，系统会给每个可执行的线程一个小时间段来处理任务，当该时间用完，系统会剥夺该线程所占用的资源，让其回到就绪状态等待下一次被调度。此时其他线程将获得执行机会，而在选择下一个线程时，系统会适当考虑线程的优先级。

**4.阻塞**

当在运行过程中的线程遇到如下情况时，会让出 CPU 并临时中止自己的执行，进入阻塞状态：

+ 线程调用了sleep()方法，主动放弃所占用的CPU资源；
+ 线程试图获取一个同步监视器，但该同步监视器正被其他线程持有；
+ 线程执行过程中，同步监视器调用了wait()，让它等待某个通知（notify）；
+ 线程执行过程中，同步监视器调用了wait(time)
+ 线程执行过程中，遇到了其他线程对象的加塞（join）；
+ 线程被调用suspend方法被挂起（已过时，因为容易发生死锁）；

当前正在执行的线程被阻塞后，其他线程就有机会执行了。针对如上情况，当发生如下情况时会解除阻塞，让该线程重新进入就绪状态，等待线程调度器再次调度它：

+ 线程的sleep()时间到；
+ 线程成功获得了同步监视器；
+ 线程等到了通知(notify)；
+ 线程wait的时间到了
+ 加塞的线程结束了；
+ 被挂起的线程又被调用了resume恢复方法（已过时，因为容易发生死锁）；

**5.死亡**

线程会以以下三种方式之一结束，结束后的线程就处于死亡状态：

+ run()方法执行完成，线程正常结束
+ 线程执行过程中抛出了一个未捕获的异常（Exception）或错误（Error）
+ 直接调用该线程的stop()来结束该线程（已过时）

### 4.2 JDK1.5及之后：6种状态
在java.lang.Thread.State的枚举类中这样定义：

```java
public enum State {
    NEW,
    RUNNABLE,
    BLOCKED,
    WAITING,
    TIMED_WAITING,
    TERMINATED;
}
```

+ `NEW（新建）`：线程刚被创建，但是并未启动。还没调用start方法。
+ `RUNNABLE（可运行）`：这里没有区分就绪和运行状态。因为对于Java对象来说，只能标记为可运行，至于什么时候运行，不是JVM来控制的了，是OS来进行调度的，而且时间非常短暂，因此对于Java对象的状态来说，无法区分。
+ `Teminated（被终止）`：表明此线程已经结束生命周期，终止运行。
+ 重点说明，根据Thread.State的定义，**阻塞状态分为三种**：`BLOCKED`、`WAITING`、`TIMED_WAITING`。
    - `BLOCKED（锁阻塞）`：在API中的介绍为：一个正在阻塞、等待一个监视器锁（锁对象）的线程处于这一状态。只有获得锁对象的线程才能有执行机会。
        * 比如，线程A与线程B代码中使用同一锁，如果线程A获取到锁，线程A进入到Runnable状态，那么线程B就进入到Blocked锁阻塞状态。
    - `TIMED_WAITING（计时等待）`：在API中的介绍为：一个正在限时等待另一个线程执行一个（唤醒）动作的线程处于这一状态。
        * 当前线程执行过程中遇到Thread类的`sleep`或`join`，Object类的`wait`，LockSupport类的`park`方法，并且在调用这些方法时，`设置了时间`，那么当前线程会进入TIMED_WAITING，直到时间到，或被中断。
    - `WAITING（无限等待）`：在API中介绍为：一个正在无限期等待另一个线程执行一个特别的（唤醒）动作的线程处于这一状态。
        * 当前线程执行过程中遇到遇到Object类的`wait`，Thread类的`join`，LockSupport类的`park`方法，并且在调用这些方法时，`没有指定时间`，那么当前线程会进入WAITING状态，直到被唤醒。
            + 通过Object类的wait进入WAITING状态的要有Object的notify/notifyAll唤醒；
            + 通过Condition的await进入WAITING状态的要有Condition的signal方法唤醒；
            + 通过LockSupport类的park方法进入WAITING状态的要有LockSupport类的unpark方法唤醒
            + 通过Thread类的join进入WAITING状态，只有调用join方法的线程对象结束才能让当前线程恢复；

说明：当从WAITING或TIMED_WAITING恢复到Runnable状态时，如果发现当前线程没有得到监视器锁，那么会立刻转入BLOCKED状态。

![](images/image-20220524203355448.png)

或

![](images/线程的生命周期Thread.State.jpg)

> 我们在翻阅API的时候会发现Timed Waiting（计时等待） 与 Waiting（无限等待） 状态联系还是很紧密的，  
比如Waiting（无限等待） 状态中wait方法是空参的，而timed waiting（计时等待） 中wait方法是带参的。  
这种带参的方法，其实是一种倒计时操作，相当于我们生活中的小闹钟，我们设定好时间，到时通知，可是  
如果提前得到（唤醒）通知，那么设定好时间在通知也就显得多此一举了，那么这种设计方案其实是一举两  
得。如果没有得到（唤醒）通知，那么线程就处于Timed Waiting状态，直到倒计时完毕自动醒来；如果在倒  
计时期间得到（唤醒）通知，那么线程从Timed Waiting状态立刻唤醒。
>

举例：

```java
/**
 * @author 尚硅谷-宋红康
 * @create 22:15
 */
public class ThreadStateTest {
    public static void main(String[] args) throws InterruptedException {
        SubThread t = new SubThread();
        System.out.println(t.getName() + " 状态 " + t.getState());
        t.start();

        while (Thread.State.TERMINATED != t.getState()) {
            System.out.println(t.getName() + " 状态 " + t.getState());
            Thread.sleep(500);
        }
        System.out.println(t.getName() + " 状态 " + t.getState());
    }
}

class SubThread extends Thread {
    @Override
    public void run() {
        while (true) {
            for (int i = 0; i < 10; i++) {
                System.out.println("打印：" + i);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            break;
        }
    }
}

```

命令行演示：

![](images/image-20220524195035355.png)

## 5. 线程安全问题及解决


多线程读写操作容易出现线程安全问题



当我们使用多个线程访问**同一资源**（可以是同一个变量、同一个文件、同一条记录等）的时候，若多个线程`只有读操作`，那么不会发生线程安全问题。但是如果多个线程中对资源有`读和写`的操作，就容易出现线程安全问题。

举例：

类比：

![](images/当我以为我的代码很安全时，等等.gif)

```java
public class WindowTest{
    //非线程安全
    public static void main(String[] args) {
        SafeTicket safeTicket = new SafeTicket();
        Thread t1 = new Thread(safeTicket);
        Thread t2 = new Thread(safeTicket);
        Thread t3 = new Thread(safeTicket);
        t1.start();
        t2.start();
        t3.start();
    }
}

class SafeTicket implements Runnable{
    int ticket = 100;
    @Override
    public void run(){
        while (true){
            if(ticket>0){
                System.out.println(Thread.currentThread().getName()+"卖出第"+ticket+"张票");
                ticket--;
            }else{
                break;
            }
        }
    }
}
```

### 5.1 同一个资源问题和线程安全问题
案例：

火车站要卖票，我们模拟火车站的卖票过程。因为疫情期间，本次列车的座位共100个（即，只能出售100张火车票）。我们来模拟车站的售票窗口，实现多个窗口同时售票的过程。注意：不能出现错票、重票。

#### 5.1.1 局部变量不能共享
示例代码：

```javascript
package com.atguigu.unsafe;

class Window extends Thread {
    public void run() {
        int ticket = 100;
        while (ticket > 0) {
            System.out.println(getName() + "卖出一张票，票号:" + ticket);
            ticket--;
        }
    }
}

public class SaleTicketDemo1 {
    public static void main(String[] args) {
        Window w1 = new Window();
        Window w2 = new Window();
        Window w3 = new Window();

        w1.setName("窗口1");
        w2.setName("窗口2");
        w3.setName("窗口3");

        w1.start();
        w2.start();
        w3.start();
    }
}
```

结果：发现卖出300张票。

问题：局部变量是每次调用方法都是独立的，那么每个线程的run()的ticket是独立的，不是共享数据。

#### 5.1.2 不同对象的实例变量不共享
```java
package com.atguigu.unsafe;

class TicketWindow extends Thread {
    private int ticket = 100;

    public void run() {
        while (ticket > 0) {
            System.out.println(getName() + "卖出一张票，票号:" + ticket);
            ticket--;
        }
    }
}

public class SaleTicketDemo2 {
    public static void main(String[] args) {
        TicketWindow w1 = new TicketWindow();
        TicketWindow w2 = new TicketWindow();
        TicketWindow w3 = new TicketWindow();

        w1.setName("窗口1");
        w2.setName("窗口2");
        w3.setName("窗口3");

        w1.start();
        w2.start();
        w3.start();
    }
}


```

结果：发现卖出300张票。

问题：不同的实例对象的实例变量是独立的。

#### 5.1.3 静态变量是共享的
示例代码：

```java
package com.atguigu.unsafe;

class TicketSaleThread extends Thread {
    private static int ticket = 100;

    public void run() {
        while (ticket > 0) {
            try {
                Thread.sleep(10);//加入这个，使得问题暴露的更明显
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(getName() + "卖出一张票，票号:" + ticket);
            ticket--;
        }
    }
}

public class SaleTicketDemo3 {
    public static void main(String[] args) {
        TicketSaleThread t1 = new TicketSaleThread();
        TicketSaleThread t2 = new TicketSaleThread();
        TicketSaleThread t3 = new TicketSaleThread();

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

运行结果：

```java
窗口1卖出一张票，票号:100
窗口2卖出一张票，票号:100
窗口3卖出一张票，票号:100
窗口3卖出一张票，票号:97
窗口1卖出一张票，票号:97
窗口2卖出一张票，票号:97
窗口1卖出一张票，票号:94
窗口3卖出一张票，票号:94
窗口2卖出一张票，票号:94
窗口2卖出一张票，票号:91
窗口1卖出一张票，票号:91
窗口3卖出一张票，票号:91
窗口3卖出一张票，票号:88
窗口1卖出一张票，票号:88
窗口2卖出一张票，票号:88
窗口3卖出一张票，票号:85
窗口1卖出一张票，票号:85
窗口2卖出一张票，票号:85
窗口3卖出一张票，票号:82
窗口1卖出一张票，票号:82
窗口2卖出一张票，票号:82
窗口2卖出一张票，票号:79
窗口3卖出一张票，票号:79
窗口1卖出一张票，票号:79
窗口3卖出一张票，票号:76
窗口1卖出一张票，票号:76
窗口2卖出一张票，票号:76
窗口1卖出一张票，票号:73
窗口2卖出一张票，票号:73
窗口3卖出一张票，票号:73
窗口2卖出一张票，票号:70
窗口1卖出一张票，票号:70
窗口3卖出一张票，票号:70
窗口2卖出一张票，票号:67
窗口3卖出一张票，票号:67
窗口1卖出一张票，票号:67
窗口1卖出一张票，票号:64
窗口3卖出一张票，票号:64
窗口2卖出一张票，票号:64
窗口2卖出一张票，票号:61
窗口3卖出一张票，票号:61
窗口1卖出一张票，票号:61
窗口1卖出一张票，票号:58
窗口2卖出一张票，票号:58
窗口3卖出一张票，票号:58
窗口2卖出一张票，票号:55
窗口1卖出一张票，票号:55
窗口3卖出一张票，票号:55
窗口3卖出一张票，票号:52
窗口1卖出一张票，票号:52
窗口2卖出一张票，票号:52
窗口2卖出一张票，票号:49
窗口1卖出一张票，票号:49
窗口3卖出一张票，票号:49
窗口2卖出一张票，票号:46
窗口3卖出一张票，票号:46
窗口1卖出一张票，票号:46
窗口2卖出一张票，票号:43
窗口3卖出一张票，票号:43
窗口1卖出一张票，票号:43
窗口3卖出一张票，票号:40
窗口1卖出一张票，票号:40
窗口2卖出一张票，票号:40
窗口2卖出一张票，票号:37
窗口3卖出一张票，票号:37
窗口1卖出一张票，票号:37
窗口2卖出一张票，票号:34
窗口1卖出一张票，票号:34
窗口3卖出一张票，票号:34
窗口3卖出一张票，票号:31
窗口2卖出一张票，票号:31
窗口1卖出一张票，票号:31
窗口1卖出一张票，票号:28
窗口2卖出一张票，票号:28
窗口3卖出一张票，票号:28
窗口2卖出一张票，票号:25
窗口1卖出一张票，票号:25
窗口3卖出一张票，票号:25
窗口2卖出一张票，票号:22
窗口3卖出一张票，票号:22
窗口1卖出一张票，票号:22
窗口3卖出一张票，票号:19
窗口1卖出一张票，票号:19
窗口2卖出一张票，票号:19
窗口2卖出一张票，票号:16
窗口3卖出一张票，票号:16
窗口1卖出一张票，票号:16
窗口2卖出一张票，票号:13
窗口1卖出一张票，票号:13
窗口3卖出一张票，票号:13
窗口2卖出一张票，票号:10
窗口1卖出一张票，票号:10
窗口3卖出一张票，票号:10
窗口3卖出一张票，票号:7
窗口1卖出一张票，票号:7
窗口2卖出一张票，票号:7
窗口3卖出一张票，票号:4
窗口1卖出一张票，票号:4
窗口2卖出一张票，票号:4
窗口3卖出一张票，票号:1
窗口2卖出一张票，票号:1
窗口1卖出一张票，票号:1
```

结果：发现卖出近100张票。

问题1：但是有重复票或负数票问题。

原因：线程安全问题

问题2：如果要考虑有两场电影，各卖100张票等

原因：TicketThread类的静态变量，是所有TicketThread类的对象共享

#### 5.1.4 同一个对象的实例变量共享
示例代码：多个Thread线程使用同一个Runnable对象

```java
package com.atguigu.safe;

class TicketSaleRunnable implements Runnable {
    private int ticket = 100;

    public void run() {
        while (ticket > 0) {
            try {
                Thread.sleep(10);//加入这个，使得问题暴露的更明显
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + "卖出一张票，票号:" + ticket);
            ticket--;
        }
    }
}

public class SaleTicketDemo4 {
    public static void main(String[] args) {
        TicketSaleRunnable tr = new TicketSaleRunnable();
        Thread t1 = new Thread(tr, "窗口一");
        Thread t2 = new Thread(tr, "窗口二");
        Thread t3 = new Thread(tr, "窗口三");

        t1.start();
        t2.start();
        t3.start();
    }
}

```

结果：发现卖出近100张票。

问题：但是有重复票或负数票问题。

原因：线程安全问题

#### 5.1.5 抽取资源类，共享同一个资源对象
示例代码：

```java
package com.atguigu.unsafe;

//1、编写资源类
class Ticket {
    private int ticket = 100;

    public void sale() {
        if (ticket > 0) {
            try {
                Thread.sleep(10);//加入这个，使得问题暴露的更明显
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + "卖出一张票，票号:" + ticket);
            ticket--;
        } else {
            throw new RuntimeException("没有票了");
        }
    }

    public int getTicket() {
        return ticket;
    }
}

public class SaleTicketDemo5 {
    public static void main(String[] args) {
        //2、创建资源对象
        Ticket ticket = new Ticket();

        //3、启动多个线程操作资源类的对象
        Thread t1 = new Thread("窗口一") {
            public void run() {
                while (true) {
                    ticket.sale();
                }
            }
        };
        Thread t2 = new Thread("窗口二") {
            public void run() {
                while (true) {
                    ticket.sale();
                }
            }
        };
        Thread t3 = new Thread(new Runnable() {
            public void run() {
                ticket.sale();
            }
        }, "窗口三");


        t1.start();
        t2.start();
        t3.start();
    }
}
```

结果：发现卖出近100张票。

问题：但是有重复票或负数票问题。

原因：线程安全问题

### 5.2 同步机制解决线程安全问题
要解决上述多线程并发访问一个资源的安全性问题:也就是解决重复票与不存在票问题，Java中提供了同步机制  
(synchronized)来解决。

![](images/1563372934332.png)

根据案例简述：

窗口1线程进入操作的时候，窗口2和窗口3线程只能在外等着，窗口1操作结束，窗口1和窗口2和窗口3才有机会进入代码去执行。也就是说在某个线程修改共享资源的时候，其他线程不能修改该资源，等待修改完毕同步之后，才能去抢夺CPU资源，完成对应的操作，保证了数据的同步性，解决了线程不安全的现象。

为了保证每个线程都能正常执行原子操作，Java引入了线程同步机制。注意:在任何时候,最多允许一个线程拥有同步锁，谁拿到锁就进入代码块，其他的线程只能在外等着(BLOCKED)。

#### 5.2.1 同步机制解决线程安全问题的原理
同步机制的原理，其实就相当于给某段代码加“锁”，任何线程想要执行这段代码，都要先获得“锁”，我们称它为同步锁。因为Java对象在堆中的数据分为分为对象头、实例变量、空白的填充。而对象头中包含：

+ Mark Word：记录了和当前对象有关的GC、锁标记等信息。
+ 指向类的指针：每一个对象需要记录它是由哪个类创建出来的。
+ 数组长度（只有数组对象才有）

哪个线程获得了“同步锁”对象之后，”同步锁“对象就会记录这个线程的ID，这样其他线程就只能等待了，除非这个线程”释放“了锁对象，其他线程才能重新获得/占用”同步锁“对象。

#### 5.2.2 同步代码块和同步方法
**同步代码块**：synchronized 关键字可以用于某个区块前面，表示只对这个区块的资源实行互斥访问。  
格式:

```java
synchronized(同步锁){
     需要同步操作的代码
}
```



**同步方法：**synchronized 关键字直接修饰方法，表示同一时刻只有一个线程能进入这个方法，其他线程在外面等着。

```java
public synchronized void method(){
    可能会产生线程安全问题的代码
}
```

说明:  
需要被同步的代码，即为操作共享数据的代码。

共享数据:即多个线程多需要操作的数据。比如:ticket  
需要被同步的代码，在被synchronized包裹以后，就使得一个线程在操作这些代码的过程中，其它线程必须等待。

同步监视器,俗称锁。哪个线程获取了锁，哪个线程就能执行需要被同步的代码。（同步监视器即是一个对象 ）

同步监视器，可以使用任何一个类的对象充当。但是，多个线程必须共用同一个同步监视器

在实现Runnable接口的方式中，同步监视器可以考虑使用:this。

在继承Thread类的方式中，同步监视器要慎用this。可以考虑是使用 当前类.class



说明:

如果操作共享数据的代码完整的声明在了一个方法中，那么我们就可以将此方法声明为同步方法即可。

非静态的同步方法，默认同步监视器是this

静态的同步方法，默认同步监视器是当前类本身。



弊端 浪费 cpu 资源

#### 5.2.3 同步锁机制
在《Thinking in Java》中，是这么说的：对于并发工作，你需要某种方式来防止两个任务访问相同的资源（其实就是共享资源竞争）。 防止这种冲突的方法就是当资源被一个任务使用时，在其上加锁。第一个访问某项资源的任务必须锁定这项资源，使其他任务在其被解锁之前，就无法访问它了，而在其被解锁之时，另一个任务就可以锁定并使用它了。

#### 5.2.4 synchronized的锁是什么
同步锁对象可以是任意类型，但是必须保证竞争“同一个共享资源”的多个线程必须使用同一个“同步锁对象”。

对于同步代码块来说，同步锁对象是由程序员手动指定的（很多时候也是指定为this或类名.class），但是对于同步方法来说，同步锁对象只能是默认的：

+ 静态方法：当前类的Class对象（类名.class）
+ 非静态方法：this

#### 5.2.5 同步操作的思考顺序
1、如何找问题，即代码是否存在线程安全？（非常重要）  
（1）明确哪些代码是多线程运行的代码  
（2）明确多个线程是否有共享数据  
（3）明确多线程运行代码中是否有多条语句操作共享数据

2、如何解决呢？（非常重要）  
对多条操作共享数据的语句，只能让一个线程都执行完，在执行过程中，其他线程不可以参与执行。  
即所有操作共享数据的这些语句都要放在同步范围中

3、切记：

范围太小：不能解决安全问题

范围太大：因为一旦某个线程抢到锁，其他线程就只能等待，所以范围太大，效率会降低，不能合理利用CPU资源。





#### 5.2.6 代码演示
##### 示例一：静态方法加锁
```java
package com.atguigu.safe;

class TicketSaleThread extends Thread{
    private static int ticket = 100;
    public void run(){//直接锁这里，肯定不行，会导致，只有一个窗口卖票
        while (ticket > 0) {
            saleOneTicket();
        }
    }

    public synchronized static void saleOneTicket(){//锁对象是TicketSaleThread类的Class对象，而一个类的Class对象在内存中肯定只有一个
        if(ticket > 0) {//不加条件，相当于条件判断没有进入锁管控，线程安全问题就没有解决
            System.out.println(Thread.currentThread().getName() + "卖出一张票，票号:" + ticket);
            ticket--;
        }
    }
}
public class SaleTicketDemo3 {
    public static void main(String[] args) {
        TicketSaleThread t1 = new TicketSaleThread();
        TicketSaleThread t2 = new TicketSaleThread();
        TicketSaleThread t3 = new TicketSaleThread();

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");

        t1.start();
        t2.start();
        t3.start();
    }
}

```

##### 示例二：非静态方法加锁
```java
package com.atguigu.safe;


public class SaleTicketDemo4 {
    public static void main(String[] args) {
        TicketSaleRunnable tr = new TicketSaleRunnable();
        Thread t1 = new Thread(tr, "窗口一");
        Thread t2 = new Thread(tr, "窗口二");
        Thread t3 = new Thread(tr, "窗口三");

        t1.start();
        t2.start();
        t3.start();
    }
}

class TicketSaleRunnable implements Runnable {
    private int ticket = 100;

    public void run() {//直接锁这里，肯定不行，会导致，只有一个窗口卖票
        while (ticket > 0) {
            saleOneTicket();
        }
    }

    public synchronized void saleOneTicket() {//锁对象是this，这里就是TicketSaleRunnable对象，因为上面3个线程使用同一个TicketSaleRunnable对象，所以可以
        if (ticket > 0) {//不加条件，相当于条件判断没有进入锁管控，线程安全问题就没有解决
            System.out.println(Thread.currentThread().getName() + "卖出一张票，票号:" + ticket);
            ticket--;
        }
    }
}
```

##### 示例三：同步代码块
```java
package com.atguigu.safe;


public class SaleTicketDemo5 {
    public static void main(String[] args) {
        //2、创建资源对象
        Ticket ticket = new Ticket();

        //3、启动多个线程操作资源类的对象
        Thread t1 = new Thread("窗口一") {
            public void run() {//不能给run()直接加锁，因为t1,t2,t3的三个run方法分别属于三个Thread类对象，
                // run方法是非静态方法，那么锁对象默认选this，那么锁对象根本不是同一个
                while (true) {
                    synchronized (ticket) {
                        ticket.sale();
                    }
                }
            }
        };
        Thread t2 = new Thread("窗口二") {
            public void run() {
                while (true) {
                    synchronized (ticket) {
                        ticket.sale();
                    }
                }
            }
        };
        Thread t3 = new Thread(new Runnable() {
            public void run() {
                while (true) {
                    synchronized (ticket) {
                        ticket.sale();
                    }
                }
            }
        }, "窗口三");


        t1.start();
        t2.start();
        t3.start();
    }
}

//1、编写资源类
class Ticket {
    private int ticket = 1000;

    public void sale() {//也可以直接给这个方法加锁，锁对象是this，这里就是Ticket对象
        if (ticket > 0) {
            System.out.println(Thread.currentThread().getName() + "卖出一张票，票号:" + ticket);
            ticket--;
        } else {
            throw new RuntimeException("没有票了");
        }
    }

    public int getTicket() {
        return ticket;
    }
}

```

### 5.3 练习
银行有一个账户。  
有两个储户分别向同一个账户存3000元，每次存1000，存3次。每次存完打印账户余额。

问题：该程序是否有安全问题，如果有，如何解决？

【提示】  
1，明确哪些代码是多线程运行代码，须写入run()方法  
2，明确什么是共享数据。  
3，明确多线程运行代码中哪些语句是操作共享数据的。

【拓展问题】可否实现两个储户交替存钱的操作












