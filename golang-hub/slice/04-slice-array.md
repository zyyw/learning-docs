# slice 与底层数组

## Code
```go
package main

import "fmt"

func change(s ...int) {
	s = append(s, 3)
}

func main() {
	slice := make([]int, 5, 5)
	slice[0] = 1
	slice[1] = 2
	change(slice...)
	fmt.Println(slice)
	change(slice[0:2]...)
	fmt.Println(slice)
}
```

## Output
```
[1 2 0 0 0]
[1 2 3 0 0]
```

## 分析
第一次调用change()的时候，传入的是一个 len=5, cap=5的切片，append()之后的s，在change()函数里底层reslice了，但是main()里面的slice切片的底层数组仍旧没变。
第二次调用change()的时候，传入的是一个 len=2, cap=5的切片，append()之后，s的底层数组从[1,2,0,0,0]变成[1,2,3,0,0], 底层数组的array[2]从0变成了3，但是没有发生reslice.