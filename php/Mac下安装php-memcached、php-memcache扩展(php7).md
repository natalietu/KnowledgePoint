## 一、安装服务器端
- `Libevent`、`memcached`	
	- 本机之前已通过homebrew安装好了

## 二、安装客户端
- `Libmemcached`、`php-memcached`扩展，正确安装顺序Libmemcached > php-memcached
- `php-memcache` 扩展

### 安装 php-memcached扩展
> 1、下载php-memcached扩展

	$ pwd
	/Users/natalietu/Webhost/php-memcached
	#从github上克隆memcached后，需切换到PHP7分支
	$ git clone -b php7 https://github.com/php-memcached-dev/php-memcached.git 
	

> 2、进入php-memcached目录

	$ cd /Users/natalietu/Webhost/php-memcached
	
	
> 3、执行phpize

	$ sudo phpize
	
	输出：
	Configuring for:
	PHP Api Version:         20151012
	Zend Module Api No:      20151012
	Zend Extension Api No:   320151012
	
- `注意1`：执行phpize可能会出现以下错误

		Cannot find config.m4.
		Make sure that you run '/usr/local/opt/php70/bin/phpize' in the top level source directory of the module
		
		报错的原因：执行phpize时，一定要在需要扩展编译的PHP模块目录(当前既 /Users/natalietu/Webhost/php-memcached)中进行
		
	> 什么是`phpize`
	> php官方说明：http://php.net/manual/en/install.pecl.phpize.php
	> phpize是用来扩展php扩展模块的，通过phpize可以建立php的外挂模块

- `注意2`：如果./configure不存在，既未安装autoconf，则会报错
	
		Cannot find autoconf.
		
		则需要先安装autoconf后，再执行phpize
		$ brew install autoconf
		
		
> 4、再执行以下代码
	
	$ ./configure --with-php-config=/usr/local/Cellar/php70/7.0.26_18/bin/php-config --with-libmemcached-dir=/usr/local/libmemcached  --disable-memcached-sasl  #终于改正确了
	
> 出现以下两处报错
 
- 报错一：
	
		checking for libmemcached location... configure: error: Unable to find memcached.h under /usr/lib/libmemcached
		
	> 解决如下：
		
	- 1)、`./configure --with-libmemcached-dir=这个目录` 可使用如下命令查找
		
			在/usr/目录下
			find ./ -name 'memcached.h'
			.//local/libmemcached/include/libmemcached/memcached.h
			.//local/libmemcached/include/libmemcached-1.0/memcached.h
			.//local/libmemcached/include/libmemcached-1.0/struct/memcached.h
	
	- 2)、那么路径改成 `/usr/local/libmemcached/include/libmemcached`，依然报错
		
			checking for libmemcached location... configure: error: Unable to find memcached.h under /usr/local/libmemcached/include/libmemcached
			
	- 3)、通过查看 
[https://github.com/php-memcached-dev/php-memcached/blob/master/config.m4#L237](https://github.com/php-memcached-dev/php-memcached/blob/master/config.m4#L237) 
	
			if test ! -f "$PHP_LIBMEMCACHED_DIR/include/libmemcached/memcached.h"; then
      			AC_MSG_ERROR(Unable to find memcached.h under $PHP_LIBMEMCACHED_DIR)
    		fi
  			else
    			export PKG_CONFIG_PATH="$PKG_CONFIG_PATH:/usr/local/$PHP_LIBDIR/pkgconfig:/usr/$PHP_LIBDIR/pkgconfig:/opt/$PHP_LIBDIR/pkgconfig"
  			fi 
  			
			原来他要去这个路径include/libmemcached/下寻找，so出错
	
	- 4)、执行以下修改
		
			--with-libmemcached-dir=/usr/local/libmemcached
	
		

- 报错二：
	
		checking for libmemcached location... configure: error: memcached support requires libmemcached. Use --with-libmemcached-dir=<DIR> to specify the prefix where libmemcached headers and library are located
	
	> 解决：需要安装依赖 `libmemcached` 
		
	- 1)、通过查看 
