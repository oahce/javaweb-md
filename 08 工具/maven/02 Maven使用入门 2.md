# 1 认识maven结构
src/main/java  存放项目的java类源文件，即：Xxx.java
src/main/resources  存放项目的资源文件，如spring、mybatis的配置文件等等
src/test/java  存放项目的用于测试的java类源文件，即：XxxTest.java
src/test/resources  存放项目的测试相关的资源文件
target 项目输出文件夹，编译后的class文件等
pom.xml 

# 2 编辑pom文件
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.oahc.eux</groupId>
  <artifactId>HelloMaven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <name>HelloMaven</name>
</project>
```
1. 第一行 是xml头，规定了该xml文档的版本和编码格式。
2. project是pom文件的根元素，它还声明了一些POM相关的命名空间和xsd元素
   这些属性不是必须的，但使用这些属性能让第三方工具提供快速编辑pom的功能。
3. modelVersion指定了pom模型的版本，对于maven2和maven3来说这个值只能是4.0.0
4. groupId、artifactId、version三个元素定义了一个项目的基本坐标，在maven中任何项目(jar、pom、war)都是通过坐标来进行区分的。
5. name是声明了一个对于用户友好的项目名称，虽然不是必须的，但还是推荐进行定义方便信息交流。

> java代码和pom代码是互相独立的，比如项目升级时只需要修改pom。
> 当pom稳定之后，日常的java代码开发也不涉及pom的修改。

# 3 编写主代码
在src/main/java下编写源代码：
```java
package com.oahc.eux;

public class HelloMaven {
	public String sayHello() {
		return "HelloMaven!";
	}
	
	public static void main(String[] args) {
		System.out.println(new HelloMaven().sayHello());
	}
}
```


当我们通过maven创建的项目时，默认的jdk版本是1.5，需要指定项目jdk版本：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.oahc.eux</groupId>
  <artifactId>HelloMaven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <name>HelloMaven</name>

  
  <properties>
	<java.version>17</java.version>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <build>
    <plugins>
        <plugin><!-- 指定maven-compiler-plugin版本和JDK 版本 -->
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <!-- <skip>true</skip> -->
                <source>${java.version}</source>
                <target>${java.version}</target>
                <compilerVersion>${java.version}</compilerVersion>
                <encoding>${project.build.sourceEncoding}</encoding>
            </configuration>
        </plugin>
        
        <plugin><!-- 指定maven-surefire-plugin版本  -->
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M4</version>
            <!-- 
            <configuration>
                <skip>true</skip>
                <skipTests>true</skipTests>
            </configuration>
            -->
        </plugin>
        
    </plugins>
  </build>

</project>

```

执行 mvn clear compile命令：
```
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< com.oahc.eux:HelloMaven >-----------------------
[INFO] Building HelloMaven 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ HelloMaven ---
[INFO] Deleting D:\javaDev\Eclipse\space\HelloMaven\target
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\main\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\classes
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.101 s
[INFO] Finished at: 2022-04-09T12:29:47+08:00
[INFO] ------------------------------------------------------------------------
```
从打印的执行结果我们可以看到maven为我们执行了三个命令，分别是 clean、resource、compile。
clean：清理输出目录target
resource：这里未定义项目资源，暂且略过
compile：编译maven项目主代码
clean:clean、resource:resource、compile:compile 对应了各自的插件及插件目标，后面详解，暂且略过

