# Spring源码环境搭建

参考：https://www.cnblogs.com/rxx1005/p/16032344.html

## spring版本与JDK对应关系

参考：https://github.com/spring-projects/spring-framework/wiki/Spring-Framework-Versions

- Spring Framework 6.0.x: JDK 17-21 (expected)
- Spring Framework 5.3.x: JDK 8-19 (expected)
- Spring Framework 5.2.x: JDK 8-15
- Spring Framework 5.1.x: JDK 8-12
- Spring Framework 5.0.x: JDK 8-10
- Spring Framework 4.3.x: JDK 6-8

## 下载代码

源码地址：https://github.com/spring-projects/spring-framework

我这里是将该代码fork到自己的github。然后通过github同步到gitee上。这样下载速度比较快

## 编译代码

1. 下载完代码后，切换分支到5.2.x

```shell
git clone xxx(源代码地址)
git checkout -b 5.2.x origin/5.2.x
```

2. 安装gradle

   **找到对应版本的gradle，然后下载放到本地。我的是放到了 D:\6_dev_tools\gradle\D:\6_dev_tools\gradle\gradle-5.6.4目录下**

   ![](.\imgs\gradle版本.jpg)

   ![](.\imgs\1651330696571.png)

   **修改系统的环境变量**

   

   新增环境变量: 

      GRADLE_HOME（设置解压后的文件目录)、

      GRADLE_USER_HOME(本地仓库地址，否则默认C盘)

   ![环境变量](.\imgs\环境变量.jpg)

   在Path中增加  ```%GRADLE_HOME%\bin```

   ![环境变量2](.\imgs\环境变量2.jpg)

   检查是否设置成功，执行 gradle -v

   ```shell
   
   $ gradle -v
   
   Welcome to Gradle 5.6.4!
   
   Here are the highlights of this release:
    - Incremental Groovy compilation
    - Groovy compile avoidance
    - Test fixtures for Java projects
    - Manage plugin versions via settings script
   
   For more details see https://docs.gradle.org/5.6.4/release-notes.html
   
   
   ------------------------------------------------------------
   Gradle 5.6.4
   ------------------------------------------------------------
   
   Build time:   2019-11-01 20:42:00 UTC
   Revision:     dd870424f9bd8e195d614dc14bb140f43c22da98
   
   Kotlin:       1.3.41
   Groovy:       2.5.4
   Ant:          Apache Ant(TM) version 1.9.14 compiled on March 12 2019
   JVM:          11.0.8 (Oracle Corporation 11.0.8+10-LTS)
   OS:           Windows 10 10.0 amd64
   
   ```

   修改下载源，以便快速下载jar包

   在目录D:\6_dev_tools\gradle\gradle-5.6.4\init.d下创建文件init.gradle

   ```properties
   allprojects {
       repositories {
           maven { url 'file:///D:/devsoft/maven_repo'}	//这是刚才新创建的本地仓库位置,最好把这段注释也删掉
           mavenLocal()
           maven { name "Alibaba" ; url "https://maven.aliyun.com/repository/public" ; }
           maven { name "Bstek" ; url "http://nexus.bsdn.org/content/groups/public/" ;  }
           mavenCentral()
       }
   
       buildscript { 
           repositories { 
               maven { name "Alibaba" ; url 'https://maven.aliyun.com/repository/public' ;  }
               maven { name "Bstek" ; url 'http://nexus.bsdn.org/content/groups/public/' ;  }
               maven { name "M2" ; url 'https://plugins.gradle.org/m2/' ;  }
           }
       }
   }
   ```

3. 配置idea的环境参数

   **使用idea打开源码，先取消idea的自动编译**

   ![Snipaste_2022-04-30_23-13-37](.\imgs\Snipaste_2022-04-30_23-13-37.jpg)

   **设置Gradle，使用刚才下载下来的Gradle**

   ![gradle设置](.\imgs\gradle设置.jpg)

   **设置java complier**

   ![javaCompiler](.\imgs\javaCompiler.jpg)

   **设置Project Structure**

   ![project](.\imgs\project.jpg)

   **设置Kotlin**

   ![1651332110081](.\imgs\1651332110081.png)

4. 编译代码

   点击编译代码了。这个时间会有点长。中间有2个步骤。一个是下载依赖。一个是idea添加项目的索引。

   这个步骤看网速和机器。不同情况不同。

5. 创建自己的demo工程

   右键spring-framework ==> 点击new ==> 点击Module ==> 选择gradle  按照步骤完成即可

   ![Snipaste_2022-04-30_23-26-57](.\imgs\Snipaste_2022-04-30_23-26-57.jpg)

   引入spring-context，在新建的项目中的build.gradle文件中引入spring-context

   ```properties
   dependencies {
       testImplementation 'org.junit.jupiter:junit-jupiter-api:5.6.0'
       testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine'
       # 增加以下一行
       compile(project(":spring-context")) 
   }
   ```

   ![Snipaste_2022-04-30_23-28-17](.\imgs\Snipaste_2022-04-30_23-28-17.jpg)

   在resources目录下增加spring.xml文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
   	   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   	   xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
   	<bean class="TestService" id="testService"/>
   	<!-- more bean definitions go here -->
   
   </beans>
   ```

   新建测试入口类

   ```java
   public class SpringDemo {
   	public static void main(String[] args) {
   		ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("classpath:spring.xml");
   
   	}
   }
   
   ```

   执行测试类，如果编译通过，且无错误，那么说明环境搭建完成

   

## 遇到的问题

+ 程序包org.springframework.cglib.core.internal不存在

  找到 spring-core对应的gradle，然后clean ==> build

+ CoroutinesUtils找不到

   参考：https://blog.csdn.net/gooaaee/article/details/104437902

  