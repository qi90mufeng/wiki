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

