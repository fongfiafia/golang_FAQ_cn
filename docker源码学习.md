# Docker源码学习

## client的创建和命令执行

诸如以下命令

```dockerfile
docker pull NAME
docker ps 
docker --daemon=true
```

`--daemon=true`这个我们叫做flag参数，在go中有个flag包专门解析这些参数。