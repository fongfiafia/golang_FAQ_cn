# Go为什么没有可变的返回类型呢?

Covariant result types （可变的返回类型）指的是下面这种接口例子：

```go
type Copyable interface {
	Copy() interface{}
}
```

会被下面的方法实现：（实际上并没有）

```go
func (v Value) Copy() Value
```

乍一看，似乎成立，因为value是实现了空接口。但是在Go中，方法必须准确地匹配。因此Value并没有实现Copyable。Go将类型的概念与类型的实现分开， 如果两种方法返回不同类型，则它们并不是在做同样的事情。程序员想要实现Covariant result types ，通常尝试通过接口表达类型层次结构。在GO语言中，应该尽可能清晰地分开表现出接口和以及它的实现。