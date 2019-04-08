### 虚拟机网络配置

虚拟机的网段必须和主机的网段是同一网段才能互相ping通

查看主机的网段

![](https://i.bmp.ovh/imgs/2019/02/d6f55016b35c9053.png)

主机ip：192.168.10.62，则桥接的适配器也必须设置为此网段：

![](https://i.bmp.ovh/imgs/2019/02/2295437655140dcf.png)

设置虚拟机网络

![](https://i.bmp.ovh/imgs/2019/02/12b13568d5fc2740.png)

进入linux，输入下列命令来修改网卡配置文件

`vi /etc/sysconfig/network-scripts/ifcfg-eth0`

其中BOOTPROTO=dhcp (动态ip)

BOOTPROTO=static (静态ip)

动态ip不用设置网关及DNS，静态网关需要设置ip，网关，子网掩码，DNS
