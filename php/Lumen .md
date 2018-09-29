## Lumen 
中文文档
https://lumen.laravel-china.org/docs/5.6
http://laravelacademy.org/laravel-docs-5_6

安装环境要求
PHP >= 5.5.9
OpenSSL PHP Extension
PDO PHP Extension
Mbstring PHP Extension

应用项目：筑英台
https://gitlab.arctron.cn/zyt/api


brew install composer
https://www.jianshu.com/p/2b96cc9f593e
在工作目录，运行composer update

配置nginx
/usr/local/etc/nginx/vhosts/heroapi.test.conf
参考：https://blog.csdn.net/skykingf/article/details/45824255
https://www.jianshu.com/p/750448a8cd95

docker配置lumen
https://www.jianshu.com/p/5b9892c25a18

筑英台lumen依赖php>7.1.3， 安装php72
brew install php72
安装目录/usr/local/Cellar/php/7.2.7

修改~/.bashrc
	
	#upgrade php 7.0.26->7.2.7
	export PATH="$(brew --prefix php72)/bin:$PATH"  #for php
	export PATH="$(brew --prefix php72)/sbin:$PATH" #for php-fpm
	
	$ source ~/.bashrc
	$ php -v
	PHP 7.2.7 (cli) (built: Jul 19 2018 09:52:27) ( NTS )
	Copyright (c) 1997-2018 The PHP Group
	Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.2.7, Copyright (c) 1999-2018, by Zend Technologies
   	$ php-fpm -v
   	PHP 7.2.7 (fpm-fcgi) (built: Jul 19 2018 09:52:34)
	Copyright (c) 1997-2018 The PHP Group
	Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.2.7, Copyright (c) 1999-2018, by Zend Technologies


运行http://127.0.0.1/index.php，如果白页，检查php.ini的`short_open_tag`是否为`On`

发现php -v与phpinfo()显示版本不一致
自制启动脚本sh /Users/natalietu/Webhost/phpfpm.sh  start|stop|restart
关于启动php-fpm报错 ERROR: unable to bind listening socket for address ‘127.0.0.1:9000’: Address already in use 
解决方法：killall php-fpm

mac安装运行多个php版本 
https://jingyan.baidu.com/article/c843ea0bc0702e77931e4a9d.html

mac不同目录运行php -v 获取的信息不同，需要在版本信息不正确的目录中再执行 source ~/.bashrc

筑英台api
todo:
- job:
	- [x]统计过去24小时的每个课程的购买量
	- [x]三天内未回答的问题，问题即自动关闭
	- [x]专家已回答，3天内未有申诉，问题即满意
	- [x]名额限制的活动，活动结束的时候发站内通知
- [x]经验值模块
- [x]系统消息模块
- [x]动态系统模块
- [x]用户有登录态后需要修改的接口
	- [x]课程详情api
	- [x]是否可以发表评论，取决于是否已购买该课程
	- [x]课时学习播放api
	- [x]课程收藏
	- [x]课程发表评论
	- [x]活动报名
- [x]活动页浏览数redis?
- 购买逻辑
	- zyt_user_classes写入
	- 线下课程生成二维码md5(classes_id|user_id|6位随机数)
	- course/qrcode  二维码信息展示 & 课程详情页生成二维码
	- zyt_ask_user_buy 写入
	- 动态
		- 购买课程
		- 购买问题答案
		- 提问购买
	- 站内消息
		- 提问购买
	- 经验值
		- 购买课程
		- 购买问题答案
		- 提问购买



    
    
   	

