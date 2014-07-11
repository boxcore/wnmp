WNMP使用说明
============

wnmp是windows+nginx+mysql+php的简称, 是windows平台下的nginx 网站服务软件. 目前网络上wnmp软件众多, 此版wnmp的nginx, mysql和php都是从官方网站下载的绿色软件包集合而成, 并对其配置进行优化打包发行.
目前此版本的wnmp使用的服务版本号如下:  

- nginx v1.6.0
- mysql v5.5
- php v5.5.13

如果你想更换nginx, mysql或php的版本, 直接到官方网站下载, 然后把相关软件目录替换即可. 本版本的WNMP套件在win8和win7下测试成功.

下载WNMP
-----------------

__WNMP v0.1__

- [网盘下载](http://yunpan.cn/QhIkKZ6DiCvHK)（访问密码 b0c3）
- [镜像下载](http://mirrors.boxcore.org/wnmp/wnmp_v0.1.zip)


安装WNMP
------------------
wnmp默认指定`D:\wnmp`为根目录, 如您不是把`D:\wnmp`作为为根目录,那么需要修改的文件有:
`{WNMP目录地址}/nginx/conf/nginx.conf`, `{WNMP目录地址}/nginx/conf/wwwroot.conf`和`{WNMP目录地址}/nginx/conf/wwwroot.map`

如何使用wnmp
-----------------

- __启动WNMP__: 运行 `start_wnmp.bat`
- __关闭WNMP__: 运行 `stop_wnmp.bat`

wnmp的软件目录结构为:
```
./mysql/            // MySQL目录, 默认版本5.5
    my.ini          // MySQL配置文件
./nginx/            // nginx目录, 默认版本1.6.0
    conf/vhost/     // 虚拟域名配置目录
    conf/nginx.conf // nginx默认配置文件
    conf/wwwroot.conf   //默认文章配置
    conf/wwwroot.map    // 使用map快捷匹配网站目录
./php/              // php软件包目录, 默认版本5.5.13
./www/              // web默认目录
    phpmyadmin/     // PMA
./RunHiddenConsole.exe    // 后端最小化运行程序
./start_wnmp.bat    // 开启wnmp服务批处理文件
./stop_wnmp.bat     // 关闭wnmp服务批处理文件
```

说明
---------------


Todo
----------------------------
- 添加绿色版的apache
- nginx使用相对目录的配置
- win XP下测试有路径转换错误问题

