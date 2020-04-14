# Go语言介绍和环境安装

### 1.Go语言介绍

> Go 语⾔是有⾕歌推出的一⻔编程语言。
> Go 是⼀个开源的编程语言，它能让构造简单、可靠且高效的软件变得容易。

#### Go 语言主要开发者

> Go 是从2007年末由Robert Griesemer, Rob Pike, Ken Thompson主持开发，后来还加入了了Ian Lance Taylor, Russ Cox等人，并最终于2009年年11月开源。

#### Go语言的几个⾥程碑

* 2007.09 Go语言设计草稿在白板上诞生
* 2008.01 Ken开发了了Go语言编译器把Go代码编译成C代码 
* 2009 Go语言诞⽣生
* 2016.01 Go 1.5 版本中实现了了自举，不再依赖C编译器 
* 2017.02 Go 1.8 版本发布，大幅度提升GC效率

#### Go 语言特点

* 简洁、快速、安全
* 并行、有趣、开源
* 内存管理、数组安全、编译迅速

#### Go 语⾔⽅方向
* ⽹络编程领域
* 区块链开发领域
* ⾼性能分布式系统领域

### 2.环境安装

> * Go 语⾔的环境安装:

	⁃	 Go安装包下载⽹网址(Go语⾔中文网):https://studygolang.com/dl 
	⁃	 根据操作系统选择对应的安装包(Mac、Linux、Windows)。 
	⁃	 不要在安装路径中出现中文。
	
> * Go 语⾔开发⼯工具: GoLand

	⁃	GoLand 是 Jetbrains 家族的 Go 语言 IDE，有 30 天的免费试用期。 
	⁃	下载安装网址:https://www.jetbrains.com/go/ 
	⁃	根据操作系统选择对应的安装包(Mac、Linux、Windows)下载对应的软件。
	
> * LiteIDE

	⁃	LiteIDE 是⼀一款开源、跨平台的轻量级 Go 语⾔集成开发环境(IDE)。 
	⁃	下载安装网址:https://sourceforge.net/projects/liteide/files/ 
	⁃	根据操作系统选择对应的安装包(Linux、Windows)下载对应的软件。
	⁃	其他开发⼯工具 ( 在IDE安装插件 ) Eclipse
	⁃	VS Code
	
# Go语言程序

### 1.工作区

> * ⼯作区是Go中的一个对应于特定⼯工程的⽬目录，其包括src，pkg，bin三个目录
    * src:⽤于以代码包的形式组织并保存Go源码⽂文件。(⽐比如:.go .c .h .s等)
    * pkg:⽤于存放经由go install命令构建安装后的代码包(包含Go库源码⽂件)的“.a”归 档⽂件。
    * bin:与pkg⽬录类似，在通过go install命令完成安装后，保存由Go命令源码文件生成的可执行⽂件。
    * 目录src⽤于包含所有的源代码，是Go命令行工具⼀个强制的规则，而pkg和bin则⽆需 ⼿动创建，如果必要Go命令行工具在构建过程中会自动创建这些⽬录。
    * 只有当环境变量量 GOPATH 中只包含一个⼯作区的⽬录路径时，go install命令才会把命令源码安装到当前⼯作区的bin⽬目录下。若环境变量 GOPATH 中包含多个工作区的⽬录 路径，像这样执行go install命令就会失效，此时必须设置环境变量GOBIN。
    
>   ```shell
        go install: no install location for .go files listed on command line(GOBIN not set)
    ```
        
> * 工作区如何设置（linux mac）
    * 工作区设置路径为环境变量的GOPATH
    
>   ```shell
         #mac设置GOPATH
        vim .bash_profile || .zshrc
        export GOPATH=/Users/guodongsheng/Desktop/WorkSpace/GoCode
    ```
> * 工作区如何设置（window）
    * ⼯作区设置路径为环境变量中的GOPATH 
    
>   ```
        我的电脑 --》 右击属性 --》 高级统设置 --》 环境变量 --》 系统环境变量 --》 添加GOPATH
    ```  
    
### 2.起步Hello World

> 使用Goland开发第一个GO程序
> ```go
    package main
    import "fmt"
    func main () {
        fmt.Println("Hello, World!") 
    }
> ```
### 3.编译过程
> 要执行Go语言代码可以使用命令或者IDE来完成编译
> 命令如下：
>>  * 编译命令 go build helloWorld.go
>>  * 编译并运行命令 go run helloWorld.go

### 4.常用命令行
> go help 
>> * 获取对应命令的帮助文档，可以获取到对应命令的作用以及对应参数

>> ```go
      go help build
>> ```

> go version 
>> * 获取系统安装go语⾔版本号
 
> go build
>> * 编译项目，使其打包成可运行程序，配合参数可以进行交叉编译
>> * 标准格式
    * go build [-o output] [-i] [build flags] [packages]
    * -o 参数决定了编译后⽂件名称，例例如我们要程序main.go编译后程序名为hello，我们 可以执⾏以下命令
 
