WNMP使用说明
============

wnmp是windows+nginx+mysql+php的简称, 是windows平台下的nginx 网站服务软件. 目前网络上wnmp软件众多, 此版wnmp的nginx, mysql和php都是从官方网站下载的绿色软件包集合而成, 并对其配置进行优化打包发行.
目前此版本的wnmp使用的服务版本号如下:  

- nginx v1.6.0
- mysql v5.5
- php v5.5.13

如果你想更换nginx, mysql或php的版本, 直接到官方网站下载, 然后把相关软件目录替换即可.

下载WNMP
-----------------

__WNMP v0.1__ : [镜像下载](http://mirrors.boxcore.org/wnmp/wnmp_v0.1.zip)

安装WNMP
------------------
wnmp默认制定目录`D:\wnmp`为根目录, 如果你更改了安装目录需要修改nginx下的配置文件中有`D:\wnmp`的部分为你所要安装的目录.

更改目录后需要修改的文件有:
{你的WNMP目录}/nginx/conf下的`nginx.conf`, `wwwroot.conf`和`wwwroot.map`

如何使用wnmp
-----------------

wnmp的软件目录结构为:
```
./mysql/            // MySQL目录, 默认版本5.5
    my.ini          // MySQL配置文件
./nginx/            // nginx目录, 默认版本1.6.0
    nginx.exe
    RunHiddenConsole.exe    // 后端最小化运行程序

./php/              // php软件包目录, 默认版本5.5.13
./www/              // web默认目录
    phpmyadmin/     // PMA
./start_wnmp.bat    // 开启wnmp服务批处理文件
./stop_wnmp.bat     // 关闭wnmp服务批处理文件
```

- 启动WNMP: 运行 `start_wnmp.bat`即可启动WNMP服务
- 关闭WNMP: 运行 `stop_wnmp.bat`即可关闭WNMP服务

Todu
----------------------------
- 添加绿色版的apache
- nginx使用相对目录的配置

