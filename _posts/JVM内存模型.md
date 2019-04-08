## JVM内存模型

![](https://i.bmp.ovh/imgs/2019/03/fce9af7f9b8b7a92.png)

#### 运行时数据区域

##### 程序计数器（Program Counter Register）

是一块比较小的内存空间，用来标识当前线程所执行的字节码的行号指示器。处于线程独占区。如果执行java代码记录的是行号；如果是native方法，值为undefined。此区域是唯一一个在Java虚拟机中没有规定任何OutOfMemoryError情况的区域

##### Java虚拟机栈（Java Virtual Machine Stacks）

描述的是Java方法执行的动态内存模型，每个方法在执行的同时都会创建一个栈帧(Stack Frame)用于存储局部变量表、操作数栈、方法出口等信息，其中局部变量表存放了编译期可知的各种基本数据类型、对象的引用和returnAddress类型。

Java虚拟机规范定义了两种异常状况：当前线程请求的栈深度大于虚拟机所允许的深度（如递归调用），将抛出StackOverFlowError异常；如果没有限定虚拟机的内存，当扩展时无法申请到足够的内存，则会抛出OutOfMemoryError异常。

##### 本地方法栈（Native Method Stack）

为虚拟机执行Native方法提供服务

##### Java堆（Java Heap）

是Java虚拟机所管理的内存中最大的一块，并且是被所有线程共享的内存区域。用来存放对象实例，是垃圾回收器管理的主要区域。如果堆内存无法再扩展时会抛出OutOfMemoryError异常。

Java堆可以分为：新生代和老年代。再细致点新生代分为：Eden、From Survivor、To Survivor，他们的比例是8:1:1。

当Eden区分配的内存不足时，会发生minorGC，由于Java对象大多存活时间较短，所以minorGC活动很频繁。同时JVM会根据复制算法将存活的对象拷贝到survivor中，如果survivor中内存不足时，会采用分配担保的策略将对象移动到老年代中区。

提到minorGC就不得不提到fullGC，它是指发生在老年代的GC，它的速度和效率都会比minorGC慢的多，而且回收时还会使程序发生停顿，所以应当尽量避免发生fullGC

下面有GC的几个名词：

* minorGC：从新生代内存区域（包括Eden和survivor）回收内存
* majorGC：回收整个老年代，当Eden去内存不足时发生
* fullGC：回收整个堆空间，包括新生代和老年代，当老年代内存不足时发生

##### 方法区（Method Area）

Java8也叫永久区（Perm），存储虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。垃圾收集行为出现较少。当方法区无法满足内存分配需求时，将抛出OutOfMemoryError异常。

##### 运行时常量池（Runtime Constant Pool）

属于方法区的一部分。编译期生成的各种字面量和符号引用都被存放在常量池中。



### 参考博客

[segmentfault:JVM完全深入解析 ](https://segmentfault.com/a/1190000014395186)

