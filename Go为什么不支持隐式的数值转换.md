# Go为什么不支持隐式的数值转换?

在C语言中，数字类型之间的自动转换，带来的便利性掩盖了其带来的困惑性。什么时候值是unsigned？数字的值多大？会溢出吗？在执行的时候是否是独立的，便携的？（PS：不解。附上原文：Is the result portable, independent of the machine on which it executes?）。它也使编译器复杂化; “通常的算术转换”并不容易在架构中实施。因此我们决定以在代码中，必须用一些明确转换，来保证清晰和简单。

相关的一个细节，和C不用，Int和Int64不同，即使Int是64位类型，也是不同的类型。 int类型是通用的; 如果您关心一个integer持有的位，我们鼓励您明确具体位数。

```go
portable 轻便的
arbitrary 随心所欲的，专断的
precision 精确的，精度
```



