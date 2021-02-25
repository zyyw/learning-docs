# const

## Code
```go
package main

import "fmt"

const (
	x uint16 = 120
	y
	s = "abc"
	z
)

func main() {
	fmt.Printf("%T %v\n", y, y)
	fmt.Printf("%T %v\n", z, z)
}
```

## Output
```
uint16 120
string abc
```

## 分析
常量组中如不指定类型和初始化值，则与上一行非空常量右值相同。