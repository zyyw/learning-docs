# 如何用 GoLang 实现一个单例
## 懒汉加锁
懒汉加锁:虽然解决并发的问题，但每次加锁是要付出代价的
```golang
type singleton struct{}

var (
    ins *singleton
    mu sync.Mutex
)

func GetInstance1() *singleton {
    mu.Lock()
    defer mu.Unlock()

    if ins == nil {
        ins = &singleton{}
    }
    return ins
}
```
## 双重加锁
双重锁:避免了每次加锁，提高代码效率
```golang
type singleton struct{}
var (
    ins *singleton
    mu sync.Mutex
)

func GetInstance2() *singleton {
    if ins == nil {
        mu.Lock()
        defer mu.Unlock()
        if ins == nil {
            ins = &signleton{}
        }
    }
    return ins
}
```
## 用 sync.Once 实现
```golang
type singleton struct{}

var (
    ins *singleton
    once sync.Once
)
fun GetInstance3() *singleton {
    once.Do(func() {
        ins = &singelton{}
    })
    return ins
}
```