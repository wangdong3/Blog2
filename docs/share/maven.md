# maven

## maven生命周期：

```tex
validate -》compile -》test -》package -》verify -》install -》deploy
```

## jar包冲突排查过程

1. 运行会有报错的现象：ClassNotFoundException  or NoSuchMethodError

2. 类来自两个jar包  

- jar包冲突的原因：

	有两个地方同时引入了一个相同的jar包，但是这两个jar包的版本不同

- 排查方式：

	使用mvn -Dverbose dependency:tree 查看maven树

	判断信息：omitted for duplicate   omitted for conflict
		
3. 解决冲突  

- （方式1）使用exclusion标签将冲突的jar排除  

	```xml
	<exclusion>
		<artifactId></artifactId>
		<group></group>
	</exclusion>  
	```
	
- （方式2）版本统一管理  

	```xml
	<properties>
      <java.version>1.8</java.version>
      <rocketmq.version>4.0.0-incubating</rocketmq.version>
  </properties>
	```