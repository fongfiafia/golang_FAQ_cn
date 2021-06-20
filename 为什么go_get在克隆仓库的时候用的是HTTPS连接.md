# 为什么go_get在克隆仓库的时候用的是HTTPS连接?

公司通常只允许在标准TCP端口80（HTTP）和443（HTTPS）上输出流量，并阻止其他端口输出流量，这包括了TCP端口9418（GIT）和TCP端口22（SSH）。 使用HTTPS而不是HTTP时，GIT默认强制执行证书验证，提供对中间人攻击，窃听和篡改攻击的保护。 因此，GO GET命令使用HTTPS进行安全。

Git可以配置为通过HTTPS进行身份验证，也可以配置使用SSH代替HTTPS。 要通过HTTPS进行身份验证，您可以向GIT Commerss的$ Home / .NETRC文件添加一行：

```go
machine github.com login USERNAME password APIKEY
```

Github账号的密码可以成为一个个人通信许可token

Git也可以通过给定前缀的URL，来配置为使用SSH，代替HTTPS连接方式。 例如，要将SSH用于所有GitHub访问，请将这些行添加到您的〜/ .gitconfig：

```go
[url "ssh://git@github.com/"]
	insteadOf = https://github.com/
```

