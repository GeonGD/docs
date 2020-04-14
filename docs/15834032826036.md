# Go关键字

### Go语言关键字

| 关键字         | 作用   | 一级分类 | 二级分类    | 三级分类  |
|-------------|------|------|---------|-------|
| var         | 变量声明 | 基本结构 | 变量与常量   |       |
| const       | 常量声明 | 基本结构 | 变量与常量   |       |
| package     | 包声明  | 基本结构 | 包管理     |       |
| import      | 包引用  | 基本结构 | 包管理     |       |
| func        | 函数声明 | 基本组件 | 函数      |       |
| return      | 函数返回 | 基本组件 | 函数      |       |
| interface   | 接口   | 基本组件 | 自定义类型   |       |
| struct      | 结构体  | 基本组件 | 自定义类型   |       |
| type        | 定义类型 | 基本组件 | 自定义类型   |       |
| map         |      | 基本组件 | 引用类型    |       |
| range       |      | 基本组件 | 引用类型    |       |
| go          |      | 流程控制 | 并发      |       |
| select      |      | 流程控制 | 并发      |       |
| chan        |      | 流程控制 | 并发      |       |
| if          |      | 流程控制 | 单任务流程控制 | 单分支流程 |
| else        |      | 流程控制 | 单任务流程控制 | 单分支流程 |
| switch      |      | 流程控制 | 单任务流程控制 | 多分支流程 |
| case        |      | 流程控制 | 单任务流程控制 | 多分支流程 |
| default     |      | 流程控制 | 单任务流程控制 | 多分支流程 |
| fallthrough |      | 流程控制 | 单任务流程控制 | 多分支流程 |
| for         |      | 流程控制 | 单任务流程控制 | 循环流程  |
| break       |      | 流程控制 | 单任务流程控制 | 循环流程  |
| continue    |      | 流程控制 | 单任务流程控制 | 循环流程  |
| goto        |      | 流程控制 | 单任务流程控制 |       |
| defer       |      | 流程控制 | 延时流程控制  |       |

### 关键字使用方式
> * var
    定义变量
    
>    ```go        //⽤于声明变量，声明⽅方式包括以下⼏几种:
        var name1 int64
        var name2 = 15 //int 类型 //在func内可以使用简写等价，但是简写不可⽤用于声明全局变量，即不能用于func外 name3 := 15
        name4,name5,name6 := "a","b","c" //同时赋值给多个变量
    ```

> * const 
    定义常量或常量集
    
>   ```go        //⽤于声明常量，可以不用声明类型，对于int类型的常量可以用于int，int64等计算 package main
        import "fmt" 
        //全局常量 
        const =14
        func main()  {
            var b = 16 //int
            var c = int64(20) //int64
            d := a + b
            e := a + c
            fmt.Println("d",d)
            fmt.Println("e",e)
        }
    ```
    
> * package
    ⽤于包声明，在Go中包的概念⼀般指同一⽂件夹下的的文件，与其它部分语言每个文件可以⾃己 就是一个包不同。 包名可以与文件夹名称不同，但是⼀般建议相同(如果文件夹带有版本号情况 可以忽略版本号部分) 需要写在程序的可执行⽂件的第一行。 go //这里是注释 package main
    
> * import 
    ⽤于包的引用，引⽤路径为工作区下的相对路径 如果程序内引用了两个不同路径下相同的包名， 可以通过设定别名的方式进行区分 如果程序内需要用到引用包的初始化或者接口实现，但是没有 显示调用，则需要使用_来进行区分
    
>   ```go        package main
        import (
        "context"
        echoContex "echo/context"
        _ "notuse/context"
        )
        func main() {
            context.Background()
            echoContex.text()
        }
    ```
    
> * func/return
    函数方法体声明 返回参数如果为⼀个且不带参数名，可以不用写括号 返回参数超过一个或者带参数名则需要⽤括号扩起 + return 函数方法体返回 如果函数返回参数带有参数名称则返回时不需要 将每个参数显示返回，否则需要显示返回
    
>   ```go        package main
        //⽆入参，⽆出参
        func main() { 
            demo1("hello") 
            demo2("hello",1,2,3) 
            intArr := []int64{1,2,3} 
            demo2("hello",intArr...) 
            demo3()
            demo4()
            demo5()
            demo6()
        }
        //有固定入参，⽆出参数
        func demo1(name string) { 
            return
        }
        //⽆固定入参，无出参数
        func demo2(name string, params ...int64) { 
            return
        }
        //⽆入参，单参数无名称 
        func demo3() int64 {
            return 0 
        }
        //⽆入参，单参数有名称
        func demo4() (age int64) { 
            return
        }
        //⽆入参，多参数无名称
        func demo5() (int64,string) { 
            return 0,""
        }
        //⽆入参，多参数有名称
        func demo6() (age int64,name string) { 
            return
        }
    ```
    
