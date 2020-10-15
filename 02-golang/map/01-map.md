# Map with struct as the value
One case that m[key].attribute1 is not an addressable value:
```go
package main

import "fmt"

type student struct {
	name string
	age int
}

func main() {
	m := make(map[int]student)
	m[1] = student{
		name: "Alex",
		age:  18,
	}
	fmt.Println(m[1].name)
	
    // the following line errors out at compile time,
    // "cannot assign to m[1].name"
	m[1].name = "Bob"
	fmt.Println(m[1].name)
}
```

To resolve this problem, you can declare the map as this `m := make(map[int]*student)`.
Working solution:
```go
package main

import "fmt"

type student struct {
	name string
	age int
}

func main() {
	m := make(map[int]*student)
	m[1] = &student{
		name: "Alex",
		age:  18,
	}
	fmt.Println(m[1].name)
	
	// the following works just fine, no error
	m[1].name = "Bob"
	fmt.Println(m[1].name)
}
```