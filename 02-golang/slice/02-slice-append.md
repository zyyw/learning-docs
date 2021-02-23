# slice, append 操作

## Code
```
func main() {
    a := []int{7, 8, 9}
    fmt.Printf("%+v\n", a)
    ap(a)
    fmt.Printf("%+v\n", a)
    app(a)
    fmt.Printf("%+v\n", a)
}

func ap(a []int) {
    a = append(a, 10)
}

func app(a []int) {
    a[0] = 1
}
```

## Output
```
[7 8 9]
[7 8 9]
[1 8 9]
```

## 分析
ap 函数里面的 append 操作导致底层数组重新分配内存了 (reslice)，append 之后的切片 a 的底层数组和 main 函数里的切片 a 已经不是同一个切片了。