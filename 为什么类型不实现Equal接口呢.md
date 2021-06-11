# 为什么类型不实现Equal接口呢?

我们来看下面一个例子：一个类型和自己进行比较

```go
// 定义一个接口
type Equaler interface {
    Equal(Equaler) bool
}

// 实现它
type T int
func (t T) Equal(u T) bool { return t == u } // does not satisfy Equaler
```

和其他多态系统的实现不同，其实上述例子中T并没有实现Equaler，因为T.Equal()的参数类型是T,并不是字面上要求的Equaler类型。（PS:可以理解为：你还没实现find方法，就想直接用接口来替代自己？这是不可能的。）

在GO语言中，类型系统不会优化Equal的参数，因为这是程序员的职责，看下面这T2的例子，它正确地实现了Equaler方法。

```go
type T2 int
func (t T2) Equal(u Equaler) bool { return t == u.(T2) }  // satisfies Equaler
```

这和其他语言的类型系统并不一样，因为在Go中，任何类型满足Equaler接口，就能当作参数传递给T2.Equal，在运行的时候，我们需要检查参数是否满足T2，而一些语言是在编译的时候就会进行检查。

```go
polymorphic 多态的
illustrate 举例说明 as illustrate
```

相关的一个例子如下：

```go
type Opener interface {
   Open() Reader
}

func (t T3) Open() *os.File
```

在Go语言中，T3并没有实现Opener，然而在其他语言中这么写可能已经实现了Opener。

尽管Go的类型系统在这方面做了较少的支持，但是也使得实现接口的限制变得很松，这样更加方便声明，因为你只需要考虑一点：函数的名字和签名真的和那个接口的定义的一样吗？我们认为这带来的好处大于自动优化的类型匹配。

Go未来会采用一些多态语言类型的组织形式吗？我们希望如果有的话，那么一定要能表达出上述例子的含义，并且能够被静态检查到问题。