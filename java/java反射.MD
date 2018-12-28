## Method

```java
public final class Method extends Executable{}

/* 
 * @since 1.8
 */
public abstract class Executable extends AccessibleObject
    implements Member, GenericDeclaration {}

/* 
 * @since 1.2
 */
public class AccessibleObject implements AnnotatedElement {}

public interface Member {}

/* 
 * @since 1.5
 */
public interface GenericDeclaration extends AnnotatedElement {}

/* 
 * @since 1.5
 */
public interface AnnotatedElement {}
```

Method内部方法

```JAVA
/*
 * 桥接方法 
 * @since 1.5
 */
public boolean isBridge() {
        return (getModifiers() & Modifier.BRIDGE) != 0;
}

编译时，会进行泛型擦除
public interface SuperClass<T> {
    void method(T t);
}

public class AClass implements SuperClass<String> {
    @Override
    public void method(String s) {
　　　　System.out.println(s);
　　} 
}
编译后
javac SuperClass.java
javap -p SuperClass.class
javap -c SuperClass.class
       
public interface SuperClass<T> {
  public abstract void method(T);
}

public class AaClass implements SuperClass<java.lang.String> {
  public com.java.reflect.AaClass();
  public void method(java.lang.String);
  public void method(java.lang.Object);
}
```

