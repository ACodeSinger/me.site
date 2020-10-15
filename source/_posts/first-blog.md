---
title: 首秀
tags:
- Nginx
- 服务器
---
我有自己的博客啦~~~~
<!--more-->

## 背景
本人身为一名前端程序员, 热情好学<font color=red>(被逼无奈)</font>, 最近开始学习Nginx, 买了个xx云服务器, 本着"花了钱就要榨干它"的原则, 开始搭建自己的博客. 

## 如何搭建自己的博客
本博客是用Hexo搭建, 然后部署到自己的服务器, 所以你需要以下的知识储备。
- Git
- Linux(vim)
- Nginx(别走啊, 跟我做就行)

### 使用Hexo搭建项目
详细文档请参考[Hexo文档](https://hexo.io/docs/)
```bash
npm i -g hexo-cli
hexo init your_project_name
npm run serve
```
### 部署到服务器
登陆到你的服务器:
```bash
ssh -p port username@server_ip
```
使用xftp将项目文件拉至服务器, 例如/root/web/blog
```bash
npm run build
```

### 配置Nginx
```bash
yum install nginx -y
cd /etc/nginx
vim nginx.conf
```
然后替换80端口的根目录即可
```nginx
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            root    /root/web/blog/public/;    // 替换此处
        }

        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
    }
```

