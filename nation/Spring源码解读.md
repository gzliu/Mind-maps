# Spring源码解读

## 1.源码分析的流程图

[GitHub - gzliu/Mind-maps](https://github.com/gzliu/Mind-maps.git)

## 2.知识点

### 2.1 依赖注入/控制反转

依赖注入描述的是对象的创建以及使用的过程。spring创建bean是通过bean的依赖关系来创建，比如创建beanA的时候，会去查找与它相关的注入的bean，并创建。

依赖注入的方式有：构造函数、工厂方法、静态工厂方法、setting方法

具体看spring官方文档：

[Core Technologies](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-type-determination)

> IoC 也称为依赖注入 (DI)。这是一个过程，对象仅通过构造函数参数、工厂方法的参数或在对象实例被构造或从工厂方法返回后设置的属性来定义它们的依赖关系（即与它们一起工作的其他对象） . 然后容器在创建 bean 时注入这些依赖项。这个过程基本上是 bean 本身通过使用类的直接构造或诸如服务定位器模式之类的机制来控制其依赖关系的实例化或位置的逆过程（因此称为控制反转）。
> 

![https://docs.spring.io/spring-framework/docs/5.2.22.RELEASE/spring-framework-reference/images/container-magic.png](https://docs.spring.io/spring-framework/docs/5.2.22.RELEASE/spring-framework-reference/images/container-magic.png)

### 2.2 什么是springbean？

被spring容器管理的对象为springbean。具体为：可以通过BeanFactory.getBean()方法获取的对象

使用ApplicationContext高级容器注入的springbean，首先会通过读取xml、注解的方式转换成BeanDefinition。BeanDefinition为一个抽象接口，定义了bean的一些行为，它有用到的一个实现为RootBeanDefinition。通过RootBeanDefinition可以修改springBean的一些属性值，比如作用域、对应是哪个class等。实例化后转换成BeanWrapper，更加丰富Bean的操作

### 2.3 springbean的生命周期？

在BeanFactory的注解中有说明：

[Flowchart Maker & Online Diagram Software](https://app.diagrams.net/#Hgzliu%2FMind-maps%2Fmain%2Fspring%E6%BA%90%E7%A0%81%E5%88%86%E6%9E%90.drawio)

![Untitled](Spring%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%2033c50b9415e54f3ca03bcfa4fe139a77/Untitled.jpeg)

### 2.4 spring容器的加载流程？

```java
AbstractApplicationContext#refresh

public void refresh() throws BeansException, IllegalStateException {
		synchronized (this.startupShutdownMonitor) {
			// Prepare this context for refreshing.
			prepareRefresh();

			// Tell the subclass to refresh the internal bean factory.
			// 实际调用的是AbstractRefreshableConfigApplicationContext.refreshBeanFactory方法创建默认的BeanFactory，同时读取xml、注解等方式获取到Bean，此时将bean转换成BeanDefinition对象，相当于java中的class加载到内存中
			ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();

			// Prepare the bean factory for use in this context.
			// 初始化BeanFactory,
			prepareBeanFactory(beanFactory);

			try {
				// Allows post-processing of the bean factory in context subclasses.
				// 用于子容器实现，此时bean都加载了，但是没有初始化
				postProcessBeanFactory(beanFactory);

				// Invoke factory processors registered as beans in the context.
				// 调用DeanFactoryPostProcessor的方法
				invokeBeanFactoryPostProcessors(beanFactory);

				// Register bean processors that intercept bean creation.
				// 读取所有实现BeanPostProcessor的类，并将之放入到ConfigurableListableBeanFactory.addBeanPostProcessor
				registerBeanPostProcessors(beanFactory);

				// Initialize message source for this context.
				// 初始化国际化，在容器内部初始化MessageSource messageSource对象
				initMessageSource();

				// Initialize event multicaster for this context.
				// 初始化事件处理器：ApplicationEventMulticaster applicationEventMulticaster
				initApplicationEventMulticaster();

				// Initialize other special beans in specific context subclasses.
				// 子容器的扩展
				onRefresh();

				// Check for listener beans and register them.
				// 注册监听bean
				registerListeners();

				// Instantiate all remaining (non-lazy-init) singletons.
				// 初始化spring bean
				finishBeanFactoryInitialization(beanFactory);

				// Last step: publish corresponding event.
				// 完成refresh方法。发送refresh事件，调用lifecycleProcessor#onRefresh()、发送ContextRefreshedEvent事件
				finishRefresh();
			}

			...
		}
	}

```

### 2.5 spring 中factorybean又是什么？

由BeanFactory中使用的对象实现的接口，这些对象本身就是各个对象的工厂。如果一个 bean 实现了这个接口，它被用作一个对象的工厂来暴露，而不是直接作为一个将自己暴露的 bean 实例。

注意：实现此接口的 bean 不能用作普通 bean。 FactoryBean 以 bean 样式定义，但为 bean 引用 ( getObject() ) 公开的对象始终是它创建的对象。

FactoryBeans 可以支持单例和原型，并且可以按需懒惰地创建对象，也可以在启动时急切地创建对象。 SmartFactoryBean接口允许公开更细粒度的行为元数据。

该接口在框架本身中被大量使用，例如用于 AOP org.springframework.aop.framework.ProxyFactoryBean或org.springframework.jndi.JndiObjectFactoryBean 。它也可以用于自定义组件；但是，这仅适用于基础设施代码。

FactoryBean是一种程序化契约。实现不应该依赖注释驱动的注入或其他反射设施。 getObjectType() getObject()调用可能会在引导过程的早期到达，甚至在任何后处理器设置之前。如果您需要访问其他 bean，请实现BeanFactoryAware并以编程方式获取它们。

容器只负责管理FactoryBean 实例的生命周期，而不是FactoryBean 创建的对象的生命周期。因此，暴露的 bean 对象（例如java.io.Closeable.close()上的销毁方法不会被自动调用。相反，FactoryBean 应该实现DisposableBean并将任何此类关闭调用委托给底层对象。

最后，FactoryBean 对象参与包含 BeanFactory 的 bean 创建同步。除了在 FactoryBean 本身（或类似的）中进行延迟初始化之外，通常不需要内部同步。

<aside>
💡 FactoryBean与spring bean的区别，FactoryBean通过getObject()来向spring容器注入spring bean 。一般FactoryBean不单独使用，而是跟其他的扩展一起使用。可以参考：`SchedulerFactoryBean`

</aside>

```java
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

### 2.6 spring中Aware接口的使用？

为了能够得到spring容器的中的各种对象，且不会影响到spring容器中原有逻辑。使用Aware接口来进行扩展，实现业务与spring容器解耦

| Aware接口类 | 说明 | spring容器中调用接口方法的地方 |
| --- | --- | --- |
| BeanNameAware#setBeanName | 获取到Bean的名称 | AbstractAutowireCapableBeanFactory#initializeBean |
| BeanClassLoaderAware#setBeanClassLoader | 获取bean的类加载器 | AbstractAutowireCapableBeanFactory#initializeBean |
| BeanFactoryAware#setBeanFactory | 获取bean工厂，可以通过来获取到BeanDefinition已经改变BeanDefinition的的属性 | AbstractAutowireCapableBeanFactory#initializeBean |
| EnvironmentAware#setEnvironment | 获取环境相关信息，如属性、配置信息等 | ApplicationContextAwareProcessor#postProcessBeforeInitialization |
| EmbeddedValueResolverAware#setEmbeddedValueResolver | 获取值解析器 | ApplicationContextAwareProcessor#postProcessBeforeInitialization |
| ResourceLoaderAware#setResourceLoader | 获取资源加载器 | ApplicationContextAwareProcessor#postProcessBeforeInitialization |
| ApplicationEventPublisherAware#setApplicationEventPublisher | 获取事件广播器，发布事件使用 | ApplicationContextAwareProcessor#postProcessBeforeInitialization |
| MessageSourceAware#setMessageSource | 获取消息资源，主要是国际化 | ApplicationContextAwareProcessor#postProcessBeforeInitialization |
| ApplicationContextAware#setApplicationContext | 获取ApplicationContext | ApplicationContextAwareProcessor#postProcessBeforeInitialization |
| ServletContextAware#setServletContext | 获取webServletContext |  ServletContextAwareProcessor#postProcessBeforeInitialization |
| ServletConfigAware#setServletConfig |  | ServletContextAwareProcessor#postProcessBeforeInitialization |
|  |  |  |

`ApplicationContextAwareProcessor#postProcessBeforeInitialization`

![Untitled](Spring%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%2033c50b9415e54f3ca03bcfa4fe139a77/Untitled.png)

`AbstractAutowireCapableBeanFactory#initializeBean`

![Untitled](Spring%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%2033c50b9415e54f3ca03bcfa4fe139a77/Untitled%201.png)

`ServletContextAwareProcessor#postProcessBeforeInitialization`

![Untitled](Spring%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%2033c50b9415e54f3ca03bcfa4fe139a77/Untitled%202.png)

### 2.7 什么是spring BeanFactory？

2.7.1 spring的容器技术说明（依赖注入）

2.7.2 spring bean是什么

2.7.3 spring beanfactory的作用

2.7.4 spring beanfactory的接口类图说明

2.7.5 spring beanfactory的使用

spring的IOC实质上相当于是一个容器，将所有业务需要用到的bean都注入到这个容器中，在使用的时候再从这个容器中去获取。当然这中间还有容器中bean相互依赖的问题。

如果要实现这个容器，那么需要保存这些bean的数据，且能够很方便的获取到对应bean以及一些日常使用到的bean的信息。而这个beanfactory就可以看做是保存这些bean的一个抽象。

spring抽象出来的方法见：`章节4.1 BeanFactory`接口详细说明

BeanFactory接口抽象出来的是一些最基本的使用方法，还有扩展出来的抽象接口：`ListableBeanFactory`、`HierarchicalBeanFactory`

BeanFactory接口定义了最简单的获取bean的方式

ListableBeanFactory接口定义了更加复杂的获取bean的方式，且获取的bean为spring加载bean后的BeanDefinition对象。接口详细说明见：`章节4.2 ListableBeanFactory`

HierarchicalBeanFactory接口定义了可以获取到父子beanfactory的接口，用于父子beanfactory场景。接口详情说明见：`章节4.3 HierarchicalBeanFactory` *[ˌhaɪəˈrɑːkɪkl]*

在spring中默认的BeanFactory的实现为：`DefaultListableBeanFactory`

### 2.8 Beanfactory 与ApplicationContext的区别

- 2.8.1 总体说明
    - ApplicationContext包含了所有的BeanFactory的方法，ApplicationContext是比BeanFactory更高级的容器。ApplicationContext主要功能有：加载配置文件、class文件的扫描、通过编程方式注册Bean、注解class等等。一般推荐使用GenericApplicationContext、AnnotationConfigApplicationContext来进行容器的自定义
    - BeanFactory为容器的基础接口，抽象定义了一些最基本的功能。如果使用BeanFactory的话，需要自己手动完成容器的全周期
    
    ![Untitled](Spring%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%2033c50b9415e54f3ca03bcfa4fe139a77/Untitled%203.png)
    
- 2.8.2 BeanFactory与ApplicationContext在功能上的区别
  
  
    | Feature | BeanFactory | ApplicationContext |
    | --- | --- | --- |
    | Bean instantiation/wiring(Bean的初始化以及修改） | Y | Y |
    | Integrated lifecycle management（生命周期管理） | N | Y |
    | Automatic BeanPostProcessor registration（自动注册BeanPostProcessor） | N | Y |
    | Automatic BeanFactoryPostProcessor registration(自动注册BeanFactoryPostProcessor) | N | Y |
    | Convenient MessageSource access (for
    internationalization) (便捷访问到MessageSource) | N | Y |
    | Built-in ApplicationEvent publication mechanism(内置容器事件) | N | Y |
- 2.8.3 代码验证
  
    ```java
    
    public static void main(String[] args) {
    		// 使用beanFactory依赖注入
    		// DefaultListableBeanFactory可以看做为BeanFactory的默认实现
    		DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory();
    		// 使用xmlBean注入
    		XmlBeanDefinitionReader reader = new XmlBeanDefinitionReader(beanFactory);
    		reader.loadBeanDefinitions("classpath:bean_factory_demo.xml");
    		Assert.notNull(beanFactory.getBean(SpringSimpleBean.class),"getBean失败");
    		Assert.notNull(beanFactory.getBeanDefinition("springSimpleBean"),"getBeanDefinition失败");
    
    		// 手动注入
    //		beanFactory.registerBeanDefinition("rootBean",new RootBeanDefinition());
    //		BeanDefinition rootBean = beanFactory.getBeanDefinition("rootBean");
    //		beanFactory.registerSingleton("fistBean",new SpringSimpleBean("myFirst"));
    //		SpringSimpleBean fistBean = beanFactory.getBean("fistBean", SpringSimpleBean.class);
    //		System.out.println(fistBean.toString());
    
    		// 使用ApplicationContext依赖注入，自动解析注入bean
    		// ClassPathXmlApplicationContext为ApplicationContext的其中一个实现
    		ClassPathXmlApplicationContext classPathXmlApplicationContext= new ClassPathXmlApplicationContext("classpath:bean_factory_demo.xml");
    		Assert.notNull(classPathXmlApplicationContext.getBean(SpringSimpleBean.class),"classPathXmlApplicationContext.getBean失败");
    		// 无法获取BeanDefinition
    	}
    
    	@Data
    	@AllArgsConstructor
    	@NoArgsConstructor
    	public static class SpringSimpleBean {
    		private String name;
    
    	}
    ```
    
- 2.8.4 BeanFactory接口详细说明
  
    用于访问Springbean容器的根接口。spring提供的低级容器，它的默认实现：`DefaultListableBeanFactory`
    
    BeanFactory实现应该尽可能支持标准的Bean初始化生命周期(也是spring bean的生命周期)：
    
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
    
    ***具体springbean生命周期说明看章节** `2.3 生命周期`*
    
    特殊接口或类说明：
    
    | 类或接口 | 说明 |
    | --- | --- |
    | BeanFactory |  |
    | HierarchicalBeanFacatory |  |
    | ConfigurableBeanFactory |  |
    | AutowireBeanFactory |  |
    | ListableBeanFactory |  |
    | ConfigurableBeanFactory |  |
    |  |  |
    |  |  |
    |  |  |
- 2.8.5 ApplicationContext接口详细说明
  
    spring提供的高级容器，它包含BeanFactory的方法。
    
    提供以下能力：
    
    1. 访问BeanFactory提供的基础方法。继承：`ListableBeanFactory`
    2. 提供以通用的方式加载访问文件资源。继承：`org.springframework.core.io.ResourceLoader`
    3. 支持事件通知。继承：`ApplicationEventPublishe`
    4. 支持解析文本，用于国际化，继承：`MessageSource`
    5. 支持父子容器。子容器的逻辑会优先处理
    6. 支持BeanFactory标准生命周期
    7. 支持`ResourceLoaderAware, ApplicationEventPublisherAware and MessageSourceAware`
    
    | 类或接口 | 说明 |
    | --- | --- |
    | AbstractApplicationContext | 抽象类的实现,核心方法refresh()。提供容器初始化的模板方法 |
    |  |  |
    |  |  |
    |  |  |
    |  |  |
    

### 2.9 循环依赖问题

通过构造函数注入的无法解决循环依赖的问题。原因是通过构造函数创建的bean，输入的参数必须优先注入。这就造成了循环依赖的问题。

只有通过setting方式且scope=singleton的方法，spring容器中会做特殊处理。

```java
// singletonObjects : 一级缓存，用于保存完整的bean
// AbstractBeanFactory#doGetBean
// DefaultSingletonBeanRegistry#getSingleton(String beanName, ObjectFactory<?> singletonFactory)
synchronized (this.singletonObjects) {
		Object singletonObject = this.singletonObjects.get(beanName);
		if (singletonObject == null) {
			...
			try {
				// spring bean的创建方法
				// ObjectFactory是一个函数接口，里边调用了AbstractAutowireCapableBeanFactory#createbean()方法
				singletonObject = singletonFactory.getObject();
				newSingleton = true;
			}
			...
			if (newSingleton) {
				addSingleton(beanName, singletonObject);
			}
		}
		return singletonObject;
	}

// earlySingletonObjects：二级缓存，用于保存创建好的对象，已经实例化，正在属性赋值。只有当前bean未完成创建，被其他bean给引用了，这个时候再次去调用doCreateBean的时候，就会将当前bean放入到二级缓冲中
/**
  处理的代码：
  AbstractBeanFactory#doGetBean

*/
// 当前bean调用doGetBean次数 > 1的时候，会将spring bean放入到二级缓存中
		// 如果是第一次getbean，那么返回null
		// 如果是不是第一次getbean，那么从三级缓冲中获取
		Object sharedInstance = getSingleton(beanName);

// AbstractAutowireCapableBeanFactory#doCreateBean

// singletonFactories：三级缓存，存放的是 Bean 工厂，主要是生产 Bean，存放到二级缓存中。
// AbstractAutowireCapableBeanFactory#doCreateBean
...
boolean earlySingletonExposure = (mbd.isSingleton() && this.allowCircularReferences &&
				isSingletonCurrentlyInCreation(beanName));
		if (earlySingletonExposure) {
			...
			// 将spring bean 放入到三级缓存，如果是代理对象，那么返回代理对象并存入三级缓存
			// 一个类只会执行一次这个方法
			addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));
		}
// Initialize the bean instance.
		Object exposedObject = bean;
		try {
			// 原对象属性赋值
			populateBean(beanName, mbd, instanceWrapper);
			// 原对象调用初始化方法
			// 如果使用了代理方式，那么这个返回的就是代理对象
			// 调用了BeanPostProcessor#postProcessAfterInitialization，而AbstractAutoProxyCreator实现了BeanPostProcessor#postProcessAfterInitialization
			// 且实现的方法中有返回的是代理对象，先去代理对象缓存中获取，如果不存在会创建代理对象并返回
			exposedObject = initializeBean(beanName, exposedObject, mbd);
		}
		...
if (earlySingletonExposure) {
			// 参数allowEarlyReference=FALSE，表示只从二级缓存中读取，如果二级缓存中没有，那么返回null
			Object earlySingletonReference = getSingleton(beanName, false);
			...	
}
...

protected Object getSingleton(String beanName, boolean allowEarlyReference) {
		// 先从一级缓存中获取spring bean
		Object singletonObject = this.singletonObjects.get(beanName);
		if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
			// 一级缓存中没有，那么从二级缓存中获取
			singletonObject = this.earlySingletonObjects.get(beanName);
			// 二级缓存中没有，且allowEarlyReference=TRUE，才从第三级缓存中获取
			// 在AbstractBeanFactory#doGetBean的时候，allowEarlyReference=TRUE
			// 在AbstractAutowireCapableBeanFactory#doCreateBean的时候allowEarlyReference=false
			if (singletonObject == null && allowEarlyReference) {
				// 加锁，一级缓存、二级缓存重新获取一次，如果一级缓存、二级缓存都不存在，那么从三级缓存获取，如果获取到，将spring bean保存到二级缓存中，删除三级缓存的数据
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

- 一级缓存就能解决循环依赖问题？为什么要引用二级、三级缓存？
    1. 如果只用一级缓存，那么保存到一级缓存中的bean有部分是并未创建完整的spring bean，这不符合spring bean的周期设定，因此引用二级缓存。
    2. 如果一个spring bean引用了一个proxy spring bean，那么这个spring bean引用的应该是一个proxy spring bean，但是在spring中proxy spring bean 应该是在初始化的时候，才创建这个代理，但是由于循环引用问题，因此需要提前初始化好这个代理对象，因此就引入了三级缓存用于区分，以及正确引用为代理对象而不是原有对象。
       
        ```java
        // AbstractAutowireCapableBeanFactory#doCreateBean
        protected Object doCreateBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args){
        ...
        
        		// 如果有是代理对象，那么提前创建代理对象，并将对象加入到三级缓存中去
        	 // 如果不是代理对象，那么将对象本身加入到三级缓存中去
           // 是否需要去提前创建代理对象
        		boolean earlySingletonExposure = (mbd.isSingleton() && this.allowCircularReferences &&
        				isSingletonCurrentlyInCreation(beanName));// 验证是否为当前创建bean
        		if (earlySingletonExposure) {
        			if (logger.isTraceEnabled()) {
        				logger.trace("Eagerly caching bean '" + beanName +
        						"' to allow for resolving potential circular references");
        			}
        			addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));// 用于AOP代理
        		}
        ...
        try {
        			// 属性赋值
        			populateBean(beanName, mbd, instanceWrapper);
        			// 初始化
        			// 在这一步中，如果当前对象为代理对象，那么返回代理对象
        			// 如果不是代理对象，那么调用对象的构造方法来创建对象
        			exposedObject = initializeBean(beanName, exposedObject, mbd);
        		}
        ...
        }
        ```
        

## 2.10 BeanFactoryBeanPostProcessor和BeanPostProcessor

> 详情见：AbstractApplicationContext.prepareBeanFactory
> 

BeanFactoryBeanPostProcessor针对的是spring容器的扩展，设计的方法有：

```java
@FunctionalInterface
public interface BeanFactoryPostProcessor {

	//当Bean工厂初始化后，可以进行自定义的修改此Bean工厂里边的内容。
  // springbean的定义被加载（从xml或者注解等方式读取到Bean，并转换成spring容器中的BeanDefinition对象），并可以重新或者新增属性，甚至可以提前初始化springBean

	void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException;

}

// 此接口的在spring容器初始化中的哪个步骤调用：
// AbstractApplicationContext#invokeBeanFactoryPostProcessors
// 此方法大致逻辑：
// 1. 先找是否有BeanDefinitionRegistryPostProcessor#postProcessBeanDefinitionRegistry，如果有那么执行该接口的方法
// 2. 在执行BeanFactoryPostProcessor#postProcessBeanFactory
// 3. 此间如果有实现了PriorityOrdered接口，那么根据此接口的实现进行排序
```

![BeanFactoryPostProcessor.png](Spring%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%2033c50b9415e54f3ca03bcfa4fe139a77/BeanFactoryPostProcessor.png)

目前已知的特殊的BeanFactoryPostProcessor

| 类名称 | 说明 |
| --- | --- |
| BeanDefinitionRegistryPostProcessor | 对标准BeanFactoryPostProcessor SPI 的扩展，允许在常规 BeanFactoryPostProcessor 检测开始之前注册进一步的 bean 定义。特别是，BeanDefinitionRegistryPostProcessor 可以注册进一步的 bean 定义，这些定义反过来定义 BeanFactoryPostProcessor 实例。 |
| CustomScopeConfigurer | 自定义scope |
| ConfigurationClassPostProcessor | 加载@Configuration注解的类、<context:annotation-config/>、<context:component-scan/> |

BeanPostProcessor针对的是spring容器中的实际的Bean的扩展，设计的方法有：

```java
// 会按照PriorityOrdered的顺序调用
public interface BeanPostProcessor {

  // 在bean初始化之前，bean的属性赋值已经处理完
	@Nullable
	default Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
		return bean;
	}

	// 1.在bean初始化之后（调用了InitializingBean.afterPropertiesSet或者执行了自定义的初始化方法<init-method=xxx>），bean的属性赋值已经处理完。
// 2.如果InstantiationAwareBeanPostProcessor.postProcessBeforeInstantiation无法往下执行，那么也会调用此方法
// 3. 此方法适用于FactoryBean、bean或者FactoryBean产生的bean
	@Nullable
	default Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
		return bean;
	}

}
```

目前已知的特殊的BeanPostProcessor：

| 类名称 | 说明 |
| --- | --- |
| ApplicationContextAwareProcessor | 用于spring容器中的*awre接口的回调 |
| ServletContextAwareProcessor | 用于spring web容器中的ServletContextAware接口回调 |
| ApplicationListenerDetector | 用于给spring容器添加的监听 |
| InstantiationAwareBeanPostProcessor | BeanPostProcessor的子接口，提供Bean的实例化之前回调，以及实例化之后但是设置属性值事前回调方法 |
| AutowiredAnnotationBeanPostProcessor | @Autowired 、@Value注解的实现。用于这些注解修饰的属性、setter、配置方法进行bean的依赖注入 |
| SmartInstantiationAwareBeanPostProcessor | 对AutowiredAnnotationBeanPostProcessor的扩展。添加bean最终返回的类型。主要用于spring框架内部的实现 |
| InstantiationAwareBeanPostProcessorAdapter | 抽象类。实现SmartInstantiationAwareBeanPostProcessor  |
| MergedBeanDefinitionPostProcessor | Post-processor callback interface for merged bean definitions at runtime. BeanPostProcessor implementations may implement this sub-interface in order to post-process the merged bean definition (a processed copy of the original bean definition) that the Spring BeanFactory uses to create a bean instance. |
| LoadTimeWeaverAwareProcessor | AOP动态加载类实现 |
|  |  |

![BeanPostProcessor.png](Spring%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%2033c50b9415e54f3ca03bcfa4fe139a77/BeanPostProcessor.png)

## 2.11 父子容器说明

## 2.12 InstantiationAwareBeanPostProcessorAdapter

## 3.重要接口说明

### GenericBeanDefinition接口关系（注入容器的普通spring

### GenericApplicationContext关系图

### SimpleApplicationEventMulticaster

### BeanWrapperImpl

初始化对象的时候，会创建此对象。以及处理PropertyEditorRegistrar的逻辑

初始化代码的位置在：AbstractAutowireCapableBeanFactory.createBeanInstance()

### InstantiationAwareBeanPostProcessorAdapter

将SmartInstantiationAwareBeanPostProcessor上的所有方法实现为无操作的适配器，这不会改变容器实例化的每个 bean 的正常处理。子类可能只覆盖他们真正感兴趣的那些方法。

请注意，仅当您确实需要InstantiationAwareBeanPostProcessor功能时才推荐使用此基类。如果您只需要简单的BeanPostProcessor功能，则更喜欢该（更简单）接口的直接实现。

`InstantiationAwareBeanPostProcessor` 

该接口定义的方法有：

```
public interface InstantiationAwareBeanPostProcessor extends BeanPostProcessor {

