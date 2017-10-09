# nginx- 流媒体服务器搭建

服务器 环境 ubuntu 14.04 
 
 需要先安装 unzip vim 工具，自行百度安装
 
### 1.先下载安装  nginx 和 nginx-rtmp 编译依赖工具


sudo apt-get install build-essential libpcre3 libpcre3-dev libssl-dev

 
如果 安装不成功，aptitude -f install 强制安装 
 


### 2. 创建一个工作目录，并切换到工作目录

mkdir /usr/jason/nginx
cd /usr/lsw/nginx

### 3. 下载 nginx 和 nginx-rtmp源码（wget是一个从网络上自动下载文件的自由工具）

wget http://nginx.org/download/nginx-1.8.1.tar.gz

wget https://github.com/arut/nginx-rtmp-module/archive/master.zip

### 4. 安装unzip工具，解压下载的安装包

sudo apt-get install unzip

### 5.解压 nginx 和 nginx-rtmp安装包

tar -zxvf nginx-1.8.1.tar.gz

-zxvf分别是四个参数

x : 从 tar 包中把文件提取出来

z : 表示 tar 包是被 gzip 压缩过的，所以解压时需要用 gunzip 解压

v : 显示详细信息

f xxx.tar.gz :  指定被处理的文件是 xxx.tar.gz

unzip master.zip

### 6. 切换到 nginx-目录

cd nginx-1.8.1

### 7.添加 nginx-rtmp 模板编译到 nginx

./configure --with-http_ssl_module --add-module=../nginx-rtmp-module-master

### 8.编译安装 

make
sudo make install

### 9. 安装nginx init 脚本

sudo wget https://raw.github.com/JasonGiedymin/nginx-init-ubuntu/master/nginx -O /etc/init.d/nginx

sudo chmod +x /etc/init.d/nginx

sudo update-rc.d nginx defaults

### 10. 启动和停止nginx 服务，生成配置文件

sudo service nginx start

sudo service nginx stop

### 11. 安装 FFmpeg 下载ffmpeg zip ，然后解压

./configure   (先配置然后才能编译)

make

make install

### 12. 配置 nginx-rtmp 服务器

打开 /usr/local/nginx/conf/nginx.conf

在末尾添加如下 配置


```bash

    rtmp {
    
        server {
    
            listen 886;
            
            chunk_size 4096;
            
            application live {
            
                    live on;
                    
                    record off;
                    
                    exec ffmpeg -i rtmp://localhost/live/$name -threads 1 -c:v libx264 -profile:v baseline -b:v 350K -s 640x360 -f flv -c:a aac -ac 1 -strict -2 -b:a 56k rtmp://localhost/live360p/$name;
                    
            }
            
            application live360p {
            
                    live on;
                    
                    record off;
                     }       
        }        
    }  
    
```
 

 
 


 
### 13. 保存上面配置文件，然后重新启动nginx服务

sudo service nginx restart

### 14. 如果你使用了防火墙，请允许端口 tcp 886
 
 
### 16: 使用 客户端，使用 rtmp协议进行视频实时采集

Field 1: rtmp://your.vultr.ip/live/

Field 2: stream-key-your-set


服务器配置测试播放器：

播放器放到 https://github.com/lsw8569013/nginx-/tree/master/FlashPlayer
将播放器复制到目录：/usr/local/nginx/html/，然后修改播放地址 sc://ip:端口

用ffplay播放RTMP直播流：

ffplay "rtmp://pub1.guoshi.com/live/newcetv1 live=1"



 ---------------------------------------------------------
 
 服务器搭建成功 测试地址在 
 
 nginx/html  index.html 
 
 可自行修改 
 
 可以在IE 输入服务器地址 查看index.html 
 不用重启
 
 
