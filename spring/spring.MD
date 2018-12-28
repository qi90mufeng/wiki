# 核心组件

## IOC

容器管理bean



## AOP

> **连接点(Joinpoint)**
>
> **切点(Pointcut)**
>
> **增强(Advice)**
>
> **目标对象(Target)**
>
> **引介(Introduction)**
>
> **织入(Weaving)**
>
> **代理(Proxy)**
>
> **切面(Aspect)**



### 1、切点类型   Pointcut

```java
public interface Pointcut {
   ClassFilter getClassFilter();
   MethodMatcher getMethodMatcher();
   Pointcut TRUE = TruePointcut.INSTANCE;
}

//通过ClassFilter定位到某些特定类上，通过MethodMatcher定位到某些特定的方法上
```

```java
 Pointcut
 	TruePointcut
 	AnnotationMatchingPointcut
 	StaticMethodMatcherPointcut
 		StaticMethodMatcherPointcutAdvisor
 		NameMatchMethodPointcut
 		AbstractRegexpMethodPointcut
 			JdkRegexpMethodPointcut
 	ExpressionPointcut
 		AbstractExpressionPointcut
 			AspectJExpressionPointcut
 	DynamicMethodMatcherPointcut
 	ControlFlowPointcut
 	ComposablePointcut
```

#### 1.1、静态方法切点

```java
StaticMethodMatcherPointcut
	NameMatchMethodPointcut
	AbstractRegexpMethodPointcut
```

#### 1.2、动态方法切点

```java
DynamicMethodMatcherPointcut
```

#### 1.3、注解切点

```java
AnnotationMatchingPointcut
```

#### 1.4、表达式切点

```java
ExpressionPointcut
```

#### 1.5、流程切点

```java
ControlFlowPointcut
```

#### 1.6、复合切点

```java
ComposablePointcut
```



### 2、切面类型   Advisor

> ```java
> public interface Advice {
> }
> public interface Advisor {
> 	Advice EMPTY_ADVICE = new Advice() {};
> 	Advice getAdvice();
> 	boolean isPerInstance();
> }
> ```

```java
Advisor
	PointcutAdvisor
		AbstractPointcutAdvisor
			AbstractGenericPointcutAdvisor
				RegexpMethodPointcutAdvisor
				NameMatchMethodPointcutAdvisor
				DefaultPointcutAdvisor
				AspectJExpressionPointcutAdvisor
			AbstractBeanFactoryPointcutAdvisor
				DefaultBeanFactoryPointcutAdvisor
		InstantiationModelAwarePointcutAdvisor
		AspectJPointcutAdvisor
	IntroductionAdvisor
		DefaultIntroductionAdvisor
		DeclareParentsAdvisor
```

#### 2.1、PointcutAdvisor

```java
public interface PointcutAdvisor extends Advisor {
   Pointcut getPointcut();
}
```

##### 2.1.1、DefaultPointcutAdvisor

##### 2.1.2、NameMatchMethodPointcutAdvisor

##### 2.1.3、RegexpMethodPointcutAdvisor

##### 2.1.4、StaticMethodMatcherPointcutAdvisor

##### 2.1.5、AspectJExpressionPointcutAdvisor

##### 2.1.6、AspectJPointcutAdvisor

#### 2.2、IntroductionAdvisor

```java
public interface IntroductionAdvisor extends Advisor, IntroductionInfo {
   ClassFilter getClassFilter();
   void validateInterfaces() throws IllegalArgumentException;
}
```

2.2.1、DefaultIntroductionAdvisor

2.2.2、DeclareParentsAdvisor

### 3、**创建代理 ** BeanPostProcessor

3.1、BeanNameAutoProxyCreator

3.2、DefaultAdvisorAutoProxyCreator

### 4、增强 Advice

