# typescript 中的 interface 和 type 到底有什么区别

### 相同点
***
#####都可以描述一个对象或函数
interface
```ts
    interface User {
        name: string
        age: number
    }
    
    interface SetUser {
        (name: string, age: number): void
    }
```

type 
```ts
    type User = {
        name: string
        age: number  
    }
    
    type SetUser = (name: string, age: number): void
```

##### 拓展与交叉类型（extends Intersection Types）
interface可以extends，但type是不允许extends和implement的。但是type可以通过交叉类型实现interface的extends行为，并且两者并不是相互独立的，也就是说interface可以extends type，type也可以与interface类型交叉

interface extends interface
```ts
    interface Name {
        name: string
    }
    
    interface User extends Name {
        age: number
    }
```

type 与 type 交叉
```ts
    type Name = {
        name: string
    }
    
    type User = Name & {age: number}
``` 

interface extends type
```ts
    type Name = {
        name: string
    }
    
    interface User extends Type {
        age: number
    }
```

type 与 interface 交叉
```ts
    interface Name {
        name: string
    }
    
    type User = Name & { age: number }
```

### 不同点
***
##### type可以，interface不行
type可以声明基本类型别名，联合类型，元组等类型
```ts
    // 基本类型别名
    type Name = string
    
    // 联合类型
    interface Name { Name: string }
    interface Age { Age: number }
    type User = Name | Age
    
    // 具体定义数组每个位置的类型
    type UserList = [Name, Age]
```

type语句还可以使用typeof获取实例类型进行赋值
```ts
    // 当你想获取一个变量的类型是，使用typeof
    let div = document.createElement("div");
    type copyDiv = typeof div;
```

其余
```ts
    type StringOrNumber = number | string
    type Text = string | { text: string }
    type NameLookup = Dictionary<string, Person>;  
    type Callback<T> = (data: T) => void;
    type Pair<T> = [T, T]
    type Coordinates = Pair<number>
    type Tree<T> = T | { left: Tree<T>, right: Tree<T>}
```

##### interface可以而type不行
interface声明合并
```ts
    interface User { name: string }
    
    interface Usre { age: number}
    
    /*
        User接口为
        {
            Name: string
            age: number
        }
    */
```

 