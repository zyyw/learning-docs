# Systemctl Commands
## 编写开机启动配置文件
```
cd /lib/systemd/system/
vim nginx.service

// file content example
[Unit]
Description=nginx
After=network.target
  
[Service]
Type=forking
ExecStart=/usr/lib/nginx/sbin/nginx
ExecReload=/usr/lib/nginx/sbin/nginx -s reload
ExecStop=/usr/lib/nginx/sbin/nginx -s quit
PrivateTmp=true
  
[Install]
WantedBy=multi-user.target
```

## 设置开机启动
```
systemctl enable nginx.service
```

## 启动nginx服务
```
systemctl start nginx.service
```

## 停止开机自启动
```
systemctl disable nginx.service
```

## 查看服务当前状态
```
systemctl status nginx.service
```

## 重新启动服务
```
systemctl restart nginx.service
```

## 查看所有已启动的服务
```
systemctl list-units --type=service
```

## CentOS安装Nginx
https://www.cnblogs.com/chnmig/p/9808723.html