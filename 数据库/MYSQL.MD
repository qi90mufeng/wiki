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





