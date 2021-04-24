# remove file
>Updated your system package manager
* sudo apt update
>Upgrades and gets python capabilities for python3
* sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools
>install python3 venv function to create python3 venv
* sudo apt install python3-venv
>create and name project venv
* python3.8 -m venv venv
>activates venv
* source venv/bin/activate
>wheel makes PIP install faster
* pip install wheel
>Flask is the Python Webframe Work
* pip install gunicorn flask
>install all pip libraries from requirements.txt
* pip install -r requirements.txt
>create your nginx [PROJECTNAME] config file
* sudo nano /etc/nginx/sites-available/PROJECTNAME
> the following config goes into youe [PROJECTNAME]
```console
	upstream gunicornapp{
		server 127.0.0.1:8000;
	}

	server{
		listen 80;
		server_name slatelight.co.za www.slatelight.co.za;

		root /root/Ava;

		access_log /root/logs/nginx-access.log;
		error_log /root/logs/nginx-error.log;


		location / {
					include proxy_params;
			proxy_pass http://gunicornapp;
		}

		location /static/.(js|css|png|jpg|jpeg|gif|ico)$ {
                expires max;
                log_not_found off;
        }

        location /uploads/ { }
	}
```
>copys your [PROJECTNAME] to another nginx dir
* sudo ln -s /etc/nginx/sites-available/[PROJECTNAME] /etc/nginx/sites-enabled
>Check for synax errors
* sudo nginx -t
>reatrt nginx
* sudo systemctl restart nginx
>allows nginx with firewall
* sudo ufw allow 'Nginx Full'
>Stats the Python App 
* gunicorn --bind 0.0.0.0:5000 [MainFileName]:app

sudo add-apt-repository ppa:certbot/certbot
sudo apt install python-certbot-nginx
sudo certbot --nginx -d your_domain -d www.your_domain
sudo ufw delete allow 'Nginx HTTP'


