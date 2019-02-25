# read-Typescript-Documentation

ts文档第一次阅读笔记

## 基本类型

### 类型

* Boolean

* Number

* String

* Array

  两种声明方式：

  ```typescript
  let list:number[] = [1,2,3]
  ```

  or 泛型（<>）

  ```typescript
  let list:Array<number> = [1,2,3]
  ```

  

* Tuple（元组）

  表示指定数量和类型的数组

* Enum（枚举）

  是一个被命名的常数集合

* Any

  支持任何类型的值，但是无法调用`any`类型的方法。

* Void

  表示没有任何类型，常用于函数没有返回值时

* Null

* Undefined

* Never

  表示的是那些永不存在的值的类型（总是会抛出异常或者根本就不会有返回值的函数）

* Object

  非原始类型

_官方文档上只有`Object`和`Array`类型的变量在声明时类型用了首字大写，其余类型全部小写_

### 泛型（elemType）

用`<类型>`的语法来表示类型，如

```typescript
let array :Array<number> = [1,2,3]
```

### 类型断言

已知某个变量的类型时，用来通过编译的方式

```typescript
// 这里是any类型
let someValue: any = "string"

// 断言
let strLength: number = (<string>someValue).length

// as 语法
let strLength: number = (someValue as string).length
```

