---
sidebar_position: 9
---

# 反向代理
程序默认监听5244端口
### nginx
在网站的配置文件的server字段中加入
```nginx
location / {
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_redirect off;
    proxy_pass http://127.0.0.1:5244;
}
```
:::caution
如果你使用宝塔，请务必删除以下默认配置
- location ~ ^/(\.user.ini|\.htaccess|\.git|\.svn|\.project|LICENSE|README.md
- location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
- location ~ .*\.(js|css)?$
:::

### Apache
在VirtualHost字段下加入反代配置项ProxyPass，比如：
```xml
<VirtualHost *:80>
    ServerName myapp.example.com
    ServerAdmin webmaster@example.com
    DocumentRoot /www/myapp/public

    AllowEncodedSlashes NoDecode
    ProxyPass "/" "http://127.0.0.1:5244/" nocanon
</VirtualHost>
```