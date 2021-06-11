# 你愿意体验Go语言吗?

人们提了很多想要提高Go的建议，例如https://groups.google.com/forum/#!forum/golang-nuts这里有一堆这样的历史讨论，但是只有很少的一部分真正地被采纳了。

虽然Go是一个开源的项目，但是语言和内库都被“https://golang.org/doc/go1compat”所保护，至少在源码级别，能防止那些已经用Go实现的程序在升级Go之后不能执行。如果你的提议破坏了Go 1 的规范，就算价值还不错，我们也不会满意并接受。未来Go一些主要的版本可能会不兼容Go 1，但是有一件事是确定的：不兼容的地方一定是十分少。此外，为了保证兼容性，我们会提供一个办法让老的程序适用新版本Go，这些都在讨论。

就算你的提议兼容Go 1版本，但是不符合Go的设计目标灵魂，也是不会接受的。https://talks.golang.org/2012/splash.article这篇文章介绍了Go的设计起源。

```go
proposal n 提议
violate v 违法
specification n 规范
entertain v 是什么满意，高兴
incompatible 不兼容的
moreever 此外
even if 就算
```