>>```go
    go build -o hello main.go
```
>> * -i install 安装作为目标的依赖关系的包(⽤于增量编译提速)，⼀般很少使用
>> * 编译参数⼀一般并不会添加，以下列举⼏个，详细信息可以使用go help build 获取

>> 
| 附件参数 | 备注                     |
|------|------------------------|
| -v   | 编译时显示包名                |
| -p n | 开启并发编译，默认情况下该值为CPU逻辑核数 |
| -a   | 强制重新构建                 |
| -n   | 打印编译时会用到的所有命令，但不真正执行   |
| -x   | 打印编译时会用到的所有命令          |
>> * packages
    * 所编译的包名，如果不填写默认为编译当前路径下的入⼝文件，⽂件名称默认为当前⽂件夹名称

> 交叉编译
> * go语⾔向下支持C语言，可以在go语言中直接编写C语言代码
> * 但是在编译时，必须支持C语言
> * Mac上编译Linux可执行二进制文件

>```go
    CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go
```

> * Mac上编译Windows可执⾏二进制文件

>```go
    CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
```

> * Linux上编译Mac可执⾏二进制文件

>```go
    CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build main.go
```

> * Linux上编译Windows可执⾏二进制文件

>```go
    CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
```

> * Windows上编译Mac可执⾏二进制文件

>```go
    SET CGO_ENABLED=0 SET GOOS=darwin SET GOARCH=amd64 go build main.go
```

> * Windows上编译Linux可执⾏二进制⽂件

>```go
    SET CGO_ENABLED=0 SET GOOS=linux SET GOARCH=amd64 go build main.go
```

> * 交叉编译参数含义
    * CGO_ENABLED 是否使用cgo编译，0为不使用，1为使用，使用cgo进行交叉编译时需 要编译机器安装对应的cgo程序
    * GOOS ⽬标操作系统标识，windows对应Windows操作系统exe可执行⽂件，darwin 对应Mac可执行文件，linux对应Linux可执行文件，freebsd对应UNIX系统
    * GOARCH ⽬标可执行程序操作系统构架，包括 386，amd64，arm
    * go build 后接所编译程序的⼊口文件

> go install
> * 编译并安装项⽬
> * 标准格式 
    * go install [-i] [build flags] [packages]
    * 参数与⽤法与go build类似
    
> go doc
> * 获取go函数帮助文档
> * 命令行形式获取某个包的介绍以及包下所有可用的公共方法列表

>```go
    go doc strconv
```

> * 命令行形式获取某个方法的文档

>```go
    go doc strconv.Itoa
```

> * 使⽤用⽹页形式查看帮助文档

>```go
    godoc -http=localhost:6060
```

> * 在浏览器中输入:http://localhost:6060/ 可以查看对应的文档信息

> go env
> * 查看当前系统内go相关的环境变量信

> go test
> * Go语⾔自带的测试工具，会自动读取源码⽬录下面名为 *_test.go 的⽂件，⽣成并运⾏测试 用的可执行文件
> * 原则
    * ⽂件名必须是 _test.go 结尾的，这样在执行 go test 的时候才会执行到相应的代码
    * 必须 import testing 这个包
> * 可执⾏测试
    * 原则
        * 所有的测试⽤例函数必须是 Test 开头
        * 测试⽤例会按照源代码中写的顺序依次执行
        * 测试函数 TestXxx() 的参数是 testing.T ，我们可以使用该类型来记录错误或者是测试状态
        * 测试格式: func TestXxx (t *testing.T) , Xxx 部分可以为任意的字母数字的组合，但是首字母不能是小写字母[a-z]
        * 函数中通过调用 testing.T 的 Error, Errorf, FailNow, Fatal, FatalIf 方法，说明测试不通过，调用 Log 方法用来记录测试的信息。
    * 创建测试文件class_test.go

>    ```go
            package main
            import (
              "testing"
              "time"
            )
            func TestHelloWorld(t *testing.T)  {
              timestamp := time.Now().Unix()
              t.Log(timestamp)
            }
    ```
    
            
            
> * 执⾏命令行查看测试结果

>```go
    go test -v class_test.go 结果
```

> * 结果

>```go    === RUN   TestHelloWorld
    --- PASS: TestHelloWorld (0.00s)
        class_test.go:10: 1571237717
    PASS
    ok   command-line-arguments  0.005s
```

>```go    + === RUN TestHelloWorld 表示开始运⾏行行名叫 TestHelloWorld 的测试⽤用例
    + --- PASS: TestHelloWorld (0.00s) 表示已经运⾏完 TestHelloWorld 的测试⽤例， PASS 表示当前⽅法测试成功，如果是FAIL 表示当前⽅法测试失败，时间表示这个测试⽤例所用的时间
    + ok command-line-arguments 0.005s 表示整体测试结果，ok 表示所有被测试⽅法测试通过，如果是FAIL则表示测试失败，command-line-arguments 是测试⽤例需要用到的⼀个包 名，0.005s 表示测试花费的时间。
```
    