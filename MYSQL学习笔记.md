# MySQL存储引擎的区别 
## InooDB 

1. 采用的是聚集索引,数据文件和索引文件存储在表空间中,主索引采用的是主键索引,使用的B+tree的存储方式,主索引指向的位置为该字段所在的物理地址,而从索引的指针指向的是主索引的地址,innodb的主键字段长度不易过大,同时最好是单调的,以避免在增长的过程中频繁的分裂,推荐使用自增主键作为主索引
2. InooDB可以支持事务
3. InooDB可支持行级锁和表级锁
4. InooDB的默认事务隔离级别为可重复读,并采用间隙锁策略防止幻读的出现
5. InooDB采用MVCC多版本并发控制机制来实现高并发场景下的应用
6. InooDB支持崩溃恢复机制,可以大幅度提升安全性
7. InooDB可以支持外键

## MyISAM

1. 采用的存储方式为非聚集索引,数据文件和索引文件分别进行存储,主索引与从索引之间没有本质的区别
2. MyISAM可对表进行压缩,压缩表只能支持读操作,当需要修改压缩表时,需要对整表进行解压,读取压缩表的效率不会有明显的下降,极大了降低了磁盘I/O
3. MyISAM只可以对表加锁
4. MyISAM存储数据是会将数据存入缓存块中,再统一进行存储,当数据库崩溃时,不保证能够恢复缓存中的数据,同时恢复的速度也远不如InooDB
5. 

# MySQL整体架构

mySQL整体可以通过

# MySQL性能优化

profile 性能剖析

慢查询日志

explain 解释器执行计划

### 优化策略

1. 尽量选用可以正确存储数据的最小数据类型
2. 选用尽可能简单的数据类型来存储数据类型,以及使用MySQL内建类型存储数据
3. 尽可能避免NULL,尤其是需要建索引的列

### 索引的特点

1. 索引大大减少了服务器需要扫描的数据量。
2. 索引可以帮助服务器避免排序和临时表。
3. 索引可以将随机I/O变为顺序I/O。