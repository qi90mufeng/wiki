java 第一代搜索引擎

Luncene



文本处理高效的做法是正则匹配



![1543149225574](C:\Users\boyuan\AppData\Roaming\Typora\typora-user-images\1543149225574.png)

搜索引擎

Solr

ES



ES下载与安装

6.5.1

集群配置:

解压三个包，重命名

​	master

​	slave

​	slave

elasticsearch.yml文件修改：

```
cluster.name: vip-demo

node.name:  vip-master

node.master: true

network.host: 127.0.0.1

```

```
cluster.name: vip-demo
node.name:  vip-slave1

network.host: 127.0.0.1
http.port: 8200

discovery.zen.ping.unicast.hosts: ["127.0.0.1"]
```

```
cluster.name: vip-demo
node.name:  vip-slave2

network.host: 127.0.0.1
http.port: 8201

discovery.zen.ping.unicast.hosts: ["127.0.0.1"]
```



cerebro   es集群web管理

可以使用kibana做web管理，不需要cerebro

kibana  6.5.1   



副本与分片



新增节点



数据扩容



custer health 



故障转移



脑裂问题





均匀分配到每个分片，避免数据热点问题



shard分片



![img](file:///C:\Users\boyuan\AppData\Roaming\Tencent\Users\478201880\QQ\WinTemp\RichOle\GYHUMFIEBY614H$SAK}{J}M.png)







相关性计算