gollum:初次见面 
==================================== 

- 参考文档：
	- [gollum:给wiki插上git的翅膀](https://www.jianshu.com/p/9c35812b9bae)
	- [gollum github](https://github.com/gollum/gollum)


#### gollum -- A git-based Wiki



## Install
> 官方推荐的安装方式

> ** The best way to install Gollum is with RubyGems **

	$ sudo gem install gollum
	
#### 遇到问题：ERROR:  Could not find a valid gem 'gollum' (>= 0), here is why:Unable to download data from http://ruby.taobao.org/ - bad response Not Found 404 (http://ruby.taobao.org/latest_specs.4.8.gz)
- 找到 [官网](https://ruby.taobao.org/) 告知镜像不可用了，RubyGems 镜像的管理工作以后将交由 [Ruby China](https://gems.ruby-china.org) 负责，如何使用？
	
		$ gem sources --add https://gems.ruby-china.org/ --remove http://ruby.taobao.org/
		$ gem sources -l
		*** CURRENT SOURCES ***

		https://gems.ruby-china.org
		# 请确保只有 gems.ruby-china.org
		$ gem install rails
		
#### 遇到问题：ERROR:  Error installing gollum: ERROR: Failed to build gem native extension.
- 参考文档找到的[解决方法](https://stackoverflow.com/questions/21568592/deploy-gollum-wiki-with-engine-yard)，办法就是在执行gem安装命令之前在命令行执行以下代码
	
		$ bundle config --local build.charlock_holmes --with-ldflags='-L.-Wl,-O1 -Wl,--as-needed -rdynamic -Wl,-export-dynamic -Wl,--no-undefined -lz -licuuc'
		执行失败，没有bundle命令，于是乎：
		sudo gem install bundler


