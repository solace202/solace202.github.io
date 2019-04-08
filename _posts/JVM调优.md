# JVM调优

主要调整两块：堆内存参数的调整、垃圾回收器的调整

### JVM参数

* -：标准参数，所有JVM都支持
* -X：非标准参数，每个JVM实现都不同
* -XX：不稳定参数，下一个版本可能会取消

### 内存溢出问题定位

![](https://i.bmp.ovh/imgs/2019/03/7e632fc3ff3a7e52.png)

-XX：HeapDumpOnOutOfMemoryError：把堆内存信息dump出来

-XX：HeapDumpPath=***  ：demp到哪个文件里面

-XX：+PrintGCDetails：打印GC信息

配置上面的参数后，会将堆信息domp到指定文件，通过各种文件来打开dump文件来分析内存信息，JDK提供了自带的Jvisualvm来分析。也可以使用其他软件打开

```java
public static void main(String[] args) {
   List<Object> lists = new ArrayList<>();

   for(int i = 0; i < 1000000000; i++) {
      lists.add(new byte[1024 * 1024]);
   }
}
```

![](https://pic.superbed.cn/item/5c90b1293a213b0417be10c2)

-Xss128k ：栈内存大小；栈越小，线程并发数量会特别多；栈越大，线程递归调用会特别深

### 常用参数设置

![](https://ww1.sinaimg.cn/large/007i4MEmgy1g1883ar737j30xt0exdi2.jpg)

### Tomcat调优

set JAVA_OPTS=

-Xms4g：程序堆内存起始4g

-Xmx4g：程序最大堆内存4g

-Xss512k：栈内存512k

-XX:+AggressiveOpts：使用所有的优化型的配置

-XX:+UseBiasedLocking：启用偏执锁

-XX:PermSize=64M：永久区64M

-XX:MaxPermSize=300M：永久区最大300M

-XX:+DisableExplicitGC：禁止显式调用GC // 禁用System.gc();

![](https://0d077ef9e74d8.cdn.sohucs.com/rl9FwDn_jpg)

### 性能测试工具

Apache开源工具JMeter，测试对于tomcat的优化



## 总结

[Oracle官网JVM文档](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/toc.html)

对于业务不同情况，对新生代和老年代的比例进行调节，

根据业务实际情况，实用不同的GC，有响应快的，低停顿

对于GC的配置，配置对于内存压缩、并行收集新生代等配置