# 4 测试代码
为了项目结构保持清晰，主代码和测试代码是分别位于独立的目录中的
src/main/java是主代码目录
src/main/test是测试代码的目录
我们需要引入新的jar，并在测试代码目录中新建测试类：
--POM--
```xml
<dependencies>
  	<dependency>
  		<groupId>junit</groupId>
  		<artifactId>junit</artifactId>
  		<version>4.7</version>
  		<scope>test</scope>
  	</dependency>
  </dependencies>
```
scope属性是指定依赖范围，值test则指明了这个范围是只对测试有效
如果不指定scope属性的值，默认是compile，也就是对编译范围有效
新增测试类：
```java
package com.oahc.eux;
import static org.junit.Assert.assertEquals;
import org.junit.Test;
public class HelloMavenTest {
	
	@Test
	public void testSayHello() {
		HelloMaven helloMaven = new HelloMaven();
		String result = helloMaven.sayHello();
		assertEquals("HelloMaven", result);
	}
}
```
执行命令：mvn clean test
```
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< com.oahc.eux:HelloMaven >-----------------------
[INFO] Building HelloMaven 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ HelloMaven ---
[INFO] Deleting D:\javaDev\Eclipse\space\HelloMaven\target
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\main\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\classes
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\test\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\test-classes
[INFO]
[INFO] --- maven-surefire-plugin:3.0.0-M4:test (default-test) @ HelloMaven ---
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/surefire-junit4/3.0.0-M4/surefire-junit4-3.0.0-M4.jar
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/surefire-junit4/3.0.0-M4/surefire-junit4-3.0.0-M4.jar (17 kB at 26 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/surefire-junit4/3.0.0-M4/surefire-junit4-3.0.0-M4.pom
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/surefire-junit4/3.0.0-M4/surefire-junit4-3.0.0-M4.pom (2.9 kB at 17 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/surefire-providers/3.0.0-M4/surefire-providers-3.0.0-M4.pom
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/surefire-providers/3.0.0-M4/surefire-providers-3.0.0-M4.pom (2.5 kB at 9.3 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/junit/junit/4.0/junit-4.0.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/junit/junit/4.0/junit-4.0.pom (210 B at 1.4 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/common-junit4/3.0.0-M4/common-junit4-3.0.0-M4.pom
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/common-junit4/3.0.0-M4/common-junit4-3.0.0-M4.pom (2.9 kB at 11 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/common-junit3/3.0.0-M4/common-junit3-3.0.0-M4.pom
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/common-junit3/3.0.0-M4/common-junit3-3.0.0-M4.pom (2.6 kB at 17 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/common-java5/3.0.0-M4/common-java5-3.0.0-M4.pom
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/common-java5/3.0.0-M4/common-java5-3.0.0-M4.pom (3.8 kB at 13 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/hamcrest/hamcrest-library/1.3/hamcrest-library-1.3.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/hamcrest/hamcrest-library/1.3/hamcrest-library-1.3.pom (820 B at 5.8 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/easytesting/fest-assert/1.4/fest-assert-1.4.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/easytesting/fest-assert/1.4/fest-assert-1.4.pom (2.4 kB at 8.4 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/easytesting/fest/1.0.8/fest-1.0.8.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/easytesting/fest/1.0.8/fest-1.0.8.pom (12 kB at 43 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/easytesting/fest-util/1.1.6/fest-util-1.1.6.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/easytesting/fest-util/1.1.6/fest-util-1.1.6.pom (1.6 kB at 5.8 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/common-junit4/3.0.0-M4/common-junit4-3.0.0-M4.jar
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/common-junit3/3.0.0-M4/common-junit3-3.0.0-M4.jar
Downloading from aliyunmaven: https://maven.aliyun.XXXrefire/common-java5/3.0.0-M4/common-java5-3.0.0-M4.jar
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/common-junit4/3.0.0-M4/common-junit4-3.0.0-M4.jar (27 kB at 166 kB/s)
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/common-junit3/3.0.0-M4/common-junit3-3.0.0-M4.jar (12 kB at 36 kB/s)
Downloaded from aliyunmaven: https://maven.aliyun.XXXrefire/common-java5/3.0.0-M4/common-java5-3.0.0-M4.jar (33 kB at 61 kB/s)
[INFO]
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.oahc.eux.HelloMavenTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.034 s - in com.oahc.eux.HelloMavenTest
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  6.603 s
[INFO] Finished at: 2022-04-10T11:50:41+08:00
[INFO] ------------------------------------------------------------------------
```

