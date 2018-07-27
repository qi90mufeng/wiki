# typora使用手册

## 标题

`一阶标题    快捷键 Ctrl+1`

`二阶标题    快捷键 Ctrl+2`

`三阶标题    快捷键 Ctrl+3`

`四阶标题    快捷键 Ctrl+4`

`五阶标题    快捷键 Ctrl+5`

`六阶标题    快捷键 Ctrl+6`



## 下划线

<u>快捷键  Ctrl+U</u>



## 删除线

~~快捷键  Alt+Shift+5~~



## 加粗

 **快捷键  Ctrl+B**



## 斜体

*快捷键  Ctrl+I*



## 居中

<center>大家好</center> 



## 表格的使用

**Ctrl+T**，`会自动跳出设置行和列的设置框 

|      |      |
| ---: | ---- |
|      |      |



## 水平分割线

`***或者--- `



## 有序列表





## 插入图片

`直接拖动图片到指定位置即可`



## 上标

`右键打开Math Block ，  用的操作符是^` 
$$
2^3
$$

## 下标



## 返回开头

`Ctrl+Home` 



## 返回结尾

`Ctrl+End` 



## 创建链接

Ctrl+K



## 复选框（或任务列表）



## 数学表达式

### latex公式法则

在数学环境中表示这些符号  $ % & ~ _ ^ \ { }，即在个字符前加上\

数学公式，即在公式之前加上\

以下是部分latex公式例子：

-  *$lim_{x\to\infty}\exp(-x)=0$* 

$$
$lim_{x\to\infty}\exp(-x)=0$
$$

- *\sum_{i=1}^n a_i=0*

$$
\sum_{i=1}^n a_i=0
$$

- *f(x)=x^{x^x}*  

$$
f(x)=x^{x^x}
$$

- *f(x_1,x_x,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2* 

$$
f(x_1,x_x,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2
$$

- *\sqrt[y]{x}：开方*

$$
\sqrt[y]{x}
$$

- *\mbox{对任意的$x>0$}, \mbox{有 }f(x)>0.* 

$$
\mbox{对任意的$x>0$}, \mbox{有 }f(x)>0.
$$

- *\left.  \frac{du}{dx}  \right. |_{x=0}*

$$
\left.  \frac{du}{dx}  \right. |_{x=0}
$$



## 省略号 

\ldots ：表示跟文本底线对齐的省略号 
$$
\ldots
$$
\cdots ：表示跟文本中线对齐的省略号 
$$
\cdots
$$


## 表情符号

`（两个冒号中间加上描述语，比如这个就是happy）`       :happy:



## 代码编写

```js
//var fs;
var fs = require('fs')
    , stdin = process.stdin
    , stdout = process.stdout;

/*fs.readdir(__dirname, function (err, files) {
    console.log(files);
});*/
```





## 流程图 flow

`st=>start: Start|past:>http://www.google.com[blank]e=>end: End:>http://www.google.comop1=>operation: My Operation|pastop2=>operation: Stuff|currentsub1=>subroutine: My Subroutine|invalidcond=>condition: Yes or No?|approved:>http://www.baidu.comc2=>condition: Good idea|rejectedio=>inputoutput: catch something...|requestst->op1(right)->condcond(yes, right)->c2cond(no)->sub1(left)->op1c2(yes)->io->ec2(no)->op2->e`

```flow
​```flow
st=>start: Start|past:>http://www.google.com[blank]
e=>end: End:>http://www.google.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes 
or No?|approved:>http://www.baidu.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|request

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
​```
```



## 时序图 sequence

```sequence
Title:连接建立的过程
客户主机->服务器主机: 连接请求（SYN=1,seq=client_isn） 
服务器主机->客户主机: 授予连接（SYN=1,seq=client_isn）\n ack=client_isn+1
客户主机->服务器主机: 确认（SYN=0,seq=client_isn+1）\nack=server_isn+1
```



## 甘特图







