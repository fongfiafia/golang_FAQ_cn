# Go的字符标识设计

我们避免过于围绕ASCII来设计Go，我们希望增大标识符的容量大小，至少比7位（bit）的ASCII容量要大。

组合字符（Combining characters）（PS：Unicode标准认为“基字符”组合成的字符叫做组合字符）不在设计之中，例如梵文。

一个Go的规定：标识符只能是字母或者数字，这是一个易懂的同时也充满限制的规则。

上述规则有一个缺点。根据定义，一个标识符要被外部引用，首字母必须是大写，而一些由字符组成的标识符无法满足这个规则（首字母大写），因此永远无法被外部引用。目前看来唯一办法是采用类似`X日本语`的方式，然而这不让人满意。

早在Go语言设计初期，设计师们就设想过通过一些原生的语言来拓展字符容量大小，并且对于程序员也更加容易接受。想法和讨论没有停止过，在未来，可能会有一个更加自由的字符设计。

但是不管怎么样，未来的字符设计一定要兼容（或者拓展）目前大小写确定可见性，这一字符特性。因为这是Go最受欢迎的一点。

```go
英语学习
1. overly ：adv 过于

2. Since an exported identifier must begin with an upper-case letter, identifiers created from characters in some languages can, by definition, not be exported. 
【Since by definition】： 根据定义。 这里把它拆开了，理解的时候可以复原为：这样才翻译的出来
 Since by definition, an exported identifier must begin with an upper-case letter, identifiers created from characters in some languages can not be exported. 

3. compatibly 适当地
4. perserving v 保持，兼容
5. letter case 字母大小写（case 有大小写的意思）
```