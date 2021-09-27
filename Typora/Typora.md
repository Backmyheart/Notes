# 下载解压

* 官网下载链接：`Typora-linux-x64.tar.gz`  

* 进入下载文件夹，解压 `Typora-linux-x64.tar.gz`  

```shell
tar -zxvf Typora-linux-x64.tar.gz
```

* 解压得到bin文件夹  

```shell
cd bin  
```

* 进入后可以看到 `Typora-linux-x64` 文件夹  

* 将 `Typora-linux-x64` 文件夹复制到默认用来存放软件的 `/opt`目录

```shell
sudo cp -ar Typora-linux-x64 /opt
```

# 快捷方式

```shell
[Desktop Entry]
Name=Typora
Exec=/opt/Typora-linux-x64/Typora
Type=Application
Icon=/opt/Typora-linux-x64/resources/assets/icon/icon_512x512.png
```

```shell
chmod 777 Typora.desktop
sudo cp Typora.desktop /usr/share/applications/
```



