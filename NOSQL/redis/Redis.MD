## 作者

antirez



## 官网

http://redisdoc.com/



## 编写语言

ANSI C语言编写



## 是否开源

开源



## 哨兵机制



## 部署方式

* 单节点部署方式

* 哨兵部署方式

* 集群部署方式


## 分布式锁

```java
@Slf4j
@Component
public class RedisService<E> implements IRedisService {

    @Autowired
    protected JedisCluster jedis;
    
       /**
     * Only set the key if it does not already exist.
     */
    private static final String SET_IF_NOT_EXIST = "NX";
    /**
     * Set the specified expire time, in milliseconds.
     */
    private static final String SET_WITH_EXPIRE_MILL_TIME = "PX";
    
      /**
     * 设置分布式锁.(过期时间毫秒)
     *
     * @param lockKey    锁的名称.
     * @param requestId  持锁人ID.
     * @param expireTime 锁的超时时间.
     * @return 是否获取锁.
     */
    public synchronized boolean tryGetDistributeLock(String lockKey, String requestId, int expireTime) {
        log.debug("lock key: {}, ownerId: {}, expire time: {}", lockKey, requestId, expireTime);
        String result = jedis.set(lockKey, requestId, SET_IF_NOT_EXIST, SET_WITH_EXPIRE_MILL_TIME, expireTime);
        if (LOCK_SUCCESS.equals(result)) {
            return true;
        }
        return false;
    }

    /**
     * 释放分布式锁.
     *
     * @param lockKey   锁
     * @param requestId 请求标识
     * @return 是否释放成功.
     */
    public synchronized boolean releaseDistributedLock(String lockKey, String requestId) {
        log.debug("release lock key: {}, ownerId: {}, expire time: {}", lockKey, requestId);
        String script = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end";
        Object result = jedis.eval(script, Collections.singletonList(lockKey), Collections.singletonList(requestId));
        if (RELEASE_SUCCESS.equals(result)) {
            return true;
        }
        return false;
    }
    
}
```







## Jedis





# Redisson

* 授权协议

  ```
  Apache License 2.0
  ```

* 开发团队

  ```
  jackygurui（中国）
  mrniko（俄罗斯）
  ```

* 开源版本、商业版本，谨慎选择

* 版本选择

  ```xml
  <!-- JDK 1.8+ compatible -->
  <dependency>
     <groupId>org.redisson</groupId>
     <artifactId>redisson</artifactId>
     <version>3.9.1</version>
  </dependency>  
  
  <!-- JDK 1.6+ compatible -->
  <dependency>
     <groupId>org.redisson</groupId>
     <artifactId>redisson</artifactId>
     <version>2.14.1</version>
  </dependency>
  ```
