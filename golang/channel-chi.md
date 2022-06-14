# Channel池

[协程池的简单设计](https://segmentfault.com/a/1190000038820497)

[深入浅出Golang的协程池设计 - Go语言中文网 - Golang中文社区](https://studygolang.com/articles/15477)

[Golang 协程池的使用 · TesterHome](https://testerhome.com/articles/30237)

```go
// Golang
ch := make(chan int)
quit := make(chan int)
for i := 0; i < 5; i++ {
   go func() {
      for {
         select {
            case p, ok := <-ch:
               if ok {
                  fmt.Println(p)
               }
            case <-quit:
               close(ch)
         }
      }
   }()
}

for i:=0;i<10000;i++{
   ch <- i
}
quit <- 1
```
