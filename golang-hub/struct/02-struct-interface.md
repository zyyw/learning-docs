# struct 实现 interfac

## Code
```go
package main

import "fmt"

type People interface {
	Speak() string
}

type Student struct{}

func (stu *Student) Speak() {
	fmt.Println("student speaking")
	return
}

func main() {
	var ppl People = Student{}
	ppl.Speak()
}
```

## 分析
compilation error, `var ppl People = Student{}`, 值类型 Student 没有实现接口的 Speak() 方法，而是指针类型 *Student 实现该方法。