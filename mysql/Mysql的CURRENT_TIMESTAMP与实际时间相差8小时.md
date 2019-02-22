## Mysql的CURRENT_TIMESTAMP与实际时间相差8小时

> 环境
> 
- CentOS Linux release 7.6.1810
- Mysql 5.7.25

> 当我们创建的表字段使用默认CURRENT_TIMESTAMP时，我们会发现，插入的时间与实际时间相差8小时

	mysql> show variables like '%zone%';
	+------------------+--------+
	| Variable_name    | Value  |
	+------------------+--------+
	| system_time_zone | CST    |
	| time_zone        | SYSTEM |
	+------------------+--------+
	2 rows in set (0.00 sec)

> 这是因为MySQL用的是标准时间，而我们所在的地方的东八区，刚好差了八个小时。解决方法有下面两种：
> 
- 1. mysql配置文件my.cnf，在mysqld部分加上一行

		default-time_zone = '+8:00'
		
- 2. 通过命令行连接mysql，执行time_zone修改命令

		mysql set time_zone = '+8:00'; 
		
> 即可：

	mysql> show variables like '%zone%';
	+------------------+--------+
	| Variable_name    | Value  |
	+------------------+--------+
	| system_time_zone | CST    |
	| time_zone        | +08:00 |
	+------------------+--------+
	2 rows in set (0.00 sec)