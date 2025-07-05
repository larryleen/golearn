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

export PATH=\$PATH:\$GOROOT/bin:$GOPATH/bin

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
    "time"
    //导入多个包
)
//main函数
func main() { //方括号一定在同一行
    fmt.Println("Hello World!") //外部可用函数首字母一定大写

    time.Sleep(1 * time.Second)
}

/*
这是注释
*/

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
 
### 四种变量声明方式

```
//方法一：声明一个变量，默认为0
var a int

//方法二：初始化一个值
var b int = 100

//方法三：自动匹配
var c = 100

//方法四：自动推导
d := 100

//打印类型
fmt.Println("%T", d)
```

### const与iota
```
const (
    a = iota    //0
    b           //1
    c           //2
    d = iota * 2 + 1    //3 * 2 + 1 = 7
)
```

### 