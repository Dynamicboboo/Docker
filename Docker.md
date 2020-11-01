### 一、Docker概述

#### 1.Docker为什么会出现？

一款产品： 开发–上线 两套环境！应用环境，应用配置！

开发 — 运维。 问题：我在我的电脑上可以允许！版本更新，导致服务不可用！对于运维来说考验十分大？

环境配置是十分的麻烦，每一个机器都要部署环境(集群Redis、ES、Hadoop…) !费事费力。

发布一个项目( jar + (Redis MySQL JDK ES) )，项目能不能带上环境安装打包！

之前在服务器配置一个应用的环境 Redis MySQL JDK ES Hadoop 配置超麻烦了，不能够跨平台。开发环境Windows，最后发布到Linux！

传统：开发jar，运维来做！

现在：开发打包部署上线，一套流程做完！

安卓流程：java — apk —发布（应用商店）一 张三使用apk一安装即可用！

docker流程： java-jar（环境） — 打包项目帯上环境（镜像） — ( Docker仓库：商店）-----

Docker给以上的问题，提出了解决方案！

**Docker的思想就来自于集装箱！**

JRE – 多个应用(端口冲突) – 原来都是交叉的！

**隔离**：Docker核心思想！打包装箱！每个箱子是互相隔离的。

Docker通过隔离机制，可以将服务器利用到极致！

本质：所有的技术都是因为出现了一些问题，我们需要去解决，才去学习！

#### 2.Dcoker的历史

2010年，几个的年轻人，就在美国成立了一家公司 dotcloud

做一些pass的云计算服务！LXC（Linux Container容器）有关的容器技术！

Linux Container容器是一种内核虚拟化技术，可以提供轻量级的虚拟化，以便隔离进程和资源。他们将自己的技术（容器化技术）命名就是 Docker。

Docker刚刚延生的时候，没有引起行业的注意！dotCloud，就活不下去！
开源
2013年，Docker开源！
越来越多的人发现docker的优点！火了。Docker每个月都会更新一个版本！
2014年4月9日，Docker1.0发布！
docker为什么这么火？十分的轻巧！
在容器技术出来之前，我们都是使用虚拟机技术！
虚拟机：在window中装一个VMware，通过这个软件我们可以虚拟出来一台或者多台电脑！笨重！
虚拟机也属于虚拟化技术，Docker容器技术，也是一种虚拟化技术！
vm : linux centos 原生镜像（一个电脑！） 隔离、需要开启多个虚拟机！ 几个G 几分钟
docker: 隔离，镜像（最核心的环境 4m + jdk + mysql）十分的小巧，运行镜像就可以了！小巧！
几个M 秒级启动！
Docker基于Go语言开发的！开源项目！
docker官网：https://www.docker.com/
文档：https://docs.docker.com/ Docker的文档是超级详细的！
仓库：https://hub.docker.com/

#### 3.Docker能做什么？

比较Docker和虚拟机技术的不同：

- 传统虚拟机，虚拟出一条硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件
- 容器内的应用直接运行在宿主机的内容，容器是没有自己的内核的，也没有虚拟我们的硬件，所以就轻便了
- 每个容器间是互相隔离，每个容器内都有一个属于自己的文件系统，互不影响

#### 4.DevOps（开发、运维）

- 应用更快速的交付和部署传统

一对帮助文档，安装程序。

Docker：打包镜像发布测试一键运行。

- 更便捷的升级和扩缩容

使用了 Docker之后，我们部署应用就和搭积木一样

项目打包为一个镜像，扩展服务器A！服务器B

- 更简单的系统运维

在容器化之后，我们的开发，测试环境都是高度一致的

- 更高效的计算资源利用

Docker是内核级别的虚拟化，可以在一个物理机上可以运行很多的容器实例！服务器的性能可以被压榨到极致。

### 二、Docker安装

#### 1.Docker的基本组成

![image-20201031165943761](upload/image-20201031165943761.png)

- **镜像**（image)：

docker镜像就好比是一个目标，可以通过这个目标来创建容器服务，tomcat镜像==>run==>容器（提
供服务器），通过这个镜像可以创建多个容器（最终服务运行或者项目运行就是在容器中的）。

- **容器**(container)：

Docker利用容器技术，独立运行一个或者一组应用，通过镜像来创建的.

启动，停止，删除，基本命令

目前就可以把这个容器理解为就是一个简易的 Linux系统。

- **仓库**(repository)：

仓库就是存放镜像的地方！

仓库分为公有仓库和私有仓库。(很类似git)

Docker Hub是国外的。

阿里云…都有容器服务器(配置镜像加速!)

#### 2.安装Docker

