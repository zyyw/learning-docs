# for range 遍历

## Code
```go
package main

import "fmt"

func main() {
	x := []string{"a", "b", "c"}
	for v := range x {
		fmt.Print(v)
	}
}
```

## Output
```
012
```

## 分析
注意区别下面的代码片段：
```go
package main

import "fmt"

func main() {
	x := []string{"a", "b", "c"}
	for _, v := range x {
		fmt.Print(v)  // 输出：abc
	}
}
```