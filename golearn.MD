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
可用于const下的递增枚举
```
const (
    a = iota    //0
    b           //1
    c           //2
    d = iota * 2 + 1    //3 * 2 + 1 = 7
)
```

### 多返回值三种写法
```
//方法一：匿名
func test1(a string, b int) (int, int) {
    c := 100
    d := 200
    return c, d
}

//方法二：非匿名
func test2(a string, b int) (r1 int, r2 int) {
    r1 = 100
    r2 = 200
    return
}

//方法三： 
func test3(a string, b int) (r1, r2 int){
    r1 = 100
    r2 = 200
    return
}
```

### 导包路径和init方法调用
1. 执行顺序
    1. import pkg1(递归解析)
    2. const ...
    3. var ...
    4. init() ...
    5. main() ...
    6. Exit

2. 示例多包结构
\$GOPATH/GolangStudy/5-init/
* lib1
    * lib1.go
* lib2
    * lib2.go
* main.go
```
//lib1.go
package lib1
import "fmt"

func Lib1Test() {
    fmt.Println("lib1Test")
}

func init() {
    fmt.Println("lib1 init")
}
```

```
//lib2.go
package lib2
import "fmt"

func Lib2Test() {
    fmt.Println("lib2Test")
}

func init() {
    fmt.Println("lib2 init")
}
```

```
package main
import (
    // 未使用module管理前导入相对路径
    "GolangStudy/5-init/lib1"
    "GolangStudy/5-init/lib2"
)

func main() {
    lib1.Lib1Test()
    lib2.Lib2Test()
}
```

执行结果：先init后Test

### import匿名与别名导包
不使用lib1函数但是想执行内部init方法：匿名导包
```
package main
import (
    // 未使用module管理前导入相对路径
    _ "GolangStudy/5-init/lib1" //匿名
    mylib2 "GolangStudy/5-init/lib2"  //别名
    //. "GolangStudy/5-init/lib2" -> lib2Test() 直接导入（不安全）
)

func main() {
    mylib2.Lib2Test()
}
```

### golang指针
```
func swap(pa *int, pb *int){
    var temp int
    temp = *pa
    *pa = *pb
    *pb = temp
}

// main
a := 10
b := 20
swap(&a, &b)
```

### defer语句调用顺序
defer语句在**生命周期结束**前调用，后进先出。
```
func deferfuc() int {
    fmt.Println("defer func called")
    return 0
}

func returnfuc() int {
    fmt.Println("return func called")
    return 0
}

func returnAndDefer() int {
    defer deferfuc()
    return returnfuc()
}

func main() {
    returnAndDefer()
}

输出内容：
defer func called
return func called
```

### 数组
1. 定义数组
```
//方法一：指定长度
var a [5]int

//方法二：根据元素个数推断长度
b := [3]int{1, 2, 3}

//遍历
for i := 0; i < len(b); i++ {
    fmt.Println(b[i])
}

for index, value := range b {
    fmt.Println(index, value)
}

//传参时必须传递完整（值传递）
func printA(a [5]int) {
    fmt.Println(a)
}
```
2. 定义slice



