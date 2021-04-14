## 方法集

## Code 2
```go
package main

import "fmt"

type data struct {
	name string
}

// 注意这里 print() 是 value receiver
func (p data) print() {
	fmt.Println("name:", p.name)
}

func main() {
	d1 := data{"one"}
	d1.print() 
	d2 := &data{"two"}
	d2.print() // 这里不报错，打印 "name: two"
}
```

## 分析 2
print() 方法是 value receiver. T 类型的方法可以被 T 类型 或者 *T 类型调用。

## Code 3
```go
package main

import "fmt"

type data struct {
	name string
}

// 注意这里 print() 是 pointer receiver
func (p *data) print() {
	fmt.Println("name:", p.name)
}

func main() {
	d1 := data{"one"}
	d1.print() // 这里不报错，打印 "name: one"
	d2 := &data{"two"}
	d2.print()
}
```

## 分析 3
print() 方法是 pointer receiver。 *T 类型的方法可以被 T 类型 或者 *T 类型调用。


## Code 1
```go
package main

import "fmt"

type data struct {
	name string
}

func (p *data) print() {
	fmt.Println("name:", p.name)
}

type printer interface {
	print()
}

func main() {
	d1 := data{"one"}
	d1.print() // 这里不报错，打印 "name: one"

	var in printer = data{"two"} // 这里报错，因为 data 实现的 print() 接口是 pointer receiver
	in.print()
}
```

## 分析 1
注意 d1 和 in 的区别, in 是接口 printer 类型。
T 类型的方法，可以被 `var obj myInterface = T{}` 或者 `var obj myInterface = &T{}` 调用，因为实现value receiver的接口函数时，隐式地实现了对应的 pointer receiver 接口函数；
*T 类型的方法，可以被 `var obj myInterface = &T{}` 调用。
