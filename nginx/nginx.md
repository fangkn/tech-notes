---
tags:
  - nginx
---

# nginx-1.0源码中文注释版  

地址：github.com/jianfengye/nginx-1.0.14_comment  
项目目标人群是是初学nginx源码的人员 ​​​

# 配置管理

```sh
sudo systemctl status nginx # nginx当前状态 
sudo systemctl reload nginx # 重新加载 nginx 
sudo systemctl restart nginx # 重启nginx 
sudo nginx -t # 检查语法 
nginx # 启动 
nginx -s reload # 重启 
nginx -s stop # 关闭进程 n
ginx -s quit # 平滑关闭nginx 
nginx -V # 查看nginx的安装状态，
```


---- 
参考：
1、[https://wangchujiang.com/reference/docs/nginx.html](https://wangchujiang.com/reference/docs/nginx.html)