虽然命令时执行clean和test，但通过打印看到执行不止2个任务
还有maven-clean-plugin:2.5:clean、maven-resources-plugin:2.6:resources、maven-compiler-plugin:3.8.1:compile、
maven-resources-plugin:2.6:testResources、 maven-compiler-plugin:3.8.1:testCompile、maven-surefire-plugin:3.0.0-M4:test
也就是在执行test之前，它会执行 主代码资源处理、主代码编译、测试资源处理、测试代码编译的过程。
这是maven的声明周期，后面的章节会讲到。
注意： maven-compiler-plugin版本是3.8.1，使用的jdk版本是17,
maven-surefire-plugin版本是3.0.0-M4，这些配置是我们在创建项目时在pom文件上就指定的，否则会按照默认版本处理。

maven-surefire-plugin:
Maven本身并不是一个单元测试框架，Java世界中主流的单元测试框架为JUnit和TestNG。
Maven所做的只是在构建执行到特定生命周期阶段的时候，通过插件来执行JUnit或者TestNG的测试用例。
这一插件就是maven-surefire-plugin，可以称之为测试运行器（Test Runner），他能很好的兼容JUnit 3、JUnit 4以及TestNG。
生命周期阶段需要绑定到某个插件的目标才能完成真正的工作，test阶段正是与maven-surefire-plugin的test目标相绑定了，这是一个内置的绑定。
在默认情况下，maven-surefire-plugin的test目标会自动执行测试源码路径（默认为src/test/java/）下所有符合一组命名模式的测试类。这组模式为：
1. XXX/Testxxx.java：任何子目录所有命名以Test开头的Java类。
2. XXX/xxxTest.java：任何子目录下所有命名以Test结尾的Java类。
3. XXX/xxxTestCase.java：任何子目录下所有命名以TestCase结尾的Java类。

测试类的编译文件在 target/test-classes 目录下。
# 5 打包和运行
## 打包
将项目编译和测试之后，下一个重要步骤就是打包。
如果pom文件没有指定打包类型，则默认打包为jar。
执行：mvn clean package
```xml
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< com.oahc.eux:HelloMaven >-----------------------
[INFO] Building HelloMaven 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ HelloMaven ---
[INFO] Deleting D:\javaDev\Eclipse\space\HelloMaven\target
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\main\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\classes
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\test\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\test-classes
[INFO]
[INFO] --- maven-surefire-plugin:3.0.0-M4:test (default-test) @ HelloMaven ---
[INFO]
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.oahc.eux.HelloMavenTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.033 s - in com.oahc.eux.HelloMavenTest
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO]
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ HelloMaven ---
[INFO] Building jar: D:\javaDev\Eclipse\space\HelloMaven\target\HelloMaven-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.801 s
[INFO] Finished at: 2022-04-10T16:21:31+08:00
[INFO] ------------------------------------------------------------------------
```

