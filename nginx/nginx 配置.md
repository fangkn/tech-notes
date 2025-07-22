# nginx 配置  ssl

在 server 中配置 ssl

```sh  

erver {
    listen 334 default ssl;
    listen [::]:334 default_server ssl;
    server_name www.xyecho.com;
    keepalive_timeout 80;


    // ssl 配置
    ssl_certificate /etc/nginx/ssl/xyecho.com.crt;
    ssl_certificate_key /etc/nginx/ssl/xyecho.com.key;
    ssl_session_timeout 5m;
    ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers "HIGH:!aNULL:!MD5 or HIGH:!aNULL:!MD5:!3DES";
    ssl_prefer_server_ciphers on;
}
```



# nginx 配置 upstream 

server 的   proxy_pass 指向 www-xyecho 如 ：proxy_pass http://www-xyecho;

```sh
upstream www-xyecho {
   server 10.20.3.104:28334 max_fails=2 fail_timeout=5s;
   server 10.20.3.105:28334 max_fails=2 fail_timeout=5s;
   server 10.20.3.106:28334 max_fails=2 fail_timeout=5s;
   keepalive 1024;
}


server {
    listen 334 default ssl;
    listen [::]:334 default_server ssl;
    server_name www.xyecho.com;
    keepalive_timeout 80;

    access_log    /data/logs/nginx/www.xyecho.com/access.log vhostu;
    error_log    /data/logs/nginx/www.xyecho.comm/error.log;

    ssl_certificate /etc/nginx/ssl/xyecho.com.crt;
    ssl_certificate_key /etc/nginx/ssl/xyecho.com.key;
    ssl_session_timeout 5m;
    ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers "HIGH:!aNULL:!MD5 or HIGH:!aNULL:!MD5:!3DES";
    ssl_prefer_server_ciphers on;

    location / {
        proxy_pass http://www-xyecho;

        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Connection "";
        proxy_http_version 1.1;

       add_header Access-Control-Allow-Origin *;
       add_header Access-Control-Allow-Methods 'GET, PUT, POST, OPTIONS';
       add_header Access-Control-Allow-Headers 'DNT,X-Mx-ReqToken,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization';
    }
}
```

# nginx 配置 负载方式

在 upstream 配置多个 server 

```sh

 upstream xy_hello {                                                                                                                                   
     server 10.173.70.133:8080      max_fails=3 fail_timeout=30s;
     #server 10.101.62.231:8080     max_fails=3 fail_timeout=30s;
     #server 10.172.13.176:8080     max_fails=3 fail_timeout=30s;
 }
 
location ~ ^/xyhello/ { 
    proxy_set_header        Host xyhello.xyecho.com;
    proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass http://xy_hello;
}
```

# 日志格式

在 nginx.conf 中可以设置日志输出的格式, 在server 中就可以使用 如下： 

```sh 
http {

    log_format vhostu '[$time_iso8601] $remote_addr $remote_user - $server_name "$http_referer" "$http_user_agent" "$http_x_forwarded_for" "$request" - $status $body_bytes_sent $request_time - $upstream_addr $upstream_status $upstream_response_time';
    log_format log_json escape=json '{'
                               '"time_local":"$time_local",'
                               '"remote_addr":"$remote_addr",'
                               '"hostname":"$hostname",'
                               '"server_name":"$server_name",'
                               '"server_addr":"$server_addr",'
                               '"server_protocol":"$server_protocol",'
                               '"hosts":"$host",'
          /                     '"body_bytes_sent":"$body_bytes_sent",'
                               '"http_referer":"$http_referer",'
                               '"http_user_agent":"$http_user_agent",'
                               '"http_x_forwarded_for":"$http_x_forwarded_for",'
                               '"upstream_addr":"$upstream_addr",'
                               '"upstream_response_time":"$upstream_response_time",'
                               '"upstream_connect_time":"$upstream_connect_time",'
                               '"upstream_status":"$upstream_status",'
                               '"request_method":"$request_method",'
                               '"request_time":"$request_time",'
                               '"request_uri":"$request_uri",'
                               '"status":"$status",'
                             '}';
}

server {

    access_log   /data/logs/nginx/nginx-test.xyecho.com/access.log log_json;
    error_log    /data/logs/nginx/nginx-test.xyecho.com/error.log;
}

```

# 多个配置文件 用 include 

在 nginx.conf 中 用 include 包含多个配置文件

```sh

http {
    include /etc/nginx/conf.d/*.conf;
    include /opt/nginx/conf/vhosts/*.conf;
    include /opt/nginx/conf/sites-enabled/*.conf;
}

```

# 白名单 

在 server 下 

```sh 
server {
    listen 80;
    server_name example.com;

    allow 203.0.113.10;
    deny all;

    location / {
        root /var/www/html;
        index index.html;
    }
}

```

可以 把白名单 写到一个 et_limit.conf 中 再被 include 引用 如：

在 server 下的  location 可以设置白句单访问 如下： 

```sh 

location ~* ^/hello/(.*) {
                include      limit/whitelist.conf;
                proxy_pass http://h5-web/$1$is_args$args;

                proxy_set_header X-REAL-IP $remote_addr;
                proxy_set_header Host $host;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

```

whitelist.conf 的配置方式：

```sh 
# /etc/nginx/whitelist.conf
allow 192.168.1.1;
allow 192.168.2.0/24;
deny all;
```

