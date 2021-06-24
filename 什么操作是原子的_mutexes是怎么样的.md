# 什么操作是原子的?mutexes是怎么样的?

Go的操作原子性详细描述在这个链接中可以看到：https://golang.org/ref/mem

低级的同步和原始原子操作实现可以使用[sync](https://golang.org/pkg/sync)和[sync/atomic](https://golang.org/pkg/sync/atomic) 包。这些包在一些简单任务比如自增或者小规模的互锁等等。

高级的操作，比如并发服务器之间的写作，使用高级的技术能够让程序运行得更好。Go是通过channels来实现的。例如，你可以设计的你程序：只有一个协程在某一个刻处理一块数据，而其他协程是碰不到这些数据的。你可以看原始总结文档：https://www.youtube.com/watch?v=PAAkCSZUG1c

不同程序之间不要通过共享内存数据来通讯，而是要通过通许来共享内存数据。

查看这篇文章了解怎么通过通讯来共享内存https://golang.org/doc/codewalk/sharemem/

大规模的并发程序也都类似使用这些工具集。