> * type / interface / struct
> * type 结构体或者接口的声明
> * interface 接⼝，可以存放任意格式数据，也可以定义接口方法 struct 结构体
> * struct 结构体

>   ```go        package main
        import "fmt"
        type demoI interface {
            funDemo1(string)int
            funDemo2(int64)string
        }
        //定义结构体实现接口方法 
        type demoS1 struct {}
        func (d *demoS1) funDemo1(string)int {
            return 0
        }
        func (d *demoS1) funDemo2(int64)string {
            return ""
        }
        func main() {
             s := &demoS1{}
             demo3(s)
        }
        //接受参数为接⼝口类型
        func demo3(d demoI)  {
            v,t := d.(*demoS1)
            fmt.Println(v)
              fmt.Println(t)
            }
        }
    ```
    一个 interface 被多种类型实现时，需要区分 interface 的变量究竟存储哪种类型的值。
go 可以使⽤用 comma, ok 的形式做区分 value, ok := em.(T):em 是 interface 类型的变量。
T代表要断言的类型，value 是 interface 变量存储的值，ok 是 bool 类型表示是否为该断⾔的类型 T ​如果是按 pointer 调用，go 会自动进行转换，因为有了指针总是能得到指针指向的值 ​ 如果是 value 调用，go 将⽆无从得知 value 的原始值是什么，因为 value 是份拷贝。go 会把指针进行隐式转换得到 value，但反过来则不行。

> * map
    map 是 Go 内置关联数据类型(在⼀些其他的语言中称为"哈希"或者"字典")

>   ```go        package main
        func main() {
            //仅进行了类型声明，并没有分配内存空间，直接调用则会报错
            var m0 map[string]int
            //声明的同时进行了了内存空间的申请
            m1 := make(map[string]int) 
            //读取数据参数，返回参数可选，一个参数时为返回值，两个参数时第二个参数表示是否存在 
            //如果数据不存在则会返回数据类型的默认数据，但数据为指针类型时则返回nil，不做判断直接使 ⽤的话会panic
            value,h := m1["key"]
            m0 = make(map[string]int,100) 
            //对变量进行初始化，并且预先分配存储空间⼤小
            _,_,_ = m0,value,h
        }
    ```
    
> * range
    与for配合，⽤于遍历，可遍历数组，map，string(string底层存储为byte数组)

> * go
    goroutine异步携程,但是不建议协程处理理⼤文件 , 可以协程来写日志和处理高IO操作，如果是cup密集型运算，则不建议使用

> * select
    * Go 中的⼀个控制结构，类似于⽤于通信的 switch 语句句。每个 case 必须是一个通信操作，要么是发送要么是接收。
    * 如果有同时多个case去处理,比如同时有多个channel可以接收数据，那么Go会伪随机 的选择一个case处理(pseudo-random)。如果没有case需要处理，则会选择default去处理，如果default case存在的情况下。如果没有default case，则select语句句会阻塞， 直到某个case需要处理。

> * chan
    * channel可以理解为⼀个先进先出的消息队列
    * channel⾥面的value buffer的容量也就是channel的容量。channel的容量为零表示这 是一个阻塞型通道，非零表示缓冲型通道[⾮阻塞型通道]。

>   ```go        package main
        var aChan chan int64 //nil chan
        var bChan = make(chan int64) //⽆缓冲
        var cChan = make(chan int64,100) //带缓冲区
    ```
    
> * if / else / switch / case / default / fallthrough
    流程控制语句
    
> * for / break / continue
    循环控制语句
    
> * goto
    goto语句可以无条件地转移到过程中指定的行。 通常与条件语句句配合使用。可用来实现条件转移， 构成循环，跳出循环体等功能。 在结构化程序设计中一般不不主张使用goto语句句， 以免造成程序流程的混乱 goto 对应(标签)既可以定义在for循环前面，也可以定义在for循环后面，当跳转到标签地方时，继续执行标签下面的代码。
    
> * defer
    * defer后面必须是函数调⽤语句，不能是其他语句，否则编译器器会出错。
    * defer后面的函数在defer语句所在的函数执行结束的时候会被调用。

>   ```go         package main
        import "fmt"
        func main() {
            defer fmt.Println("性感法师") 
            defer fmt.Println("在线教学") 
            defer fmt.Println("⽇日薪越亿") 
            defer fmt.Println("轻松就业")
        }
    ```