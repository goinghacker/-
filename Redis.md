
一.redis 数据类型有哪些?
	a.字符串;b.列表;c.集合;d.有序集合;e.哈希;

二. redis与memcache的区别?

	1.在存储位置上，memcache存储在内存中，redis存储在内存中，也可以存储在磁盘中，达到持久化的功能，当断电时，memecache数据会全部丢失，
	 而redis可以利用快照或AOF将数据写入磁盘，当来电时候，从磁盘中读取数据写入内存中，当物理内存使用完可以将数据存储在磁盘；
	2.存储数据类型上，memcache多数存储字符串，redis可以存储多种数据类型，如字符串、列表、hash、集合、有序集合；
	3.存储数据大小上，memcache存储单个value值最大100M，而redis最大值为1M；
	4.redis只支持单核，memcache可支持多核；
	5.memcache支持分布式，redis支持主从；
