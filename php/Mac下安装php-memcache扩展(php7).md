## 一、安装服务器端
- `memcached`	
	- 本机之前已通过homebrew安装好了

## 二、安装客户端
- `php-memcache` 扩展

### 安装 php-memcache扩展
> PECL下载php-memcache扩展

- 从[这里](http://pecl.php.net/package/memcache)选择[稳定版2.2.7](http://pecl.php.net/get/memcache-2.2.7.tgz)，PECL 还不支持在 PHP7 下安装 memcache 扩展

- 进入php-memcache目录
	
		$ tar zxvf memcache-2.2.7.tgz	#解压
		$ cd memcache-2.2.7
	
- 执行phpize

		$ sudo phpize
	
		输出：
		Configuring for:
		PHP Api Version:         20151012
		Zend Module Api No:      20151012
		Zend Extension Api No:   320151012

- 再执行以下代码

		$ sudo ./configure
	
- 编译 & 安装
	
	$sudo make
	
> 出现以下报错

- 报错一：
	
		/Users/natalietu/Downloads/memcache-2.2.7/memcache.c:40:10: fatal error: 'ext/standard/php_smart_str.h' file not found
		#include "ext/standard/php_smart_str.h"
      	   		^
		1 error generated.
		make: *** [memcache.lo] Error 1	
		
	> 解决方案
	
	- 此次有个[说法](https://github.com/phalcon/cphalcon/issues/10378)供参考：In PHP7 `etc/standard/php_smart_str.h` has been renamed to `etc/standard/php_smart_string.h`

			查找相应文件
			$ pwd
			/usr/local/Cellar/
			
			$ find / -name php_smart_str.h
			/usr/include/php/ext/standard/php_smart_str.h
			/usr/local/Cellar/php53/5.3.28/include/php/ext/standard/php_smart_str.h
			/usr/local/Cellar/php55/5.5.37/include/php/ext/standard/php_smart_str.h
			
			$ find / -name php_smart_string.h
			/usr/local/Cellar/php@7.0/7.0.23_15/include/php/ext/standard/php_smart_string.h
			/usr/local/Cellar/php@7.0/7.0.26_18/include/php/ext/standard/php_smart_string.h
			
	- so 编辑 memcache.c 文件

			$ vim memcache.c
			将 #include "ext/standard/php_smart_str.h
			替换成 #include "ext/standard/php_smart_string.h
	

- 报错二：
		
		./php_memcache.h:38:10: fatal error: 'ext/standard/php_smart_str_public.h' file not found
		#include "ext/standard/php_smart_str_public.h"
        	 	^
		1 error generated.
		make: *** [memcache.lo] Error 1	
		
	> 解决方案
	
	- so 编辑 memcache.c 文件

			$ vim php_memcache.h
			将 #include "ext/standard/php_smart_str_public.h"
			替换成 #include "ext/standard/php_smart_string_public.h"

- 解决了以上两个报错后，继续
	
		fatal error: too many errors emitted, stopping now [-ferror-limit=]
		32 warnings and 20 errors generated.
		make: *** [memcache.lo] Error 1
		
		奔溃啊啊啊啊啊啊~~~~貌似原因是 PECL 还不支持在 PHP7 下安装 memcache 扩展，2013年以来未更新过
		
> 寻求其他源码包：去github 上碰碰运气。搜索 pecl memcache

- 这就是想要的[https://github.com/websupport-sk/pecl-memcache](https://github.com/websupport-sk/pecl-memcache)

		$ git clone https://github.com/websupport-sk/pecl-memcache.git php-memcache
		
		$ sudo phpize
		
		$ sudo ./configure --with-php-config=/usr/local/Cellar/php70/7.0.26_18/bin/php-config
		
		$ sudo make
		$ sudo make test
		$ sudo make install
		输出：
		/bin/sh /Users/natalietu/Downloads/php-memcache/libtool --mode=install cp ./memcache.la /Users/natalietu/Downloads/php-memcache/modules
		cp ./.libs/memcache.so /Users/natalietu/Downloads/php-memcache/modules/memcache.so
		cp ./.libs/memcache.lai /Users/natalietu/Downloads/php-memcache/modules/memcache.la
		----------------------------------------------------------------------
		Libraries have been installed in:
   		/Users/natalietu/Downloads/php-memcache/modules

		If you ever happen to want to link against installed libraries
		in a given directory, LIBDIR, you must either use libtool, and
		specify the full pathname of the library, or use the `-LLIBDIR'
		flag during linking and do at least one of the following:
   		- add LIBDIR to the `DYLD_LIBRARY_PATH' environment variable 
   		during execution

		See any operating system documentation about shared libraries for
		more information, such as the ld(1) and ld.so(8) manual pages.
		----------------------------------------------------------------------
		Installing shared extensions:     /usr/local/Cellar/php70/7.0.26_18/lib/php/extensions/no-debug-non-zts-20151012/
		
- 修改php.ini
	
		修改文件：/usr/local/etc/php/7.0/php.ini 
		添加一行：extension=memcache.so
		
		$ sh /Users/natalietu/Webhost/phpfpm.sh restart  #重启php-fpm



---------------
- 参考文档
	- [PHP7 下安装 memcache 和 memcached 扩展](http://www.lnmp.cn/install-memcache-and-memcached-extends-under-php7.html)
			
		