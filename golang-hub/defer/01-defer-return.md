# 匿名返回函数/具名返回函数 + defer 

## Code
```go
package main

import "fmt"

func increaseA() int {
	var i int
	defer func() {
		i++
	}()
	return i
}

func increaseB() (r int) {
	defer func() {
		r++
	}()
	return r
}

func main() {
	fmt.Println(increaseA())
	fmt.Println(increaseB())
}
```

## Output
```
0
1
```

## 分析
匿名返回函数执行过程：
* 首先函数返回时会自动创建一个返回变量假设为ret，函数返回时要将 i 赋值给ret，即有ret = i，也就是说ret=0
* 然后检查函数中是否有defer存在，若有则执行defer中部分，此时就到了 i++
* 最后返回ret

具名返回函数：
返回值在函数定义时已经存在，return时不需要再创建另外的变量ret，返回的ret就是 r，只有一个变量，所以 r++ 就是给实际返回的ret做加减，最终返回结果当然是1了。