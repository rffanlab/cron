# 说明
内容来自于doc.go 翻译这个内容是为了方便英文不太好的小伙伴的，也顺便我自己能够深入理解这个包的功能

# 用途
调用者需要注册一个方法来供一个队列引用。Cron 会在它自己的goroutine 里调用它们。
示例代码如下
```golang 
    
    c := cron.New()
	c.AddFunc("0 30 * * * *", func() { fmt.Println("Every hour on the half hour") })
	c.AddFunc("@hourly",      func() { fmt.Println("Every hour") })
	c.AddFunc("@every 1h30m", func() { fmt.Println("Every hour thirty") })
	c.Start()
	..
	// Funcs are invoked in their own goroutine, asynchronously.
  // 方法会被异步调用（使用goroutine）
	...
	// Funcs may also be added to a running Cron
  // 方法也可以添加到一个在运行中的cron里
	c.AddFunc("@daily", func() { fmt.Println("Every day") })
	..
	// Inspect the cron job entries' next and previous run times.
	inspect(c.Entries())
	..
	c.Stop()  // Stop the scheduler (does not stop any jobs already running). 结束队列（并不意味着结束已经在运行的任务）
```