```
Advice
	BeforeAdvice
		MethodBeforeAdvice
			AspectJMethodBeforeAdvice
	AfterAdvice
		AfterReturningAdvice
			AspectJAfterReturningAdvice
		AfterReturningAdviceInterceptor
		AspectJAfterThrowingAdvice
		AspectJAfterReturningAdvice
	DynamicIntroductionAdvice
		IntroductionInterceptor
	ThrowsAdvice
	Interceptor
		MethodInterceptor
		ConstructorInterceptor
	AbstractAspectJAdvice
		AspectJMethodBeforeAdvice
		AspectJAroundAdvice
		AspectJAfterAdvice
		AspectJAfterReturningAdvice
		AspectJAfterThrowingAdvice
```

#### 4.1、前置增强

```
Advice
	AfterAdvice
		ThrowsAdvice
```

org.springframework.aop.MethodBeforeAdvice，表示在目标方法执行前实施增强。

#### 4.2、 后置增强

org.springframework.aop.AfterReturningAdvice，表示在目标方法执行后实施增强。

#### 4.3、 环绕增强

org.aopalliance.intercept.MethodInterceptor，表示在目标方法执行前后实施增强。

#### 4.4、异常增强

org.springframework.aop.ThrowsAdvice，表示在目标方法抛出异常后后实施增强。

#### 4.5、引介增强

org.springframework.aop.IntroductionInterceptor，表示在目标类中添加一些新的方法和属性。

### 5、Interceptor

```
Interceptor
	MethodInterceptor
		IntroductionInterceptor
			DelegatingIntroductionInterceptor
			DelegatePerTargetObjectIntroductionInterceptor
		AbstractTraceInterceptor
			SimpleTraceInterceptor
				DebugInterceptor
			AbstractMonitoringInterceptor
				PerformanceMonitorInterceptor
				JamonPerformanceMonitorInterceptor
			CustomizableTraceInterceptor
		ExposeInvocationInterceptor
		ConcurrencyThrottleInterceptor
		AsyncExecutionInterceptor
		ThrowsAdviceInterceptor
		MethodBeforeAdviceInterceptor
		AfterReturningAdviceInterceptor
		AspectJAroundAdvice
		AspectJAfterThrowingAdvice
		AspectJAfterAdvice
	ConstructorInterceptor
```

### 6、Joinpoint

```
Joinpoint
	Invocation
		ConstructorInvocation
		MethodInvocation
			ProxyMethodInvocation
				ReflectiveMethodInvocation
	
		
```

### 7、代理类型 AopProxy

```
AopProxy
	JdkDynamicAopProxy
	CglibAopProxy
		ObjenesisCglibAopProxy
SpringProxy
	TransactionalProxy
```

7.1、JdkDynamicAopProxy

7.2、CglibAopProxy



### 8、MethodMatcher

```
MethodMatcher
	TrueMethodMatcher
	StaticMethodMatcher
		AnnotationMethodMatcher
		StaticMethodMatcherPointcut
	IntroductionAwareMethodMatcher
	DynamicMethodMatcher
		DynamicMethodMatcherPointcut
```

### 9、ClassFilter

```
ClassFilter
	TrueClassFilter
	AnnotationClassFilter
	RootClassFilter
	TypePatternClassFilter
```

### 10、TargetClassAware

```
TargetClassAware
	TargetSource
		JndiObjectTargetSource
	Advised
		AdvisedSupport
			ProxyCreatorSupport
				ProxyFactory
```

### 11、RawTargetAccess

```
RawTargetAccess
```

### 12、IntroductionInfo

```
IntroductionInfo
	IntroductionInfoSupport
		DelegatingIntroductionInterceptor
		DelegatePerTargetObjectIntroductionInterceptor
```

### 13、AopProxyFactory

```
AopProxyFactory
	DefaultAopProxyFactory
```

### 14、AdvisorChainFactory

```
AdvisorChainFactory
	DefaultAdvisorChainFactory
```

### 15、AdvisedSupportListener

```
AdvisedSupportListener
```

### 16、AdvisorAdapter

