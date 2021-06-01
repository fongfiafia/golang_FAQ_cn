# Go为什么基于CSP理论设计并发?

这么多年以来，并发设计和多线程编程变成了“复杂”的代名词。我们认为这一部分是因为诸如[Pthreads](https://en.wikipedia.org/wiki/POSIX_Threads)复杂的设计，一部分也是因为诸如互斥器、条件参数、内存屏障这些过分强调极低细节的设计。但是如果设计出一个更高水平的接口，可能内部还是有互斥器这些设计，但是能够掩盖住它们，让编程更加简单。

Communicating Sequential Processes（CSP），是最成功的语言并发设计之一。Occam和Erlang两个著名语言都是成起源于CSP。Go的并发设计理念起源于一个管道（channel）的设计。早期一些语言尝试了CSP的设计，证明了CSP模型十分适合程序性框架语言。

```go
stem from 起源于
primitive 老式的
derive from 导出、探究、起源于
notion 观念
procedural 程序性的
```

