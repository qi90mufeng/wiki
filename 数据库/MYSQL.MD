## mysql优化

### 1、服务器硬件



### 2、mysql服务器优化



### 3、sql本身优化

* 关联查询   子查询   关联子查询



### 4、反范式设计优化

* 针对范式化而言
* 为了性能和读取效率考虑适当得违反数据库设计范式的要求
* 允许存在少量冗余，换句话来说，就是空间换时间



### 5、物理设计优化

​	为表中得字段选择合适的数据类型

* 当一个列可以选择多种数据类型时

  * 优先考虑数字类型
  * 其次是日期、时间类型
  * 最后是字符类型
  * 对于相同级别得数据类型，应该优先选择占用空间小的数据类型

  存储引擎选择


### 6、索引优化

#### 	执行计划 explain

```
关键字段：  key  key_len
```

#### 	key_len 计算

```
char和varchar类型key_len计算公式:
varchr(N)变长字段且允许NULL   =  N * ( character set：utf8=3,gbk=2,latin1=1)+1(NULL)+2(变长字段)
varchr(N)变长字段且不允许NULL =  N * ( character set：utf8=3,gbk=2,latin1=1)+2(变长字段)

char(N)固定字段且允许NULL     =  N * ( character set：utf8=3,gbk=2,latin1=1)+1(NULL)
char(N)固定字段且允许NULL     =  N * ( character set：utf8=3,gbk=2,latin1=1)

 

数值数据的key_len计算公式：
TINYINT允许NULL = 1 + 1(NULL)
TINYINT不允许NULL = 1

SMALLINT允许为NULL = 2+1(NULL)
SMALLINT不允许为NULL = 2

INT允许为NULL = 4+1(NULL)
INT不允许为NULL = 4


日期时间型的key_len计算：（针对mysql5.5及之前版本）
DATETIME允许为NULL =  8 + 1(NULL)
DATETIME不允许为NULL = 8

TIMESTAMP允许为NULL = 4 + 1(NULL)
TIMESTAMP不允许为NULL = 4
```





## mysql基本知识

### 1、数据库锁

* 排它锁

* 共享锁

### 2、引擎

* InnoDB

* MyISAM

* ARCHIVE

  可以实现高并发的插入

  适合存储大量日志、历史数据

* BLACKHOLE

* MEMORY

* MRG_MYISAM

* PERFORMANCE_SCHEMA

* SPHINX

* TokuDB

* CSV

### 3、页

系统从磁盘读取数据到内存时是以磁盘块（block）为基本单位的，位于同一个磁盘块中的数据会被一次性读取出来，而不是需要什么取什么。

InnoDB存储引擎中有页（Page）的概念，页是其磁盘管理的最小单位。

InnoDB存储引擎中默认每个页的大小为16KB，可通过参数innodb_page_size将页的大小设置为4K、8K、16K，

```mysql
show variables like 'innodb_page_size';
```

### 4、多版本并发控制

​	mvvc





### 5、查询表大小等信息

```mysql
SELECT
	TABLE_NAME,
	TABLE_ROWS,
	concat(
		TRUNCATE (data_length / 1024 / 1024, 2),
		' MB'
	) AS data_size,
	concat(
		TRUNCATE (index_length / 1024 / 1024, 2),
		' MB'
	) AS index_size,
	ENGINE
FROM
	information_schema.TABLES
WHERE
	TABLE_SCHEMA = '库名';
```



## mysql性能指标

1、当前线程连接数

```mysql
show global status like 'threads_%';
```

| Threads_cached    | 当前此时此刻线程缓存中有多少空闲线程 | 70   |
| ----------------- | ------------------------------------ | ---- |
| Threads_connected | 当前已建立连接的数量                 | 30   |
| Threads_created   | 最近一次服务启动，已经创建线程的数量 | 103  |
| Threads_rejected  |                                      | 0    |
| Threads_running   | 当前激活（非睡眠）的线程数           | 1    |

2、连接数和最大连接数

```mysql
show global status like '%connections';
```

| Connection_errors_max_connections |      |      |
| --------------------------------- | ---- | ---- |
| Connections                       |      |      |
| Max_used_connections              |      |      |



```mysql
show global status like '%abort%';

show global status like '%table_lock%';

show global status like '%innodb_row_lock%';

show global status like '%slow_queries%';

show global status like '%binlog%';

show global status like 'select%';
```

