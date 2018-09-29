下载 4.1.1版本 http://pecl.php.net/package/redis
/Users/natalietu/Webhost/redis-4.1.1.tgz 
phpize //phpize是用来扩展php扩展模块的，通过phpize可以建立php的外挂模块 
./configure
make //编译程序 
make install

配置扩展
在php配置文件中（我电脑中的php.ini在/usr/local/etc/php/7.2/php.ini）添加

extension=redis.so

lumen + redis
https://www.cnblogs.com/XiongMaoMengNan/p/6505621.html
https://blog.csdn.net/qq_38191191/article/details/81354599

PHP+Redis 实例【一】点赞 + 热度 
https://www.cnblogs.com/sunshine-H/p/7922285.html