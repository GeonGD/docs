# TypeScript自定义常用类型

### Weaken
***
使用 typescript 有时候需要重写一个库提供的 interface 的某个属性，但是重写 interface 有可能会导致冲突：
```ts
    interface Test {
      name: string
      say(word: string): string
    }
    
    interface Test2  extends Test{
      name: Test['name'] | number
    }
    // error: Type 'string | number' is not assignable to type 'string'.
```
那么可以通过一些 type 来曲线救国实现我们的需求：
```ts
    // 原理是，将 类型 T 的所有 K 属性置为 any，
    // 然后自定义 K 属性的类型，
    // 由于任何类型都可以赋予 any，所以不会产生冲突
    type Weaken<T, K extends keyof T> = {
      [P in keyof T]: P extends K ? any : T[P];
    };
    
    
    interface Test2  extends Weaken<Test, 'name'>{
      name: Test['name'] | number
    }
    // ok
```    

### 数组 转换 成 union
***
有时候需要
```ts
    const ALL_SUITS = ['hearts', 'diamonds', 'spades', 'clubs'] as const; // TS 3.4
    type SuitTuple = typeof ALL_SUITS; // readonly ['hearts', 'diamonds', 'spades', 'clubs']
    type Suit = SuitTuple[number];  // union type : 'hearts' | 'diamonds' | 'spades' | 'clubs'
```

根据 enum 生成 union
*   enum 的 key 值 union   
    ```ts
        enum Weekday {
          Mon = 1
          Tue = 2
          Wed = 3
        }
        type WeekdayName = keyof typeof Weekday // 'Mon' | 'Tue' | 'Wed'
    ```
    
*   enum 无法实现value-union , 但可以 object 的 value 值 union
    ```ts
        const lit = <V extends keyof any>(v: V) => v;
        const Weekday = {
          MONDAY: lit(1),
          TUESDAY: lit(2),
          WEDNESDAY: lit(3)
        }
        type Weekday = (typeof Weekday)[keyof typeof Weekday] // 1|2|3
    ```
 
### PartialRecord
***
Record 类型，我们会常用到
```ts
    interface Model {
        name: string
        email: string
        id: number
        age: number
    }
    
    // 定义表单的校验规则
    const validateRules: Record<keyof Model, Validator> = {
        name: {required: true, trigger: `blur`},
        id: {required: true, trigger: `blur`},
        email: {required: true, message: `...`},
        // error: Property age is missing in type...
    }
```
这里出现了一个问题，validateRules 的 key 值必须和 Model 全部匹配，缺一不可，但实际上我们的表单可能只有其中的一两项，这时候我们就需要：
```ts
    type PartialRecord<K extends keyof any, T> = Partial<Record<K, T>>

    const validateRules: PartialRecord<keyof Model, Validator> = {
       name: {required: true, trigger: `blur`} 
    }
```
这个例子组合使用了 typescript 内置的 类型别名 Partial 和 Partial。

### Unpacked
***
解压抽离关键类型
```ts
    type Unpacked<T> =
        T extends (infer U)[] ? U :
        T extends (...args: any[]) => infer U ? U :
        T extends Promise<infer U> ? U :
        T;
    
    type T0 = Unpacked<string>;  // string
    type T1 = Unpacked<string[]>;  // string
    type T2 = Unpacked<() => string>;  // string
    type T3 = Unpacked<Promise<string>>;  // string
    type T4 = Unpacked<Promise<string>[]>;  // Promise<string>
    type T5 = Unpacked<Unpacked<Promise<string>[]>>;  // string
```

### DeepPartial
***
递归 Partial
```ts
    type RecursivePartial<T> = {
      [P in keyof T]?:
        T[P] extends (infer U)[] ? RecursivePartial<U>[] :
        T[P] extends object ? RecursivePartial<T[P]> :
        T[P];
    };
```

### DeepRequired
***
递归 Required
```ts
    type DeepRequired<T> = {
      [P in keyof T]-?:   // 给最顶层的 key 去除 `?:`
      T[P] extends ((infer U)[]|undefined) ? DeepRequired<U>[] :   // 如果 value 值是数组，那么递归数组内每一项的类型值
      T[P] extends (object|undefined) ? DeepRequired<T[P]> :  // 如果 value 还是object，递归值类型
      T[P]  // 其他类型，不进行操作
    }
```