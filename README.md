# 此脚本仅用于远程连接家中局域网内机器，请勿用于任何非法行为！
## 适用于64位Linux系统。
## 运行完毕后屏幕显示psk，默认端口号7770，按照标准填入Surge即可。
## 请使用root用户运行
## 建议使用docker
## https://github.com/primovist/snell-docker
## https://hub.docker.com/repository/docker/primovist/snell-docker

## 先进行系统的更新及组件安装
```
apt update -y          #Debian/Ubuntu 
apt install -y curl    #Debian/Ubuntu 
apt-get install wget   #Debian/Ubuntu 
yum update -y          #CentOS 
yum install -y curl    #CentOS 
yum -y install wget    #CentOS
```
开启系统自带bbr加速

```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
lsmod | grep bbr
```


## 非docker使用方法
Debian & Ubuntu 用户请运行

```
wget --no-check-certificate -O snell.sh https://raw.githubusercontent.com/Evan07NE/snell.sh/master/snell.sh
chmod +x snell.sh
./snell.sh
```

Centos & RedHat 用户请运行

```
wget --no-check-certificate -O snell.sh https://raw.githubusercontent.com/Evan07NE/snell.sh/master/snell.centos.sh
chmod +x snell.sh
./snell.sh
```

首次安装默认端口号7770，如需修改请在所有脚本运行结束后运行

```
nano /etc/snell/snell-server.conf #或使用 vi /etc/snell/snell-server.conf
systemctl restart snell
```

自行修改。

查看运行状态：

```
systemctl status snell
```

管理Snell服务命令：

```
systemctl status snell #查看运行状态
systemctl restart snell #重启Snell服务
systemctl start snell #启动Snell服务
systemctl stop snell #停止Snell服务
cat /etc/snell/snell-server.conf #查看Snell配置文件
vi /etc/snell/snell-server.conf #修改Snell配置文件
```

卸载方法：

```
wget --no-check-certificate -O uninstall-snell.sh https://raw.githubusercontent.com/primovist/snell.sh/master/uninstall-snell.sh
chmod +x uninstall-snell.sh
./uninstall-snell.sh
```

## Docker使用方法（此方法可能使用的为旧版snell协议 --2.05）
```
curl -sSL https://get.docker.com/ | sh #安装docker
service docker start #运行
docker pull primovist/snell-docker #拉取镜像文件
```

#你可以直接运行以下命令来配置snell,也可以自行修改
```
docker run -d --env PORT=7770 --env PSK=dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg --env OBFS=tls -p 7770:7770 -p 7770:7770/udp --name snell-server -v /etc/snell/:/etc/snell/ 
--restart=always primovist/snell-docker
```
其中：

端为7770

PSK为dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg

配置文件目录为/etc/snell/

OBFS为tls

查看snell配置:
```
docker logs snell
```


## Snell客户端配置
目前，支持Snell协议的常用客户端有 Trojan-Qt5、Clash、Shadowrocket 和 Surge，其中 Trojan-Qt5 只支持Windows/MacOS/Linux，Clash客户端支持Windows/MacOS/Linux/Android/网关路由器等平台（不支持iOS系统），安卓端使用 Clash for Android，苹果iOS端使用 Shadowrocket 或 Surge for iOS，Mac端也可以使用 surge for Mac 。

搭建成功的Snell服务器配置参数只有4个，具体配置示例如下：
```
 IP地址：x.x.x.x
 端口：7770
 PSK ：dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg
 obfs ： tls
```
