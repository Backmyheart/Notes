# wifi的一些基本概念

### WLAN
Wireless Local Area Networks，无线局域网络。它利用射频（Radio Frequency，RF）的技术，使用电磁波代替双绞线进行网络通讯。  

### Wi-Fi
Wireless Fidelity是一个无线网络通信技术的品牌，由Wi-Fi联盟所有。目的是改善基于IEEE 802.11标准的无线网路产品之间的互通性。  

### cfg80211
内核空间中用于配置管理无线设备的部分，nl80211为用户空间用于配置管理无线设备。cf80211 与 FullMAC驱动 或 基于mac80211的驱动一起工作。  

### nl80211
用户空间用于配置管理无线设置，它是一个基于NETLink的用户空间协议。cfg80211用于内核空间配置管理无线设备。  
利用NL80211可使用多个用户空间应用。  

### mac80211
用于SoftMac无线芯片的一组驱动API。  

### WIPHY
wireless PYH，无线物理层。  

### PHY
physical-layer，物理层。  

### SSID
Service Set IDentifier。（wifi名称）  

### CLI
command-line interface，提供可以在控制台或终端中运行的调试工具。  

### AP
即无线接入点，是一个无线网络的中心节点。通常使用的无线路由器就是一个AP，其它无线终端可以通过AP相互连接。  

### STA
即无线站点，是一个无线网络的终端。如笔记本电脑、PDA等。  

* 参考连接：https://blog.csdn.net/h784707460/article/details/83750175  

# wifi的几种工作模式

wifi的配置 具体模式主要有以下这几种：STA模式、AccessPoint模式、Monitor模式、Ad-hoc（IBSS）模式、WDS模式、Mesh模式。  

### STA模式  

任何一种无线网卡都可以运行在此模式下，这种模式也可以称为默认模式。在此模式下，无线网卡发送连接与认证消息给热点，热点接收到完成认证后，发回成功认证消息，此网卡接入无线网络。这种模式下，wifi工作于从模式。  

此模式由一个AP和许多STA组成，如下图。其特点是AP处于中心地位，STA之间的相互通信都通过AP转发完成。  

![image-20210826110413518](/home/kylin/.config/Typora/typora-user-images/image-20210826110413518.png)  

### AP模式  

在一个无线网络环境中，无线热点是作为一个主设备，工作于主模式（Master Mode）。通过管理可控制的STA，从而组成无线网络，也有相应的安全控制策略。由AP形成的网络，由AP的MAC地址唯一识别。热点完成创建后，会由热点创建一个被别的设备可识别的名称，称为SSID。在Linux下，要使用AP模式，必须使系统支持hostapd。  

工作在AP模式下，手机、PAD、电脑等设备可以直接连上模块，可以很方便对用户设备进行控制。  

![image-20210826110538254](/home/kylin/.config/Typora/typora-user-images/image-20210826110538254.png)  

### Monitor模式  

这种模式下，所有的数据包无过滤地传输到主机，此模式下主要查看网络中出了那些故障。在支持MAC80211的一般设备中，工作于Monitor模式下，可以有效地对整个网络进行监控，在此模式下，可以实现数据包的注入，在用户模式下，想要在应用程序中部署MLME（Media Access Control (MAC) Sublayer Management Entity）非常有用。  

### Ad-hoc（IBSS）模式

Ad-hoc又称为独立基本业务集，用以创建一个无线网络，此网络中不需要热点（AP），此网络中的每个节点的地位都是对等的，此模式用以连接几个不能通过基站进行通信的电脑。ad-hoc模式就和以前的直连双绞线概念一样，是P2P的连接，所以也就无法与其它网络沟通了。一般无线终端设备像PMP、PSP、DMA等用的就是ad-hoc模式。  

在家庭无线局域网的组建，大家都知道最简单的莫过于两台安装有无线网卡的计算机实施无线互联，其中一台计算机连接Internet就可以共享带宽。Ad-Hoc结构是一种省去了无线AP而搭建起的对等网络结构，只要安装了无线网卡的计算机彼此之间即可实现无线互联；其原理是网络中的一台电脑主机建立点对点连接相当于虚拟AP，而其它电脑就可以直接通过这个点对点连接进行网络互联与共享。  

由于省去了无线AP，Ad-Hoc无线局域网的网络架设过程十分简单，不过一般的无线网卡在室内环境下传输距离通常为40m左右，当超过此有效传输距离，就不能实现彼此之间的通讯；因此该种模式非常适合一些简单甚至是临时性的无线互联需求。  

### WDS模式