```
AdvisorAdapter
	ThrowsAdviceAdapter
	MethodBeforeAdviceAdapter
    AfterReturningAdviceAdapter
    
```

### 17、AspectJAdvisorFactory

```
AspectJAdvisorFactory
	AbstractAspectJAdvisorFactory
```



## 类解读

```java
public class ContextNamespaceHandler extends NamespaceHandlerSupport {
	@Override
	public void init() {
		registerBeanDefinitionParser("property-placeholder", new PropertyPlaceholderBeanDefinitionParser());
		registerBeanDefinitionParser("property-override", new PropertyOverrideBeanDefinitionParser());
		registerBeanDefinitionParser("annotation-config", new AnnotationConfigBeanDefinitionParser());
		registerBeanDefinitionParser("component-scan", new ComponentScanBeanDefinitionParser());
		registerBeanDefinitionParser("load-time-weaver", new LoadTimeWeaverBeanDefinitionParser());
		registerBeanDefinitionParser("spring-configured", new SpringConfiguredBeanDefinitionParser());
		registerBeanDefinitionParser("mbean-export", new MBeanExportBeanDefinitionParser());
		registerBeanDefinitionParser("mbean-server", new MBeanServerBeanDefinitionParser());
	}
}
```

# 功能

## 数据库路由