> https://docs.docker.com/engine/install/ 

选择相应的本版本即可

阿里云镜像加速

1、登录阿里云找到容器服务

2、找到镜像加速器

![image-20201031170412531](upload/image-20201031170412531.png)

### 3.底层原理

![image-20201031171030184](upload/image-20201031171030184.png)

- **Docker是怎么工作的？**

Docker是一个Client-Server结构的系统，Docker的守护进程运行在主机上。通过Socket从客户端访问！

Docker-Server接收到Docker-Client的指令，就会执行这个命令！

### 三、Docker常用命令

#### 1.帮助命令

```shell
docker version   #显示docker的版本信息。
docker info    #显示docker的系统信息，包括镜像和容器的数量
docker 命令 --help #帮助命令
#帮助文档的地址：https://docs.docker.com/engine/reference/commandline/build/
```

#### 2.镜像命令

**docker images**查看本地的主机上的镜像

```shell
root@Tj129qi:~# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        10 months ago       13.3kB
REPOSITORY     镜像的仓库
TAG			   镜像的标签
IMAGE ID	   镜像的id
CREATED        镜像的创建时间
SIZE           镜像的大小
# 可选项
-a, --all      #列出所有的镜像
-q,--quiet	   #只显示镜像的id

~ docker images -aq ＃显示所有镜像的id
e73346bdf465
d03312117bb0
d03312117bb0
602e111c06b6
```

**docker pull 下载镜像**

```shell
➜ ~ docker rmi -f 镜像id #删除指定的镜像
➜ ~ docker rmi -f 镜像id 镜像id 镜像id 镜像id#删除指定的镜像
➜ ~ docker rmi -f $(docker images -aq) #删除全部的镜像
```

#### 3.容器命令

说明：我们有了镜像才可以创建容器，linux，下载一个centos镜像来测试学习

> docker pull centos

**新建并启动**

```shell
docker run[可选参数] image
# 参数说明  
--name=“Name”   容器名字tomcat01 tomcat02,用来区分容器
-d 				后台方式运行
-it				使用交互方式运行，进入容器查看内容
-p				指定容器的端口 -p 8080:8080
-P(大写)		   随机指定端口
# 测试： 启动并进入容器
root@Tj129qi:~# docker run -it centos /bin/bash
[root@c86ed7ef9553 /]# ls  # 查看内部容器未见
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@c86ed7ef9553 /]# exit  # 退出容器命令
exit
root@Tj129qi:~#
```

**列出所有运行的容器**

```shell
# docker ps 命令
	#列出当前正在运行的容器
-a # 列出当前正在运行的容器+带出历史运行过的容器
-n=？ #显示最近创建的容器
-q #只显示容器的编号
root@Tj129qi:~# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                          PORTS               NAMES
c86ed7ef9553        centos              "/bin/bash"         3 minutes ago       Exited (0) About a minute ago                       clever_lichterman
e85fb389fd25        bf756fb1ae65        "/hello"            28 hours ago        Exited (0) 28 hours ago                             gracious_rosalind

```

**推出容器**

```shell
exit     #直接容器停止并退出
Ctrl + p + q #容器不停止退出
```

**删除容器**

```shell
docker rm 容器id #删除指定 但不能删除运行的容器  强制删除 rm -f
docker rm -f $(docker ps -aq) #删除所有的
```

**启动和停止容器的动作**

```shell
docker start 容器id 	#启动容器
docker restart 容器id #重启容器
docker stop 容器id	#停止当前正在运行的容器
docker kill 容器id 	#强制停止当前容器
```

#### 4.常用命令

```shell
# 命令 docker run -d 镜像名
➜ ~ docker run -d centos
a8f922c255859622ac45ce3a535b7a0e8253329be4756ed6e32265d2dd2fac6c
➜ ~ docker ps     
CONTAINER ID    IMAGE        COMMAND       CREATED      
STATUS          PORTS        NAMES
# 问题docker ps. 发现centos 停止了
# 常见的坑，docker容器使用后台运行，就必须要有要一个前台进程，docker发现没有应用，就会自动停止
# nginx，容器启动后，发现自己没有提供服务，就会立刻停止，就是没有程序了
```

##### **查看日志**

```shell
docker logs --help
Options:
   --details    Show extra details provided to logs
*  -f, --follow     Follow log output
   --since string  Show logs since timestamp (e.g. 2013-01-02T13:23:37) or
relative (e.g. 42m for 42 minutes)
*    --tail string  Number of lines to show from the end of the logs
(default "all")
*  -t, --timestamps   Show timestamps
   --until string  Show logs before a timestamp (e.g. 2013-01-02T13:23:37)
or relative (e.g. 42m for 42 minutes)
➜ ~ docker run -d centos /bin/sh -c "while true;do echo 6666;sleep 1;done" #模
拟日志   
#显示日志
-tf #显示日志信息（一直更新）
--tail number #需要显示日志条数
docker logs -t --tail n 容器id #查看n行日志
docker logs -ft 容器id #跟着日志
```

