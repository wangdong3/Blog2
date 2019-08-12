# JVM  

## JVM内存区域

- 线程共享
	堆（对象实例、对象数组）
	方法区（类信息、常量、静态变量、即时编译器编译的代码）

- 线程私有
	程序计数器（指向当前线程正在执行的字节码的指令的地址（行号））
	本地方法栈（当前线程运行native方法所需数据、指令、返回地址）
	虚拟机栈
		栈帧（方法）
			局部变量表（方法中定义的变量）
			操作数栈
			动态链接
			返回地址
			
	
## JVM内存模型  

- 堆
> 基于分代的思想：
	
	新生代
	
	老年代
	
	永久代 | 元空间（JDK8）