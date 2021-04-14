## interface 动态类型， 动态值

## Code
```go
package main

import "fmt"

type Coder interface {
	code()
}

type Gopher struct {
	name string
}

func (g Gopher) code() {
	fmt.Printf("%s is coding\n", g.name)
}

func main() {
	var c Coder
	fmt.Println(c == nil) // true
	fmt.Printf("c: %T, %v\n", c, c)

	var g *Gopher
	fmt.Println(g == nil) // true

	c = g
	fmt.Println(c == nil) // false, 因为 c 的动态类型为 *main.Gopher, 动态值为 nil
	fmt.Printf("c: %T, %v\n", c, c)
}
```

## 分析
"一个接口的值是由【一个具体类型】和【具体类型的值】两部分组成的。这两部分分别称为接口的【动态类型】和【动态值】。"
https://www.liwenzhou.com/posts/Go/12_interface/