和上面一样，除了clean和package之外，依然需要遵循生命周期的各个步骤，编译、测试等还是需要执行。
maven-jar-plugin:2.4:jar 将包文件存至：`Building jar: D:\javaDev\Eclipse\space\HelloMaven\target\HelloMaven-1.0-SNAPSHOT.jar` 
HelloMaven-1.0-SNAPSHOT.jar这个名字是通过artifact-version-SNAPSHOP.jar 的规则命名的，想要自定义可以通过finalName来重命名，后面的章节会讲到。
## 运行
此时这个jar被打包完成，如何让其他项目可以引用这个jar那？
执行：mvn clean install
```
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< com.oahc.eux:HelloMaven >-----------------------
[INFO] Building HelloMaven 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ HelloMaven ---
[INFO] Deleting D:\javaDev\Eclipse\space\HelloMaven\target
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\main\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\classes
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\test\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\test-classes
[INFO]
[INFO] --- maven-surefire-plugin:3.0.0-M4:test (default-test) @ HelloMaven ---
[INFO]
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.oahc.eux.HelloMavenTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.033 s - in com.oahc.eux.HelloMavenTest
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO]
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ HelloMaven ---
[INFO] Building jar: D:\javaDev\Eclipse\space\HelloMaven\target\HelloMaven-1.0-SNAPSHOT.jar
[INFO]
[INFO] --- maven-install-plugin:2.4:install (default-install) @ HelloMaven ---
[INFO] Installing D:\javaDev\Eclipse\space\HelloMaven\target\HelloMaven-1.0-SNAPSHOT.jar to D:\javaDev\apache-maven-3.8.3\local\com\oahc\eux\HelloMaven\1.0-SNAPSHOT\HelloMaven-1.0-SNAPSHOT.jar
[INFO] Installing D:\javaDev\Eclipse\space\HelloMaven\pom.xml to D:\javaDev\apache-maven-3.8.3\local\com\oahc\eux\HelloMaven\1.0-SNAPSHOT\HelloMaven-1.0-SNAPSHOT.pom
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.936 s
[INFO] Finished at: 2022-04-10T16:29:10+08:00
[INFO] ------------------------------------------------------------------------
```
将项目包文件安装至maven本地仓库：
通过 maven-install-plugin:2.4:install 
`Installing HelloMaven-1.0-SNAPSHOT.jar to D:\javaDev\apache-maven-3.8.3\local\com\oahc\eux\HelloMaven\1.0-SNAPSHOT\HelloMaven-1.0-SNAPSHOT.jar`
`Installing HelloMaven\pom.xml to D:\javaDev\apache-maven-3.8.3\local\com\oahc\eux\HelloMaven\1.0-SNAPSHOT\HelloMaven-1.0-SNAPSHOT.pom`
此时我们可以在其他项目中引入HelloMaven项目了。

这里有个小问题，当我们执行 java -jar HelloMaven-1.0-SNAPSHOT.jar 时会提示：
HelloMaven-1.0-SNAPSHOT.jar中没有主清单属性
我们的主代码的类中虽然定义了main方法，但是在生成的jar文件中的 manifest(META-INF/MANIFEST.MF) 中并没有Main-Class属性。

我们可以通过maven-shade-plugin插件进行解决
maven-shade-plugin提供了两大基本功能：
1.  将依赖的jar包打包到当前jar包（常规打包是不会将所依赖jar包打进来的）；
2.  对依赖的jar包进行重命名（用于类的隔离）；

新增pom设置：
参见[此处]https://maven.apache.org/plugins/maven-shade-plugin/examples/executable-jar.html
```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-shade-plugin</artifactId>
	<version>3.3.0</version>
	<executions>
	  <execution>
		<phase>package</phase>
		<goals>
		  <goal>shade</goal>
		</goals>
		<configuration>
		  <transformers>
			<transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
			  <mainClass>com.oahc.eux.HelloMaven</mainClass>
			</transformer>
		  </transformers>
		</configuration>
	  </execution>
	</executions>
 </plugin>
```

