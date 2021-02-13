sudo apt update
sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools


sudo apt install python3-venv


python3.8 -m venv venv

source venv/bin/activate

pip install wheel
pip install gunicorn flask

#pip install -r requirements.txt


sudo nano /etc/nginx/sites-available/PROJECTNAME
    	upstream gunicornapp{
        		server 127.0.0.1:8000;
	}

	server{
        		listen 80;
        		server_name slatelight.co.za www.slatelight.co.za;

        		location / {
    	            		include proxy_params;
             		proxy_pass http://gunicornapp;
        		}
	}


sudo ln -s /etc/nginx/sites-available/PROJECTNAME /etc/nginx/sites-enabled

sudo sudo nginx -t	# Check for synax errors

sudo systemctl restart nginx

sudo ufw allow 'Nginx Full'


gunicorn --bind 0.0.0.0:5000 wsgi:app