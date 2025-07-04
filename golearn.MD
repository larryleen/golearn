# golang学习笔记
## go的前置学习
### go安装
选择镜像：https://golang.google.cn/dl/
### go源码包结构
1. go/src
go代码源码
![go/scr结构](image.png)
2. go/bin
go指令源码
### 环境配置
vim ~/.bashrc

export GOROOT=/usr/local/go

export GOPATH=/Users/wps/go

export PATH=$PATH:\$GOROOT/bin:$GOPATH/bin

source ~/.bashrc

### 验证
go version
### 验证环境变量
echo $GOROOT

echo $GOPATH

echo $PATH

### 项目构建
在go/src下构建项目文件夹：GolangStudy/firstGolang

## go语法
### 代码结构
```
//分号可选（默认不使用）
package main //程序包名
import (
    "fmt"
)
//main函数
func main() {
    fmt.Println("Hello World!")
}
```

### golang编译
1. 编译
```
golang build 项目名.go
```
生成.exe可执行文件。
2. 编译并运行
```
go run 项目名.go
```
 
