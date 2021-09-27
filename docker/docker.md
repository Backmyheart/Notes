# docker配置文件


vim  /etc/docker/key.conf (后缀是 conf 配置文件):  

```shell
{
        "graph":"/mnt/docker-data",
        "storage-driver":"overlay"
}


{
        "registry-mirrors" : [
                "http://ovfftd6p.mirror.aliyuncs.com",
                "http://registry.docker-cn.com",
                "http://docker.mirrors.ustc.edu.cn",
                "http://hub-mirror.c.163.com"
        ],
        "insecure-registries" : [
                "registry.docker-cn.com",
                "docker.mirrors.ustc.edu.cn"
        ],
        "debug" : true,
        "experimental" : true                                                                                                                                                                    
}
```


# 在用户目录下在新建一个脚本

```shell
mkdir /home/kylin/zhulei/wechat
vim wechat.sh
```

```shell
sudo docker run -d --name wechat    \
    --device /dev/snd --ipc=host    \
    -v /tmp/.X11-unix:/tmp/.X11-unix    \
    -v $HOME/WeChatFiles:/WeChatFiles   \
    -e DISPLAY=unix$DISPLAY \
    -e XMODIFIERS=@im=fcitx \
    -e QT_IM_MODULE=fcitx   \
    -e GTK_IM_MODULE=fcitx  \
    -e VIDEO_GID=`getent group video | cut -d: -f3` \
    -e AUDIO_GID=`getent group audio | cut -d: -f3` \
    -e GID=`id -g`  \
    -e UID=`id -u`  \
    bestwu/wechat
```

# 运行

sudo ./wechat.sh

启动微信：  

docker start wechat  

停止微信：  

docker stop wechat

查看当前容器开启的东西：  

docker ps -a



