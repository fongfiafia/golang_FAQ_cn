# Go有’运行时‘设计吗？

Go是有“运行时”库(`runtime`)的，它是每一个Go程序不可缺少的一部分。“运行时”库实现了垃圾回收、并发、栈管理以及其他Go重要的特性。Go的“运行时”库类似于C语言的`libc`库。

但是要知道一点，Go的“运行时”库并不是指虚拟机的设计，这点和Java的“运行时”设计不同（PS：Java的“运行时”，是指JVM）。因为Go程序会提前编译为原生机器代码（可能会是Javascript、WebAssembly....），所以，尽管“运行时”通常描述为某种程序运行的虚拟环境，但是在Go中，“运行时”（`runtime`）只是一个重要库的命名（PS：比如会有方法runtime.gc()，这里看起来其实runtime表示一个包）。


```go
1. 英语学习：Go programs are compiled ahead of time to native machine code
ahead of time  是一个副词，要先单独看compiled...to...。然后再加上副词来理解

2. 英语学习：Thus
可以尝试再它前面的语句加上【因为】，然后再thus地方加上【所以】来翻译

```