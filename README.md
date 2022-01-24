# 此脚本仅用于远程连接家中局域网内机器，请勿用于任何非法行为！
## 适用于64位Linux系统。
## 运行完毕后屏幕显示psk，默认端口号7770，按照标准填入Surge即可。
# 请使用root用户运行
# 建议使用docker
## https://github.com/primovist/snell-docker
## https://hub.docker.com/repository/docker/primovist/snell-docker

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

Docker使用方法
```
curl -sSL https://get.docker.com/ | sh #安装docker
service docker start #运行
docker pull primovist/snell-docker #拉取镜像文件
```
#运行docker容器的模版，可自行修改

#docker run -d [--env PORT=SERVER_PORT] [--env PSK=PSK_KEYS] [--env OBFS=tls] -p PORT:PORT -p PORT:PORT/udp --name snell-server [-v CONFIG_DIR:/etc/snell/] 
--restart=always primovist/snell-docker

其中：

SERVER_PORT为端口自定义端口CONFIG为自定义配置文件位置

PSK_KEYS为自定义PSK

CONFIG_DIR为自定义配置文件目录

“OBFS=”后可改为http(推荐使用tls)

#或者你也可以直接运行这条命令
```
docker run -d --env PORT=7770 --env PSK=dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg --env OBFS=tls -p 7770:7770 -p 7770:7770/udp --name snell-server -v /etc/snell/:/etc/snell/ 
--restart=always primovist/snell-docker
```
其中：

端为7770

PSK为dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg

配置文件目录为/etc/snell/

OBFS为tls


docker logs snell #查看snell配置
