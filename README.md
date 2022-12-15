# traffic-forward

[中文README](https://github.com/doudoudedi/traffic_forward/blob/main/README_cn.md)

>Traffic forward is a traffic forwarding tool developed by python. It can be run with python script lines or encapsulated with command lines. It can also be run as an executable file under Macos, Linux and Windows using tools such as pyinstaller. It can be used for local traffic forwarding and intranet (remote) traffic forwarding

### 1. Download (Optional)

​	This tool completely uses python native modules for development. It does not require any third-party modules to be secure. If you need to use the command line, you may need sudo

```
pip(3) install traffic_forward
```

![image-20221215192747158](https://raw.githubusercontent.com/doudoudedi/blog-img/master/uPic/image-20221215192747158.png)

### 2. Use

​	lport and lhost are the ports to be forwarded
​	rhost and rport are the target ports for forwarding

#### 2.1 Forwarding local traffic

```
traffic_forward -mode trans -lhost 127.0.0.1 -lport 22 -rhost 127.0.0.1 -rport 9999
```

![image-20221215193437861](https://raw.githubusercontent.com/doudoudedi/blog-img/master/uPic/image-20221215193437861.png)

​	It is normal to use control+c to exit after using, and there will be error output

#### 2.2 Forwarding traffic to public network machines

​	The host on the public network listens to two ports

```
traffic_forward -mode listen -lport 8088 -rport 8089
```

​	The intranet host connects to any port (any of the two) that the public network host listens on. Join the debug to check the connection problems. At this point, the local port 22 is forwarded to the 8088 port of the public network machine

```
traffic_forward -mode slave -lhost 127.0.0.1 -lport 22 -rhost x.x.x.x -rport 8088 -debug 1
```

​	then

```
ssh name@x.x.x.x -p 8089
```

#### 2.3 Forwarding local UDP traffic

​	Because of UDP, only local forwarding of UDP is developed here. If you want to help me develop remote forwarding

```
traffic_forward -mode Utrans -lhost 127.0.0.1 -lport 8090 -rhost 127.0.0.1 -rport 9999
```

#### 2.4 log

​	This tool will generate logs in the current directory. The detailed log function can be deleted if not needed