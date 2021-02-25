# json struct lowercase attribute

## Code
```go
package main

import (
	"encoding/json"
	"fmt"
)

type People struct {
	name string `json:"name"`
}

func main() {
	js := `{
        "name":"seekload"
    }`
	var p People
	err := json.Unmarshal([]byte(js), &p)
	if err != nil {
		fmt.Println("err: ", err)
		return
	}
	fmt.Println(p)
}
```

## Output
```
{}
```

## 分析
知识点：结构体访问控制，因为 name 首字母是小写，导致其他包不能访问，所以输出为空结构体。

```go
type People struct {
    Name string `json:"name"`
}
```