	// 在实例化之前调用
	@Nullable
	default Object postProcessBeforeInstantiation(Class<?> beanClass, String beanName) throws BeansException {
		return null;
	}

    // 实例化之后调用
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

    // 即将废弃的接口，功能与postProcessProperties一致
	@Deprecated
	@Nullable
	default PropertyValues postProcessPropertyValues(
			PropertyValues pvs, PropertyDescriptor[] pds, Object bean, String beanName) throws BeansException {

		return pvs;
	}
}
```

BeanPostProcessor的子接口，它在实例化之前添加一个回调，并在实例化之后、设置显式属性或进行自动装配之前添加一个回调。

通常用于抑制特定目标Bean的默认实例化，例如创建具有特殊TargetSource的代理(池化目标、延迟初始化目标等)，或实现其他注入策略，如字段注入。

注意：该接口是一个特殊用途的接口，主要供框架内部使用。建议尽可能实现纯BeanPostProcessor接口，或从InstantiationAwareBeanPostProcessorAdapter派生，以屏蔽对此接口的扩展。

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

![AutowiredAnnotationBeanPostProcessor.png](Spring%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%2033c50b9415e54f3ca03bcfa4fe139a77/AutowiredAnnotationBeanPostProcessor.png)

总体接口设计图

## 4.特殊类及接口说明

### 4.1 **BeanFactory**

spring的顶层接口，用于扩展spring

### 4.2 ListableBeanFactory

```java
由Bean工厂实现的BeanFactory接口的扩展，它可以枚举其所有Bean实例，而不是按照客户端的请求逐个尝试按名称查找Bean。预加载其所有Bean定义的BeanFactory实现(例如基于XML的工厂)可以实现该接口。如果这是一个HierarchicalBeanFactory，则返回值将不考虑任何BeanFactory层次结构，而只与当前工厂中定义的Bean相关。使用BeanFactoryUtils助手类也可以考虑祖先工厂中的Bean。此接口中的方法将仅遵循此工厂的Bean定义。它们将忽略通过其他方式注册的任何单例Bean，例如org.springframework.beans.factory.config.ConfigurableBeanFactory‘s RegisterSingleton方法，但getBeanNamesForType和getBeansOfType除外，它们也将检查此类手动注册的单例Bean。当然，BeanFactory的getBean也允许对这种特殊的Bean进行透明访问。然而，在典型的场景中，所有的Bean都将由外部Bean定义来定义，因此大多数应用程序不需要担心这种区别。注意：除了getBeanDefinitionCount和ContainsBeanDefinition之外，此接口中的方法并不是为频繁调用而设计的。实施可能会很慢。
```

### 4.3 HierarchicalBeanFactory

```java
由Bean工厂实现的子接口，可以是层次结构的一部分。可以在ConfigurableBeanFactory接口中找到Bean工厂的相应setParentBeanFactory方法，该方法允许以可配置的方式设置父级。
```

### 4.4 DefaultListableBeanFactory

```java
Spring 的ConfigurableListableBeanFactory和BeanDefinitionRegistry
接口的默认实现：
一个基于 bean 定义元数据的成熟 bean 工厂，可通过后处理器进行扩展。
典型用法是在访问 bean 之前首先注册所有 bean 定义（可能从 bean 定义文件中读取）。
因此，按名称查找 Bean 是本地 bean 定义表中的一种廉价操作，它对预先解析的 bean 定义元数据对象进行操作。
请注意，特定 bean 定义格式的读取器通常是单独实现的，而不是作为 bean 工厂子类：
例如参见org.springframework.beans.factory.xml.XmlBeanDefinitionReader 。
对于org.springframework.beans.factory.ListableBeanFactory接口的替代实现，
请查看StaticListableBeanFactory ，它管理现有的 bean 实例，而不是基于 bean 定义创建新实例。
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