```java
/**
 * Abstract {@link javax.sql.DataSource} implementation that routes {@link #getConnection()}
 * calls to one of various target DataSources based on a lookup key. The latter is usually
 * (but not necessarily) determined through some thread-bound transaction context.
 *
 * @author Juergen Hoeller
 * @since 2.0.1
 * @see #setTargetDataSources
 * @see #setDefaultTargetDataSource
 * @see #determineCurrentLookupKey()
 */
public abstract class AbstractRoutingDataSource extends AbstractDataSource implements InitializingBean {

	private Map<Object, Object> targetDataSources;

	private Object defaultTargetDataSource;

	private boolean lenientFallback = true;

	private DataSourceLookup dataSourceLookup = new JndiDataSourceLookup();

	private Map<Object, DataSource> resolvedDataSources;

	private DataSource resolvedDefaultDataSource;


	/**
	 * Specify the map of target DataSources, with the lookup key as key.
	 * The mapped value can either be a corresponding {@link javax.sql.DataSource}
	 * instance or a data source name String (to be resolved via a
	 * {@link #setDataSourceLookup DataSourceLookup}).
	 * <p>The key can be of arbitrary type; this class implements the
	 * generic lookup process only. The concrete key representation will
	 * be handled by {@link #resolveSpecifiedLookupKey(Object)} and
	 * {@link #determineCurrentLookupKey()}.
	 */
	public void setTargetDataSources(Map<Object, Object> targetDataSources) {
		this.targetDataSources = targetDataSources;
	}

	/**
	 * Specify the default target DataSource, if any.
	 * <p>The mapped value can either be a corresponding {@link javax.sql.DataSource}
	 * instance or a data source name String (to be resolved via a
	 * {@link #setDataSourceLookup DataSourceLookup}).
	 * <p>This DataSource will be used as target if none of the keyed
	 * {@link #setTargetDataSources targetDataSources} match the
	 * {@link #determineCurrentLookupKey()} current lookup key.
	 */
	public void setDefaultTargetDataSource(Object defaultTargetDataSource) {
		this.defaultTargetDataSource = defaultTargetDataSource;
	}

	/**
	 * Specify whether to apply a lenient fallback to the default DataSource
	 * if no specific DataSource could be found for the current lookup key.
	 * <p>Default is "true", accepting lookup keys without a corresponding entry
	 * in the target DataSource map - simply falling back to the default DataSource
	 * in that case.
	 * <p>Switch this flag to "false" if you would prefer the fallback to only apply
	 * if the lookup key was {@code null}. Lookup keys without a DataSource
	 * entry will then lead to an IllegalStateException.
	 * @see #setTargetDataSources
	 * @see #setDefaultTargetDataSource
	 * @see #determineCurrentLookupKey()
	 */
	public void setLenientFallback(boolean lenientFallback) {
		this.lenientFallback = lenientFallback;
	}

	/**
	 * Set the DataSourceLookup implementation to use for resolving data source
	 * name Strings in the {@link #setTargetDataSources targetDataSources} map.
	 * <p>Default is a {@link JndiDataSourceLookup}, allowing the JNDI names
	 * of application server DataSources to be specified directly.
	 */
	public void setDataSourceLookup(DataSourceLookup dataSourceLookup) {
		this.dataSourceLookup = (dataSourceLookup != null ? dataSourceLookup : new JndiDataSourceLookup());
	}


	@Override
	public void afterPropertiesSet() {
		if (this.targetDataSources == null) {
			throw new IllegalArgumentException("Property 'targetDataSources' is required");
		}
		this.resolvedDataSources = new HashMap<Object, DataSource>(this.targetDataSources.size());
		for (Map.Entry<Object, Object> entry : this.targetDataSources.entrySet()) {
			Object lookupKey = resolveSpecifiedLookupKey(entry.getKey());
			DataSource dataSource = resolveSpecifiedDataSource(entry.getValue());
			this.resolvedDataSources.put(lookupKey, dataSource);
		}
		if (this.defaultTargetDataSource != null) {
			this.resolvedDefaultDataSource = resolveSpecifiedDataSource(this.defaultTargetDataSource);
		}
	}

	/**
	 * Resolve the given lookup key object, as specified in the
	 * {@link #setTargetDataSources targetDataSources} map, into
	 * the actual lookup key to be used for matching with the
	 * {@link #determineCurrentLookupKey() current lookup key}.
	 * <p>The default implementation simply returns the given key as-is.
	 * @param lookupKey the lookup key object as specified by the user
	 * @return the lookup key as needed for matching
	 */
	protected Object resolveSpecifiedLookupKey(Object lookupKey) {
		return lookupKey;
	}

	/**
	 * Resolve the specified data source object into a DataSource instance.
	 * <p>The default implementation handles DataSource instances and data source
	 * names (to be resolved via a {@link #setDataSourceLookup DataSourceLookup}).
	 * @param dataSource the data source value object as specified in the
	 * {@link #setTargetDataSources targetDataSources} map
	 * @return the resolved DataSource (never {@code null})
	 * @throws IllegalArgumentException in case of an unsupported value type
	 */
	protected DataSource resolveSpecifiedDataSource(Object dataSource) throws IllegalArgumentException {
		if (dataSource instanceof DataSource) {
			return (DataSource) dataSource;
		}
		else if (dataSource instanceof String) {
			return this.dataSourceLookup.getDataSource((String) dataSource);
		}
		else {
			throw new IllegalArgumentException(
					"Illegal data source value - only [javax.sql.DataSource] and String supported: " + dataSource);
		}
	}


	@Override
	public Connection getConnection() throws SQLException {
		return determineTargetDataSource().getConnection();
	}

	@Override
	public Connection getConnection(String username, String password) throws SQLException {
		return determineTargetDataSource().getConnection(username, password);
	}

	@Override
	@SuppressWarnings("unchecked")
	public <T> T unwrap(Class<T> iface) throws SQLException {
		if (iface.isInstance(this)) {
			return (T) this;
		}
		return determineTargetDataSource().unwrap(iface);
	}

	@Override
	public boolean isWrapperFor(Class<?> iface) throws SQLException {
		return (iface.isInstance(this) || determineTargetDataSource().isWrapperFor(iface));
	}

	/**
	 * Retrieve the current target DataSource. Determines the
	 * {@link #determineCurrentLookupKey() current lookup key}, performs
	 * a lookup in the {@link #setTargetDataSources targetDataSources} map,
	 * falls back to the specified
	 * {@link #setDefaultTargetDataSource default target DataSource} if necessary.
	 * @see #determineCurrentLookupKey()
	 */
	protected DataSource determineTargetDataSource() {
		Assert.notNull(this.resolvedDataSources, "DataSource router not initialized");
		Object lookupKey = determineCurrentLookupKey();
		DataSource dataSource = this.resolvedDataSources.get(lookupKey);
		if (dataSource == null && (this.lenientFallback || lookupKey == null)) {
			dataSource = this.resolvedDefaultDataSource;
		}
		if (dataSource == null) {
			throw new IllegalStateException("Cannot determine target DataSource for lookup key [" + lookupKey + "]");
		}
		return dataSource;
	}

	/**
	 * Determine the current lookup key. This will typically be
	 * implemented to check a thread-bound transaction context.
	 * <p>Allows for arbitrary keys. The returned key needs
	 * to match the stored lookup key type, as resolved by the
	 * {@link #resolveSpecifiedLookupKey} method.
	 */
	protected abstract Object determineCurrentLookupKey();

}
```



