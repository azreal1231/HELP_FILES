sudo apt-get install goaccess

goaccess -f /var/log/nginx/access.log

cd /var/log/nginx/

goaccess access.log --log-format=COMBINED -a -o report.html --real-time-html

 mv report.html /var/www/html/
 
 http://[ip of server youre ssh ed into]/report.html
 
 goaccess access.log --log-format=COMBINED -o /var/www/html/report.html --real-time-html
 