转载自： https://my.oschina.net/qbj/blog/2998164

由于早上到公司发现`/var/lib/docker/overlay2` 占用空间很大，决定做一下`/var/lib/docker`目录迁移工作

1. 首先需要停止docker服务

```bash
systemctl stop docker
```

2. 通过命令df -h 先去看下磁盘大概的情况，找一个大的空间

3. 创建docker的新目录，我这边找了data, 所以我这边的新目录地址是 `/data/docker/lib/`

```bash
mkdir -p /data/docker/lib
```

注：参数-p 确保目录名称存在，如果目录不存在的就新创建一个。

4. 开始迁移

```bash
rsync -avzP /var/lib/docker /data/docker/lib/
```

先确认是否安装了rsync.

参数解释：

```
-a，归档模式，表示递归传输并保持文件属性。
-v，显示rsync过程中详细信息。可以使用"-vvvv"获取更详细信息。
-P，显示文件传输的进度信息。(实际上"-P"="--partial --progress"，其中的"--progress"才是显示进度信息的)。
-z,   传输时进行压缩提高效率。
```

5. 指定新的docker目录

```bash
vim /lib/systemd/system/docker.service
```

在ExecStart加入: 

```
 --graph=/data/docker/lib/docker
```

注：之前文档里这一步是采用另一种方式的如下图，也是可以的，但建议以新的为准。

6. 重启docker

```bash
systemctl daemon-reload
 
systemctl restart docker
 
systemctl enable docker
```

7. 启动之后确认docker 没有问题，删除旧的`/var/lib/docker/`目录