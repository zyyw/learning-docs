# pointer, method

## Code
```go
package main

type X struct{}

func (x *X) test() {
	println(x)
}

func main() {
	var a *X
	a.test()  // 这里 a == nil, 是个有效的方法调用

	X{}.test() // X{} 是 struct literal, 不可寻址，不能直接调用方法
}
```

## 分析
在方法中，指针类型的接收者必须是合法指针（包括 nil）,或能获取实例地址。

修复代码：
```go
func main() {

    var a *X
    a.test()    // 相当于 test(nil)

    var x = X{}
    x.test()
}
```

## Code 2
```go
package main

type T struct {
	n int
}

func (t *T) Set(n int) {
	t.n = n
}

func getT() T {
	return T{}
}

func main() {
	getT().Set(1)
}
```

## 分析 2
1. 直接返回的 T{} 不可寻址；
1. 不可寻址的结构体不能调用带结构体指针接收者的方法；

修复代码：
```go
func main() {
    t := getT()  // 尽管 getT() 返回 T 类型，Set() 需要 pointer，t.Set(2) 有效，因为这里 t 隐性转成 *T 了
    t.Set(2)
    fmt.Println(t.n)
}
```

## Code 3
```go
package main

type T struct {
	n int
}

func getT() T {
	return T{}
}

func main() {
	getT().n = 1 // 这里不能直接赋值
}
```

## 分析 3
直接返回的 T{} 无法寻址，不可直接赋值。

修复代码：
```go
func main() {
	t := getT()
	//p := &t.n // <=> p = &(t.n)
	//*p = 1
	t.n = 2
	fmt.Println(t.n)
}
```