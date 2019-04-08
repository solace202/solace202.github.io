## 无监控不调优 : JVM监控 - Jconsole

### 

Jconsole是JDK自带一个监控JVM运行情况的GUI工具，稳定。

[官方Jconsole使用文档](https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html)

启动：使用命令行切换到tomcat的bin目录下，执行jconsole即可

* 概览（Overview）

  在需要保存的图标上右键单击可保存为（CSV）文件中，可以使用Excel打开查看数据

  ![](https://i.bmp.ovh/imgs/2019/03/1976d465893d9de8.png)

* 内存（Memory）

  提供有关内存消耗和内存池的信息

  ![](https://i.bmp.ovh/imgs/2019/03/9192c0ec4122be1e.png)

  “内存”选项卡具有“执行GC”按钮，可以随时单击按钮来执行垃圾回收

  可以查看多种内存度量

  还可以查看堆和非堆内存区域的运行情况

* 线程（Threads）

  ![](https://i.bmp.ovh/imgs/2019/03/88fafda4165c0ab0.png)

  该图表显示了一段时间内的活动线程数，显示两行：红色代表峰值线程数；蓝色显示活动线程数。

  还可以监测哪些线程有死锁

* 类（Classes）

  ![](https://i.bmp.ovh/imgs/2019/03/9099e22b8d5e983b.png)

  该图表绘制了随时间加载的类数：红线是加载的类总数；蓝色是当前加载的类数。

* VM概要（VM Summary）

  ![](https://i.bmp.ovh/imgs/2019/03/9c68e0eb78f65af9.png)

  该界面显示了VM基本所有的信息和参数，包括JVM运行情况、线程、加载类、内存、系统等信息，一览无余

* MBean

  ![](https://i.bmp.ovh/imgs/2019/03/418101e997f6b8bf.png)