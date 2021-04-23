# json marshal empty slice or nil slice

## Code
```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	s1 := []int{}
	var s2 []int

	b1, err1 := json.Marshal(s1)
	if err1 != nil {
		fmt.Println("err1:", err1)
	} else {
		fmt.Println(string(b1))
	}

	b2, err2 := json.Marshal(s2)
	if err2 != nil {
		fmt.Println("err1:", err2)
	} else {
		fmt.Println(string(b2))
	}
}
```

## Output
```
[]
null
```

## 分析
json.Marshal empty 切片返回 "[]"; json.Marshal nil 切片返回 "null"