# 注释

## @Autowired



```java
package org.springframework.beans.factory.annotation;
/* @author Juergen Hoeller
 * @author Mark Fisher
 * @since 2.5
 * @see AutowiredAnnotationBeanPostProcessor
 * @see Qualifier
 * @see Value
 */
@Target({ElementType.CONSTRUCTOR, ElementType.METHOD, ElementType.PARAMETER, ElementType.FIELD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Autowired {

	/**
	 * Declares whether the annotated dependency is required.
	 * <p>Defaults to {@code true}.
	 */
	boolean required() default true;

}
```

## @Primary



```java
package org.springframework.context.annotation;
/* @author Chris Beams
 * @since 3.0
 * @see Lazy
 * @see Bean
 * @see ComponentScan
 * @see org.springframework.stereotype.Component
 */
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
public @interface Primary {

}
```



## @EnableAsync

```java
package org.springframework.scheduling.annotation;

/* @author Chris Beams
 * @author Juergen Hoeller
 * @author Stephane Nicoll
 * @author Sam Brannen
 * @since 3.1
 * @see Async
 * @see AsyncConfigurer
 * @see AsyncConfigurationSelector
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Import(AsyncConfigurationSelector.class)
public @interface EnableAsync {
    Class<? extends Annotation> annotation() default Annotation.class;
    boolean proxyTargetClass() default false;
    AdviceMode mode() default AdviceMode.PROXY;
    int order() default Ordered.LOWEST_PRECEDENCE;
}
```

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.scheduling.annotation.EnableAsync;
import org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor;

import java.util.concurrent.Executor;
import java.util.concurrent.ThreadPoolExecutor;

@SpringBootApplication
@EnableAsync
public class MonitorServerApplication{
    
	public static void main(String[] args) {
		SpringApplication.run(MonitorCenterConfig.class, args);
	}

    @Bean("store-async")
    public Executor executor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setMaxPoolSize(40);
        executor.setCorePoolSize(20);
        executor.setQueueCapacity(200);
        executor.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy());
        executor.initialize();
        return executor;
    }
}
```







# 事务

## 目的

 保持数据或资源一致性

## 特性

* A 原子性
* C 一致性
* I  隔离性
* D 持久性

## 事务支持

### Java Transaction API  (JTA)

```xml
<bean id="transactionManager"
    class="org.springframework.transaction.jta.JtaTransactionManager">
    <property name="transactionManagerName" value="java:/TransactionManager" />
</bean>
```



### jdbc事务

```xml
<bean id="transactionManager"
    class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="dataSource" ref="dataSource" />
