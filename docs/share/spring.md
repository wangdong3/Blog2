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
@Bean
@Scope 默认单例;
@Lazy 懒加载;
@Conditional
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

## IOC
​	Spring注入的几种方式：set注入；构造函数注入；p命名空间注入

## AOP

## 事务

## spring源码，设计模式
