# defer + nested function

## Code
```go
package main

import "fmt"

func main() {
	a := 1
	b := 2
	defer calc("1", a, calc("10", a, b))
	a = 0
	defer calc("2", a, calc("20", a, b))
	b = 1
}

func calc(index string, a, b int) int {
	ret := a + b
	fmt.Println(index, a, b, ret)
	return ret
}
```

## Output
```
10 1 2 3
20 0 2 2
2 0 2 2
1 1 3 4
```

## 分析
```
/*
    "10" 1 2 3
    "20" 0 2 2
    "2" 0 2 2
    "1" 1 3 4

    ("2" 0 2)
    ("1" 1 3)
*/
```