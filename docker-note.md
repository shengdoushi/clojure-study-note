# Docker 琐碎

## 容器内应用信号捕获

docker stop 可以向容器发出 SIGTERM 信号, 如果10s(可以通过 stop 参数修改此时间)后容器没有停止，则发出 SIGKILL 命令，并立即关闭容器。

docker kill --signal="SIGTERM" 来发出各种信号，但是 kill 命令只是发出信号，没有等待停止容器操作，是一个安全的信号发出命令。

发出的信号发往 PID 为 1 的命令中，所以一个应用容器尽量设置 ENTRYPOINT 为启动应用，避免 sh 为 PID 1 导致的应用捕获不到的问题。

## entrypoint 与 cmd

可以组合使用， cmd 可以被run的参数覆盖， 组合情况见 todo 

## attach 后安全离开容器

尽量使用 run -it 来启动一个容器， 然后 attach 后通过 Ctrl+p Ctrl+q 来安全离开容器。不要使用 Ctrl+c， 会发出 SIGINTERUPT 信号。

## 临时容器

临时容器值得是如果容器关闭，将其删除。 通过 run --rm 来启动一个临时容器。

## 镜像体积

多个操作组合在一个 RUN 中书写，安装的一些临时包也用后删除。如 debian/ubuntu 中:

```
RUN fetchDeps='wget gcc g++ make pkg-config libtool autoconf automake perl' && \
	apt-get update && \
	apt-get install -y  --no-install-recommends $fetchDeps && \
	rm -rf /var/lib/apt/lists/* && \
	...... \
	apt-get purge -y --auto-remove $fetchDeps  
	
```	

## 不使用 Dockerfile 构建过程中的缓存

可以通过 docker build 的  --no-cache 参数

## docker 客户端关闭某个 registry 的 https

只使用 http， 在docker的配置文件中写入:

```json
{
  "insecure-registries" : [ // 数组中填入
    "12.123.123.121:5000"
  ]
}
```

配置文件在 mac 上可以通过 docker 配置对话框中的 Daemon/Advanced 中修改。


