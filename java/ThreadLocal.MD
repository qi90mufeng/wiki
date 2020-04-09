ThreadLocal相关见识

## 1、类

```java
public class ThreadLocal<T> {
	public void set(T value) {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null)
            map.set(this, value);
        else
            createMap(t, value);
    }
    public T get() {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null) {
            ThreadLocalMap.Entry e = map.getEntry(this);
            if (e != null) {
                @SuppressWarnings("unchecked")
                T result = (T)e.value;
                return result;
            }
        }
        return setInitialValue();
    }
}
```

```java
public class InheritableThreadLocal<T> extends ThreadLocal<T> {

}
```

```java
static class ThreadLocalMap {
    static class Entry extends WeakReference<ThreadLocal<?>> {
            /** The value associated with this ThreadLocal. */
            Object value;
            Entry(ThreadLocal<?> k, Object v) {
                super(k);
                value = v;
            }
        }
}
```



## 2、知识点

1、弱引用

2、哈希冲突

3、变量传递



## 3、理解

##### 1、为什么ThreadLocalMap中Entry设计成弱引用（即key值设计成弱引用）？

> 线程内存管理角度看
>
>

##### 2、为什么ThreadLocalMap放在ThreadLocal中？

>

##### 3、ThreadLocal应用场景

>

##### 4、ThreadLocalMap处理哈希冲突的方式

> 开放定址法, 不是传统的链路法

##### 5、InheritableThreadLocal应用场景

>调用链监控
>
>

##### 6、父子线程如何传递变量

>