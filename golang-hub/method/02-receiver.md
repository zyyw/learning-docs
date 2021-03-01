# method, value receiver / pointer receiver
在调用方法的时候，值类型既可以调用值接收者的方法，也可以调用指针接收者的方法; 指针类型既可以调用指针接收者的方法，也可以调用值接收者的方法。也就是说，不管方法的接收者是什么类型，该类型的值和指针都可以调用，不必严格符合接收者的类型。

## Code 1
```go
package main

import "fmt"

type Person struct {
    age int
}

func (p Person) howOld() int {
    return p.age
}

func (p *Person) growUp() {
    p.age += 1
}

func main() {
    // qcrao 是值类型
    qcrao := Person{age: 18}

    // 值类型 调用接收者也是值类型的方法
    fmt.Println(qcrao.howOld())

    // 值类型 调用接收者是指针类型的方法
    qcrao.growUp()
    fmt.Println(qcrao.howOld())

    // ----------------------

    // stefno 是指针类型
    stefno := &Person{age: 100}

    // 指针类型 调用接收者是值类型的方法
    fmt.Println(stefno.howOld())

    // 指针类型 调用接收者也是指针类型的方法
    stefno.growUp()
    fmt.Println(stefno.howOld())
}
```

## Output 1
```
18
19
100
101
```

先说结论：实现了接收者是值类型的方法，相当于自动实现了接收者是指针类型的方法；而实现了接收者是指针类型的方法，不会自动生成对应接收者是值类型的方法。

## Code 2
```go
package main

import "fmt"

type coder interface {
    code()
    debug()
}

type Gopher struct {
    language string
}

func (p Gopher) code() {
    fmt.Printf("I am coding %s language\n", p.language)
}

func (p *Gopher) debug() {
    fmt.Printf("I am debuging %s language\n", p.language)
}

func main() {
    var c coder = &Gopher{"Go"}
    c.code()
    c.debug()
}
```

## Output 2
```
I am coding Go language
I am debuging Go language
```

## 分析 2
如果把 main 函数的第一条语句换成下面这个：
```go
func main() {
    var c coder = Gopher{"Go"}
    c.code()
    c.debug()
}
```
运行，报错：
```
./main.go:23:6: cannot use Gopher literal (type Gopher) as type coder in assignment:
	Gopher does not implement coder (debug method has pointer receiver)
```

## Reference
1. https://qcrao91.gitbook.io/go/interface/zhi-jie-shou-zhe-he-zhi-zhen-jie-shou-zhe-de-qu-bie
