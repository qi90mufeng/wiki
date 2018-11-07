## pom.xml解析

### POM 4

---

#### dependencyManagement

> 声明公共依赖的版本号，不引入依赖

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>Finchley SR1</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

#### dependency



#### scope

> 默认值为：compile 