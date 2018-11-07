# spring boot系列

## 数据库JDBC

### 数据源 Dataource

* 类型

  * 通用型数据库  javax.sql.DataSource

    > 主要使用场景：通用型数据库，本地事务  一般用Socket方式连接

  * 分布式数据源  javax.sql.XADataSource

    > 主要使用场景：通用型数据库，分布式事务  一般用Socket方式连接
    >
    > 主要是在ejb，互联网应用少

  * 嵌入式数据源  org.springframework.jdbc.datasource.embedded.EmbeddedDatabase

    > 应用：浏览器历史记录、
    >
    > 主要使用场景：本地文件系统数据库，如： HSQL、H2、Derby等
    >
    > 枚举：org.springframework.jdbc.datasource.embedded.EmbeddedDatabaseType

    ```java
    package org.springframework.jdbc.datasource.embedded;
    import javax.sql.DataSource;
    public interface EmbeddedDatabase extends DataSource {
        void shutdown();
    }
    ```

    ```java
    package org.springframework.jdbc.datasource.embedded;
    public enum EmbeddedDatabaseType {
        HSQL,H2,DERBY;
        private EmbeddedDatabaseType() {
        }
    }
    ```

    

### 事务

### JDBC 4.0（JSR-221）

### springboot整合

### 问答互动