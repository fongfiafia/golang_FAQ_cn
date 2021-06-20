# 为什么我的Go程序用了那么多的虚拟内存?

Go Memory 分配器会使用一个大空间，用于给Go程序分配内存。 此虚拟内存是GO的本地内存，不会剥夺其他内存进程。

要查找分配给Go流程的实际内存量，请使用UNIX TOP命令并，观察RES（Linux）或RSIZE（MacOS）列信息。

```go
reserve 存储
arena 圆形剧场，活动空间
deprive 剥夺
```

