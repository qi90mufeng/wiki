备注：此次研究的mybatis 3.4.6版本

# 项目结构

## annotations

## binding

## builder

## cache

## cursor

## datasource

## execeptions

## executor



## io

### VFS

> 虚拟文件系统



## jdbc

## lang



## logging 

* Log 

  ```java
  public interface Log {
    boolean isDebugEnabled();
    boolean isTraceEnabled();
    void error(String s, Throwable e);
    void error(String s);
    void debug(String s);
    void trace(String s);
    void warn(String s);
  }
  ```

* LogFactory

  > 运行时自省机制选择合适的日志工具，选择第一个查找到的日志工具

  ```java
  public final class LogFactory {
    public static final String MARKER = "MYBATIS";
    private static Constructor<? extends Log> logConstructor;
  
    static {
      tryImplementation(()->
          useSlf4jLogging()
      );
      tryImplementation(new Runnable() {
        @Override
        public void run() {
          useCommonsLogging();
        }
      });
      tryImplementation(new Runnable() {
        @Override
        public void run() {
          useLog4J2Logging();
        }
      });
      tryImplementation(new Runnable() {
        @Override
        public void run() {
          useLog4JLogging();
        }
      });
      tryImplementation(new Runnable() {
        @Override
        public void run() {
          useJdkLogging();
        }
      });
      tryImplementation(new Runnable() {
        @Override
        public void run() {
          useNoLogging();
        }
      });
    }
  
    private LogFactory() {
      // disable construction
    }
  
    public static Log getLog(Class<?> aClass) {
      return getLog(aClass.getName());
    }
  
    public static Log getLog(String logger) {
      try {
        return logConstructor.newInstance(logger);
      } catch (Throwable t) {
        throw new LogException("Error creating logger for logger " + logger + ".  Cause: " + t, t);
      }
    }
  
    public static synchronized void useCustomLogging(Class<? extends Log> clazz) {
      setImplementation(clazz);
    }
  
    public static synchronized void useSlf4jLogging() {
      setImplementation(org.apache.ibatis.logging.slf4j.Slf4jImpl.class);
    }
  
    public static synchronized void useCommonsLogging() {
      setImplementation(org.apache.ibatis.logging.commons.JakartaCommonsLoggingImpl.class);
    }
  
    public static synchronized void useLog4JLogging() {
      setImplementation(org.apache.ibatis.logging.log4j.Log4jImpl.class);
    }
  
    public static synchronized void useLog4J2Logging() {
      setImplementation(org.apache.ibatis.logging.log4j2.Log4j2Impl.class);
    }
  
    public static synchronized void useJdkLogging() {
      setImplementation(org.apache.ibatis.logging.jdk14.Jdk14LoggingImpl.class);
    }
  
    public static synchronized void useStdOutLogging() {
      setImplementation(org.apache.ibatis.logging.stdout.StdOutImpl.class);
    }
  
    public static synchronized void useNoLogging() {
      setImplementation(org.apache.ibatis.logging.nologging.NoLoggingImpl.class);
    }
  
    private static void tryImplementation(Runnable runnable) {
      if (logConstructor == null) {
        try {
          runnable.run();
        } catch (Throwable t) {
          // ignore
        }
      }
    }
  
    private static void setImplementation(Class<? extends Log> implClass) {
      try {
        Constructor<? extends Log> candidate = implClass.getConstructor(String.class);
        Log log = candidate.newInstance(LogFactory.class.getName());
        if (log.isDebugEnabled()) {
          log.debug("Logging initialized using '" + implClass + "' adapter.");
        }
        logConstructor = candidate;
      } catch (Throwable t) {
        throw new LogException("Error setting Log implementation.  Cause: " + t, t);
      }
    }
  }
  ```


## mapping

## parsing

## plugin

## reflection

## scripting

## session

## transaction

## type









