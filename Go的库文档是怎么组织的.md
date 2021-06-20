# Go的库文档是怎么组织的?

在Go中有个程序”Godoc“，它能从源代码中提取包的文档（就是注释），并且能够生成一个网站进行访问。 在[golang.org/pkg](https://golang.org/pkg/https://golang.org/pkg/)运行。 事实上这个网站就是Godoc实现的。

可以配置Godoc，来显示你程序中一些符号、静态分析等更多详细内容，实现方法可以参考https://golang.org/lib/godoc/analysis/help.html。

想要从命令行访问文档，Go tool具有DOC子命令，可提供一些文本接口。

```go
textual 原文的，文本的
interactive 互动的，交互的
```

