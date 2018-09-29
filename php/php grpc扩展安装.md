## php grpc扩展安装
- [下载地址](下载地址： http://pecl.php.net/package/gRPC)

> 1、进入目录

	$ cd /Users/natalietu/Downloads/grpc-1.13.0/grpc-1.13.0
	
> 2、执行phpize

  	$ phpize
  	Configuring for:
	PHP Api Version:         20170718
	Zend Module Api No:      20170718
	Zend Extension Api No:   320170718

> 3、再执行
	
	$ ./configure --with-php-config=/usr/local/Cellar/php/7.2.7/bin/php-config
	$ make
	$ make test
	$ make install
	Installing shared extensions:     /usr/local/Cellar/php/7.2.7/pecl/20170718/
	
> 4、修改php.ini
	
	修改文件：/usr/local/etc/php/7.2/php.ini 
	
	添加一行：extension=gprc.so
	
> 5、重启php-fpm

	sh /Users/natalietu/Webhost/phpfpm.sh restart
	
