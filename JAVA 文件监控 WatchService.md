# 	JAVA 文件监控 WatchService的示例方法

## **概述**

java1.7中 提供了WatchService来监控系统中文件的变化。该监控是基于操作系统的文件系统监控器，可以监控系统是所有文件的变化，这种监控是无需遍历、无需比较的，是一种基于信号收发的监控，因此效率一定是最高的；现在Java对其进行了包装，可以直接在Java程序中使用OS的文件系统监控器了。

## **使用场景**

1. 场景一：比如系统中的配置文件，一般都是系统启动的时候只加载一次，如果想修改配置文件，还须重启系统。如果系统想热加载一般都会定时轮询对比配置文件是否修改过，如果修改过重新加载。

2. 场景二：监控磁盘中的文件变化，一般需要把磁盘中的所有文件全部加载一边，定期轮询一遍磁盘，跟上次的文件状态对比。如果文件、目录过多，每次遍历时间都很长，而且还不是实时监控。

   而以上两种场景就比较适合使用 WatchService 进行文件监控。

## 文件事件类型

* `StandardWatchEventKinds.ENTRY_CREATE`:创建
* `StandardWatchEventKinds.ENTRY_MODIFY`:修改
* `StandardWatchEventKinds.ENTRY_DELETE`:删除
* `StandardWatchEventKinds.OVERFLOW`:异常

> OVERFLOW是一种特殊类型的事件。我们不必注册OVERFLOW事件来接收它。当接收到这种类型的事件时，这意味着队列溢出，并且没有空间来添加当前创建的事件。 
>
> 示例:
>
> 假设我们有一个新的目录注册到监控服务的情况，并且在那个时候，大量的文件（例如10,000）被复制到该目录或在该目录内部创建。然后，监视服务将检测所有文件并排队处理。但是，如果文件的出队处理部分比将文件排入队列慢，则会抛出事件OVERFLOW。 

## 示例

```java
import com.sun.nio.file.SensitivityWatchEventModifier;
import java.io.File;
import java.io.IOException;
import java.nio.file.*;
import java.util.List;

/**
 * 1）对指定目录及其子目录下文件及文件夹监控有效，如果创建了更深的目录，则不再有效
 * 		监听:d:/test 只能监听到D:\test\aa 这一级下面的活动,D:\test\aa\bb里面的活动监听不到
 * 2）对指定的文件夹属性无法改动，比如：指定监听d:/test目录，如果修改或删除b目录名称是无法监听的
 * 3) 只能监控文件夹,不能监控文件
 */
@Slf4j
public class WatchServiceDemo {
	public static void main(String[] args) throws IOException {
		//获取文件监控的类WatchServcie
		WatchService watchService = FileSystems.getDefault().newWatchService();
		//设置监控指定的路径
		Path dir = Paths.get("d:/test");
		//参数1:WatchService,参数2:文件监控类型,参数3:文件监控灵敏度
		dir.register(watchService,
					new WatchEvent.Kind[]
						{StandardWatchEventKinds.ENTRY_MODIFY,
						StandardWatchEventKinds.ENTRY_CREATE,
						StandardWatchEventKinds.ENTRY_DELETE},
				SensitivityWatchEventModifier.HIGH);//可选参数
		new Thread(() -> {
			try {
				while (true) {
					//watchService.take():该方法是阻塞方法，如果没有文件修改，则一直阻塞。
					WatchKey watchKey = watchService.take();
					List<WatchEvent<?>> watchEvents = watchKey.pollEvents();
					for (WatchEvent<?> event : watchEvents) {
                     /**
					* TODO 根据事件类型采取不同的操作
					* ENTRY_CREATE :创建事件需要注意:上传文件并没有完全成功就会立即被监控到
					* 如果我们要在文件创建完成后做一些处理,那么可以通过比较5s前后的文件大小来判断
					*/
						System.out.printf("事件:%s,目录:%s\n",
								event.kind().name(),
								dir + File.separator + event.context());
					}
					//每次的到新的事件后，需要重置监听池
					watchKey.reset();
				}
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}).start();

		//添加jvm关闭时候的钩子,kill -15可以kill -9 不行
		Runtime.getRuntime().addShutdownHook(new Thread(() -> {
			try {
				//关闭wathcservice服务
				watchService.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}));
	}
}
```

```properties
//创建了文件夹abc
事件:ENTRY_CREATE,目录:d:\test\abc
//修改目录abc -> abcd
事件:ENTRY_DELETE,目录:d:\test\abc
事件:ENTRY_CREATE,目录:d:\test\abcd
//删除abcd
事件:ENTRY_DELETE,目录:d:\test\abcd
//修改文件text.txt内容
事件:ENTRY_MODIFY,目录:d:\test\test.txt
```

