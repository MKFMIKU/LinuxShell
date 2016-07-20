## Command or config in Nginx

1. 80端口转发到SSL

```
server {
  listen          80;
  server_name     www.kffuck.com;
  return          301 https://$server_name$request_uri;
}
server
    {
        listen 443 ssl;
        server_name www.kffuck.com;
        root  /home/wwwroot/www.kffuck.com;

        ssl_certificate /etc/letsencrypt/live/www.kffuck.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/www.kffuck.com/privkey.pem;
        location / {
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Nginx-Proxy true;
                proxy_pass http://127.0.0.1:3000;
        }
        access_log off;
    }
```

2. Nginx状态管理：`/etc/init.d/nginx {start|stop|reload|restart}`