重新执行 mvn clean install
```
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< com.oahc.eux:HelloMaven >-----------------------
[INFO] Building HelloMaven 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ HelloMaven ---
[INFO] Deleting D:\javaDev\Eclipse\space\HelloMaven\target
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\main\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\classes
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ HelloMaven ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory D:\javaDev\Eclipse\space\HelloMaven\src\test\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ HelloMaven ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to D:\javaDev\Eclipse\space\HelloMaven\target\test-classes
[INFO]
[INFO] --- maven-surefire-plugin:3.0.0-M4:test (default-test) @ HelloMaven ---
[INFO]
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.oahc.eux.HelloMavenTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.033 s - in com.oahc.eux.HelloMavenTest
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO]
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ HelloMaven ---
[INFO] Building jar: D:\javaDev\Eclipse\space\HelloMaven\target\HelloMaven-1.0-SNAPSHOT.jar
[INFO]
[INFO] --- maven-shade-plugin:3.3.0:shade (default) @ HelloMaven ---
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/slf4j/slf4j-api/1.7.32/slf4j-api-1.7.32.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/slf4j/slf4j-api/1.7.32/slf4j-api-1.7.32.pom (3.8 kB at 5.7 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/slf4j/slf4j-parent/1.7.32/slf4j-parent-1.7.32.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/slf4j/slf4j-parent/1.7.32/slf4j-parent-1.7.32.pom (14 kB at 49 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm/9.2/asm-9.2.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm/9.2/asm-9.2.pom (2.4 kB at 16 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-commons/9.2/asm-commons-9.2.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-commons/9.2/asm-commons-9.2.pom (3.0 kB at 11 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-tree/9.2/asm-tree-9.2.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-tree/9.2/asm-tree-9.2.pom (2.6 kB at 16 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-analysis/9.2/asm-analysis-9.2.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-analysis/9.2/asm-analysis-9.2.pom (2.6 kB at 15 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/jdom/jdom2/2.0.6.1/jdom2-2.0.6.1.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/jdom/jdom2/2.0.6.1/jdom2-2.0.6.1.pom (4.6 kB at 17 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/apache/maven/shared/maven-dependency-tree/3.0.1/maven-dependency-tree-3.0.1.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/apache/maven/shared/maven-dependency-tree/3.0.1/maven-dependency-tree-3.0.1.pom (7.5 kB at 46 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/vafer/jdependency/2.7.0/jdependency-2.7.0.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/vafer/jdependency/2.7.0/jdependency-2.7.0.pom (14 kB at 77 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/apache/commons/commons-collections4/4.2/commons-collections4-4.2.pom
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/apache/commons/commons-collections4/4.2/commons-collections4-4.2.pom (23 kB at 152 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/slf4j/slf4j-api/1.7.32/slf4j-api-1.7.32.jar
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-commons/9.2/asm-commons-9.2.jar
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm/9.2/asm-9.2.jar
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-analysis/9.2/asm-analysis-9.2.jar
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-tree/9.2/asm-tree-9.2.jar
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-tree/9.2/asm-tree-9.2.jar (53 kB at 145 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/jdom/jdom2/2.0.6.1/jdom2-2.0.6.1.jar
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm/9.2/asm-9.2.jar (122 kB at 301 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/apache/maven/shared/maven-dependency-tree/3.0.1/maven-dependency-tree-3.0.1.jar
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-analysis/9.2/asm-analysis-9.2.jar (34 kB at 62 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/vafer/jdependency/2.7.0/jdependency-2.7.0.jar
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/ow2/asm/asm-commons/9.2/asm-commons-9.2.jar (73 kB at 126 kB/s)
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/slf4j/slf4j-api/1.7.32/slf4j-api-1.7.32.jar (42 kB at 72 kB/s)
Downloading from aliyunmaven: https://maven.aliyun.com/repository/public/org/apache/commons/commons-collections4/4.2/commons-collections4-4.2.jar
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/jdom/jdom2/2.0.6.1/jdom2-2.0.6.1.jar (328 kB at 484 kB/s)
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/apache/maven/shared/maven-dependency-tree/3.0.1/maven-dependency-tree-3.0.1.jar (37 kB at 52 kB/s)
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/vafer/jdependency/2.7.0/jdependency-2.7.0.jar (233 kB at 295 kB/s)
Downloaded from aliyunmaven: https://maven.aliyun.com/repository/public/org/apache/commons/commons-collections4/4.2/commons-collections4-4.2.jar (753 kB at 838 kB/s)
[INFO] Replacing original artifact with shaded artifact.
[INFO] Replacing D:\javaDev\Eclipse\space\HelloMaven\target\HelloMaven-1.0-SNAPSHOT.jar with D:\javaDev\Eclipse\space\HelloMaven\target\HelloMaven-1.0-SNAPSHOT-shaded.jar
[INFO]
[INFO] --- maven-install-plugin:2.4:install (default-install) @ HelloMaven ---
[INFO] Installing D:\javaDev\Eclipse\space\HelloMaven\target\HelloMaven-1.0-SNAPSHOT.jar to D:\javaDev\apache-maven-3.8.3\local\com\oahc\eux\HelloMaven\1.0-SNAPSHOT\HelloMaven-1.0-SNAPSHOT.jar
[INFO] Installing D:\javaDev\Eclipse\space\HelloMaven\pom.xml to D:\javaDev\apache-maven-3.8.3\local\com\oahc\eux\HelloMaven\1.0-SNAPSHOT\HelloMaven-1.0-SNAPSHOT.pom
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  7.107 s
[INFO] Finished at: 2022-04-10T18:18:07+08:00
[INFO] ------------------------------------------------------------------------
```
此时target生成了2个jar文件：HelloMaven-1.0-SNAPSHOT.jar和original-HelloMaven-1.0-SNAPSHOT.jar
前者是带有Main-Class信息的可执行jar，后者是原始的jar
执行  target> java -jar HelloMaven-1.0-SNAPSHOT.jar
HelloMaven

