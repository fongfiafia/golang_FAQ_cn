# 能把[]T转换为[]interface{}吗?

答案是：不能直接转换。这是因为根据语言的规范，这两种类型在内存中的表现并不相同。如果要转的话，就一定需要把slice中的元素单独地一个地个得转化。下面是一个把int数组转化为interface数组的例子。

```go
t := []int{1, 2, 3, 4}
s := make([]interface{}, len(t))
for i, v := range t {
    s[i] = v
}
```

```go
specification 规范
```

