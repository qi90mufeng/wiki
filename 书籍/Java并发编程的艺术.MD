## Java并发编程的艺术

###### 作者  

> 阿里系和1号店
>
> 方腾飞 魏鹏 程晓明

###### 特色

> 结合JDK的源码介绍了Java并发框架、线程池的实现原理

###### 建议

> 强烈建议多使用JDK并发包提供的并发容器和工具类来解决并发
> 问题

#### 并发编程挑战

* 上下文切换的问题
  * 概念
  * 
* 死锁的问题
  * 概念
  * 避免死锁
* 受限于硬件和软件的资源限制问题
  * 硬件资源限制
    * 
  * 软件资源限制
    * 可以考虑资源池将资源复用

#### Java并发机制的底层实现原理

* synchronized

  * 实现原理

    ![1533806122778](C:\Users\boyuan\AppData\Local\Temp\1533806122778.png)

  * 应用

* volatile



#### java内存模型

> java采用的是共享内存模型

###### 2个关键问题(并发编程中)

* 线程之间如何通信

  > 通信是指线程之间以何种机制来交换信息

  * 通信机制

    * 命令式编程

      * 共享内存

        > 线程之间共享程序的公共状态，通过写-读内存中的公共状态
        > 进行隐式通信

      * 消息传递

        > 线程之间没有公共状态，线程之间必须通过发送消
        > 息来显式进行通信

* 线程之间如何同步

  > 同步是指程序中用于控制不同线程间操作发生相对顺序的机制

  * 共享内存

    > 程序员必须显式指定某个方法或某段代码需要在线程之间互斥执行，同步是显式进行的

  * 消息传递

    > 由于消息的发送必须在消息的接收之前，因此同步是隐式进行的

抽象的角度

> JMM定义了线程和主内存之间的抽象关系

###### 共享变量的存储

* 主内存  Main Memory

  * 共享变量

* 本地内存  Local Memory 

  > 本地内存是JMM的一个抽象概念，并不真实存在。它涵盖了缓存、写缓冲区、寄存器以及其他的硬件和编译器优化

  * 共享变量的副本

###### 重排序

> 重排序可能会导致多线程程序出现内存可见性问题
>
> 分为编译器重排序和处理器重排序

* 源代码
* 编译器优化重排序
* 指令级并行重排序
* 内存系统重排序
* 最终执行的指令序列

###### 

###### as-if-serial



###### volatile

> 从JSR-133开始（即从JDK5开始），volatile变量的写-读可以实现线程之间的通信
>
> volatile使用内存屏障解决

###### 内存屏障

* 概念

> （Memory Barriers，Intel称之为Memory Fence）
>
> 通过内存屏障指令来禁止特定类型的处理器重排序
>
> JMM内存屏障插入策略是基于保守策略的

* 分类
  - Load Barrier    读屏障 
  - Store Barrier   写屏障 
* 作用
  * 阻止屏障两侧的指令重排序 
  * 强制把写缓冲区/高速缓存中的脏数据等写回主内存，让缓存中相应的数据失效 
* java内存屏障
  * StoreStore
  * StoreLoad
  * LoadLoad
  * LoadStore



###### 锁的内存含义

> synchronized 

* 内存语义
* ReentrantLock分类
  * 公平锁
  * 非公平锁





###### final关键字

* 重排序规则
  * 

```java
public class FinalExample {

    int i; // 普通变量
    final int j; // final变量
    static FinalExample obj;
    public FinalExample () { // 构造函数
        i = 1; // 写普通域
        j = 2; // 写final域
    }

    public static void writer () { // 写线程A执行
    	obj = new FinalExample ();
    }	

    public static void reader () { // 读线程B执行
        FinalExample object = obj; // 读对象引用
        int a = object.i; // 读普通域
        int b = object.j; // 读final域
    }

}

```



###### happens-before

* JMM核心



###### as-if-serial 与 happens-before



###### 延迟初始化



