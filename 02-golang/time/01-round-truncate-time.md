# Round & Truncate Time

## Code
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	dSecond := 1 * time.Second
	dMinute := 1 * time.Minute
	dHour := 1 * time.Hour

	t := time.Now()
	fmt.Println(t)
	rtSecond := t.Round(dSecond)
	rtMinute := t.Round(dMinute)
	rtHour := t.Round(dHour)
	rtDay := t.Round(24 * dHour)
	fmt.Println("rtSecond:", rtSecond)
	fmt.Println("rtMinute:", rtMinute)
	fmt.Println("rtHour:", rtHour)
	fmt.Println("rtDay:", rtDay)
	fmt.Println("----------------")
	ttSecond := t.Truncate(dSecond)
	ttMinute := t.Truncate(dMinute)
	ttHour := t.Truncate(dHour)
	ttDay := t.Truncate(24 * dHour)
	fmt.Println("ttSecond:", ttSecond)
	fmt.Println("ttMinute:", ttMinute)
	fmt.Println("ttHour:", ttHour)
	fmt.Println("ttDay:", ttDay)
	yy, mm, dd := t.Date()
	fmt.Println(time.Date(yy, mm, dd, 0, 0, 0, 0, t.Location()))
}
```

## Output
```
2020-12-25 11:32:21.972448 +0800 CST m=+0.000093278
rtSecond: 2020-12-25 11:32:22 +0800 CST
rtMinute: 2020-12-25 11:32:00 +0800 CST
rtHour: 2020-12-25 12:00:00 +0800 CST
rtDay: 2020-12-25 08:00:00 +0800 CST
----------------
ttSecond: 2020-12-25 11:32:21 +0800 CST
ttMinute: 2020-12-25 11:32:00 +0800 CST
ttHour: 2020-12-25 11:00:00 +0800 CST
ttDay: 2020-12-25 08:00:00 +0800 CST
2020-12-25 00:00:00 +0800 CST
```
