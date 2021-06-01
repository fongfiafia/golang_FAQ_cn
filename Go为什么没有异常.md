# Go为什么没有异常？

我们认为把“异常”（exception）机制设计成一个控制结构（control structure）（PS:理解为闭环是否会好一点？）会让代码变得很复杂，例如常见的`try-catch-finally`的设计。这种设计隐性在鼓励人们把一些诸如打开文件失败等常见的错误，当成是异常。

Go采用了一种不一样的设计。对于简单的错误处理，通过Go的多值返回特性能够让报告一个错误变得简单，而且这样不会重载返回值。（PS: 在Java中通过throws exception来实现报告错误，Go是通过直接return error来报告错误）。https://blog.golang.org/error-handling-and-go 这篇文章有更详细的errors的介绍，让你体验到Go error相比于其他语言更加的舒适。（PS：后面翻译一下）

Go同样有一些内置的方法来从真正那些异常的情况中唤起或者恢复程序。恢复机制（recovery mechanism）只有在**程序**状态为崩溃的时候才会执行，这种机制足够应付程序的崩溃，而且不需要使用上述那种控制结构便能做到，这样代码也会很整洁。

详细的可以看https://blog.golang.org/defer-panic-and-recover 这篇文章，同样的https://blog.golang.org/errors-are-values这篇博客基于“error 是值”的原则示范了如何写出更整洁的error处理代码。

```go
1. idiom n 成语
2. convoluted 复杂的
3. sufficient 充分的
4. demonstrate v 示范
```