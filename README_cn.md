# traffic-forward

>traffic-forward 是一款python开发的流量转发工具，可以使用python脚本行运行，也可以封装使用命令行，同样可以使用pyinstaller等工具进行封装成Macos，Linux, Windows 下的可执行文件运行，可用于本地流量转发，与内网（远程）流量转发

### 1. 安装（可选）

​	此工具完全使用python原生的模块进行开发不需要安全任何的第三方模块，如果需要使用命令行可能需要sudo

```
pip(3) install traffic_forward
```

![image-20221215192747158](https://raw.githubusercontent.com/doudoudedi/blog-img/master/uPic/image-20221215192747158.png)

### 2. 使用

​	lport与lhost是需要转发的端口

​	rhost与rport是转发到的目标端口

#### 2.1 转发本地流量

```
traffic_forward -mode trans -lhost 127.0.0.1 -lport 22 -rhost 127.0.0.1 -rport 9999
```


​	在使用完后使用control+c退出会有错误输出这是正常的	

#### 2.2 将流量转发到公网机器

​	在公网上的主机监听2个端口

```
traffic_forward -mode listen -lport 8088 -rport 8089
```

​	内网主机连接公网主机监听的任意端口（2个中任意一个），加入debug可以查看连接出现的问题，此时是讲本地的22端口转发到公网机器的8088口

```
traffic_forward -mode slave -lhost 127.0.0.1 -lport 22 -rhost x.x.x.x -rport 8088 -debug 1
```

​	然后

```
ssh name@x.x.x.x -p 8089
```



#### 2.3 转发本地的UDP流量

​	由于UDP原因，这里只开发到了UDP的本地转发，如果可以希望可以帮组我开发远程转发

```
traffic_forward -mode Utrans -lhost 127.0.0.1 -lport 8090 -rhost 127.0.0.1 -rport 9999
```



#### 2.4. 日志

​	此工具会在当前目录下生成日志，详细日志的功能等待开发可以如果不需要请直接删去
