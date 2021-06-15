# 为什么空值的error和nil并不相等?

在底层，接口都实现了2个元素，类型`T`和值`V`,V是一个实实在在的值，比如int，struct，point，甚至接口本身。例如，如果我们在一个接口中，存储int的值为3，这样这个接口结果大致是（T=int，V=3）。V也就是我们常说的接口的动态值，因为在程序的执行过程中，接口的V可能会是不同的值。

一个接口如果是nil，那么意味着他的T和V都没有被设置(T=nil，v is not set)。换个角度说，一个nil的接口，它的类型T一定是nil。如果我们把一个空指针类型的*int存入一个接口的值（V）中，那么这个接口的类型会是 *int（T= *int,V=nil），例如下面的例子代码。

这种情况会让人困惑，尤其是当一个nil的值被存在一个接口的V中，例如error

```go
func returnsError() error {
	var p *MyError = nil // 这个可以这么理解：新建一个变量p，他的type是*myError value是nil
	if bad() {
		p = ErrBad
	}
	return p // Will always return a non-nil error.
}
```

如果程序正常运行结束，这个函数返回的p是nil，p是error接口，这个接口内部是（T=*MyError,V=nil）。这样就会导致，外部如果把p和nil进行比较，会发现永远都是有错误，即使你的程序其实并没有发生什么异常。为了返回一个合适的nil error，方法必须要返回一个明确的nil值来表示没有异常发生：

```go
func returnsError() error {
	if bad() {
		return ErrBad
	}
	return nil
}
```

一个很好的原则就是函数的签名永远都是使用error这类型（就像我们上面做的一样），而不是一个具体的类型，如上述的*myError,这样能够保证error被正确的创建（PS：其实就是新建一个error就在返回的时候新建就行了，如return error.new()，而不要在外部新建一个error，这样如最上的例子一样，你可能会设置为nil，并且认为它是nil了，然而其实它的type并不是空）。举个例子，例如os.open()方法，返回的错误都是 *os.PathError。（PS: 我贴一下它的用法）

```go
func openFileNolog(name string, flag int, perm FileMode) (*File, error) {
	if name == "" {
		return nil, &PathError{"open", name, syscall.ENOENT} // 直接返回的error
	}
	r, errf := openFile(name, flag, perm)
	if errf == nil {
		return r, nil
	}
	r, errd := openDir(name)
	if errd == nil {
		if flag&O_WRONLY != 0 || flag&O_RDWR != 0 {
			r.Close()
			return nil, &PathError{"open", name, syscall.EISDIR}
		}
		return r, nil
	}
	return nil, &PathError{"open", name, errf}
}
```

牢记一点，只要任何具体的值被存在了一个接口中，那么这个接口就不会是nil。更多详细的内容可以看https://blog.golang.org/laws-of-reflection

```go
concrete 混凝土，具象的，实在的
schematically 大致的，有计划的
```

