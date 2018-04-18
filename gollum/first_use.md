gollum: 初次见面 
==================================== 

- 参考文档：
	- [gollum:给wiki插上git的翅膀](https://www.jianshu.com/p/9c35812b9bae)
	- [Mac下基于Github和jekyll搭建博客](https://www.jianshu.com/p/779379e48ee9)
	- [gollum github](https://github.com/gollum/gollum)
	


#### gollum -- A git-based Wiki

#### 本地的环境：
- MacBook Pro 10.10.5
- Homebrew 1.6.0
- ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-darwin14]

## Install
> 官方推荐的安装方式
> ** The best way to install Gollum is with RubyGems **

### 尝试方法一

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
	
		a命令：$ bundle config --local build.charlock_holmes --with-ldflags='-L.-Wl,-O1 -Wl,--as-needed -rdynamic -Wl,-export-dynamic -Wl,--no-undefined -lz -licuuc'
		执行失败，没有bundle命令，于是乎：
		sudo gem install bundler
		继续执行a命令
		You are replacing the current local value of build.charlock_holmes, which is currently nil
		执行以下命令：（你可以用 Bundler 的 Gem 源代码镜像命令，这样你不用改你的 Gemfile 的 source）
		$ bundle config mirror.https://rubygems.org https://gems.ruby-china.org
		再执行a命令，貌似ok了
		最终安装依旧失败，尝试方法二


### 尝试方法二
- 参考文档：[Mac OS X 下使用 Ruby Gem 的两个坑](https://blog.csdn.net/u011303816/article/details/70185448)
1. 安装依赖
		
		brew install icu4c
		
2. 用homebrew重装一遍ruby

		brew install ruby
		
3. 再安装gollum
	
		sudo gem install gollum  成功！
		
		


> homebrew安装方式

	brew install gollum
	但是会碰到 **fatal: unable to access 'https://go.googlesource.com/tools.git/': Failed to connect to go.googlesource.com port 443: Operation timed out** 如果能翻墙的话可以尝试此方法
	
	
## 开始折腾
1. 进入到wiki目录，在wiki目录下启动gollum
	
		$ mkdir myWiki
		$ cd myWiki
		$ git init
		$ gollum
		
2. 命令行显示如下

		[2018-04-13 14:51:15] INFO  WEBrick 1.4.2
		[2018-04-13 14:51:15] INFO  ruby 2.5.1 (2018-03-29) [x86_64-darwin14]
		== Sinatra (v1.4.8) has taken the stage on 4567 for development with backup from WEBrick
		[2018-04-13 14:51:15] INFO  WEBrick::HTTPServer#start: pid=6964 port=4567
		
3. 打开浏览器 **localhost:4567**
		
		终端开始刷屏了。。。
		127.0.0.1 - - [13/Apr/2018:15:12:46 CST] "GET / HTTP/1.1" 302 0
		- -> /
		127.0.0.1 - - [13/Apr/2018:15:12:46 CST] "GET /Home HTTP/1.1" 302 0
		- -> /Home
		127.0.0.1 - - [13/Apr/2018:15:12:46 CST] "GET /create/Home HTTP/1.1" 200 6600
		- -> /create/Home
		127.0.0.1 - - [13/Apr/2018:15:12:46 CST] "GET /css/gollum.css HTTP/1.1" 200 14923
		http://localhost:4567/create/Home -> /css/gollum.css
		
## 使用中遇到的问题
- 安装后，执行gollum时有报错：`== Someone is already performing on port 4567!`
	
		说明4567的端口被占用，解决方法是：
		使用命令 lsof -i tcp:port（port替换成端口号如4567）查看端口被占用情况
		kill进程，执行kill -9 PID。
		
- gollum 如何退出

		CTRL+C  
