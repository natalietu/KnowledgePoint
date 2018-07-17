## golang: protobuf

### protoc安装
	$ brew install protobuf
	
### protoc-gen-go 安装
	$ go get -u github.com/golang/protobuf/protoc-gen-go
	package github.com/golang/protobuf/protoc-gen-go: remote origin not found
	解决方案：删掉or重命名{GOPATH}/src/github.com/golang/protobuf，重新执行以上命令
	原因：可能之前没有下载完整导致的
	
### 创建.proto文件并编译
	编译：
	$ protoc --go_out=. *.proto
	
	
	
	
##### 参考文档
- [golang/protobuf](https://github.com/golang/protobuf)
- [在Golang中使用protobuf](https://my.oschina.net/ifraincoat/blog/510971)
- [Protobuf学习入门](https://www.cnblogs.com/autyinjing/p/6495103.html)