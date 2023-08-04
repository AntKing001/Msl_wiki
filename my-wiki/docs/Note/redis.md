---
title: "Redis"
date: 2023-02-15T10:22:14+08:00
draft: false
---

### redis 的安装

	1. wget http://download.redis.io/releases/redis-6.0.8.tar.gz。  

	2. tar xzf redis-6.0.8.tar.gz  

	3. cd redis-6.0.8  

	4. make  

	redis 服务程序:redis-server  

	测试的客户端程序:redis-cli：  
	 



下面启动 redis 服务：  

* cd src
* ./redis-server

注意这种方式启动 redis 使用的是默认配置。也可以通过启动参数告诉 redis 使用指定配置文件使用下面命令启动。

* cd src
* ./redis-server ../redis.conf

redis.conf 是一个默认的配置文件。我们可以根据需要使用自己的配置文件。

启动 redis 服务进程后，就可以使用测试客户端程序 redis-cli 和 redis 服务交互了。 比如：

1. cd src  

2. ./redis-cli  

3. redis> set foo bar  
	
	OK  

4. redis> get foo  

	"bar"  
	
### HyperLogLog  

	Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 	的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定 的、并且是很小的。
	
	在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基 数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。  
	
	但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。


### redis 发布订阅

	redis 127.0.0.1:6379> SUBSCRIBE runoobChat  

	1 "subscribe"  
	
	2 "runoobChat"  
	
	3 (integer) 1  


### redis事务
以下是一个事务的例子， 它先以 MULTI 开始一个事务， 然后将多个命令入队到事务中， 最后由 EXEC 命令触发事务， 一并执行事务中的所有命令：

	1. redis 127.0.0.1:6379> MULTI   

	OK

	2. redis 127.0.0.1:6379> SET book-name "Mastering C++ in 21 days"  

	QUEUED

	3. redis 127.0.0.1:6379> GET book-name  

	QUEUED

	4. redis 127.0.0.1:6379> SADD tag "C++" "Programming" "Mastering Series"  

	QUEUED

	5. redis 127.0.0.1:6379> SMEMBERS tag  

	QUEUED

	6. redis 127.0.0.1:6379> EXEC  
	
		OK  
	
		"Mastering C++ in 21 days"  
		
		(integer) 3  
		
		"Mastering Series"  

		"C++"  
   	
      	"Programming"  


* 单个 Redis 命令的执行是原子性的，但 Redis 没有在事务上增加任何维持原子性的机制，所以 Redis 事务的执行并不是原子性的。  


* 事务可以理解为一个打包的批量执行脚本，但批量指令并非原子化的操作，中间某条指令的失败不会导致前面已做指令的回滚，也不会造成后续的指令不做。

