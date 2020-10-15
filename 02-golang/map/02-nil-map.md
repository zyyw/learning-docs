# Assign to nil map
我们可以使用 append() 函数对为 nil 的 slice 增加元素，但是不能对 nil 的 map 直接赋值。
```go
package main

func main() {
	var s []int // 此时 s == nil
	s = append(s, 1)

    var m map[string]int // 此时 m == nil
    // the following line will "panic: assignment to entry in nil map"
	m["one"] = 1
}
```
Solution:
```go
package main

func main() {
	var s []int
	s = append(s, 1)

	//var m map[string]int
	m := make(map[string]int)
	m["one"] = 1
}
```