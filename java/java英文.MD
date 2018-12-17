#### Primitive 

​	本原，最原始的

```java
static byte[] convertToPrimitiveArray(Byte[] objects) {
    final byte[] bytes = new byte[objects.length];
    for (int i = 0; i < objects.length; i++) {
      bytes[i] = objects[i];
    }
    return bytes;
  }
```