</bean>
```

```java
public class DataSourceTransactionManager extends AbstractPlatformTransactionManager  
        implements ResourceTransactionManager, InitializingBean {  
    //注入数据源  
    private DataSource dataSource;  
//数据源事务处理器默认构造方法，创建一个数据源事务处理器实例，并设置允许嵌套事务  
    public DataSourceTransactionManager() {  
        setNestedTransactionAllowed(true);  
    }  
    //根据给定数据源，创建一个数据源事务处理器实例  
    public DataSourceTransactionManager(DataSource dataSource) {  
        this();  
        setDataSource(dataSource);  
        afterPropertiesSet();  
    }  
    //设置数据源  
    public void setDataSource(DataSource dataSource) {  
        if (dataSource instanceof TransactionAwareDataSourceProxy) {  
            //如果数据源是一个事务包装数据源代理，则获取事务包装代理的目标数据源   
            this.dataSource = ((TransactionAwareDataSourceProxy) dataSource).getTargetDataSource();  
        }  
        else {  
            this.dataSource = dataSource;  
        }  
    }  
    //获取数据源  
    public DataSource getDataSource() {  
        return this.dataSource;  
    }  
    //数据源事务处理器对象构造方法的回调函数  
    public void afterPropertiesSet() {  
        if (getDataSource() == null) {  
            throw new IllegalArgumentException("Property 'dataSource' is required");  
        }  
    }  
public Object getResourceFactory() {  
        return getDataSource();  
    }  
//创建事务，对数据库而言，是由Connection来完成事务工作的。该方法把数据库的//Connection对象放到一个ConnectionHolder对象中，然后封装到一个  
//DataSourceTransactionObject对象中  
    protected Object doGetTransaction() {  
        //创建数据源事务对象  
        DataSourceTransactionObject txObject = new DataSourceTransactionObject();  
        //设置数据源事务对象对嵌套事务使用保存点  
        txObject.setSavepointAllowed(isNestedTransactionAllowed());  
        //从事务管理容器中获取存放数据库Connection的对象  
        ConnectionHolder conHolder =  
            (ConnectionHolder) TransactionSynchronizationManager.getResource(this.dataSource);  
        txObject.setConnectionHolder(conHolder, false);  
        return txObject;  
    }  
    //判断是否已经存在事务  
    protected boolean isExistingTransaction(Object transaction) {  
        DataSourceTransactionObject txObject = (DataSourceTransactionObject) transaction;  
    //根据存放数据库连接的ConnectionHolder的isTransactionActive属性来判断  
        return (txObject.getConnectionHolder() != null && txObject.getConnectionHolder().isTransactionActive());  
    }  
    //处理事务开始的方法  
    protected void doBegin(Object transaction, TransactionDefinition definition) {  
        DataSourceTransactionObject txObject = (DataSourceTransactionObject) transaction;  
        Connection con = null;  
        try {  
            //如果数据源事务对象的ConnectionHolder为null或者是事务同步的  
            if (txObject.getConnectionHolder() == null ||  
        txObject.getConnectionHolder().isSynchronizedWithTransaction()) {  
                //获取当前数据源的数据库连接  
                Connection newCon = this.dataSource.getConnection();  
                if (logger.isDebugEnabled()) {  
                    logger.debug("Acquired Connection [" + newCon + "] for JDBC transaction");  
                }  
                //为数据源事务对象设置ConnectionHolder  
                txObject.setConnectionHolder(new ConnectionHolder(newCon), true);  
            }  
    //设置数据源事务对象的事务同步    txObject.getConnectionHolder().setSynchronizedWithTransaction(true);  
            //获取数据源事务对象的数据库连接  
            con = txObject.getConnectionHolder().getConnection();  
            //根据数据连接和事务属性，获取数据库连接的事务隔离级别  
            Integer previousIsolationLevel = DataSourceUtils.prepareConnectionForTransaction(con, definition);  
    //为数据源事务对象设置事务隔离级别  
    txObject.setPreviousIsolationLevel(previousIsolationLevel);  
            //如果数据库连接设置了自动事务提交属性，则关闭自动提交  
            if (con.getAutoCommit()) {  
                //保存数据库连接设置的自动连接到数据源事务对象中  
                txObject.setMustRestoreAutoCommit(true);  
                if (logger.isDebugEnabled()) {  
                    logger.debug("Switching JDBC Connection [" + con + "] to manual commit");  
                }  
                //设置数据库连接自动事务提交属性为false，即禁止自动事务提交  
                con.setAutoCommit(false);  
            }  
            //激活当前数据源事务对象的事务配置  
            txObject.getConnectionHolder().setTransactionActive(true);  
            //获取事务配置的超时时长  
int timeout = determineTimeout(definition);  
//如果事务配置的超时时长不等于事务的默认超时时长  
            if (timeout != TransactionDefinition.TIMEOUT_DEFAULT) {  
        //数据源事务对象设置超时时长  
        txObject.getConnectionHolder().setTimeoutInSeconds(timeout);  
            }  
            //把当前数据库Connection和线程绑定  
            if (txObject.isNewConnectionHolder()) {  
        TransactionSynchronizationManager.bindResource(getDataSource(), txObject.getConnectionHolder());  
            }  
        }  
        catch (Exception ex) {  
            DataSourceUtils.releaseConnection(con, this.dataSource);  
            throw new CannotCreateTransactionException("Could not open JDBC Connection for transaction", ex);  
        }  
    }  
    //事务挂起  
    protected Object doSuspend(Object transaction) {  
        //获取事务对象  
        DataSourceTransactionObject txObject = (DataSourceTransactionObject) transaction;  
        //将事务对象中的ConnectionHolders设置为null  
        txObject.setConnectionHolder(null);  
        ConnectionHolder conHolder = (ConnectionHolder)  
        //解除事务对象和当前线程的绑定    TransactionSynchronizationManager.unbindResource(this.dataSource);  
        return conHolder;  
    }  
    //事务恢复  
    protected void doResume(Object transaction, Object suspendedResources) {  
        //获取已暂停事务的ConnectionHolder  
        ConnectionHolder conHolder = (ConnectionHolder) suspendedResources;  
        //重新将事务对象和当前线程绑定  
        TransactionSynchronizationManager.bindResource(this.dataSource, conHolder);  
    }  
    //事务提交  
    protected void doCommit(DefaultTransactionStatus status) {  
        //获取事务对象  
        DataSourceTransactionObject txObject = (DataSourceTransactionObject) status.getTransaction();  
        //通过事务对象获取数据库连接  
        Connection con = txObject.getConnectionHolder().getConnection();  
        if (status.isDebug()) {  
            logger.debug("Committing JDBC transaction on Connection [" + con + "]");  
        }  
        try {  
            //使用数据库连接手动进行事务提交  
            con.commit();  
        }  
        catch (SQLException ex) {  
            throw new TransactionSystemException("Could not commit JDBC transaction", ex);  
        }  
    }  
    //事务回滚  
    protected void doRollback(DefaultTransactionStatus status) {  
        //获取事务对象  
        DataSourceTransactionObject txObject = (DataSourceTransactionObject) status.getTransaction();  
        //通过事务对象获取数据库连接  
        Connection con = txObject.getConnectionHolder().getConnection();  
        if (status.isDebug()) {  
            logger.debug("Rolling back JDBC transaction on Connection [" + con + "]");  
        }  
        try {  
            //通过调用数据库连接的回滚方法完成事务回滚操作  
            con.rollback();  
        }  
        catch (SQLException ex) {  
            throw new TransactionSystemException("Could not roll back JDBC transaction", ex);  
        }  
    }  
    //设置回滚  
    protected void doSetRollbackOnly(DefaultTransactionStatus status) {  
        DataSourceTransactionObject txObject = (DataSourceTransactionObject) status.getTransaction();  
        if (status.isDebug()) {  
            logger.debug("Setting JDBC transaction [" + txObject.getConnectionHolder().getConnection() +  
                    "] rollback-only");  
        }  
        txObject.setRollbackOnly();  
    }  
    //操作完成之后清除操作  
    protected void doCleanupAfterCompletion(Object transaction) {  
        DataSourceTransactionObject txObject = (DataSourceTransactionObject) transaction;  
        //移除当前线程绑定的ConnectionHolder  
        if (txObject.isNewConnectionHolder()) {  
    TransactionSynchronizationManager.unbindResource(this.dataSource);  
        }  
        Connection con = txObject.getConnectionHolder().getConnection();  
        try {  
        //如果事务对象保存了自动事务提交属性，则设置数据库连接的自动事务提交属性  
            if (txObject.isMustRestoreAutoCommit()) {  
                con.setAutoCommit(true);  
            }  
            //事务结束后重置数据库连接  
            DataSourceUtils.resetConnectionAfterTransaction(con, txObject.getPreviousIsolationLevel());  
        }  
        catch (Throwable ex) {  
            logger.debug("Could not reset JDBC Connection after transaction", ex);  
        }  
        //如果事务对象中有新的ConnectionHolder   
        if (txObject.isNewConnectionHolder()) {  
            if (logger.isDebugEnabled()) {  
                logger.debug("Releasing JDBC Connection [" + con + "] after transaction");  
            }  
            //释放数据库连接  
            DataSourceUtils.releaseConnection(con, this.dataSource);  
        }  
        //清除事务对象的ConnectionHolder  
        txObject.getConnectionHolder().clear();  
    }  
//数据源事务对象，内部类  
    private static class DataSourceTransactionObject extends JdbcTransactionObjectSupport {  
        //是否有新的ConnectionHolder  
        private boolean newConnectionHolder;  
        //是否保存自动提交  
        private boolean mustRestoreAutoCommit;  
        //设置ConnectionHolder  
        public void setConnectionHolder(ConnectionHolder connectionHolder, boolean newConnectionHolder) {  
            //为父类JdbcTransactionObjectSupport设置ConnectionHolder  
            super.setConnectionHolder(connectionHolder);  
            this.newConnectionHolder = newConnectionHolder;  
        }  
        public boolean isNewConnectionHolder() {  
            return this.newConnectionHolder;  
        }  
        //调用父类JdbcTransactionObjectSupport的相关方法，查询收费存在事务  
        public boolean hasTransaction() {  
            return (getConnectionHolder() != null && getConnectionHolder().isTransactionActive());  
        }  
        //设置是否保存自动提交  
        public void setMustRestoreAutoCommit(boolean mustRestoreAutoCommit) {  
            this.mustRestoreAutoCommit = mustRestoreAutoCommit;  
        }  
        public boolean isMustRestoreAutoCommit() {  
            return this.mustRestoreAutoCommit;  
        }  
        //设置数据库连接在操作失败是，是否只回滚处理  
        public void setRollbackOnly() {  
            getConnectionHolder().setRollbackOnly();  
        }  
        public boolean isRollbackOnly() {  
            return getConnectionHolder().isRollbackOnly();  
        }  
    }  
}  
```



### hibernate事务

```xml
<bean id="transactionManager"
    class="org.springframework.orm.hibernate4.HibernateTransactionManager">
    <property name="sessionFactory" ref="sessionFactory" />
</bean>
```



### JPA 事务

java persitence API

```
<bean id="transactionManager"
    class="org.springframework.orm.jpa.JpaTransactionManager">
    <property name="entityManagerFactory" ref="entityManagerFactory" />
</bean>
```





## Spring事务

### 编程式事务



### 声明式事务

```java
事务只读  read_only

传播行为  propagation

隔离级别  isolation

回滚规则  rollback_for     no_rollback_for

事务超时   timeout
```





事务问题

* 脏读
* 不可重复度
* 幻读







# springmvc

@Controller @Service 

 DispatcherServlet原理与机制



1、Class<?> clazz = Class.forName(com.xx.service.impl.OrderServiceImpl);

![1543235257802](C:\Users\boyuan\AppData\Roaming\Typora\typora-user-images\1543235257802.png)











































