# 应该用Go_get来管理包吗?

Go Tool系统有一个内置的用于管理版本化的相关包集，称为`modules`。 模块在1.11中引入，从1.14版本后可以正式使用。

如果要创建一个使用`modules`的项目，只需要执行`go mod init`，这个命令会创建一个`go.mod`文件，这个文件主要作用就是用来记录项目的依赖包版本信息。

```go
go mod init example.com/project
```

如果要新增、升级、下载一个依赖，只需要执行`go get`

```go
go get golang.org/x/text@v0.3.5
```

可以在[Tutorial: Create a module](https://golang.org/doc/tutorial/create-module.html)中查看怎么开始使用`modules`的更多内容。

[Developing modules](https://golang.org/doc/#developing-modules)中指导了怎么管理包

使用`modules`模块中的软件包应保持历史兼容性，请遵循导入兼容性规则：

- 如果旧包和新包具有相同的导入路径，新包必须向后兼容旧包。

[Go 1兼容性指南](https://golang.org/doc/go1compat.html)在此处是一个很好的参考，例如：不要删除导出的名称，鼓励注释文字，等等。 如果需要不同的功能，请添加新名称，而不是更改旧名称。

模块使用[语义版本控制](https://semver.org/)和语义导入版本控制编码。 如果需要中断兼容性，请在新的主要版本中修改模块。 主要版本2和更高版本的模块需要一个主要版本后缀作为路径的一部分（如/ v2）。 这保留了导入兼容性规则：模块中不同主要版本中的软件包具有不同的路径。

```go
codify 编纂，把---变成法典
```

