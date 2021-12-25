# runtime运行时是怎么实现的?

还是因为由于启动bootstrap问题，运行时（runtime）代码最初主要是用 C 编写的（带有一点汇编程序），但后来被翻译成 Go（除了一些汇编程序）。 Gccgo 的运行时支持使用 glibc。 gccgo 编译器使用了名为分段堆栈的技术来实现 goroutines，此技术得以与最近对黄金链接器（gold linker）的升级。 Gollvm 同样建立在相应的 LLVM 基础架构上。