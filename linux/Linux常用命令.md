####参考文档
- [Linux Shell脚本攻略](http://man.linuxde.net/shell-script)
- [Shell正则表达式](http://man.linuxde.net/docs/shell_regex.html)

### cp
	
	将文件file复制到目录/usr/men/tmp下，并改名为file1
	cp file /usr/men/tmp/file1
	
	将目录/usr/men下的所有文件及其子目录复制到目录/usr/zh中
	cp -r /usr/men /usr/zh


### scp
- 基于SSH安全协议的文件传输命令

> 复制local_file 到远程目录remote_folder下

	scp local_file remote_user@host:remote_folder

> 复制local_folder 到远程remote_folder（需要加参数 -r 递归）

    scp –r local_folder remote_user@host:remote_folder


### nc

	服务器文件下载-》本地
	源服务器 nc -l 1234 < 257831_customer.xls
	目标服务器 nc 10.126.125.96 1234 > /Users/natalietu/Webhost/257831_customer.xls

### curl

	curl -H "Content-Type: application/json" -X POST  -d 'a=xxx&b=yyy'  http://xxx.xxx.com/api/v1/loupan
	
	curl -H "Content-Type: application/json" -X PUT  -d '{"auth":{"app_id":"anjuke","time":1463476608,"token":"f7faf4d01a585755e6dbe1b843101ce"},"data":{"id":1,"name":"\u6d4b\u8bd5abc","address":"xxx\u8def"}}'  http://fangapi.ganji.com/api/v1/anjuke/v1/loupan