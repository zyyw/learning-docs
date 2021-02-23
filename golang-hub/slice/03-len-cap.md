# 切片的 len 和 cap

## Code
```go
package main

import "fmt"

func main() {
	s := [3]int{1, 2, 3}
	a := s[:0]
	b := s[:2]
	c := s[1:2:cap(s)]

	fmt.Println("len(a) =", len(a), ", cap(a) =", cap(a))
	fmt.Println("len(b) =", len(b), ", cap(b) =", cap(b))
	fmt.Println("len(c) =", len(c), ", cap(c) =", cap(c))
}
```

## Output
```
len(a) = 0 , cap(a) = 3
len(b) = 2 , cap(b) = 3
len(c) = 1 , cap(c) = 2
```