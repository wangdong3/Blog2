## jdk8新特性  

### lambda表达式：
  允许函数作为一个方法的参数；(param -> expression)  

### 函数式接口：

```java
@FunctionalInterface 注解
注解的接口要有且仅有一个抽象方法 
可以被lambda表达式和函数引用表达式代替
```

### 方法引用：  

通过方法的名字来指向方法；使用**::**

```java
//::new 引用构造方法
list.stream().map(YsjzResource::new).collect(Collectors.toList());

//::getId 引用对象的实例方法
.map(JzclEntity::getId)
```

### 接口默认方法

default

```
default boolean exists(String key) {
	return get(key) != null;
}
```

### optional类  

一个可以为null的容器对象；optional主要用作返回类型，在获取到这个类型的实例后，如果它有值，则可以取得这个值，否则进行一些替代行为  

- 访问Optional对象的值：get()

- 返回默认值：orElse()

```
//如果为空则默认
bookletService.select(record.getFcId()).map(JzfcEntity::getExpose).orElse(2);
```

- 返回异常：oeElseThrow(()-> new IllegalArgumentException)

```
return tokenService.getByServer(ysJzServer).orElseThrow(RuntimeException::new);
```

- 转换值：Optional.ofNullable().map().orElse()

- 过滤值：Optional.ofNullable.filter()

### Stream：  

类似用 SQL 语句从数据库查询数据的直观方式来提供一种对 Java 集合运算和表达的高阶抽象  

使用stream，3个阶段：

	1. 创建一个stream
	2. 指定的中间操作将初始stream转化为其他stream
	3. 最终的操作会产生一个结果，在调用最终操作前都会延迟执行的。在这之后，stream不会再被使用。


- stream为集合创建串行流

```java
ResponseEntity.ok(list.stream().map(YsjzResource::new).collect(Collectors.toList()));
```

- map方法用于映射每个元素到对应的处理结果

- filter方法通过设置过滤条件过滤出元素

```
corps.stream().filter(corpInfo -> StringUtils.isBlank(corpInfo.getPcorpId())).collect(Collectors.toList());
```

- limit用于获取指定数量的流

- forEach迭代流中的每个数据

- sorted对流进行排序

- Collectors实现很多归约操作：将流转换成集合和聚合元素

- count

```
long count = words.stream().filter(w -> w.length() > 12).count();
```