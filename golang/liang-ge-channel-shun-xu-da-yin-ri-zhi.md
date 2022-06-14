# 两个channel顺序打印日志

{% embed url="https://blog.csdn.net/qianghaohao/article/details/97007270" %}

```go
// Some code
a := make(chan bool, 1)
b := make(chan bool, 1)
Exit := make(chan bool)
a <- true
i, j := 1, 2
go func() {
   defer close(Exit)
   for i < 100 {
      if <-a {
         fmt.Println(i)
         i += 2
         b <- true
      }
   }
   close(b)
}()
go func() {
   for j < 100 {
      if <-b {
         fmt.Println(j)
         j += 2
         a <- true
      }
   }
   close(a)
}()

<-Exito
```
