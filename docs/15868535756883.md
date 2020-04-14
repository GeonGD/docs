# TypeScript内置类型

### Partial
***
将类型T的所有属性标记为可选属性
``` ts
    type Partial<T> = {
         [P in keyof T]?: T[P];
    }
```

使用场景
```ts
    interface AccountInfo {
        name: string
        email: string
        age: number
        vip: 0 | 1  // 1 是vip，0 是非vip
    }
    
    // 当我们需要渲染一个账号表格是，我们需要定义
    const accountList = AccountInfo[] = []
    
    // 但当我们需要查询过滤账号信息，需要通过表单，
    // 但明显我们可能并不一定需要用到所有属性进行搜索，此时可以定义
    const model: Partial<AccountInfo> = {
        name: "",
        vip: undefind
    }
```

###Required
***
与Partial相反，Required将类型T的所有属性标记为必选属性
```ts
    type Required<T> = {
        [P in Keyof T]-?: T[P]
    }
```

### Readonly
***
将所有属性标记为 reafonly， 即不可修改
```ts
    type Readonly<T> = {
        readonly [P in keyof T]: T[P]
    }
```

### Pick<T, K>
***
从T中过滤出属性K
type Pick<T, K extends keyof T> = {
    [P in K]: T[P]
}

使用场景
```ts
    interface AccountInfo {
        name: string 
        email: string 
        age: number 
        vip?: 0 | 1 // 1 是vip ，0 是非vip
    }
    
    type CoreInfo = Pick<AccountInfo, "name" | "email">
    /* 
    { 
      name: string
      email: stirng
    }
    */
```

### Record<K, T>
***
标记对象的key value类型
```ts
    type Record<K extends keyof any, T> = {
        [P in K]: T
    }
``` 

使用场景
```ts
    interface AccountInfo {
        name: string 
        email: string 
        age: number 
        vip?: 0 | 1 // 1 是vip ，0 是非vip
    }
    
    // 定义 学号（key）- 账号信息（value）的对象
    const accountMap: Record<number, AccoountInfo> = {
        1001: {
            name: "",
            email: ""
        }
    }
    
    const userInfo: Record<"name" | "email", string> = {
        name: "",
        email: "”
    }
```

```ts
    // 复杂的类型推断
    function mapObject<K extends string | number, T, U>(obj: Record<K, T>, f: (x: T) => U): Record<K, U>
    
    const names = {foo: "hello", bar: "world", baz: "bye"}
    // 此处推断K，T值为string，U为number
    const lengths = mapObject(names, s => s.length)
    // { foo: number, bar: number, baz: number }
```

### Exclude<T, U>，Omit<T, K>    
***
移除T中的U属性
```ts
    type Exclude<T, U> = T extends U ? never : T;
```

使用场景
```ts
    // "a" | "d"
    type A = Exclude<'a'|'b'|'c'|'d', 'b'|'c'|'e'>
    // 乍一看好像这个没啥卵用，但是，我们通过一番操作，之后就可以得到 Pick 的反操作：
    type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>
    
    interface AccountInfo {
        name: string 
        email: string 
        age: number 
        vip?: 0 | 1 // 1 是vip ，0 是非vip
    }
    
    type NonCoreInfo = Omit<AccountInfo, 'name' | 'email'>
    /*
    {
      age: number 
      vip: 0|1,
    }
    */
```

### Extract<T, U>
***
Exclude的反操作，取T，U两者的交集属性
```ts
    type Extract<T, U> = T extends U ? T : never;
```

使用场景
```ts
    // 'b'|'c'
    type A = Extract<'a'|'b'|'c'|'d' ,'b'|'c'|'e' >  
```
### NonNullable
***
排除类型T的null和undefind属性
```ts
    type NonNullable<T> = T extends null | undefined ? never : T
```

使用场景
```ts
    type A = string | number | undefined
    type B = NonNullable<A> // string | number
    
    function fuc<T extends string | undefined>(x: T, y: NonNullable<T>) {
        let s1: string = x; // Error,x可能为undefind
        let s2: string = y; // 正确
    }
```

### Parameters
***
获取一个函数的所有参数
```ts
    // 此处使用 infer P 将参数定为推断类型
    // T符合函数特征时，返回参数类型，否则返回never
    type Parameters<T extends (...arg: any) => any> = T extends (...arg: infer P) => any ? P : never;
```

使用场景
```ts
    interface Ifunc {
        (person: IPerson, count: number): boolean
    }
    
    type P = Parameters<Ifunc> // [IPerson, number]
    const person01: P[0] = {
      // ...
    }
```
另一种使用场景是，快速获取未知函数的参数类型
```ts
    import {somefun} from 'somelib'
    // 从其他库导入的一个函数，获取其参数类型
    type SomeFuncParams = Parameters<typeof somefun>
    
    // 内置函数
    // [any, number?, number?]
    type FillParams = Parameters<typeof Array.prototype.fill>
```

### ConstructorParameters
***
类似于Parameters<T>, ConstructorParameters 获取一个类的构造函数参数
```ts
    type ConstructorParameters<T extends new (...args: any) => any> = T extends new (...args: infer P) => any ? P : never;
```

使用场景
```ts
    // string | number | Date 
    type DateConstrParams = ConstructorParameters<typeof Date>
```

### ReturnType
***
获取函数类型T的返回类型
```ts
    type ReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer R ? R : any;
```

### InstanceType
***
获取一个类的返回类型
```ts
    type InstanceType<T extends new (...args: any) => any> = T extends new (...args: any) => infer R ? R : any;
```


