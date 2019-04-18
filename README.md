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

  ```typescript
  let obj:{a:string} = {a:''}
  ```

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

## 变量声明

### let/const

主要讲`let/const`声明与`var`声明的区别，通过`let/const`声明的变量会存在块级作用域（词法作用域），不能在作用域以外访问。

### 解构/展开运算符

解构，重命名属性名，缺省值（为undefined时的默认值）

可以用于函数声明时。

## 接口

为类型命名，为代码定义契约。

### interface

```typescript
interface LabelledValue {
  label: string;
}
```

### 可选

```typescript
interface LabelledValue {
  label?: string;
}
```

### 只读

属性名前加上`readonly`

```typescript
interface LabelledValue {
  readonly label?: string;
}
```

### 字符串索引签名

传入的数据中有多余的属性会进行__额外的属性检查__，造成报错，可以用类型断言解决

```typescript
interface SquareConfig {
    color?: string;
    width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
    // ...
}

// 类型断言
let mySquare = createSquare({ width: 100, opacity: 0.5 } as SquareConfig);
```

or 索引签名，可以带有任意数量的其他属性

`[propName: string]: any`

```typescript
interface SquareConfig {
    color?: string;
    width?: number;
    [propName: string]: any;
}
```

### 描述函数类型

```typescript
interface SearchFunc {
  (source: string, subString: string): boolean;	// （参数属性名及类型）: 返回值类型	
}
```

### 可索引的类型

描述那些能够"通过索引得到"的类型，关于索引签名支持字符串和数值，使用数值的返回值必须和使用字符串一样。

字符串索引签名能够很好的描述`dictionary`模式，确保所有属性与其返回值类型相匹配。

```typescript
interface StringArray {
  [index: number]: string;// 其他属性也必须可以通过number索引返回string的值
}
```

### 类类型

明确的强制一个类去符合某种契约（implements）,描述的是类的公共部分（可以是方法，属性等）

```typescript
interface ClockInterface {
    currentTime: Date;
}

class Clock implements ClockInterface {
    currentTime: Date;
    constructor(h: number, m: number) { }
}
```

类静态部分与实例部分的区别，原文给出的示例是通过两个接口来分别限定类的静态部分（构造函数）和实例部分。此处不是很明白。原代码中并没有表现出接口对`构造函数`的限制。

```typescript
interface ClockConstructor {
    new (hour: number, minute: number): ClockInterface;
}
interface ClockInterface {
    tick();
}

function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
    return new ctor(hour, minute);
}

class DigitalClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() {
        console.log("beep beep");
    }
}
class AnalogClock implements ClockInterface {
    constructor(h: number, m: number) { }	// 没有构造函数也不会报错
    tick() {
        console.log("tick tock");
    }
}

let digital = createClock(DigitalClock, 12, 17);
let analog = createClock(AnalogClock, 7, 32);
```

### 继承接口

可以通过`extends`相互继承，也可继承多个

```typescript
interface Square extends Shape, PenStroke {
    sideLength: number;
}
```

### 混合类型

```typescript
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}
```

### 继承类

当接口继承了一个类类型时，它会继承类的成员但不包括其实现，接口类型只能被这个__类或其子类__所实现（implement）。个人理解就是只有通过继承这个这个类，并且implement接口才能符合规范。



## 类

### class

类的类型、类的构造函数

### 继承

### 修饰符

#### 公共

#### 私有

#### 受保护

#### 只读

#### 存取器（get/set）

#### 静态

### 抽象类

### 可作为接口使用



## 函数

### function

### 函数类型

#### 参数类型

#### 返回值类型

#### 推断类型

### 可选参数

### 默认参数

### 剩余参数

### this

### 重载



## 泛型

### 泛型变量

### 泛型接口

### 泛型类



## 枚举

### 数字枚举

### 字符串枚举

### 异构枚举

### 计算的和常量成员

### 联合枚举与枚举成员的类型？

### 运行时存在

### 反向映射

### 外部枚举



## 类型推论

在没有明确提供类型的地方，类型推论会帮助提供类型。

根据已有的值类型进行推论

### 按上下文归类

反向的推论



## 类型兼容性

ts的类型兼容性是**基于结构子类型的**，是基于类型的组成结构，与名义类型不同，不要求一定要显示声明对应的类型。

### 函数参数双向协变？

### 可选参数及剩余参数

### 函数重载

### 枚举

### 类

### 泛型

### 子类型和赋值