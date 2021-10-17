## Start Nginx
```
service nginx start
```

## Stop Nginx
```
service nginx stop
```
*   OR
```
killall -9 nginx
```

## Quit Nginx
```
service nginx quit
```

## Restart Nginx
```
service nginx restart
```

## Reload Nginx
```
service nginx reload
```

## View Server Status
```
service nginx status
```

## Test Nginx Configuration
```
nginx -t
```

## Check Nginx Version
```
service nginx -v
```

## Show Command Help
```
service nginx -h
```
___
___
___
## Configuration
```
ls /etc/nginx
```
## Config file
```
ls /etc/nginx/nginx.comf
```
## sites enabled
```
 ls /etc/nginx/sites-enabled/
```
## sites available
```
 ls /etc/nginx/sites-available/
```


## set access to share another Web UI
```
nano /etc/nginx/sites-available/couch


server {
    listen 80;
    server_name 147.182.138.232 www.147.182.138.232;

    location / {
        include proxy_params;
        proxy_pass http://127.0.0.1:5984;
    }
}
```

## WhiteList external IP and blacklist all others
```
sudo nano /etc/nginx/nginx.conf

http{
	allow 197.245.218.239;
	allow another IP
	deny all;
}
```