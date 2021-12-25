# 为什么 Go 在基准 X 上表现不佳

Go 的设计目标之一是拥有接近 C语言一样的性能，但在某些基准测试中它的表现相当糟糕，包括 [golang.org/x/exp/shootout](https://go.googlesource.com/exp/+/master/shootout/) 中的几个。表现最慢的几个是因为在 Go 中，他们依赖的库性能都不太行。例如，[pidigits.go](https://go.googlesource.com/exp/+/master/shootout/pidigits.go) 依赖于多精度数学包，而 C 版本与 Go 不同，使用 [GMP](https://gmplib.org/)（用优化的汇编程序编写）。依赖于正则表达式的基准测试（例如 regex-dna.go）本质上是将 Go 的原生 regexp 包与成熟的、高度优化的正则表达式库（如 PCRE）进行比较。

其实基准测试这个东西是通过广泛的调整赢得的，如果你在考虑这个事情，那么请有这个概念。如果您对比等效的 C 和 Go 程序（reverse-complement.go 是一个示例），您会发现这两种语言的原始性能表现差异，会比一些测试套件显示的要接近得多。

尽管如此，仍有改进的余地。编译器很好但可以做的更好，许多库需要进行主要的性能提升，垃圾收集器还不够快。 （即使是这样，尽量不要产生不必要的垃圾，因为这会产生巨大的影响。）

无论如何，Go语言通常非常具有竞争力。随着语言和工具的发展，许多程序的性能有了显着提高。有关信息丰富的示例，请参阅有关分析 Go 程序的博客文章。

```
essentially   基本上
extensive  广阔的
```