##### **查看容器中进程信息 ps**

```shell
# docker top 容器id
root@Tj129qi:~# docker top fe1de6d32573
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                12240               12211               0                   21:03               pts/0               00:00:00            /bin/bash

```

##### **查看镜像的元数据**

```shell
root@Tj129qi:~# docker inspect fe1de6d32573
[
    {
        "Id": "fe1de6d3257307d5ff53904f12b8ebb7f255bdf3e0a9d43b2ca4d73a4f0c0f04",
        "Created": "2020-11-01T13:03:07.966474625Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 12240,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-11-01T13:03:08.580050763Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:0d120b6ccaa8c5e149176798b3501d4dd1885f961922497cd0abef155c869566",
        "ResolvConfPath": "/var/lib/docker/containers/fe1de6d3257307d5ff53904f12b8ebb7f255bdf3e0a9d43b2ca4d73a4f0c0f04/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/fe1de6d3257307d5ff53904f12b8ebb7f255bdf3e0a9d43b2ca4d73a4f0c0f04/hostname",
        "HostsPath": "/var/lib/docker/containers/fe1de6d3257307d5ff53904f12b8ebb7f255bdf3e0a9d43b2ca4d73a4f0c0f04/hosts",
        "LogPath": "/var/lib/docker/containers/fe1de6d3257307d5ff53904f12b8ebb7f255bdf3e0a9d43b2ca4d73a4f0c0f04/fe1de6d3257307d5ff53904f12b8ebb7f255bdf3e0a9d43b2ca4d73a4f0c0f04-json.log",
        "Name": "/wizardly_curie",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/01769c375db4b4b75fd300d6b5e43f538cc7739b006fa50991187fb09288a33b-init/diff:/var/lib/docker/overlay2/b739f96fe7b5dd88dcecd6126932b5e3b311a04d66936bb1d606265babb91cc1/diff",
                "MergedDir": "/var/lib/docker/overlay2/01769c375db4b4b75fd300d6b5e43f538cc7739b006fa50991187fb09288a33b/merged",
                "UpperDir": "/var/lib/docker/overlay2/01769c375db4b4b75fd300d6b5e43f538cc7739b006fa50991187fb09288a33b/diff",
                "WorkDir": "/var/lib/docker/overlay2/01769c375db4b4b75fd300d6b5e43f538cc7739b006fa50991187fb09288a33b/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "fe1de6d32573",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20200809",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "ab6544825715ec4b86b3c70ff20643ee50f5727622e981b5e5d43f971bf75044",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/ab6544825715",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "46a0b535896d00aeb98ca976ae7e48fdb40ac153c18cdd9fc5edb96c2be0c3cf",
            "Gateway": "172.18.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.18.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:12:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "ecf8e3a34fcef3422310d930d98d80ce1d179e0fa3f9b6488904240497634ece",
                    "EndpointID": "46a0b535896d00aeb98ca976ae7e48fdb40ac153c18cdd9fc5edb96c2be0c3cf",
                    "Gateway": "172.18.0.1",
                    "IPAddress": "172.18.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:12:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

##### **进入当前正在运行的容器**

```shell
# 我们通常容器都是使用后台方式运行的，需要进入容器，修改一些配置
# 命令
root@Tj129qi:~# docker exec -it fe1de6d32573 /bin/bash
[root@fe1de6d32573 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@fe1de6d32573 /]# 


# 方式二
docker attach 容器id
#测试
root@Tj129qi:~# docker attach fe1de6d32573
正在执行当前的代码...
区别
#docker exec #进入当前容器后开启一个新的终端，可以在里面操作。（常用）
#docker attach # 进入容器正在执行的终端
```

##### **从容器内拷贝到主机上**

```shell
# docker内创建文件
[root@7419d03cd951 home]# touch t.java
[root@7419d03cd951 home]# ls
t.java
# 将docker拷贝到 /目录下
root@Tj129qi:~# docker cp 7419d03cd951:/home/t.java /
root@Tj129qi:~# cd /
root@Tj129qi:/# ls
bin   etc         initrd.img.old  lib64       mnt   project  sbin      sys     usr      vmlinuz.old
boot  home        jz              lost+found  opt   root     srv       t.java  var
dev   initrd.img  lib             media       proc  run      swapfile  tmp     vmlinuz

```



