### GenericBeanDefinition

```java
GenericBeanDefinition 是用于标准 bean 定义目的的一站式商店。
像任何 bean 定义一样，它允许指定一个类以及可选的构造函数参数值和属性值。
此外，可以通过“parentName”属性灵活配置从父 bean 定义派生。
通常，使用此GenericBeanDefinition类来注册用户可见的 bean 定义
（后处理器可能对其进行操作，甚至可能重新配置父名称）。
使用RootBeanDefinition / ChildBeanDefinition ，
其中父/子关系恰好是预先确定的。
```

### GenericApplicationContext

```java
包含单个内部DefaultListableBeanFactory实例且不采用特定 bean 定义格式的通用 ApplicationContext 实现。实现BeanDefinitionRegistry接口以允许对其应用任何 bean 定义读取器。
典型用法是通过BeanDefinitionRegistry接口注册各种 bean 定义，
然后调用refresh()以使用应用程序上下文语义初始化这些 bean（处理org.springframework.context.ApplicationContextAware ，自动检测BeanFactoryPostProcessors等）。
与为每次刷新创建新的内部 BeanFactory 实例的其他 ApplicationContext 实现相比，
此上下文的内部 BeanFactory 从一开始就可用，以便能够在其上注册 bean 定义。 refresh()只能被调用一次。
```

