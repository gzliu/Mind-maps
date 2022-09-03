## 1.源码分析的流程图

[GitHub - gzliu/Mind-maps](https://github.com/gzliu/Mind-maps)

## 2.接口架构图

###  ClasspathXmlApplicationContext接口关系

![](https://tcs.teambition.net/storage/312h688124c2e5d209d82fea585b5c7f7659?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmg2ODgxMjRjMmU1ZDIwOWQ4MmZlYTU4NWI1YzdmNzY1OSJ9.eEB2--Du-HcRpaR9CAs2zymZIElCXBggAhu8sE2Pc7A&download=ClassPathXmlApplicationContext2.png "")

![](https://tcs.teambition.net/storage/312h1739913730b879d9c240b6a54f5d2881?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmgxNzM5OTEzNzMwYjg3OWQ5YzI0MGI2YTU0ZjVkMjg4MSJ9.gRuR5tK-jofqymSJnjcmRKa2Aq7Vycu6Zy6yXDn4yHo&download=ClassPathXmlApplicationContext.png "")

### GenericBeanDefinition接口关系（注入容器的普通springBean）

![](https://tcs.teambition.net/storage/312ha49da9abd37cb59f108e1926e68b62ad?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmhhNDlkYTlhYmQzN2NiNTlmMTA4ZTE5MjZlNjhiNjJhZCJ9.F04GuezgIUQmtuyTaSu1MKj5mxl1F1iei1cguWOx76s&download=diagram.png "")

### RootBeanDefintion接口关系

![](https://tcs.teambition.net/storage/312h5514c6ce9f6f8f7a0949b77a9de6384a?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmg1NTE0YzZjZTlmNmY4ZjdhMDk0OWI3N2E5ZGU2Mzg0YSJ9.bQkApWwk8F9inbgNlFPD7A99-bw0NkGfrUzCkpZin4s&download=rootbeandefinition.png "")

### GenericApplicationContext关系图

![](https://tcs.teambition.net/storage/312h1264ea76d01f9c8d4a32795ace98f614?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmgxMjY0ZWE3NmQwMWY5YzhkNGEzMjc5NWFjZTk4ZjYxNCJ9.eoOnyuGmZV65_uNdcw1oN8HSp7GEJIiturXu876Zzso&download=GenericApplicationContext.png "")

### BeanFactoryPostProcessor接口关系图

容器的扩展接口。通过refresh()的模板设计模式进行初始化容器

![](https://tcs.teambition.net/storage/312h8477fff55ab47ee8f42e89d474b318b3?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmg4NDc3ZmZmNTVhYjQ3ZWU4ZjQyZTg5ZDQ3NGIzMThiMyJ9.mYzACoD5NNQlu6gtoUZN8yGi_hcwVml4Gmtr_tXb2Fc&download=BeanDefinitionRegistryPostProcessor.png "")



### SimpleApplicationEventMulticaster

![](https://tcs.teambition.net/storage/312hc0030e96b64d9cdcd16a3ff5a71964ed?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmhjMDAzMGU5NmI2NGQ5Y2RjZDE2YTNmZjVhNzE5NjRlZCJ9.WpM62gy_16P28VbBaALC9Zx5iqC5OAfeKsxoupj3RpU&download=SimpleApplicationEventMulticaster.png "")

### BeanWrapperImpl

初始化对象的时候，会创建此对象。以及处理PropertyEditorRegistrar的逻辑

初始化代码的位置在：AbstractAutowireCapableBeanFactory.createBeanInstance()

![](https://tcs.teambition.net/storage/312h79d6ad651e5f0444c5c9a22af8167b7e?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmg3OWQ2YWQ2NTFlNWYwNDQ0YzVjOWEyMmFmODE2N2I3ZSJ9.I-kkOUUJVOpNT01PTzVLaLy-UUk3k9QW6aS_m8TQNhQ&download=BeanWrapperImpl.png "")

### InstantiationAwareBeanPostProcessorAdapter

将SmartInstantiationAwareBeanPostProcessor上的所有方法实现为无操作的适配器，这不会改变容器实例化的每个 bean 的正常处理。子类可能只覆盖他们真正感兴趣的那些方法。

请注意，仅当您确实需要InstantiationAwareBeanPostProcessor功能时才推荐使用此基类。如果您只需要简单的BeanPostProcessor功能，则更喜欢该（更简单）接口的直接实现。

```java
// 调用postProcessBeforeInstantiation方法
// 入口AbstractAutowireCapableBeanFactory.createBean  
if (!mbd.isSynthetic() && hasInstantiationAwareBeanPostProcessors()) {
	Class<?> targetType = determineTargetType(beanName, mbd);
	if (targetType != null) {
		bean = applyBeanPostProcessorsBeforeInstantiation(targetType, beanName);
		if (bean != null) {
			bean = applyBeanPostProcessorsAfterInitialization(bean, beanName);
		}
	}
}

// applyBeanPostProcessorsBeforeInstantiation
 for (BeanPostProcessor bp : getBeanPostProcessors()) {
	if (bp instanceof InstantiationAwareBeanPostProcessor) {
		InstantiationAwareBeanPostProcessor ibp = (InstantiationAwareBeanPostProcessor) bp;
		Object result = ibp.postProcessBeforeInstantiation(beanClass, beanName);
		if (result != null) {
			return result;
		}
	}
}

// applyBeanPostProcessorsAfterInitialization
for (BeanPostProcessor processor : getBeanPostProcessors()) {
	Object current = processor.postProcessAfterInitialization(result, beanName);
	if (current == null) {
		return result;
	}
	result = current;
}

// 调用postProcessAfterInstantiation方法
// 入口AbstractAutowireCapableBeanFactory.populateBean
if (!mbd.isSynthetic() && hasInstantiationAwareBeanPostProcessors()) {
	for (BeanPostProcessor bp : getBeanPostProcessors()) {
		if (bp instanceof InstantiationAwareBeanPostProcessor) {
			InstantiationAwareBeanPostProcessor ibp = (InstantiationAwareBeanPostProcessor) bp;
			if (!ibp.postProcessAfterInstantiation(bw.getWrappedInstance(), beanName)) {
				return;
			}
		}
	}
}
// ....
for (BeanPostProcessor bp : getBeanPostProcessors()) {
	if (bp instanceof InstantiationAwareBeanPostProcessor) {
		InstantiationAwareBeanPostProcessor ibp = (InstantiationAwareBeanPostProcessor) bp;
		PropertyValues pvsToUse = ibp.postProcessProperties(pvs, bw.getWrappedInstance(), beanName);
		if (pvsToUse == null) {
			if (filteredPds == null) {
				filteredPds = filterPropertyDescriptorsForDependencyCheck(bw, mbd.allowCaching);
			}
			pvsToUse = ibp.postProcessPropertyValues(pvs, filteredPds, bw.getWrappedInstance(), beanName);
			if (pvsToUse == null) {
				return;
			}
		}
		pvs = pvsToUse;
	}
}
```

![](https://tcs.teambition.net/storage/312hbf50120b94554648e9b67915c7c4927b?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmhiZjUwMTIwYjk0NTU0NjQ4ZTliNjc5MTVjN2M0OTI3YiJ9.lI-ROmmGyrCnPz_Kah7grNi_wARhQ9fU2fiUSP_EAlc&download=InstantiationAwareBeanPostProcessorAdapter.png "")



### 总体接口设计图

![](https://tcs.teambition.net/storage/312h4b0f031fe89a04cd168b7ac4e1a15e2f?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmg0YjBmMDMxZmU4OWEwNGNkMTY4YjdhYzRlMWExNWUyZiJ9.saKf5yqVu0fxrbJwxV-s_zKv-QNYwkQ4tSvxkyuzmfE&download=BeanFactory.png "")



## 3.特殊类及接口说明

###  **BeanFactory**

spring的顶层接口，用于扩展spring

```java
用于访问 Spring bean 容器的根接口。
这是 bean 容器的基本客户端视图；
其他接口，如ListableBeanFactory和org.springframework.beans.factory.config.ConfigurableBeanFactory可用于特定目的。
该接口由包含许多 bean 定义的对象实现，每个定义由一个字符串名称唯一标识。
根据 bean 定义，工厂将返回包含对象的独立实例（原型设计模式）或单个共享实例（单例设计模式的更好替代方案，其中实例是范围内的单例）工厂）。
将返回哪种类型的实例取决于 bean 工厂配置：API 相同。
从 Spring 2.0 开始，根据具体的应用程序上下文（例如，Web 环境中的“请求”和“会话”范围），可以使用更多范围。
这种方法的要点是 BeanFactory 是应用程序组件的中央注册表，并集中了应用程序组件的配置（例如，单个对象不再需要读取属性文件）。
有关这种方法的好处的讨论，请参阅“专家一对一 J2EE 设计和开发”的第 4 章和第 11 章。
请注意，通常最好依靠依赖注入（“推”配置）通过设置器或构造器来配置应用程序对象，而不是使用任何形式的“拉”配置，
如 BeanFactory 查找。 Spring 的依赖注入功能是使用这个 BeanFactory 接口及其子接口实现的。
通常，BeanFactory 会加载存储在配置源（例如 XML 文档）中的 bean 定义，并使用org.springframework.beans包来配置 bean。
但是，实现可以简单地返回它根据需要直接在 Java 代码中创建的 Java 对象。对如何存储定义没有限制：LDAP、RDBMS、XML、属性文件等。
鼓励实现支持 bean 之间的引用（依赖注入）。
与ListableBeanFactory中的方法相比，此接口中的所有操作也会检查父工厂是否为HierarchicalBeanFactory 。
如果在该工厂实例中找不到 bean，则会询问直接父工厂。这个工厂实例中的 bean 应该覆盖任何父工厂中的同名 bean。
Bean 工厂实现应尽可能支持标准的 bean 生命周期接口。全套初始化方法及其标准顺序为：
	1.BeanNameAware 的setBeanName
	2.BeanClassLoaderAware 的setBeanClassLoader
	3.BeanFactoryAware 的setBeanFactory
	4.EnvironmentAware 的setEnvironment
	5.EmbeddedValueResolverAware 的setEmbeddedValueResolver
	6.ResourceLoaderAware 的setResourceLoader （仅在应用程序上下文中运行时适用）
	7.ApplicationEventPublisherAware 的setApplicationEventPublisher （仅在应用程序上下文中运行时适用）
	8.MessageSourceAware 的setMessageSource （仅在应用程序上下文中运行时适用）
	9.ApplicationContextAware 的setApplicationContext （仅在应用程序上下文中运行时适用）
	10.ServletContextAware 的setServletContext （仅适用于在 Web 应用程序上下文中运行时）
	11.BeanPostProcessors 的postProcessBeforeInitialization方法
	12.InitializingBean 的afterPropertiesSet
	13.自定义初始化方法定义
	14.BeanPostProcessors 的postProcessAfterInitialization方法
在关闭 bean 工厂时，将应用以下生命周期方法：
	1.DestructionAwareBeanPostProcessors 的postProcessBeforeDestruction方法
	2.DisposableBean 的destroy
	3.自定义销毁方法定义
自从：2001 年 4 月 13 日
也可以看看：
ApplicationContextAwareProcessor.postProcessBeforeInitialization,
BeanNameAware.setBeanName , 
BeanClassLoaderAware.setBeanClassLoader , 
BeanFactoryAware.setBeanFactory , 
org.springframework.context.ResourceLoaderAware.setResourceLoader , 
org.springframework.context.ApplicationEventPublisherAware.setApplicationEventPublisher , 
org.springframework.context.MessageSourceAware.setMessageSource , 
org.springframework.context.ApplicationContextAware.setApplicationContext ， 
org.springframework.web.context.ServletContextAware.setServletContext ， 
org.springframework.beans.factory.config.BeanPostProcessor.postProcessBeforeInitialization ， 
InitializingBean.afterPropertiesSet ， 
org.springframework.beans.factory.support.RootBeanDefinition.getInitMethodName ， 
org.springframework.beans.factory.config.BeanPostProcessor.postProcessAfterInitialization ， 
DisposableBean.destroy ， 
org.springframework.beans.factory.support.RootBeanDefinition.getDestroyMethodName
```

### Aware

```java
一个标记超接口，指示 bean 有资格通过回调样式方法由特定框架对象的 Spring 容器通知。
实际的方法签名由各个子接口确定，但通常应仅包含一个接受单个参数的返回 void 的方法。
请注意，仅实现Aware不会提供默认功能。
相反，必须明确地进行处理，
例如在org.springframework.beans.factory.config.BeanPostProcessor中。
有关处理特定*Aware接口回调的示例，
请参阅org.springframework.context.support.ApplicationContextAwareProcessor 。

All Known Subinterfaces:
ApplicationContextAware, ApplicationEventPublisherAware, ApplicationStartupAware, BeanClassLoaderAware, BeanFactoryAware, 
BeanNameAware, BootstrapContextAware, EmbeddedValueResolverAware, EnvironmentAware, ImportAware, LoadTimeWeaverAware, 
MessageSourceAware, NotificationPublisherAware, ResourceLoaderAware, SchedulerContextAware, ServletConfigAware, ServletContextAware

```

### BeanPostProcessor

给bean做特殊处理的接口类



```java
org.springframework.beans.factory.config.BeanPostProcessor.postProcessBeforeInitialization ， 
org.springframework.beans.factory.config.BeanPostProcessor.postProcessAfterInitialization ， 
```

### MergedBeanDefinitionPostProcessor

运行时合并bean 定义的后处理器回调接口。 BeanPostProcessor实现可以实现这个子接口，以便对 Spring BeanFactory用来创建 bean 实例的合并 bean 定义（原始 bean 定义的已处理副本）进行后处理。

postProcessMergedBeanDefinition方法可以例如内省 bean 定义，以便在后处理 bean 的实际实例之前准备一些缓存的元数据。也允许修改 bean 定义，但仅限于实际用于并发修改的定义属性。本质上，这仅适用于在RootBeanDefinition本身上定义的操作，而不适用于其基类的属性。

```java
// 入口
// AbstractAutowireCapableBeanFactory.doCreateBean
synchronized (mbd.postProcessingLock) {
	if (!mbd.postProcessed) {
		try {
			applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
		}
		catch (Throwable ex) {
			throw new BeanCreationException(mbd.getResourceDescription(), beanName,
					"Post-processing of merged bean definition failed", ex);
		}
		mbd.postProcessed = true;
	}
}
```

### ApplicationContextAwareProcessor

装载aware接口对应的实现类，实现了BeanPostProcessor类。实现了方法postProcessBeforeInitialization。

```java
BeanPostProcessor实现，将ApplicationContextAware的ApplicationContext 、 
Environment或StringValueResolver提供给实现EnvironmentAware 、 
EmbeddedValueResolverAware 、 ResourceLoaderAware 、 
ApplicationEventPublisherAware 、 MessageSourceAware和/或
ApplicationContext接口的 bean。
实现的接口按照上面提到的顺序得到满足。
应用程序上下文将自动将其注册到其底层 bean 工厂。应用程序不直接使用它。
自从：2003 年 10 月 10 日
也可以看看：
EnvironmentAware ， EmbeddedValueResolverAware ， 
ResourceLoaderAware ， ApplicationEventPublisherAware ， 
MessageSourceAware ， ApplicationContextAware ， 
AbstractApplicationContext.refresh()
```

```java
private void invokeAwareInterfaces(Object bean) {
   if (bean instanceof EnvironmentAware) {
      ((EnvironmentAware) bean).setEnvironment(this.applicationContext.getEnvironment());
   }
   if (bean instanceof EmbeddedValueResolverAware) {
      ((EmbeddedValueResolverAware) bean).setEmbeddedValueResolver(this.embeddedValueResolver);
   }
   if (bean instanceof ResourceLoaderAware) {
      ((ResourceLoaderAware) bean).setResourceLoader(this.applicationContext);
   }
   if (bean instanceof ApplicationEventPublisherAware) {
      ((ApplicationEventPublisherAware) bean).setApplicationEventPublisher(this.applicationContext);
   }
   if (bean instanceof MessageSourceAware) {
      ((MessageSourceAware) bean).setMessageSource(this.applicationContext);
   }
   if (bean instanceof ApplicationContextAware) {
      ((ApplicationContextAware) bean).setApplicationContext(this.applicationContext);
   }
}
```

### DefaultListableBeanFactory

```java
Spring 的ConfigurableListableBeanFactory和BeanDefinitionRegistry接口的默认实现：
一个基于 bean 定义元数据的成熟 bean 工厂，可通过后处理器进行扩展。
典型用法是在访问 bean 之前首先注册所有 bean 定义（可能从 bean 定义文件中读取）。
因此，按名称查找 Bean 是本地 bean 定义表中的一种廉价操作，它对预先解析的 bean 定义元数据对象进行操作。
请注意，特定 bean 定义格式的读取器通常是单独实现的，而不是作为 bean 工厂子类：
例如参见org.springframework.beans.factory.xml.XmlBeanDefinitionReader 。
对于org.springframework.beans.factory.ListableBeanFactory接口的替代实现，
请查看StaticListableBeanFactory ，它管理现有的 bean 实例，而不是基于 bean 定义创建新实例。
自从：2001 年 4 月 16 日
也可以看看：
registerBeanDefinition ， 
addBeanPostProcessor ， 
getBean ， 
resolveDependency
```

### GenericBeanDefinition

```java
GenericBeanDefinition 是用于标准 bean 定义目的的一站式商店。
像任何 bean 定义一样，它允许指定一个类以及可选的构造函数参数值和属性值。
此外，可以通过“parentName”属性灵活配置从父 bean 定义派生。
通常，使用此GenericBeanDefinition类来注册用户可见的 bean 定义
（后处理器可能对其进行操作，甚至可能重新配置父名称）。
使用RootBeanDefinition / ChildBeanDefinition ，
其中父/子关系恰好是预先确定的。
自从：2.5
也可以看看：
setParentName , RootBeanDefinition , ChildBeanDefinition
```

### GenericApplicationContext

```java
包含单个内部DefaultListableBeanFactory实例且不采用特定 bean 定义格式的通用 ApplicationContext 实现。实现BeanDefinitionRegistry接口以允许对其应用任何 bean 定义读取器。
典型用法是通过BeanDefinitionRegistry接口注册各种 bean 定义，
然后调用refresh()以使用应用程序上下文语义初始化这些 bean（处理org.springframework.context.ApplicationContextAware ，自动检测BeanFactoryPostProcessors等）。
与为每次刷新创建新的内部 BeanFactory 实例的其他 ApplicationContext 实现相比，
此上下文的内部 BeanFactory 从一开始就可用，以便能够在其上注册 bean 定义。 refresh()只能被调用一次。
使用示例：
   GenericApplicationContext ctx = new GenericApplicationContext();
   XmlBeanDefinitionReader xmlReader = new XmlBeanDefinitionReader(ctx);
   xmlReader.loadBeanDefinitions(new ClassPathResource("applicationContext.xml"));
   PropertiesBeanDefinitionReader propReader = new PropertiesBeanDefinitionReader(ctx);
   propReader.loadBeanDefinitions(new ClassPathResource("otherBeans.properties"));
   ctx.refresh();
  
   MyBean myBean = (MyBean) ctx.getBean("myBean");
   ...
对于 XML bean 定义的典型情况，只需使用ClassPathXmlApplicationContext或FileSystemXmlApplicationContext ，
它们更容易设置 - 但不太灵活，因为您可以只使用 XML bean 定义的标准资源位置，而不是混合任意 bean 定义格式。
 Web 环境中的等价物是org.springframework.web.context.support.XmlWebApplicationContext 。
对于应该以可刷新方式读取特殊 bean 定义格式的自定义应用程序上下文实现，请考虑从AbstractRefreshableApplicationContext基类派生。
自从：
1.1.2 也可以看看：
registerBeanDefinition , refresh() , 
org.springframework.beans.factory.xml.XmlBeanDefinitionReader , 
org.springframework.beans.factory.support.PropertiesBeanDefinitionReader

```

### DefaultListableBeanFactory.preInstantiateSingletons()

时序图

![](https://tcs.teambition.net/storage/312hf227aac2cb9e6353070d13588e477200?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmhmMjI3YWFjMmNiOWU2MzUzMDcwZDEzNTg4ZTQ3NzIwMCJ9.72uOZFBQRGK20sd4nQtPVb9OHOx1sy227FxuESV0_F8&download=DefaultListableBeanFactory_preInstantiateSingletons%20(2).png "")

### InstantiationAwareBeanPostProcessor

添加实例化前回调的BeanPostProcessor子接口，以及实例化后但在设置显式属性或发生自动装配之前的回调。

通常用于抑制特定目标 bean 的默认实例化，例如创建具有特殊 TargetSources 的代理（池化目标、延迟初始化目标等），或实现额外的注入策略，如字段注入。

注意：此接口为专用接口，主要供框架内部使用。建议尽可能实现普通的BeanPostProcessor接口，或者从InstantiationAwareBeanPostProcessorAdapter派生，以屏蔽对该接口的扩展。

```java
/**
	DestructionAwareBeanPostProcessor, 
	InstantiationAwareBeanPostProcessor, 
	MergedBeanDefinitionPostProcessor, 
	SmartInstantiationAwareBeanPostProcessor
*/
public interface InstantiationAwareBeanPostProcessor extends BeanPostProcessor {

	/**
	 * Apply this BeanPostProcessor <i>before the target bean gets instantiated</i>.
	 * The returned bean object may be a proxy to use instead of the target bean,
	 * effectively suppressing default instantiation of the target bean.
	 * <p>If a non-null object is returned by this method, the bean creation process
	 * will be short-circuited. The only further processing applied is the
	 * {@link #postProcessAfterInitialization} callback from the configured
	 * {@link BeanPostProcessor BeanPostProcessors}.
	 * <p>This callback will be applied to bean definitions with their bean class,
	 * as well as to factory-method definitions in which case the returned bean type
	 * will be passed in here.
	 * <p>Post-processors may implement the extended
	 * {@link SmartInstantiationAwareBeanPostProcessor} interface in order
	 * to predict the type of the bean object that they are going to return here.
	 * <p>The default implementation returns {@code null}.
	 * @param beanClass the class of the bean to be instantiated
	 * @param beanName the name of the bean
	 * @return the bean object to expose instead of a default instance of the target bean,
	 * or {@code null} to proceed with default instantiation
	 * @throws org.springframework.beans.BeansException in case of errors
	 * @see #postProcessAfterInstantiation
	 * @see org.springframework.beans.factory.support.AbstractBeanDefinition#getBeanClass()
	 * @see org.springframework.beans.factory.support.AbstractBeanDefinition#getFactoryMethodName()
	 */
	@Nullable
	default Object postProcessBeforeInstantiation(Class<?> beanClass, String beanName) throws BeansException {
		return null;
	}

	/**
	 * Perform operations after the bean has been instantiated, via a constructor or factory method,
	 * but before Spring property population (from explicit properties or autowiring) occurs.
	 * <p>This is the ideal callback for performing custom field injection on the given bean
	 * instance, right before Spring's autowiring kicks in.
	 * <p>The default implementation returns {@code true}.
	 * @param bean the bean instance created, with properties not having been set yet
	 * @param beanName the name of the bean
	 * @return {@code true} if properties should be set on the bean; {@code false}
	 * if property population should be skipped. Normal implementations should return {@code true}.
	 * Returning {@code false} will also prevent any subsequent InstantiationAwareBeanPostProcessor
	 * instances being invoked on this bean instance.
	 * @throws org.springframework.beans.BeansException in case of errors
	 * @see #postProcessBeforeInstantiation
	 */
	default boolean postProcessAfterInstantiation(Object bean, String beanName) throws BeansException {
		return true;
	}

	/**
	 * Post-process the given property values before the factory applies them
	 * to the given bean, without any need for property descriptors.
	 * <p>Implementations should return {@code null} (the default) if they provide a custom
	 * {@link #postProcessPropertyValues} implementation, and {@code pvs} otherwise.
	 * In a future version of this interface (with {@link #postProcessPropertyValues} removed),
	 * the default implementation will return the given {@code pvs} as-is directly.
	 * @param pvs the property values that the factory is about to apply (never {@code null})
	 * @param bean the bean instance created, but whose properties have not yet been set
	 * @param beanName the name of the bean
	 * @return the actual property values to apply to the given bean (can be the passed-in
	 * PropertyValues instance), or {@code null} which proceeds with the existing properties
	 * but specifically continues with a call to {@link #postProcessPropertyValues}
	 * (requiring initialized {@code PropertyDescriptor}s for the current bean class)
	 * @throws org.springframework.beans.BeansException in case of errors
	 * @since 5.1
	 * @see #postProcessPropertyValues
	 */
	@Nullable
	default PropertyValues postProcessProperties(PropertyValues pvs, Object bean, String beanName)
			throws BeansException {

		return null;
	}

	/**
	 * Post-process the given property values before the factory applies them
	 * to the given bean. Allows for checking whether all dependencies have been
	 * satisfied, for example based on a "Required" annotation on bean property setters.
	 * <p>Also allows for replacing the property values to apply, typically through
	 * creating a new MutablePropertyValues instance based on the original PropertyValues,
	 * adding or removing specific values.
	 * <p>The default implementation returns the given {@code pvs} as-is.
	 * @param pvs the property values that the factory is about to apply (never {@code null})
	 * @param pds the relevant property descriptors for the target bean (with ignored
	 * dependency types - which the factory handles specifically - already filtered out)
	 * @param bean the bean instance created, but whose properties have not yet been set
	 * @param beanName the name of the bean
	 * @return the actual property values to apply to the given bean (can be the passed-in
	 * PropertyValues instance), or {@code null} to skip property population
	 * @throws org.springframework.beans.BeansException in case of errors
	 * @see #postProcessProperties
	 * @see org.springframework.beans.MutablePropertyValues
	 * @deprecated as of 5.1, in favor of {@link #postProcessProperties(PropertyValues, Object, String)}
	 */
	@Deprecated
	@Nullable
	default PropertyValues postProcessPropertyValues(
			PropertyValues pvs, PropertyDescriptor[] pds, Object bean, String beanName) throws BeansException {

		return pvs;
	}

}

```



### AbstractBeanFactory.doGetBean()

初始化Bean



### BeanDefinitionRegistryPostProcessor

对标准BeanFactoryPostProcessor SPI 的扩展，允许在常规 BeanFactoryPostProcessor 检测开始之前注册进一步的 bean 定义。特别是，BeanDefinitionRegistryPostProcessor 可以注册进一步的 bean 定义，这些定义反过来定义 BeanFactoryPostProcessor 实例。

```java
void postProcessBeanDefinitionRegistry(BeanDefinitionRegistry registry) throws BeansException
```

### **BeanFactoryPostProcessor**

工厂挂钩，允许自定义修改应用程序上下文的 bean 定义，调整上下文底层 bean 工厂的 bean 属性值。

对于针对覆盖应用程序上下文中配置的 bean 属性的系统管理员的自定义配置文件很有用。有关满足此类配置需求的开箱即用解决方案，请参阅PropertyResourceConfigurer及其具体实现。

BeanFactoryPostProcessor可以与 bean 定义交互和修改，但不能与 bean 实例交互。这样做可能会导致过早的 bean 实例化，违反容器并导致意外的副作用。如果需要 bean 实例交互，请考虑实现BeanPostProcessor 。

注册

ApplicationContext在其 bean 定义中自动检测BeanFactoryPostProcessor bean，并在创建任何其他 bean 之前应用它们。 BeanFactoryPostProcessor也可以通过ConfigurableApplicationContext以编程方式注册。

排序

在ApplicationContext中自动检测到的BeanFactoryPostProcessor bean 将根据org.springframework.core.PriorityOrdered和org.springframework.core.Ordered语义进行排序。相反，使用ConfigurableApplicationContext以编程方式注册的BeanFactoryPostProcessor bean 将按注册顺序应用；对于以编程方式注册的后处理器，将忽略通过实现PriorityOrdered或Ordered接口表达的任何排序语义。此外，对于BeanFactoryPostProcessor bean，不考虑@Order注释。

```java
void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException
```



### ConfigurableListableBeanFactory

大多数可列出的bean工厂要实现的配置接口。除了ConfigurableBeanFactory之外，它还提供了分析和修改 bean 定义以及预实例化单例的工具。

org.springframework.beans.factory.BeanFactory的这个子接口并不意味着在正常的应用程序代码中使用：对于典型用例，请坚持使用org.springframework.beans.factory.BeanFactory或ListableBeanFactory 。这个接口只是为了允许框架内部的即插即用，即使在需要访问 bean 工厂配置方法时也是如此。

可以通过实现：**BeanFactoryPostProcessor的接口进行扩展，实现方法**



```java

/**
 * Configuration interface to be implemented by most listable bean factories.
 * In addition to {@link ConfigurableBeanFactory}, it provides facilities to
 * analyze and modify bean definitions, and to pre-instantiate singletons.
 *
 * <p>This subinterface of {@link org.springframework.beans.factory.BeanFactory}
 * is not meant to be used in normal application code: Stick to
 * {@link org.springframework.beans.factory.BeanFactory} or
 * {@link org.springframework.beans.factory.ListableBeanFactory} for typical
 * use cases. This interface is just meant to allow for framework-internal
 * plug'n'play even when needing access to bean factory configuration methods.
 *
 * @author Juergen Hoeller
 * @since 03.11.2003
 * @see org.springframework.context.support.AbstractApplicationContext#getBeanFactory()
 */
public interface ConfigurableListableBeanFactory
		extends ListableBeanFactory, AutowireCapableBeanFactory, ConfigurableBeanFactory {

	/**
	 * Ignore the given dependency type for autowiring:
	 * for example, String. Default is none.
	 * @param type the dependency type to ignore
	 */
	void ignoreDependencyType(Class<?> type);

	/**
	 * Ignore the given dependency interface for autowiring.
	 * <p>This will typically be used by application contexts to register
	 * dependencies that are resolved in other ways, like BeanFactory through
	 * BeanFactoryAware or ApplicationContext through ApplicationContextAware.
	 * <p>By default, only the BeanFactoryAware interface is ignored.
	 * For further types to ignore, invoke this method for each type.
	 * @param ifc the dependency interface to ignore
	 * @see org.springframework.beans.factory.BeanFactoryAware
	 * @see org.springframework.context.ApplicationContextAware
	 */
	void ignoreDependencyInterface(Class<?> ifc);

	/**
	 * Register a special dependency type with corresponding autowired value.
	 * <p>This is intended for factory/context references that are supposed
	 * to be autowirable but are not defined as beans in the factory:
	 * e.g. a dependency of type ApplicationContext resolved to the
	 * ApplicationContext instance that the bean is living in.
	 * <p>Note: There are no such default types registered in a plain BeanFactory,
	 * not even for the BeanFactory interface itself.
	 * @param dependencyType the dependency type to register. This will typically
	 * be a base interface such as BeanFactory, with extensions of it resolved
	 * as well if declared as an autowiring dependency (e.g. ListableBeanFactory),
	 * as long as the given value actually implements the extended interface.
	 * @param autowiredValue the corresponding autowired value. This may also be an
	 * implementation of the {@link org.springframework.beans.factory.ObjectFactory}
	 * interface, which allows for lazy resolution of the actual target value.
	 */
	void registerResolvableDependency(Class<?> dependencyType, @Nullable Object autowiredValue);

	/**
	 * Determine whether the specified bean qualifies as an autowire candidate,
	 * to be injected into other beans which declare a dependency of matching type.
	 * <p>This method checks ancestor factories as well.
	 * @param beanName the name of the bean to check
	 * @param descriptor the descriptor of the dependency to resolve
	 * @return whether the bean should be considered as autowire candidate
	 * @throws NoSuchBeanDefinitionException if there is no bean with the given name
	 */
	boolean isAutowireCandidate(String beanName, DependencyDescriptor descriptor)
			throws NoSuchBeanDefinitionException;

	/**
	 * Return the registered BeanDefinition for the specified bean, allowing access
	 * to its property values and constructor argument value (which can be
	 * modified during bean factory post-processing).
	 * <p>A returned BeanDefinition object should not be a copy but the original
	 * definition object as registered in the factory. This means that it should
	 * be castable to a more specific implementation type, if necessary.
	 * <p><b>NOTE:</b> This method does <i>not</i> consider ancestor factories.
	 * It is only meant for accessing local bean definitions of this factory.
	 * @param beanName the name of the bean
	 * @return the registered BeanDefinition
	 * @throws NoSuchBeanDefinitionException if there is no bean with the given name
	 * defined in this factory
	 */
	BeanDefinition getBeanDefinition(String beanName) throws NoSuchBeanDefinitionException;

	/**
	 * Return a unified view over all bean names managed by this factory.
	 * <p>Includes bean definition names as well as names of manually registered
	 * singleton instances, with bean definition names consistently coming first,
	 * analogous to how type/annotation specific retrieval of bean names works.
	 * @return the composite iterator for the bean names view
	 * @since 4.1.2
	 * @see #containsBeanDefinition
	 * @see #registerSingleton
	 * @see #getBeanNamesForType
	 * @see #getBeanNamesForAnnotation
	 */
	Iterator<String> getBeanNamesIterator();

	/**
	 * Clear the merged bean definition cache, removing entries for beans
	 * which are not considered eligible for full metadata caching yet.
	 * <p>Typically triggered after changes to the original bean definitions,
	 * e.g. after applying a {@link BeanFactoryPostProcessor}. Note that metadata
	 * for beans which have already been created at this point will be kept around.
	 * @since 4.2
	 * @see #getBeanDefinition
	 * @see #getMergedBeanDefinition
	 */
	void clearMetadataCache();

	/**
	 * Freeze all bean definitions, signalling that the registered bean definitions
	 * will not be modified or post-processed any further.
	 * <p>This allows the factory to aggressively cache bean definition metadata.
	 */
	void freezeConfiguration();

	/**
	 * Return whether this factory's bean definitions are frozen,
	 * i.e. are not supposed to be modified or post-processed any further.
	 * @return {@code true} if the factory's configuration is considered frozen
	 */
	boolean isConfigurationFrozen();

	/**
	 * Ensure that all non-lazy-init singletons are instantiated, also considering
	 * {@link org.springframework.beans.factory.FactoryBean FactoryBeans}.
	 * Typically invoked at the end of factory setup, if desired.
	 * @throws BeansException if one of the singleton beans could not be created.
	 * Note: This may have left the factory with some beans already initialized!
	 * Call {@link #destroySingletons()} for full cleanup in this case.
	 * @see #destroySingletons()
	 */
	void preInstantiateSingletons() throws BeansException;

}
```

### FactoryBean

由BeanFactory中使用的对象实现的接口，这些对象本身就是各个对象的工厂。如果一个 bean 实现了这个接口，它被用作一个对象的工厂来暴露，而不是直接作为一个将自己暴露的 bean 实例。

注意：实现此接口的 bean 不能用作普通 bean。 FactoryBean 以 bean 样式定义，但为 bean 引用 ( getObject() ) 公开的对象始终是它创建的对象。

FactoryBeans 可以支持单例和原型，并且可以按需懒惰地创建对象，也可以在启动时急切地创建对象。 SmartFactoryBean接口允许公开更细粒度的行为元数据。

该接口在框架本身中被大量使用，例如用于 AOP org.springframework.aop.framework.ProxyFactoryBean或org.springframework.jndi.JndiObjectFactoryBean 。它也可以用于自定义组件；但是，这仅适用于基础设施代码。

FactoryBean是一种程序化契约。实现不应该依赖注释驱动的注入或其他反射设施。 getObjectType() getObject()调用可能会在引导过程的早期到达，甚至在任何后处理器设置之前。如果您需要访问其他 bean，请实现BeanFactoryAware并以编程方式获取它们。

容器只负责管理FactoryBean 实例的生命周期，而不是FactoryBean 创建的对象的生命周期。因此，暴露的 bean 对象（例如java.io.Closeable.close()上的销毁方法不会被自动调用。相反，FactoryBean 应该实现DisposableBean并将任何此类关闭调用委托给底层对象。

最后，FactoryBean 对象参与包含 BeanFactory 的 bean 创建同步。除了在 FactoryBean 本身（或类似的）中进行延迟初始化之外，通常不需要内部同步。

```java
/**
  All Known Subinterfaces: SmartFactoryBean<T>
  实际应用：ListFactoryBean
*/
public interface FactoryBean<T> {

	/**
	 * The name of an attribute that can be
	 * {@link org.springframework.core.AttributeAccessor#setAttribute set} on a
	 * {@link org.springframework.beans.factory.config.BeanDefinition} so that
	 * factory beans can signal their object type when it can't be deduced from
	 * the factory bean class.
	 * @since 5.2
	 */
	String OBJECT_TYPE_ATTRIBUTE = "factoryBeanObjectType";


	/**
	 * Return an instance (possibly shared or independent) of the object
	 * managed by this factory.
	 * <p>As with a {@link BeanFactory}, this allows support for both the
	 * Singleton and Prototype design pattern.
	 * <p>If this FactoryBean is not fully initialized yet at the time of
	 * the call (for example because it is involved in a circular reference),
	 * throw a corresponding {@link FactoryBeanNotInitializedException}.
	 * <p>As of Spring 2.0, FactoryBeans are allowed to return {@code null}
	 * objects. The factory will consider this as normal value to be used; it
	 * will not throw a FactoryBeanNotInitializedException in this case anymore.
	 * FactoryBean implementations are encouraged to throw
	 * FactoryBeanNotInitializedException themselves now, as appropriate.
	 * @return an instance of the bean (can be {@code null})
	 * @throws Exception in case of creation errors
	 * @see FactoryBeanNotInitializedException
	 */
	@Nullable
	T getObject() throws Exception;

	/**
	 * Return the type of object that this FactoryBean creates,
	 * or {@code null} if not known in advance.
	 * <p>This allows one to check for specific types of beans without
	 * instantiating objects, for example on autowiring.
	 * <p>In the case of implementations that are creating a singleton object,
	 * this method should try to avoid singleton creation as far as possible;
	 * it should rather estimate the type in advance.
	 * For prototypes, returning a meaningful type here is advisable too.
	 * <p>This method can be called <i>before</i> this FactoryBean has
	 * been fully initialized. It must not rely on state created during
	 * initialization; of course, it can still use such state if available.
	 * <p><b>NOTE:</b> Autowiring will simply ignore FactoryBeans that return
	 * {@code null} here. Therefore it is highly recommended to implement
	 * this method properly, using the current state of the FactoryBean.
	 * @return the type of object that this FactoryBean creates,
	 * or {@code null} if not known at the time of the call
	 * @see ListableBeanFactory#getBeansOfType
	 */
	@Nullable
	Class<?> getObjectType();

	/**
	 * Is the object managed by this factory a singleton? That is,
	 * will {@link #getObject()} always return the same object
	 * (a reference that can be cached)?
	 * <p><b>NOTE:</b> If a FactoryBean indicates to hold a singleton object,
	 * the object returned from {@code getObject()} might get cached
	 * by the owning BeanFactory. Hence, do not return {@code true}
	 * unless the FactoryBean always exposes the same reference.
	 * <p>The singleton status of the FactoryBean itself will generally
	 * be provided by the owning BeanFactory; usually, it has to be
	 * defined as singleton there.
	 * <p><b>NOTE:</b> This method returning {@code false} does not
	 * necessarily indicate that returned objects are independent instances.
	 * An implementation of the extended {@link SmartFactoryBean} interface
	 * may explicitly indicate independent instances through its
	 * {@link SmartFactoryBean#isPrototype()} method. Plain {@link FactoryBean}
	 * implementations which do not implement this extended interface are
	 * simply assumed to always return independent instances if the
	 * {@code isSingleton()} implementation returns {@code false}.
	 * <p>The default implementation returns {@code true}, since a
	 * {@code FactoryBean} typically manages a singleton instance.
	 * @return whether the exposed object is a singleton
	 * @see #getObject()
	 * @see SmartFactoryBean#isPrototype()
	 */
	default boolean isSingleton() {
		return true;
	}

}
```

### AbstractAutowireCapableBeanFactory

实现默认 bean 创建的抽象 bean 工厂超类，具有RootBeanDefinition类指定的全部功能。除了 AbstractBeanFactory 的createBean方法外，还实现了AutowireCapableBeanFactory接口。

提供 bean 创建（使用构造函数解析）、属性填充、连接（包括自动连接）和初始化。处理运行时 bean 引用、解析托管集合、调用初始化方法等。支持自动装配构造函数、按名称的属性和按类型的属性。

子类要实现的主要模板方法是resolveDependency(DependencyDescriptor, String, Set, TypeConverter) ，用于按类型自动装配。如果工厂能够搜索其 bean 定义，匹配的 bean 通常将通过这样的搜索来实现。对于其他工厂风格，可以实现简化的匹配算法。

请注意，此类不假定或实现 bean 定义注册表功能。有关org.springframework.beans.factory.ListableBeanFactory和BeanDefinitionRegistry接口的实现，请参见DefaultListableBeanFactory ，它们分别表示此类工厂的 API 和 SPI 视图。

![](https://tcs.teambition.net/storage/312h02a2a2f3e91bd0b16694061953b6a226?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmgwMmEyYTJmM2U5MWJkMGIxNjY5NDA2MTk1M2I2YTIyNiJ9._BQMDecjN75M9VSEEfNk_KdmZnmX4S7fySbPotHriE0&download=AbstractAutowireCapableBeanFactory.png "")

## 知识点

## 依赖注入/控制反转

依赖注入描述的是对象的创建以及使用的过程。spring创建bean是通过bean的依赖关系来创建，比如创建beanA的时候，会去查找与它相关的注入的bean，并创建。

依赖注入的方式有：构造函数、工厂方法、静态工厂方法、setting方法

具体看spring官方文档：

[Core Technologies](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-type-determination)

> IoC 也称为依赖注入 (DI)。这是一个过程，对象仅通过构造函数参数、工厂方法的参数或在对象实例被构造或从工厂方法返回后设置的属性来定义它们的依赖关系（即与它们一起工作的其他对象） . 然后容器在创建 bean 时注入这些依赖项。这个过程基本上是 bean 本身通过使用类的直接构造或诸如服务定位器模式之类的机制来控制其依赖关系的实例化或位置的逆过程（因此称为控制反转）。

![](https://tcs.teambition.net/storage/312he300c48e81accc6380af5c9f730e1d05?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmhlMzAwYzQ4ZTgxYWNjYzYzODBhZjVjOWY3MzBlMWQwNSJ9.WsefiPH9vwx9S3Fcd35AgGzEo5CqGTzedThuXaSKqjM&download=image.png "")

## 循环依赖问题

通过构造函数注入的无法解决循环依赖的问题。原因是通过构造函数创建的bean，输入的参数必须优先注入。这就造成了循环依赖的问题。

只有通过setting方式且scope=singleton的方法，spring容器中会做特殊处理。

```java
// DefaultSingletonBeanRegistry.getSingleton
protected Object getSingleton(String beanName, boolean allowEarlyReference) {
	// Quick check for existing instance without full singleton lock
	Object singletonObject = this.singletonObjects.get(beanName);
	if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
		singletonObject = this.earlySingletonObjects.get(beanName);
		if (singletonObject == null && allowEarlyReference) {
			synchronized (this.singletonObjects) {
				// Consistent creation of early reference within full singleton lock
				singletonObject = this.singletonObjects.get(beanName);
				if (singletonObject == null) {
					singletonObject = this.earlySingletonObjects.get(beanName);
					if (singletonObject == null) {
						ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
						if (singletonFactory != null) {
							singletonObject = singletonFactory.getObject();
							this.earlySingletonObjects.put(beanName, singletonObject);
							this.singletonFactories.remove(beanName);
						}
					}
				}
			}
		}
	}
	return singletonObject;
}
```

## spring容器默认使用的BeanPostProcessor

> 详情见：AbstractApplicationContext.prepareBeanFactory



### ApplicationContextAwareProcessor

用于初始容器内部的默认beanpostprocessor：

EnvironmentAware，

EmbeddedValueResolverAware，

ResourceLoaderAware，

ApplicationEventPublisherAware，

MessageSourceAware，

ApplicationContextAware



### ApplicationListenerDetector

用于初始容器内部的容器启动监听事件



### LoadTimeWeaverAwareProcessor



# 附件

## 流程图

![](https://tcs.teambition.net/storage/312hb7ee70ff0edc4720f0d8da4a41df7efe?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjc5MjkwMiwiaWF0IjoxNjYyMTg4MTAyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmhiN2VlNzBmZjBlZGM0NzIwZjBkOGRhNGE0MWRmN2VmZSJ9.2w3zUThCTMpgnoYgWENnkUAbjKK5lwsB-SOQg938y3s&download=spring%E6%B5%81%E7%A8%8B%E5%9B%BE.png "")



## 官方文档

[Spring Framework](https://spring.io/projects/spring-framework#learn)

[Spring Framework Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/)

[Spring Framework 5.3.19 API](https://docs.spring.io/spring-framework/docs/current/javadoc-api/)

## 待研究项目

1. 如何实现BeanDefinitionRegistryPostProcessor.postProcessBeanDefinitionRegistry(),进行Bean注册（推算可以参考mybatis-spring项目）

1. 调用Aware接口的地方没找到

1. 使用了哪些设计模式

1. GenericBeanDefinition与RootBeanDefinition的区别

1. BeanFactoryPostProcessor接口的使用

1. FactoryBean的使用（MyBatis3 提供 mybatis-spring项目中的 org.mybatis.spring.SqlSessionFactoryBean）



