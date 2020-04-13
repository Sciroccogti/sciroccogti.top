---
title:      "完整建站历程"
date:       2020-02-03T20:07:28+08:00
tags:       ["软件"]
summary:    Ubuntu 18.04下的完整网站搭建
---

# 完整建站历程

眼见着弟兄们都搭起了自己的个人网站，我也按捺不住手痒，入坑搭网站，走起！

！！注意：本页环境均为 *Ubuntu18.04*

## 初试：Github Pages + Jekyll

这个组合是最简单的、最适合新手入门的，只要会使用 *github* 和 *markdown* ，就完全没压力。

可能有同学会在安装本地 *nodejs* 的 *jekyll* 模块的步骤上遇到问题。
事实上，我从头到尾都没有在本地预览过（没错，这个本机的 *jekyll* 模块只是用来给你预览的）。
反正主题也是抄的，文字是 *markdown* 写的也能直接预览，其它的一些小设定多试几次就好了。

如果你从没接触过网站搭建，甚至连 *linux* 都没摸过，那显然用 *Github Pages* + *Jekyll* 是再适合不过的了。
教程满天飞，也不怕翻车，甚至不花一分钱。

## 晋级：新的需求

有一天突然想买个服务器，想拿它做[贴吧一键签到](https://github.com/MoeNetwork/Tieba-Cloud-Sign)，做[密码保管箱](https://github.com/dani-garcia/bitwarden_rs)，做云盘。
于是就到阿里云买了一个（一开始是和同学合用的，后来我嫌他占用了80端口，很烦躁，就自己单飞了😂

然而还是从静态博客开始，改用 *Hugo* 。
其实这跟 *Jekyll* 没区别，甚至文档更少、更乱（但是想抄同学主题🙃）。
不过之前 *Github Pages* 做的工作，就得自己完成了。

### 使用内网穿透工具 frp

有了服务器上的稳定ip地址后，我就可以把宿舍里的NAS映射出来了。

这时候自然选用久负盛名的 *frp* 来实现内网穿透了。

这里提一下花生壳。
花生壳虽然部分免费，并且许多功能也集成在了NAS里，非常方便，但是对于已经有财力购买服务器的我来说，实属束缚。
不过，由于NAS的 *Linux* 并非完全放开，只能运行有限的命令，因此我只好曲线救国，修改了内置的花生壳的自启动命令来自启动 *frp* 。

```ini
# frps.ini，在服务器上
[common]
bind_port = aaaa
vhost_http_port = bbbb
```

```ini
# frpc.ini，在内网主机上，暂缺
```
### 使用静态博客系统 Hugo

基本上就是`hugo new xxx.md`或者`hugo new xxx/`以及`hugo -s ./`这几条命令，别的就看选用的主题的要求了。

### 使用web服务器 Caddy

在我转入使用自己的服务器后，就开始摸索使用 *LAMP* 或者 *LNMP* 。
然而，无论是 *Apache* 还是 *Nginx* 对于新用户都非常不友好，各种RTFM和STFW都无济于事。
在咨询同学后，隔壁大佬推荐我用 *Caddy* 入门。

不得不说，真香。
仅需一个文件一个命令就能完成所有的任务

（教程暂缺）

但是 *Caddy* 的自启动我却始终摸不透，无法启用。
同时，当要搭建的网站多起来的时候，入门级的 *Caddy* 就不是很适合了。

## 完善：更全面的功能

经过数月的时间，我购置了自己的域名，也用来一周做好了备案，整个网站的基本功能都已经实现。

但是，要想在合适的地方提供贴吧签到跳转，而不是要求用户输入奇怪的端口好，成为了新的需求。
这就需要完善的反向代理服务。

### 使用web服务器 Apache2

再次咨询同学后，我转身推开 *Apache* 的大门。

 *Apache* 功能非常完善，但是使用起来也十分复杂，更何况教程并不多。
不过，使用`sudo apt install apache2`安装 *apache2* 后，只需在`/etc/apache2`内修改配置文件，就能够实现想要的功能。
（别忘了`sudo service apache2 restart`）

以下给出我的配置文件（以`/etc/apache2`为根目录）

```conf
# apache2.conf
DefaultRuntimeDir ${APACHE_RUN_DIR}
PidFile ${APACHE_PID_FILE}
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 5
User ${APACHE_RUN_USER}
Group ${APACHE_RUN_GROUP}
HostnameLookups Off
ErrorLog ${APACHE_LOG_DIR}/error.log
LogLevel warn
IncludeOptional mods-enabled/*.load
IncludeOptional mods-enabled/*.conf
Include ports.conf

<Directory />
	Options FollowSymLinks
	AllowOverride None
	Require all denied
</Directory>

<Directory /usr/share>
	AllowOverride None
	Require all granted
</Directory>

# /var/www 是lamp示例文件所在地
<Directory /var/www/>
	Options Indexes FollowSymLinks
	AllowOverride None
	Require all granted
</Directory>
```

下面这个配置文件借鉴自[阿里云教程](https://help.aliyun.com/document_detail/98727.html)
```conf
# sites-enabled/000-default.conf
# https代理，借鉴自https://help.aliyun.com/document_detail/98727.html
<VirtualHost *:80>
ServerName sciroccogti.top
	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
    # 自动转发到https
    RewriteEngine on
    RewriteCond %{SERVER_PORT} !^443$
    RewriteRule ^(.*)$ https://%{SERVER_NAME}$1 [L,R]
</VirtualHost>

<VirtualHost *:443>     
    ServerName   www.sciroccogti.top
    #修改为申请证书时绑定的域名www.YourDomainName1.com。
    DocumentRoot  /var/www/html
    SSLEngine on   
    SSLProtocol all -SSLv2 -SSLv3 
    # 添加SSL协议支持协议，去掉不安全的协议。
    SSLCipherSuite HIGH:!RC4:!MD5:!aNULL:!eNULL:!NULL:!DH:!EDH:!EXP:+MEDIUM
    # 修改加密套件。
    SSLHonorCipherOrder on
    SSLCertificateFile cert/domain name1_public.crt
    # 将domain name1_public.crt替换成您证书文件名。
    SSLCertificateKeyFile cert/domain name1.key
    # 将domain name1.key替换成您证书的密钥文件名。
    SSLCertificateChainFile cert/domain name1_chain.crt
    # 将domain name1_chain.crt替换成您证书的密钥文件名；证书链开头如果有#字符，请删除。
</VirtualHost>
```

下面这个配置文件借鉴自[Bitwarden_rs Wiki](https://github.com/dani-garcia/bitwarden_rs/wiki/Proxy-examples)，用于下一节中的密码管理器 *Bitwarden_rs* 
```conf
# sites-enabled/password.conf
<VirtualHost *:80>
    # 正常的http反向代理部分
	ServerName password.sciroccogti.top

    ProxyRequests off
     
    <proxy http://a.b.c.d:xxx>
        ProxyPass http://password.sciroccogti.top
        ProxyPassReverse http://password.sciroccogti.top
        Order Allow,Deny
        Allow from all
    </proxy>

    ProxyPass / "http://a.b.c.d:xxx/"
    ProxyPassReverse / "http://a.b.c.d:xxx/"

	ServerAdmin webmaster@localhost

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

	# 自动转发到https
    RewriteEngine on
    RewriteCond %{SERVER_PORT} !^443$
    RewriteRule ^(.*)$ https://%{SERVER_NAME}$1 [L,R]
</VirtualHost>

<VirtualHost *:443>
    # https反向代理部分
    ServerName      password.sciroccogti.top
    #修改为申请证书时绑定的域名www.YourDomainName1.com。
    ProxyRequests Off
    ProxyPreserveHost On
    ProxyPass / "http://a.b.c.d:8080/"

    SSLEngine on   
    SSLProtocol all -SSLv2 -SSLv3 
    # 添加SSL协议支持协议，去掉不安全的协议。
    SSLCipherSuite HIGH:!RC4:!MD5:!aNULL:!eNULL:!NULL:!DH:!EDH:!EXP:+MEDIUM
    # 修改加密套件。
    SSLHonorCipherOrder on
    SSLCertificateFile cert/domain name1_public.crt
    # 将domain name1_public.crt替换成您证书文件名。
    SSLCertificateKeyFile cert/domain name1.key
    # 将domain name1.key替换成您证书的密钥文件名。
    SSLCertificateChainFile cert/domain name1_chain.crt
    # 将domain name1_chain.crt替换成您证书的密钥文件名；证书链开头如果有#字符，请删除。
    
    # 用于开启websocket通知
    #RewriteEngine On
    #RewriteCond %{HTTP:Upgrade} =websocket [NC]
    #RewriteRule /notifications/hub(.*) ws://47.103.78.58:3012/$1 [P,L]
    
</VirtualHost>
```

### 使用密码管理器 Bitwarden_rs

```Bash
docker pull bitwardenrs/server:latest
docker run -d --name bitwarden   -e WEBSOCKET_ENABLED=true   -v /bw-data/:/data/   -p xxx:80   -p 3012:3012   bitwardenrs/server:latest
# xxx：自定义端口，一般为80；3012：开启浏览器推送功能
```

 *Bitwarden_rs* 是用 *Rust* 重写的 *Bitwarden* ，这个版本的 *Docker* 容器不仅内存占用小，而且功能全面，直接实现了原本的高级功能。
美中不足的是，必须开启https才能在 *chrome* 浏览器以及 *iOS* 客户端使用。
（并未测试原版镜像）

！友情提示：使用https的时候记得开启服务器的443端口！
（我搞了一整天没开启https，结果发现是443没开。。其实 *apache* 配置容错度没那么小的）

### Nginx

最近需要使用 gzip 功能，但是 Apache 配置实在太难了！

#### 安装

`sudo apt install nginx`

配置文件位于：`/etc/nginx`

修改完配置后：`sudo nginx -s reload`