[https://github.com/php-memcached-dev/php-memcached/blob/master/config.m4#L244](https://github.com/php-memcached-dev/php-memcached/blob/master/config.m4#L244)

			if ! $PKG_CONFIG --exists libmemcached; then
    			AC_MSG_ERROR([memcached support requires libmemcached. Use --with-libmemcached-dir=<DIR> to specify the prefix where libmemcached headers and library are located])
  			else
    			PHP_LIBMEMCACHED_VERSION=`$PKG_CONFIG libmemcached --modversion`
    			PHP_LIBMEMCACHED_DIR=`$PKG_CONFIG libmemcached --variable=prefix`
	


> 5、编译&安装
	
	$ sudo make
	输出：
	......
	Build complete.
	Don't forget to run 'make test'.
	
	$ sudo make test
	输出：
	......
	=====================================================================
	FAILED TEST SUMMARY
	---------------------------------------------------------------------
	Memcached::getByKey() with CAS [tests/experimental/get_bykey_cas.phpt]
	Memcached::getDelayedByKey() with CAS [tests/experimental/getdelayed_bykey_cas.phpt]
	Memcached::getDelayedByKey() with callback exception [tests/experimental/getdelayed_cbthrows.phpt]
	Memcached::getMulti() bad server [tests/experimental/getmulti_badserver.phpt]
	Memcached::getStats() [tests/experimental/stats.phpt]
	Memcached::getStats() with bad server [tests/experimental/stats_badserver.phpt]
	=====================================================================

	=====================================================================
	WARNED TEST SUMMARY
	---------------------------------------------------------------------
	Memcached store, fetch & touch expired key [tests/expire.phpt] (warn: XFAIL section but test passes)
	=====================================================================
	......
	
	
	$ sudo make install
	输出：
	Installing shared extensions:     /usr/local/Cellar/php70/7.0.26_18/lib/php/extensions/no-debug-non-zts-20151012/
	
> 6、修改php.ini
	
	修改文件：/usr/local/etc/php/7.0/php.ini 
	
	添加一行：extension=memcached.so
	
> 7、重启php-fpm

	sh /Users/natalietu/Webhost/phpfpm.sh restart
	


### 安装 libmemcached	
> `注意`：以上第4、点提示依赖`libmemcached`，实际本机未安装，执行安装，然后再执行./configure...

> 1、brew安装	
	$ brew install libmemcached
	
	输出：
	Updating Homebrew...
	==> Installing dependencies for libmemcached: libevent, memcached
	==> Installing libmemcached dependency: libevent
	==> Downloading https://homebrew.bintray.com/bottles/libevent-2.1.8.yosemite.bottle.tar.gz
	######################################################################## 100.0%
	==> Pouring libevent-2.1.8.yosemite.bottle.tar.gz
	🍺  /usr/local/Cellar/libevent/2.1.8: 847 files, 2.2MB
	==> Installing libmemcached dependency: memcached
	==> Downloading https://www.memcached.org/files/memcached-1.5.7.tar.gz

	curl: (35) Server aborted the SSL handshake
	Error: Failed to download resource "memcached"
	Download failed: https://www.memcached.org/files/memcached-1.5.7.tar.gz
		
		
- 以上安装fail，寻求其他方式：
	- 1)、下载包安装，libmemcached下载地址：https://launchpad.net/libmemcached/+download
	- 2)、文件：libmemcached-1.0.18.tar.gz 
		
			$ tar zxvf libmemcached-1.0.18.tar.gz
			$ cd libmemcached-1.0.18
			$ ./configure --prefix=/usr/local/libmemcached --with-memcached  #success
			$ sudo make
			$ sudo make install
	- 3)、 编译 & 安装
			
			$ sudo make
			$ sudo make install
			
		> 出现以下两处报错
				
		 - 报错一：
				
				libmemcached/byteorder.cc:66:10: error: use of undeclared identifier 'ntohll'
  				return ntohll(value);
         			^
				libmemcached/byteorder.cc:75:10: error: use of undeclared identifier 'htonll'
  				return htonll(value);
         			^
				2 errors generated.	
				
			> 解决如下：编辑 libmemcached/byteorder.cc 文件
			
				$ vim libmemcached/byteorder.cc
				在 #include "libmemcached/byteorder.h" 下面增加，
				以下内容：
				#ifdef HAVE_SYS_TYPES_H
				#include <sys/types.h>
				#endif		
					
		- 报错二：
			
				clients/memflush.cc:42:19: error: comparison between pointer and integer ('char *' and 'int')
  				if (opt_servers == false)
      			~~~~~~~~~~~ ^  ~~~~~
				clients/memflush.cc:51:21: error: comparison between pointer and integer ('char *' and 'int')
    			if (opt_servers == false)
        		~~~~~~~~~~~ ^  ~~~~~
				2 errors generated.
					
			> 解决如下：编辑 clients/memflush.cc 文件
				
				vim clients/memflush.cc
				将两处 if (opt_servers == false)
				替换成 if (opt_servers == NULL)
		
	- 4)、最终安装目录
	
		- `/usr/local/libmemcached/`		
				
				
---------------
- 参考文档
	- [mac中安装并配置memcached](https://www.jianshu.com/p/4984c652161f)
	- [Mac & Linux下php7添加memcached和redis扩展](https://blog.csdn.net/houzhiwen_yy/article/details/69950836)
	- [编译php-memcached 扩展时候遇到的问题Unable to find memcached.h](https://blog.csdn.net/wjc19911118/article/details/52522584)
	- [Linux基于libmemcached，php扩展memcached的安装](https://www.cnblogs.com/cyun/p/6738451.html)
	- [Memcached连接](http://www.runoob.com/memcached/memcached-connection.html)
		
		