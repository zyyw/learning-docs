# 切片初始化

## Code
```
关于整型切片的初始化，下面正确的是？
A. s := make([]int)
B. s := make([]int, 0)
C. s := make([]int, 5, 10)
D. s := []int{1, 2, 3, 4, 5}
答：B C D
```

## 分析
make([]int, 0) 必须指定切片的length; make(chan int) 声明一个 unbuffered channel, make(chan int, 2) 声明一个 buffered channel, 均有效。
