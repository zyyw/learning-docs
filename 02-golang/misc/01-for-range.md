# Misc 01 - for range

## Code
```go
package main

import "fmt"

func main() {
	slice := []int{1, 2, 3, 4}
	m := make(map[int]*int)

	for k, v := range slice {
		fmt.Println("&v =", &v)
		m[k] = &v
	}

	for k, v := range m {
		fmt.Println(k, "->", *v)
	}
}
```

## Output
```
&v = 0xc00001e0a0
&v = 0xc00001e0a0
&v = 0xc00001e0a0
&v = 0xc00001e0a0
2 -> 4
3 -> 4
0 -> 4
1 -> 4
```

## references: 
* day 2: https://seekload.net/2019/08/24/go-interview-2-day.html
