1. 安装 nginx 需要先将官网下载的源码进行编译，编译依赖 gcc 环境，如果没有 gcc 环境，则需要

        yum install gcc-c++
        
2. PCRE（Perl Compatible Regular Expressions）是一个Perl库，包括 perl 兼容的正则表达式库。 nginx 的 http 模块使用 pcre 来解析正则表达式，
所以需要在 linux 上安装 pcre 库，pcre-devel 是使用 pcre 开发的一个二次开发库。nginx也需要此库。

        yum install -y pcre pcre-devel
        
3. zlib 库提供了很多种压缩和解压缩的方式， nginx 使用 zlib 对 http 包的内容进行 gzip 

        yum install -y zlib zlib-devel
        
4. OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理
   
   功能及 SSL 协议，并提供丰富的应用程序供测试或其它目的使用。
   
   nginx 不仅支持 http 协议，还支持 https（即在ssl协议上传输http），所以需要在 Centos 安装
   
   OpenSSL 库。
   
        yum install -y openssl openssl-devel
        
 5. 使用wget命令下载（推荐）。确保系统已经安装了wget，如果没有安装，执行 yum install wget 安装。  (也可以直接到官网下载压缩包，但建议使用wget)
 
        yum install wget 
        // 下载当前最稳定的版本  目前是1.18.0
        wget -c https://nginx.org/download/nginx-1.18.0.tar.gz
 
 6. 解压并进入文件夹
 
        tar -zxvf nginx-1.12.0.tar.gz
        cd nginx-1.12.0
        
 7. 配置
        
        //1 使用默认配置
        ./configure
    
        
        //2 自定义配置
        ./configure \
        --prefix=/usr/local/nginx \
        --conf-path=/usr/local/nginx/conf/nginx.conf \
        --pid-path=/usr/local/nginx/conf/nginx.pid \
        --lock-path=/var/lock/nginx.lock \
        --error-log-path=/var/log/nginx/error.log \
        --http-log-path=/var/log/nginx/access.log \
        --with-http_gzip_static_module \
        --http-client-body-temp-path=/var/temp/nginx/client \
        --http-proxy-temp-path=/var/temp/nginx/proxy \
        --http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
        --http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
        --http-scgi-temp-path=/var/temp/nginx/scgi
        注：将临时文件目录指定为/var/temp/nginx，需要在/var下创建temp及nginx目录

8. 编译安装

        make
        make install 
        或 make install PREFIX=/usr/nginx #这里可以指定安装位置
        
        查找安装路径：
        whereis nginx
        
9. 启动

        cd /usr/local/nginx/sbin/ #进入bin目录
        ./nginx #启动
        ./nginx -s stop #此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程
        ./nginx -s quit #此方式停止步骤是待nginx进程处理任务完毕进行停止
        ./nginx -s reload #刷新
        
        
        浏览器输入ip进入欢迎页面则正确