## golang: dep

### 安装
	$ go get -u github.com/golang/dep/cmd/dep

### 验证安装
	$ dep
	
	Dep is a tool for managing dependencies for Go projects

	Usage: "dep [command]"

	Commands:

  	init     Set up a new Go project, or migrate an existing one
  	status   Report the status of the project's dependencies
  	ensure   Ensure a dependency is safely vendored in the project
 	version  Show the dep version information

	Examples:
  	dep init                               set up a new project
  	dep ensure                             install the project's dependencies
  	dep ensure -update                     update the locked versions of all dependencies
  	dep ensure -add github.com/pkg/errors  add a dependency to the project

	Use "dep help [command]" for more information about a command.
	
	出现以上信息，代表安装成功！
	
	
- 参考文档
	- [Golang官方依赖管理工具：dep](https://studygolang.com/articles/10589)
	