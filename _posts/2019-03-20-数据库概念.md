PostgreSQL 数据类型
	整数类型：
		SMALLINT
		INT
	任意精度浮点数类型
		REAL
		NUMERIC(m, n)   m位数保留n位
	时间类型
		TIME  		10:05:00
		DATE     	1989-10-01
		TIMESTAMP  	2019-01-14 21:52:10

RDBMS：
	A: Atomicity（原子性）事务中执行多个操作是原子性的，要么事务中的操作全部执行，要么一个都不执行
	C: Consistency（一致性）代表一致性，即保证进行事务的过程中整个数据库的状态是一致的，不会出现数据花掉的情况
	I: Isolation（隔离性）代表隔离性，即两个事务不会相互影响，覆盖彼此数据等
	D: Durability（持久性）表示持久化，即事务一旦完成，那么数据应该是被写到安全的，持久化存储的设备上

// https://baike.baidu.com/item/CAP原则/5712863?fr=aladdin
分布式系统的CAP理论:
	C: Consistency(强一致性)
	A: Availability(可用性)
	P: Partition tolerance(分区容错性)

所有分布式的思想就是通过让系统放松对某一时刻数据的一致性来换取系统整体伸缩性和性能上的改观，CAP理论就是说在分布式存储系统中，
最多只能实现上面的两点。而由于当前的网络硬件肯定会出现延迟丢包等问题，所以分区容忍性是我们必须需要实现的。所以我们只能在一致性和可用性之间进行权衡，没有NoSQL系统能同时保证这三点。
大部分网站选择的是：弱一致性 + AP


分布式：	不同的多台服务器上面部署不同的服务模块，他们之间通过RPC/RMI之间通信和调用，对外提供服务和组内协作
集群：	不同的多台服务器上面部署相同的服务模块，通过分布式调度软件进行统一的调度，对外提供服务和访问


BASE就是为了解决关系数据库强一致性引起的问题而引起的可用性降低而提出的解决方案。
	BASE是下面三个术语的缩写：
	基本可用（Basically Available）
		目前最快的KV数据库,10W次/S, 满足了高可用性。
	软状态（Soft state）
		Redis的k-v上的v可以是普通的值（基本操作：get/set/del） v可以是数值（除了基本操作之外还可以支持数值的计算） v可以是数据结构比如基于链表存储的双向循环list（除了基本操作之外还可以支持数值的计算，可以实现list的二头pop,push）。如果v是list，可以使用redis实现一个消息队列。如果v是set,可以基于redis实现一个tag系统。与mongodb不同的地方是后者的v可以支持文档，比如按照json的结构存储。redis也可以对存入的Key-Value设置expire时间。
	最终一致（Eventually consistent）
		Redis的v的最大远远超过memcache。这也是实现消息队列的一个前提。


Redis（Remote Dictionary Server）:
    Redis支持数据的持久化，可以将内存中的数据保持在磁盘中，重启的时候可以再次加载使用
    Redis不仅仅支持简单的K-V类型的数据，同时提供lsit、set、zset、hash等数据结构的存储
    Redis支持数据的备份，即master-slave模式的数据备份

		KV、 Cache、 Persistence





