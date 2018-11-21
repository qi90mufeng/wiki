## 作者

Trustin Lee



## 官方文档

http://netty.io/wiki/user-guide.html 



## 应用场景

1、Hadoop的RPC框架avro使用netty作为底层通信框架

2、dubbo

3、





## 版本变更

* netty3.x
* netty4.x
* netty5.x



## 服务端需要处理的糟糕情况

1、处理网络闪退

2、客户端的重复接入

3、客户端的安全认证

4、消息的编解码

5、半包读写



## TCP粘包拆包问题

* 解码器
  * FixedLengthFrameDecoder
  * DelimiterBasedFrameDecoder
  * LineBasedFrameDecoder
  * StringDecoder



## 编解码器框架

* 评价优劣

```
1、是否支持跨语言，支持的语言种类是否丰富
2、编码后的码流大小
3、编解码的性能
4、类库是否小巧，API使用是否方便
5、使用者需要手工开发的工作量和难度
```

* 框架

  * Protobuf

    ```
    Google
    ```

  * Thrift

    ```
    Facebook
    ```

  * 



## netty4研究

