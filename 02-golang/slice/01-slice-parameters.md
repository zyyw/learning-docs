# slice 作为参数传递

## Code
```go
package main

import "fmt"

func hello(num ...int) {
	fmt.Printf("hello &num = %p\n", &num)
	fmt.Printf("hello &num[0] = %p\n", &num[0])
	num[0] = 18
}

func hello2(num []int) {
	fmt.Printf("hello2 &num = %p\n", &num)
	fmt.Printf("hello2 &num[0] = %p\n", &num[0])
	num[0] = 108
}

func main() {
	i := []int{5, 6, 7}
	fmt.Printf("&i = %p\n", &i)
	fmt.Printf("&i[0] = %p\n", &i[0])

	hello(i...)
	fmt.Println(i[0])

	hello2(i)
	fmt.Println(i[0])
}
```

## Output
```
&i = 0xc00011a000
&i[0] = 0xc00011c000
hello &num = 0xc00011a020
hello &num[0] = 0xc00011c000
18
hello2 &num = 0xc00011a040
hello2 &num[0] = 0xc00011c000
108
```

## 分析
```
&i[0], hello &num[0], hello2 &num[0] 的值相同，表示切片 i, hello num, hello2 num 指向的是同一个底层数组。
```
