# certbot-dns-aliyun
certbot-dns-aliyun



## 应用certbot-dns-aliyun
在项目目录创建文件夹
~~~
# 创建文件夹certbot和certbot/letsencrypt
mkdir certbot
cd certbot
mkdir letsencrypt
# 创建文件credentials.ini
nano credentials.ini
# 粘贴下边内容进文件内（注意添你的AccessKeyID和你的AccessKeySecret）：
dns_aliyun_access_key = 你的AccessKeyID
dns_aliyun_access_key_secret = 你的AccessKeySecret
~~~
文件credentials.ini授权
~~~
chmod 600 credentials.ini
~~~
回到项目跟目录（certbot同级目录）创建docker-compose.yml
~~~
services:
  certbot:
    image: camel52zhang/certbot-dns-aliyun:latest
    container_name: camelznav-certbot
    volumes:
      - ./certbot/letsencrypt:/etc/letsencrypt
      - ./certbot/credentials.ini:/etc/letsencrypt/aliyun.ini:ro
    command: >
      certonly
      --authenticator dns-aliyun
      --dns-aliyun-credentials /etc/letsencrypt/aliyun.ini
      --dns-aliyun-propagation-seconds 30
      -d yourdomain.com
      --email youremail@qq.com
      --agree-tos
      --non-interactive
~~~

## 可搭配Nginx使用
搭配我的项目camelznav-frontend和camelznav-backend，暂不配置。

[cloudflare certbot-dns](https://github.com/camel52zhang/certbot-dns-cloudflare)

~~~
camel52zhang/certbot-dns-cloudflare:latest
~~~

[腾讯云 certbot-dns](https://github.com/camel52zhang/certbot-dns-tencent)

~~~
camel52zhang/certbot-dns-tencent:latest
~~~







