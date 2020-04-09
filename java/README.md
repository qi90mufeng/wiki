# JAVA架构体系

### 基本数据类型

| 基本类型 | 字节数 | 位数  | 最大值                 | 最小值     |
| -------- | ------ | ----- | ---------------------- | ---------- |
| byte     | 1byte  | 8bit  | 2^7 - 1                | -2^7       |
| short    | 2byte  | 16bit | 2^15 - 1               | -2^15      |
| int      | 4byte  | 32bit | 2^31 - 1               | -2^31      |
| long     | 8byte  | 64bit | 2^63 - 1               | -2^63      |
| float    | 4byte  | 32bit | 3.4028235E38           | 1.4E - 45  |
| double   | 8byte  | 64bit | 1.7976931348623157E308 | 4.9E - 324 |
| char     | 2byte  | 16bit | 2^16 - 1               | 0          |



### 元注解

@Target

```java
package java.lang.annotation;
/* 
 * @since 1.5
 * @jls 9.6.4.1 @Target
 * @jls 9.7.4 Where Annotations May Appear
 */
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Target {
    /**
     * Returns an array of the kinds of elements an annotation type
     * can be applied to.
     * @return an array of the kinds of elements an annotation type
     * can be applied to
     */
    ElementType[] value();
}
```



@Retention

```java
package java.lang.annotation;
/* 
 * @author  Joshua Bloch
 * @since 1.5
 * @jls 9.6.3.2 @Retention
 */
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Retention {
    /**
     * Returns the retention policy.
     * @return the retention policy
     */
    RetentionPolicy value();
}
```

@Document

```java
package java.lang.annotation;
/*
 * @author  Joshua Bloch
 * @since 1.5
 */
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Documented {
}
```

@Inherited

```java
package java.lang.annotation;
/*
 * @author  Joshua Bloch
 * @since 1.5
 * @jls 9.6.3.3 @Inherited
 */
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Inherited {
}
```



### 四种引用类型(Reference)

#### 1、强引用

```java
Object obj =new Object();  // 强引用
obj = null;//这时候为垃圾回收器回收这个对象，至于什么时候回收，取决于垃圾回收器的算法
```

#### 2、软引用(SoftReference )

> 适合需要cache场景，面向实现内存敏感的缓存

```java
String value = new String(“sy”);
// 声明一个引用队列rq
ReferenceQueue<String> rq = new ReferenceQueue<>();
// 声明一个软引用,并且将sfRefer1指向value所指的对象
SoftReference<String> sfRefer1 = new SoftReference<String>(value);
// 声明一个软引用,并且将sfRefer2指向value所指的对象，并将他和引用队列绑定
SoftReference<String> sfRefer2 = new SoftReference<String>(value, rq);
sfRefer1.get();//可以获得引用对象值
```

#### 3、弱引用(WeakReference)

> 适合某些场景为了无法防止被回收的规范性映射

```java
String value = new String(“sy”);
WeakReference weakRefer = new WeakReference(value );
System.gc();
weakRefer.get();//null
```

#### 4、虚引用(PhantomReference)

> 虚引用主要用于检测对象是否已经从内存中删除

```java
Object obj = new Object();
PhantomReference<Object> pf = new PhantomReference<Object>(obj);
obj=null;
pf.get();//永远返回null
pf.isEnQueued();//返回是否从内存中已经删除
```

### 关键字





### 多线程

#### Future体系

ForkJoinTask

CompletableFuture

RunnableFuture

ScheduledFuture