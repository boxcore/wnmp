WNMP使用说明
============

wnmp是windows+nginx+mysql+php的简称, 是windows平台下的nginx 网站服务软件. 目前网络上wnmp软件众多, 此版wnmp的nginx, mysql和php都是从官方网站下载的绿色软件包集合而成, 并对其配置进行优化打包发行.
目前此版本的wnmp使用的服务版本号如下:  

- nginx v1.6.0
- apache v2.2( `WNMP+`版 )
- mysql v5.5
- php v5.3.29

如果你想更换nginx, mysql或php的版本, 直接到官方网站下载, 然后把相关软件目录替换即可.

下载WNMP
-----------------
- __WNMP Plus v2.1__ : [百度网盘下载](http://pan.baidu.com/s/1pK82pOf)  [备份镜像](http://mirrors.mianfeibang.cn/wnmp/wnmp_plus_v2.1.zip)   

- __WNMP v0.1__ : [百度网盘下载](http://pan.baidu.com/s/1i4KjMw1) [备份镜像](http://mirrors.mianfeibang.cn/wnmp/wnmp_v0.1.zip)  

安装WNMP
------------------
wnmp默认制定目录`D:\wnmp`为根目录, 如果你更改了安装目录需要修改nginx下的配置文件中有`D:\wnmp`的部分为你所要安装的目录.

更改目录后您需要修改的文件有:
{你的WNMP目录}/nginx/conf下的`nginx.conf`, `wwwroot.conf`和`wwwroot.map`

如何使用wnmp
-----------------

wnmp的软件目录结构为:
```
./apache2/                  // Apache目录, 默认版本2.2, WNMP+版才有此目录
./apache2/conf/httpd.ini    // Apache默认配置文件
./apache2/conf/extra/httpd-vhosts.conf      //Apache虚拟网站配置文件
    
./mysql/                    // MySQL目录, 默认版本5.5
./mysql/my.ini              // MySQL配置文件

./nginx/                    // nginx目录, 默认版本1.6.0
./nginx/nginx.exe
./nginx/conf/nginx.conf     // nginx默认配置文件
./nginx/conf/wwwroot.conf   // 网站默认配置 
./nginx/conf/wwwroot.map    // 网站列表
./nginx/conf/vhost/*.conf   // 虚拟网站配置

./php/                      // php软件包目录, 默认版本5.5.13
./php/php.ini               // php配置文件

./www/                      // web默认目录
./www/phpmyadmin/           // PMA

./RunHiddenConsole.exe      // 后端最小化运行程序
./start_wnmp.bat            // 开启wnmp服务批处理文件
./stop_wnmp.bat             // 关闭wnmp服务批处理文件
./start_wamp.bat            // 开启wamp服务批处理文件
./stop_wamp.bat             // 关闭wamp服务批处理文件
```

- 启动WNMP: 运行 `start_wnmp.bat`即可启动WNMP服务
- 关闭WNMP: 运行 `stop_wnmp.bat`即可关闭WNMP服务

`WNMP+`版添加了apache的服务, 启用WAMP相应的服务文件有:

- 启动WAMP: 运行 `start_wamp.bat`即可启动WAMP服务
- 关闭WAMP: 运行 `stop_wamp.bat`即可关闭WAMP服务

添加环境变量
-----------------
右击【我的电脑】-> 选择【属性】-> 选择【高级】选项卡 ->  【环境变量】 ->  设置PATH中添加如下的环境变量配置: 

`;D:\wnmp\mysql\bin;D:\wnmp\nginx;D:\wnmp\php`

然后在cmd中输入`PATH=%PATH%;D:\wnmp\mysql\bin;D:\wnmp\nginx;D:\wnmp\php`使系统环境生效.


Nginx配置网站说明
-----------------

本版的WNMP的网站配置添加了map列表来遍历网站配置, 而不需要为单独一个网站配置一个配置文件, 具体实现原理可以看文件`./nginx/conf/wwwroot.conf`如:

```bash
server {
    
    listen       80; 
    server_name  $host ;
    index  index.php index.html index.htm index.shtml;
    root   D:/wnmp/www/$wwwroot;

    location ~ ^.+\.php {
        fastcgi_split_path_info ^(.+\.php)(.*)$;
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
        fastcgi_connect_timeout 60;
        fastcgi_send_timeout    180;
        fastcgi_read_timeout    180;
        fastcgi_buffer_size 128k;
        fastcgi_buffers 4 256k;
        fastcgi_busy_buffers_size 256k;
        fastcgi_temp_file_write_size 256k;
        fastcgi_intercept_errors on;
        include     fastcgi_params;      
    }
}
```

上面的`$host`变量和`$wwwroot`分别配置网站域名和网站目录, 目录必须在`D:/wnmp/www/`下创建, 域名和目录的配置列表保存在`./nginx/conf/wwwroot.map`下, 一行配置一个域名和目录并以分号结束, 如: 
`hello.lc.boxcore.org       sites/hello;`, 是用来指定网站hello.lc.boxcore.org的文件目录在`D:/wnmp/www/sites/hello`下.

另外注意wwwroot.map中配置的网站默认为index.php单入口, 这对框架开发很便捷, 当然, 也可以创建`./nginx/conf/vhost/*.conf`类似的文件添加网站配置文件. 

Apache配置网站说明
------------------

WNMP+中的apache虚拟网站配置在文件`./apache2/conf/extra/httpd-vhosts.conf`中, 添加一个网站test.com配置如: 

```
<VirtualHost *:80>
    ServerAdmin admin@localhost
    DocumentRoot "d:/wnmp/www/sites/{DIR}"
    ServerName www.test.com
    ServerAlias test.com
    ErrorLog "d:/wnmp/logs/test-error.log"
    CustomLog "d:/wnmp/logs/test-access.log" common
</VirtualHost>
```



Todo
-------------------------------------
- windows下apache+nginx协同工作机制研究

