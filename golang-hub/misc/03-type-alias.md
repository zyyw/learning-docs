# Misc 03 - type alias v.s. new type

## Code
```go
package main

import "fmt"

type MyInt1 int
type MyInt2 = int

func main() {
	var i int = 0
	var i1 MyInt1 = i
	var i2 MyInt2 = i
	fmt.Println(i1, i2)
}
```

## Output
```
编译不通过，cannot use i (type int) as type MyInt1 in assignment
```

## 分析
`type MyInt1 int` 是创建了新类型 MyInt1; `type MyInt2 = int` 是创建了 int 的类型别名 MyInt2, 注意类型别名的定义时用了 =。
`var i1 MyInt1 = i` 是将 int 类型的变量赋值给 MyInt1 类型的变量，由于Go是强类型语言，编译不能通过；而 MyInt2 只是 int 的别名，
本质上还是 int, 可以直接赋值。

## Code 2
```go
// 下面这段代码能否编译通过？如果通过，输出什么？
package main

import "fmt"

type User struct{}
type User1 User
type User2 = User

func (i User1) m1() {
	fmt.Println("m1")
}
func (i User) m2() {
	fmt.Println("m2")
}

func main() {
	var i1 User1
	var i2 User2
	i1.m1()
	i2.m2()
}
```

## Output 2
```
能，输出m1 m2
```

## 分析 2
`type User1 User` 是基于类型 User 创建了新类型 User1， `type User2 = User` 是创建了 User 的类型别名 User2，注意使用 = 定义类型别名。
因为 User2 是别名，完全等价于 User，所以 User2 具有 User 所有的方法。但是 `i1.m2()` 和 `i2.m1()` 是不能执行的，因为 User1 和 User2/User 没有定义该方法。

## Code 3
```
关于类型转化，下面选项正确的是？
A.
type MyInt int
var i int = 1
var j MyInt = i

B.
type MyInt int
var i int = 1
var j MyInt = (MyInt)i

C.
type MyInt int
var i int = 1
var j MyInt = MyInt(i)

D.
type MyInt int
var i int = 1
var j MyInt = i.(MyInt)
```

## 分析 3
答：C。知识点：强制类型转化