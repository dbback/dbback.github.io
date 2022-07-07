搭建指令：


```python

docker run -d  --privileged=true  --restart unless-stopped --net=host pppv/xx

```



- port  9999(x-ui)     5555(snell)

- 镜像是在 pppv/centos-systemd 基础上 commit并push出来的

- 搬瓦工的需要 yum update ,docker 才能正常


```python

 docker commit
 docker login
 docker push

```
