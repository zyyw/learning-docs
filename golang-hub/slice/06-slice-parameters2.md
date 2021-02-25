# slice, struct, parameter

## Code
```go
package main

import (
	"fmt"
)

type T struct {
	ls []int
}

func foo(t T) {
	t.ls[0] = 100
	fmt.Printf("3: &(t.ls) = %p\n", &(t.ls))
	fmt.Printf("4: &(t.ls[0]) = %p\n", &(t.ls[0]))
}

func main() {
	var t = T{
		ls: []int{1, 2, 3},
	}

	fmt.Printf("1: &(t.ls) = %p\n", &(t.ls))
	fmt.Printf("2: &(t.ls[0]) = %p\n", &(t.ls[0]))
	foo(t)
	fmt.Println(t.ls[0])
}
```

## Output
```
1: &(t.ls) = 0xc000128020
2: &(t.ls[0]) = 0xc00013a000
3: &(t.ls) = 0xc000128040
4: &(t.ls[0]) = 0xc00013a000
100
```

## 分析
调用 foo() 函数时虽然是传值，但 foo() 函数中，字段 ls 依旧可以看成是指向底层数组的指针。