WDS全名为无线分布式系统。以往在无线应用领域中它都是帮助无线基站与无线基站之间进行联系通讯的系统。WDS的功能是充当无线网络的中继器，通过在无线路由器上开启WDS功能，让其可以延伸扩展无线信号，从而覆盖更广更大的范围。WDS可以让无线AP或者无线路由器之间通过无线进行桥接（中继），而在中继的过程中并不影响其无线设备覆盖效果的功能。这样我们就可以用两个无线设备，让其之间建立WDS信任和通讯关系，从而将无线网络覆盖范围扩展到原来的一倍以上，大大方便了我们无线上网。  

### mesh模式

Mesh接口使设备之间动态建立路由，从而实现通信。无线Mesh网络中，任何无线设备节点都可以同时作为AP和路由器，网络中的每个节点都可以发送和接收信号，每个节点都可以与一个或者多个对等节点进行直接通信。这种结构的最大好处在于：如果最近的AP由于流量过大而导致拥塞的话，那么数据可以自动重新路由到一个通信流量较小的邻近节点进行传输。依此类推，数据包还可以根据网络的情况，继续路由到与之最近的下一个节点进行传输，直到到达最终目的地为止。这样的访问方式就是多跳访问。  


# wifi三种安全模式

目前，无线网络中已存在好几种加密技术，最常使用的是 WEP 和 WPA 两种加密方式。无线局域网的第一个安全协议——802.11 Wired Equivalent Privacy（WEP)，一直受到人们的质疑。虽然WEP可以阻止窥探者进入无线网络，但是人们还是有理由怀疑它的安全性，因为WEP破解起来非常容 易，就像一把锁在门上的塑料锁。  

### WEP安全加密方式

WEP 特性里使用了rsa数据安全性公司开发的rc4 prng算法。全称为有线对等保密（Wired Equivalent Privacy，WEP），是一种数据加密算法，用于提供等同于有线局域网的保护能力。使用了该技术的无线局域网，所有客户端与无线接入点的数据都会以一个 共享的密钥进行加密，密钥的长度有40位至256位两种，密钥越长，黑客就需要更多的时间去进行破解，因此能够提供更好的安全保护。  

### WPA安全加密方式

WPA加密即Wi-Fi Protected Access，其加密特性决定了它比WEP更难以入侵，所以如果对数据安全性有很高要求，那就必须选用WPA加密方式了（Windows XP SP2已经支持WPA加密方式）。  

WPA作为IEEE 802.11通用的加密机制WEP的升级版，在安全的防护上比WEP更为周密，主要体现在身份认证、加密机制和数据包检查等方面，而且它还提升了无线网络的管理能力。  









---

# hostapd配置AP热点

### 配置hostapd.cfg

```shell
interface=wlp0s20f3
ctrl_interface=/var/run/hostapd
ssid=ap_ssid
channel=3
driver=nl80211
hw_mode=g
auth_algs=1
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=CCMP
wpa_passphrase=12345678
wme_enabled=1
ieee80211n=1
ht_capab=[SHORT_GI_20][SHORT_GI_40][HT40+]
max_num_sta=8
```

### 设置网卡IP

设置当前网卡IP为192.168.43.1，命令如下：  

ifconfig wlp0s20f3 192.168.43.1 up

### 启动hostapd 工具，记得-B表示后台运行

hostapd -B hostapd.cfg

### 安装配置dhcp服务器

`sudo apt-get install isc-dhcp-server`  

修改配置文件/etc/dhcp/dhcpd.conf：  

```shell
mv dhcpd.conf ./dhcpd.conf.bak	# 备份原来的配置文件
vim dhcpd.conf
```

加入如下内容：  

```shell
# 指定确省租赁时间的长度，单位是秒
default-lease-time 600;

# 指定最大租赁时间长度，单位是秒 
max-lease-time 7200;

# subnet: 描述一个IP地址是否属于该子网
# range: 起始IP 终止IP 提供动态分配IP 的范围
# routers: 为客户端设定默认网关
# broadcast-address: 为客户端设定广播地址
option domain-name-servers 114.114.114.114;
subnet 192.168.43.0 netmask 255.255.255.0 {    
range 192.168.43.20 192.168.1.250;
option routers 192.168.43.1;    
option broadcast-address 192.168.43.255;
}
```

重启服务：  

`sudo /etc/init.d/isc-dhcp-server restart`  

### 打开linux转发功能

`sudo sysctl -w net.ipv4.ip_forward=1`

### 开启防火墙NAT转发

**`iptables -o enp0s31f6` 这儿修改为你有线上网的网口名称。**  

```shell
iptables -t nat -I POSTROUTING -o enp0s31f6 -j MASQUERADE      
iptables -A FORWARD -s 192.168.43.0/24 -j ACCEPT  
iptables -A FORWARD -d 192.168.43.0/24 -j ACCEPT
```











