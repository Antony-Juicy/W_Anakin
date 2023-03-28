## 原始数据类型 -：

- Boolean
- Null
- Undefined
- Number
- BigInt
- String
- Symbol

```
注意 undefined 和 null 是所有类型的子类型。也就是说 undefined 类型的变量，可以赋值给 number 类型的变量：
  let num: number = undefined
```

[any 类型](https://www.typescriptlang.org/docs/handbook/basic-types.html#any)

```
let notSure: any = 4
notSure = 'maybe it is a string'
notSure = 'boolean'
// 在任意值上访问任何属性都是允许的：
notSure.myName
// 也允许调用任何方法：
notSure.getName()

```

## 类 - Class

```
<!--  继承的特性 -->

class Dog extends Animal {
bark() {
return `${this.name} is barking`
}
}

const xiaobao = new Dog('xiaobao')
console.log(xiaobao.run())
console.log(xiaobao.bark())

```

```

 <!-- 这里我们重写构造函数，注意在子类的构造函数中，必须使用 super 调用父类的方法，要不就会报错。 -->

class Cat extends Animal {
constructor(name) {
super(name)
console.log(this.name)
}
run() {
return 'Meow, ' + super.run()
}
}
const maomao = new Cat('maomao')
console.log(maomao.run())

```

```
<!-- 类与接口 -->

interface Radio {
switchRadio(trigger: boolean): void;
}
class Car implements Radio {
switchRadio(trigger) {
return 123
}
}
class Cellphone implements Radio {
switchRadio() {
}
}

interface Battery {
checkBatteryStatus(): void;
}

 <!-- 要实现多个接口，我们只需要中间用 逗号 隔开即可。 -->

class Cellphone implements Radio, Battery {
switchRadio() {
}
checkBatteryStatus() {

}
}

```

## [类成员的访问修饰符](https://www.typescriptlang.org/docs/handbook/classes.html#public-private-and-protected-modifiers)

- **public** 修饰的属性或方法是公有的，可以在任何地方被访问到，默认所有的属性和方法都是 public 的
- **private** 修饰的属性或方法是私有的，不能在声明它的类的外部访问
- **protected** 修饰的属性或方法是受保护的，它和 private 类似，区别是它在子类中也是允许被访问的

## interface 接口

```

 <!-- 我们定义了一个接口 Person -->

interface Person {
name: string;
age: number;
}

 <!-- 接着定义了一个变量 viking，它的类型是 Person。这样，我们就约束了 viking 的形状必须和接口 Person 一致。 -->

let viking: Person ={
name: 'viking',
age: 20
}

 <!-- 有时我们希望不要完全匹配一个形状，那么可以用可选属性： -->

interface Person {
name: string;
age?: number;
}
let viking: Person = {
name: 'Viking'
}

 <!-- 接下来还有只读属性，有时候我们希望对象中的一些字段只能在创建的时候被赋值，那么可以用 readonly 定义只读属性 -->

interface Person {
readonly id: number;
name: string;
age?: number;
}
viking.id = 9527

```

## 枚举 Enums

```

<!-- 数字枚举，一个数字枚举可以用 enum 这个关键词来定义，我们定义一系列的方向，然后这里面的值，枚举成员会被赋值为从 0 开始递增的数字, -->

enum Direction {
Up,
Down,
Left,
Right,
}
console.log(Direction.Up)

 <!-- 还有一个神奇的点是这个枚举还做了反向映射 -->

console.log(Direction[0])

 <!-- 字符串枚举 -->

enum Direction {
Up = 'UP',
Down = 'DOWN',
Left = 'LEFT',
Right = 'RIGHT',
}
const value = 'UP'
if (value === Direction.Up) {
console.log('go up!')
}

```

## 泛型 Generics

泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。

```

function echo(arg) {
return arg
}
const result = echo(123)

 <!-- 这时候我们发现了一个问题，我们传入了数字，但是返回了 any -->

function echo<T>(arg: T): T {
return arg
}
const result = echo(123)

 <!-- 泛型也可以传入多个值 -->

function swap<T, U>(tuple: [T, U]): [U, T] {
return [tuple[1], tuple[0]]
}

const result = swap(['string', 123])

```

## keyof 和 typeof 关键字的作用

keyof 索引类型查询操作符 获取索引类型的属性名，构成联合类型。
typeof 获取一个变量或对象的类型

## implements 与 extends 的区别

extends 子类会继承父类的所有属性和方法
implements 使用该关键字的类将需要实现的需要实现的类的所有属性和方法。

## interface 和 type 区别

interface：接口主要用于类型检查，它只是一个结构契约，定义了具有相似的名称和类型的对象结构。除此之外，接口还可以定义方法和事件,声明两个相同接口会合并，interface extends type

type：不同于 interface 只能定义对象类型，type 声明还可以定义基础类型、联合类型或交叉类型。type 可以使用 typeof 获取实例类型 type x = typeof div type y = string & interface yy{x:1}|

两者最关键的差别在于类型别名本身无法添加新的属性，而接口是可以扩展的

## [Array 和 Tuple](https://www.typescriptlang.org/docs/handbook/basic-types.html#array)

```

<!-- 最简单的方法是使用「类型 + 方括号」来表示数组： -->

let arrOfNumbers: number[] = [1, 2, 3, 4]

<!--  数组的项中不允许出现其他的类型： -->
<!--  数组的一些方法的参数也会根据数组在定义时约定的类型进行限制： -->

arrOfNumbers.push(3)
arrOfNumbers.push('abc')

<!-- 元祖的表示和数组非常类似，只不过它将类型写在了里面 这就对每一项起到了限定的作用 -->

let user: [string, number] = ['viking', 20]

<!-- 但是当我们写少一项 就会报错 同样写多一项也会有问题 -->

user = ['molly', 20, true]

```

## 类型别名 和 交叉类型

[类型别名 Type Aliases](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases)

就是给类型起一个别名，让它可以更方便的被重用。

```

let sum: (x: number, y: number) => number
const result = sum(1,2)
type PlusType = (x: number, y: number) => number
let sum2: PlusType

<!--  支持联合类型 -->

type StrOrNumber = string | number
let result2: StrOrNumber = '123'
result2 = 123

<!--  字符串字面量 -->

type Directions = 'Up' | 'Down' | 'Left' | 'Right'
let toWhere: Directions = 'Up'

```

## [联合类型 - union types](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html#union-types)

```

 <!-- 我们只需要用中竖线来分割两个 -->

let numberOrString: number | string

<!-- 当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，我们只能访问此联合类型的所有类型里共有的属性或方法： -->

numberOrString.length
numberOrString.toString()

```

## [类型断言 - type assertions](https://www.typescriptlang.org/docs/handbook/basic-types.html#type-assertions)

```

 <!-- 这里我们可以用 as 关键字，告诉typescript 编译器，你没法判断我的代码，但是我本人很清楚，这里我就把它看作是一个 string，你可以给他用 string 的方法。 -->

function getLength(input: string | number): number {
const str = input as string
if (str.length) {
return str.length
} else {
const number = input as number
return number.toString().length
}
}

```

## [类型守卫 - type guard](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-guards-and-differentiating-types)

```

 <!-- typescript 在不同的条件分支里面，智能的缩小了范围，这样我们代码出错的几率就大大的降低了。 -->

function getLength2(input: string | number): number {
if (typeof input === 'string') {
return input.length
} else {
return input.toString().length
}
}

```

###

## 类型别名 通过交集(&)扩展类型

```

type Person = {
name: string
}

type Student = Person & {
stuNo: string
}

const stu: Student = {
name: 'hsh',
stuNo: '01'
}

stu.name // ok
stu.stuNo // ok

```

## [交叉类型 Intersection Types](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html#intersection-types)

```

interface IName {
name: string
}
type IPerson = IName & { age: number }
let person: IPerson = { name: 'hello', age: 12}

```

## [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html) (可选)

```

 <!-- partial，它可以把传入的类型都变成可选 -->

interface IPerson {
name: string
age: number
}

let viking: IPerson = { name: 'viking', age: 20 }
type IPartial = Partial<IPerson>
let viking2: IPartial = { }

```

## [Omit](https://www.typescriptlang.org/docs/handbook/utility-types.html)（忽略传入类型的某个属性）

```

<!-- 它返回的类型可以忽略传入类型的某个属性 -->

interface Todo {
title: string;
description: string;
completed: boolean;
createdAt: number;
}

type TodoPreview = Omit<Todo, "description">;

const todo: TodoPreview = {
title: "Clean room",
completed: false,
createdAt: 1615544252770,
};

```

## [Exclude](https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers)<T, U>(去交集，返回剩余的。)

```

<!-- 此工具是在 T 类型中，去除 T 类型和 U 类型的交集，返回剩余的部分 -->

type T0 = Exclude<"a" | "b" | "c", "a">;

type T0 = "b" | "c"
type T1 = Exclude<"a" | "b" | "c", "a" | "b">;

type T1 = "c"
type T2 = Exclude<string | number | (() => void), Function>;

type T2 = string | number

```

## [Required](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union)(某个必选项)

```

<!-- 将某个类型里的属性全部变为必选项 -->

interface Props {
a?: number;
b?: string;
}

const obj: Props = { a: 5 };

const obj2: Required<Props> = { a: 5 };
Property 'b' is missing in type '{ a: number; }' but required in type 'Required<Props>'.

```

## [Partial](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union)(必选项)

```

<!-- 将某个类型里的属性全部变为必选项 -->

interface Todo {
title: string;
description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
return { ...todo, ...fieldsToUpdate };
}

const todo1 = {
title: "organize desk",
description: "clear clutter",
};

const todo2 = updateTodo(todo1, {
description: "throw out trash",
});

```

## [Readonly](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union)(无法被修改)

```

<!-- 会转换类型的所有属性，以使它们无法被修改 -->

interface Todo {
title: string;
}

const todo: Readonly<Todo> = {
title: "Delete inactive users",
};

todo.title = "Hello";
Cannot assign to 'title' because it is a read-only property.

```

## [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union)(抽取)

```

<!-- 抽取一个类型/接口中的一些子集作为一个新的类型 -->

interface Todo {
title: string;
description: string;
completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

const todo: TodoPreview = {
title: "Clean room",
completed: false,
};

todo;

const todo: TodoPreview

```

## [Extract](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union)(取交集)

```

<!-- 提取T中可以赋值给U的类型--取交集 -->

type T0 = Extract<"a" | "b" | "c", "a" | "f">;

type T0 = "a"
type T1 = Extract<string | number | (() => void), Function>;

type T1 = () => void

```

## [Record](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type)(映射到另一个类型)

```

<!-- 此工具可帮助你构造具有给定类型T的一组属性K的类型。将一个类型的属性映射到另一个类型的属性时，Record非常方便。 -->

interface CatInfo {
age: number;
breed: string;
}

type CatName = "miffy" | "boris" | "mordred";

const cats: Record<CatName, CatInfo> = {
miffy: { age: 10, breed: "Persian" },
boris: { age: 5, breed: "Maine Coon" },
mordred: { age: 16, breed: "British Shorthair" },
};

cats.boris;

const cats: Record<CatName, CatInfo>

```

## [NonNullable](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type)(剔除 null 和 undefined)

```

<!-- -- 从 T 中剔除 null 和 undefined -->

type T0 = NonNullable<string | number | undefined>;

type T0 = string | number
type T1 = NonNullable<string[] | null | undefined>;

type T1 = string[]

```

## React + TypeScript 怎么设置全局方法 & 全局变量

根目录下心间一个 d.ts 文件 如下：

```
export {}; //使用 export {} 使文件成为模块。

declare global {
  /**
   * 现在声明进入全局命名空间的类型，或者增加全局命名空间中的现有声明。
   */
  interface Employee {
    id: number;
    name: string;
    salary: number;
  }

  type Person = {
    name: string;
    age: number;
  };
}

```