### DefaultListableBeanFactory.preInstantiateSingletons()

时序图

### InstantiationAwareBeanPostProcessor

添加实例化前回调的BeanPostProcessor子接口，以及实例化后但在设置显式属性或发生自动装配之前的回调。

通常用于抑制特定目标 bean 的默认实例化，例如创建具有特殊 TargetSources 的代理（池化目标、延迟初始化目标等），或实现额外的注入策略，如字段注入。

注意：此接口为专用接口，主要供框架内部使用。建议尽可能实现普通的BeanPostProcessor接口，或者从InstantiationAwareBeanPostProcessorAdapter派生，以屏蔽对该接口的扩展。

```java
public interface InstantiationAwareBeanPostProcessor extends BeanPostProcessor {

	
	@Nullable
	default Object postProcessBeforeInstantiation(Class<?> beanClass, String beanName) throws BeansException {
		return null;
	}

	
	default boolean postProcessAfterInstantiation(Object bean, String beanName) throws BeansException {
		return true;
	}

	
	@Nullable
	default PropertyValues postProcessProperties(PropertyValues pvs, Object bean, String beanName)
			throws BeansException {

		return null;
	}

	
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

### AbstractAutowireCapableBeanFactory

实现默认 bean 创建的抽象 bean 工厂超类，具有RootBeanDefinition类指定的全部功能。除了 AbstractBeanFactory 的createBean方法外，还实现了AutowireCapableBeanFactory接口。

提供 bean 创建（使用构造函数解析）、属性填充、连接（包括自动连接）和初始化。处理运行时 bean 引用、解析托管集合、调用初始化方法等。支持自动装配构造函数、按名称的属性和按类型的属性。

子类要实现的主要模板方法是resolveDependency(DependencyDescriptor, String, Set, TypeConverter) ，用于按类型自动装配。如果工厂能够搜索其 bean 定义，匹配的 bean 通常将通过这样的搜索来实现。对于其他工厂风格，可以实现简化的匹配算法。

请注意，此类不假定或实现 bean 定义注册表功能。有关org.springframework.beans.factory.ListableBeanFactory和BeanDefinitionRegistry接口的实现，请参见DefaultListableBeanFactory ，它们分别表示此类工厂的 API 和 SPI 视图。

[https://tcs.teambition.net/storage/312h02a2a2f3e91bd0b16694061953b6a226?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjk2OTQyMiwiaWF0IjoxNjYyMzY0NjIyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmgwMmEyYTJmM2U5MWJkMGIxNjY5NDA2MTk1M2I2YTIyNiJ9.H5NNVohQzmaTsbc6mNs6_aCaDIqbBuLoChFASpWYEUw&download=AbstractAutowireCapableBeanFactory.png](https://tcs.teambition.net/storage/312h02a2a2f3e91bd0b16694061953b6a226?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9hcHBJZCI6IjU5Mzc3MGZmODM5NjMyMDAyZTAzNThmMSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY2Mjk2OTQyMiwiaWF0IjoxNjYyMzY0NjIyLCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzMxMmgwMmEyYTJmM2U5MWJkMGIxNjY5NDA2MTk1M2I2YTIyNiJ9.H5NNVohQzmaTsbc6mNs6_aCaDIqbBuLoChFASpWYEUw&download=AbstractAutowireCapableBeanFactory.png)

## LifeCycle

作用：

在spring初始化完成后，为容器注入生命周期。主要是 start(),stop()

上层接口为：Lifecycle，扩增接口：LifecycProcessor、SmartLifecycle

Phased接口用于自定义后的执行顺序

使用方式：

1. 手动注入DefaultLifecycleProcessor，并可以修改timeoutPershutdownPhase的值
2. 如果没有手动注入，那么容器会自动注入DefaultLifecycleProcessor

类图：

代码的入口地方：

```java
// AbstractApplicationContext.finishRefresh() --> initLifecycleProcessorprotected void finishRefresh() {    // Clear context-level resource caches (such as ASM metadata from scanning).    clearResourceCaches();    // Initialize lifecycle processor for this context.    initLifecycleProcessor();    // Propagate refresh to lifecycle processor first.    getLifecycleProcessor().onRefresh();    // Publish the final event.    publishEvent(new ContextRefreshedEvent(this));    // Participate in LiveBeansView MBean, if active.    LiveBeansView.registerApplicationContext(this);}protected void initLifecycleProcessor() {    ConfigurableListableBeanFactory beanFactory = getBeanFactory();    if (beanFactory.containsLocalBean(LIFECYCLE_PROCESSOR_BEAN_NAME)) {        this.lifecycleProcessor =                beanFactory.getBean(LIFECYCLE_PROCESSOR_BEAN_NAME, LifecycleProcessor.class);        if (logger.isTraceEnabled()) {            logger.trace("Using LifecycleProcessor [" + this.lifecycleProcessor + "]");        }    }    else {        // 初始化DefaultLifecycleProcessor 用于入口执行LifeCycle功能        DefaultLifecycleProcessor defaultProcessor = new DefaultLifecycleProcessor();        defaultProcessor.setBeanFactory(beanFactory);        this.lifecycleProcessor = defaultProcessor;        beanFactory.registerSingleton(LIFECYCLE_PROCESSOR_BEAN_NAME, this.lifecycleProcessor);        if (logger.isTraceEnabled()) {            logger.trace("No '" + LIFECYCLE_PROCESSOR_BEAN_NAME + "' bean, using " +                    "[" + this.lifecycleProcessor.getClass().getSimpleName() + "]");        }    }}
```

# 附件

## 流程图

## 官方文档

[Spring Framework](https://spring.io/projects/spring-framework#learn)

[Spring Framework Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/)

[Spring Framework 5.3.19 API](https://docs.spring.io/spring-framework/docs/current/javadoc-api/)

## 待研究项目

1. 如何实现BeanDefinitionRegistryPostProcessor.postProcessBeanDefinitionRegistry(),进行Bean注册（推算可以参考mybatis-spring项目）
2. 调用Aware接口的地方没找到
3. 使用了哪些设计模式
4. GenericBeanDefinition与RootBeanDefinition的区别
5. BeanFactoryPostProcessor接口的使用
6. FactoryBean的使用（MyBatis3 提供 mybatis-spring项目中的 org.mybatis.spring.SqlSessionFactoryBean）