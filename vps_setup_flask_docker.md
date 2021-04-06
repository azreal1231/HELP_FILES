>Upgrades and gets python capabilities for python3
* sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools
>install python3 venv function to create python3 venv
* sudo apt install python3-venv
> Settings Up Flask App
* sudo mkdir [PROJECT_NAME]
* cd [PROJECT_NAME]
* sudo mkdir -p app/static app/templates
* sudo nano app/__init__.py
```python
    # File name - app/__init__.py
   from flask import Flask
    app = Flask(__name__)
    from app import views
```
* sudo nano app/views.py
```python
    # File name - app/app/views.py
    from flask import render_template
    from app import app

    @app.route('/')
    def home():
        return "Hello world!"
    
    @app.route('/template')
    def template():
        return render_template('home.html')
```
* sudo nano uwsgi.ini
```bash
    # File name - [PROJECT_NAME]/uwsgi.ini
   from app import app

    @app.route('/')
    def home():
       return "hello world!"
```
* sudo nano main.py
```python
    # File name - app/main.py
   from app import app
```
* sudo nano requirements.txt
```bash
    # File name - [PROJECT_NAME]/requirements.txt
   Flask==1.0.2
```
> Settings Up Docker
* sudo nano Dockerfile
```bash
    # File name - app/Dockerfile
    FROM tiangolo/uwsgi-nginx-flask:python3.6-alpine3.7
    RUN apk --update add bash nano
    ENV STATIC_URL /static
    ENV STATIC_PATH /[PROJECT_NAME]/app/static
    COPY ./requirements.txt /[PROJECT_NAME]/requirements.txt
    RUN pip install -r /[PROJECT_NAME]/requirements.txt
```
* sudo nano start.sh
```bash
    # File name - [PROJECT_NAME]/start.sh
    #!/bin/bash
    app="docker.test"
    docker build -t ${app} .
    docker run -d -p 8000:80 \
    --name=${app} \
    -v $PWD:/app ${app}
```
* sudo bash start.sh
* sudo docker ps
```
Output
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                            NAMES
58b05508f4dd        docker.test         "/entrypoint.sh /sta…"   12 seconds ago      Up 3 seconds       443/tcp, 0.0.0.0:8000->80/tcp   docker.test
```
> Serving Template Files
* sudo nano app/templates/home.html
```html
    # File name - app/templates/home.html
    <!doctype html>

    <html lang="en-us">
      <head>
        <meta charset="utf-8">
        <meta http-equiv="x-ua-compatible" content="ie=edge">
        <title>Welcome home</title>
      </head>
    
      <body>
        <h1>Home Page</h1>
        <p>This is the home page of our application.</p>
      </body>
    </html>
```
* sudo docker stop docker.test && sudo docker start docker.test

>create your nginx [PROJECTNAME] config file
* sudo nano /etc/nginx/sites-available/PROJECTNAME
> the following config goes into youe [PROJECTNAME]
```console
server {
    listen   80;
    server_name  example.com www.example.com;
    location / {
        proxy_pass http://0.0.0.0:[DOCKER_IMAGE_PORT];
        include /etc/nginx/proxy_params;
    }
}
```
>copys your [PROJECTNAME] to another nginx dir
* sudo ln -s /etc/nginx/sites-available/[PROJECTNAME] /etc/nginx/sites-enabled
>Check for synax errors
* sudo nginx -t
>reatrt nginx
* sudo systemctl restart nginx