# 6 使用archetype生成项目结构(骨架)
当执行 mvn archetype:generate 时，maven3不会像maven2那样直接下载最新版本，而是解析最新的稳定版本。
我们已经很熟悉了，这个命令实际上执行的还是maven的插件：
groupId：org.apache.maven.plugins 
aritifactId：maven-archetype-plugin
version：

```
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------< org.apache.maven:standalone-pom >-------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] --------------------------------[ pom ]---------------------------------
[INFO]
[INFO] >>> maven-archetype-plugin:3.2.1:generate (default-cli) > generate-sources @ standalone-pom >>>
[INFO]
[INFO] <<< maven-archetype-plugin:3.2.1:generate (default-cli) < generate-sources @ standalone-pom <<<
[INFO]
[INFO]
[INFO] --- maven-archetype-plugin:3.2.1:generate (default-cli) @ standalone-pom ---
[INFO] Generating project in Interactive mode
[WARNING] No archetype found in remote catalog. Defaulting to internal catalog
[INFO] No archetype defined. Using maven-archetype-quickstart (org.apache.maven.archetypes:maven-archetype-quickstart:1.0)
Choose archetype:
1: internal -> org.apache.maven.archetypes:maven-archetype-archetype (An archetype which contains a sample archetype.)
2: internal -> org.apache.maven.archetypes:maven-archetype-j2ee-simple (An archetype which contains a simplifed sample J2EE application.)
3: internal -> org.apache.maven.archetypes:maven-archetype-plugin (An archetype which contains a sample Maven plugin.)
4: internal -> org.apache.maven.archetypes:maven-archetype-plugin-site (An archetype which contains a sample Maven plugin site.
      This archetype can be layered upon an existing Maven plugin project.)
5: internal -> org.apache.maven.archetypes:maven-archetype-portlet (An archetype which contains a sample JSR-268 Portlet.)
6: internal -> org.apache.maven.archetypes:maven-archetype-profiles ()
7: internal -> org.apache.maven.archetypes:maven-archetype-quickstart (An archetype which contains a sample Maven project.)
8: internal -> org.apache.maven.archetypes:maven-archetype-site (An archetype which contains a sample Maven site which demonstrates
      some of the supported document types like APT, XDoc, and FML and demonstrates how
      to i18n your site. This archetype can be layered upon an existing Maven project.)
9: internal -> org.apache.maven.archetypes:maven-archetype-site-simple (An archetype which contains a sample Maven site.)
10: internal -> org.apache.maven.archetypes:maven-archetype-webapp (An archetype which contains a sample Maven Webapp project.)
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 7: //选择模板 建议选择7


```