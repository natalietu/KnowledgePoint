Mac下golang环境配置安装
====================
- 参考文档
	- [MacOs下安装golang](https://blog.csdn.net/skytoup/article/details/48877839)
	- [IntelliJ IDEA开发golang环境配置](https://studygolang.com/articles/6011)
	- [Go开发：Mac上安装Go环境和VsCode](https://www.jianshu.com/p/0b2b80336d47)
	
### 安装
#### 1. 尝试brew安装
	
	brew install go
	......
	Failed to connect to go.googlesource.com port 443: Operation timed out
	看样子还是得翻墙

#### 2. 安装包下载安装
> 国内一个go社区[下载安装包](https://golangtc.com/download)

> 安装版：go1.9.2.darwin-amd64.pkg，下载完成之后，直接双击打开安装即可
>
> 压缩版：go1.9.2.darwin-amd64.tar.gz，下载完成后需要解压，然后自己移动到要存放的路径下，并且配置环境变量等信息。
	
### 设置环境变量
	$ vim ~/.bashrc 添加设置
	
	# go
	export GOROOT=/usr/local/go #默认安装都是这个路径
	export GOPATH=/Users/natalietu/Webhost/myGolang #日常开发的根目录
	export GOBIN=$GOPATH/bin		#GOPATH下的bin目录
	export PATH=$PATH:$GOROOT/bin:$GOPATH/bin  #GOPATH bin 以及GOPATH root bin
	
	$ source ~/.bashrc
	$ go version
	go version go1.9.2 darwin/amd64  #安装配置成功
	
- GOPATH：日常开发的根目录，这个目录用来存放Go源码，Go的可运行文件，以及相应的编译之后的包文件。所以，这个目录下面有三个子目录：src、bin、pkg
	- `src` 存放源代码（比如：.go .c .h .s等）
	- `pkg` 编译后生成的文件（比如：.a）
	- `bin` 编译后生成的可执行文件

### Hello World
> 学习一门新语言，输出hello world是一种情怀般的开始

> GOPATH目录下新建一个hello.go文件
	
	package main
	import "fmt"
	func main() {
   		fmt.Printf("hello, world!\n")
	}
	
	保存后执行 go run hello.go
	输出：hello, world!  #成功



