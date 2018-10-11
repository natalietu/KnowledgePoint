## node js

> 1、[安装node.js](https://nodejs.org/zh-cn/)
> 
> 2、npm换成淘宝的镜像地址
> 
> NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题
	
	$ npm get registry
	$ https://registry.npmjs.org/
	设成淘宝的
	$ npm config set registry http://registry.npm.taobao.org/
	

> 3、安装cnpm
	
	$ npm install -g cnpm --registry=https://registry.npm.taobao.org
	npm WARN deprecated socks@1.1.10: If using 2.x branch, please upgrade to at least 2.1.6 to avoid a serious bug with socket data flow and an import issue introduced in 2.1.0
	npm WARN checkPermissions Missing write access to /usr/local/lib/node_modules
	npm ERR! path /usr/local/lib/node_modules
	npm ERR! code EACCES
	npm ERR! errno -13
	npm ERR! syscall access
	npm ERR! Error: EACCES: permission denied, access '/usr/local/lib/node_modules'
	npm ERR!  { Error: EACCES: permission denied, access '/usr/local/lib/node_modules'
	npm ERR!   stack: 'Error: EACCES: permission denied, access \'/usr/local/lib/node_modules\'',
	npm ERR!   errno: -13,
	npm ERR!   code: 'EACCES',
	npm ERR!   syscall: 'access',
	npm ERR!   path: '/usr/local/lib/node_modules' }
	npm ERR!
	npm ERR! Please try running this command again as root/Administrator.

	npm ERR! A complete log of this run can be found in:
	npm ERR!     /Users/natalietu/.npm/_logs/2018-08-30T07_56_15_086Z-debug.log
	
	
	重新尝试
	$ npm install -g cnpm --registry=https://registry.npm.taobao.org
	npm WARN deprecated socks@1.1.10: If using 2.x branch, please upgrade to at least 2.1.6 to avoid a serious bug with socket data flow and an import issue introduced in 2.1.0
	/usr/local/bin/cnpm -> /usr/local/lib/node_modules/cnpm/bin/cnpm
	+ cnpm@6.0.0
	added 626 packages in 23.847s
	
	这次成功了
	$ cnmp -v
	cnpm@6.0.0 (/usr/local/lib/node_modules/cnpm/lib/parse_argv.js)
	npm@6.4.1 (/usr/local/lib/node_modules/cnpm/node_modules/npm/lib/npm.js)
	node@8.11.4 (/usr/local/bin/node)
	npminstall@3.11.0 (/usr/local/lib/node_modules/cnpm/node_modules/npminstall/lib/index.js)
	prefix=/usr/local
	darwin x64 14.5.0
	registry=https://registry.npm.taobao.org

> 4、安装webpack
	
	$ sudo cnpm install webpack -g
	
> 5、全局安装vue-cli
	
	$ sudo cnpm install -g vue-cli
	
> 6、创建项目 or clone项目
 
 
 - 创建基于webpack的新项目
 	
 		$ vue init webpack zyt
 		zyt：项目名称	
 	
 - clone项目
 		
 		$ git clone git@gitlab.xxx.com:zyt/web.git zyt
 		
> 7、安装项目依赖
 	
 	$ cd zyt
 	$ cnpm install
 	
> 8、compile	
	
	$ npm run dev
	
	
	
	
 	
 	
 	
	