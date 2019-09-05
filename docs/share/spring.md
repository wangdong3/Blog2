# Spring

## spring bean生命周期

**定义 ---- 初始化 ---- 销毁**

1.我们可以自定义初始化和销毁方法，容器在bean进行到当前生命周期时，调用我们自定义的初始化和销毁方法：

	init() destory()
	通过@Bean 指定init-method 和 destory-method；

2.让bean实现InitializingBean(定义初始化逻辑)，DisposableBean(定义销毁逻辑)

3.使用@PostConstruct，在bean创建完成，并且属性赋值完成，执行初始化方法，@PreDestory，在容器销毁bean之前，通知我们进行清理工作

4.BeanPostProcessor，bean的后置处理器，在bean初始化前后进行一些后置处理工作；

	postProcessBeforeInitialization();在初始化之前
	postProcessAfterInitialization();在初始化之后

> spring底层对BeanPostProcessor的使用：
>
> ​	bean赋值、注入其他组件、@Autowired、生命周期注解、@Async等等

1) 构造（对象创建）：

```java
创建IOC容器：
AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(配置类.class);

单实例：容器启动时创建
多实例：获取时创建
```

2) 初始化：

	对象创建完成，并赋值好，调用初始化方法

3) 销毁：

	容器关闭，对象销毁

## spring注解
```java
@Configuration 配置类;
@Bean 注册组件
@Scope 默认单例;
@Lazy 懒加载;
@Conditional 按照条件给容器中注册组件
@ComponentScan

@Import：快速给容器导入一个组件;
	ImportSelector
	ImportBeanDefinitionRegister
	
@PropertySource(value={"classpath:/xx.properties"})，加载外部配置文件;
@Value赋值：基本数值、#{}、${};

@Autowired：自动装配 spring利用依赖注入，完成对容器中各个组件的依赖关系赋值；
	1）默认按照类型去容器中找对应的组件;
	2）如果找到多个类型相同的组件，再将属性的名称作为组件的ID去容器中查找;
	3）@Qualifier("属性名称")，指定需要装配的组件的ID，而不是使用属性名;
	4）自动装配默认要将属性赋值好，没有就会报错，可以使用@Autowired(required=false);
	5）@Primary，让spring自动装配的时候，默认使用首选bean，也可以继续使用@Qualifier指定装配
	
@Resource [JSR250 java规范的注解]
	可以和@Autowired一样实现自动装配功能，默认按照属性名称来装配
	没有支持@Primary使用首选bean
	没有支持@Autowired(required=false)
        
@Inject [JSR330 java规范的注解]
	需要导入javax.inject的包，和@Autowired的功能一样
```


## 自动装配	

@Autowired：构造器、属性、方法、参数，都是从容器中获取组件的值

	1）标注在方法位置
	2）标在构造器上，如果组件只有一个有参构造器，这个有参构造器的@Autowired可以省略
	3）放在参数位置

@Profile：指定组件在哪个环境下才能被注册到容器中，不指定则任何环境都不能注册该组件

	1）加了环境标识的bean，只有这个环境被激活的时候，才能注册到容器中；默认是default环境
	
	2）该注解写在配置类上，在指定环境，该配置类中的配置才能生效
	
	3）没有标注环境标识的bean，任何环境都是加载的
	
	激活环境方式：
		1）使用命令行动态参数，在虚拟机参数位置加载-Dspring.profiles.active=dev
		2）代码的方式激活环境 		
			1.创建IOC容器
			2.设置需要激活的环境（applicationContext.getEnvironment().setActiveProfiles("test","dev")）
			3.注册主配置类（applicationContext.register(Config.class)）
			4.启动刷新容器refresh()

## IOC

## AOP：【动态代理】

> 程序在运行期间，动态的将某段代码切入到指定方法指定位置进行运行

	1.导入aop模块
	2.定义业务逻辑类
	3.定义切面类
		通知方法：
			前置通知（@Before）：在目标方法运行前运行
			后置通知（@After）：在目标方法运行结束之后运行
			返回通知（@AfterReturning）：目标方法正常返回后运行
			异常通知（@AfterThrowing）：出现异常时运行
			环绕通知（@Around）：动态代理，手动推进目标方法运行（joinPoint.procced）
	4.切面类的方法上标注通知注解，写切入点表达式
	5.切面类和业务逻辑类都加入到容器中
	6.告诉spring哪个类是切面类，切面类上加注解@Aspect
	7.给配置类加@EnableAspectJAutoProxy，开启基于注解的aop模式

AOP原理

	@EnableAspectJAutoProxy
		@Import(AspectJAutoProxyRegistrar.class)
			利用AspectJAutoProxyRegistrar自定义给容器中注册bean，AnnotationAwareAspectJAutoProxyCreator
			
		AnnotationAwareAspectJAutoProxyCreator
			---
			---implements 后置处理器、自动装配beanFactory
			
	    创建AnnotationAwareAspectJAutoProxyCreator过程：
	        1）传入配置类，创建IOC容器
	        2）注册配置类，调用refresh()，刷新容器
	        3）registerBeanPostProcessor(beanFactory);注册bean的后置处理器，来方便拦截bean的创建
	            1）先获取IOC容器已经定义了的需要创建对象的所有的BeanPostProcessor
	            2）给容器中加别的BeanPostProcessor
	            3）优先注册实现了PriorityOrdered接口的BeanPostProcessor
	            4）在容器中注册实现了Ordered接口的BeanPostProcessor
	            5）注册没实现优先级接口的BeanPostProcessor
	            6）注册BeanPostProcessor，实际上是创建BeanPostProcessor对象，保存在容器中
	            7）把BeanPostProcessor添加到BeanFactory中
	        4）完成BeanFactory的初始化

## 事务

	@EnableTransactionManagement
		利用TransactionManagementConfigurationSelector给容器中导入组件，
			AutoProxyRegistrar，给容器中注册AutoProxyCreator组件，利用后置处理器机制在对象创建以后，包装对  象，返回一个代理对象（增强器），代理对象执行方法利用拦截器链调用
			ProxyTransactionManagementConfiguration，给容器中注册事务增强器，事务拦截器

## spring源码，设计模式
