# Project Item Catalog
Project use to study Udacity Full Stack Developer which can be use for small invenotry project

## Project Host
Amazon lightsail 
- Link : https://lightsail.aws.amazon.com

## Application Path :
- http://13.229.131.118

## Project Detail : 
- Develop using Flask as Back-end host with Ubuntu version 16.04 LTS
- React as Front-end host with Ubuntu version 16.04 LTS

## Project Setup

1. Connect to server using SSH key
2. Run update
```
sudo apt-get update
```
3. Install python pip
```
sudo apt-get install python-pip
```
4. Install apache
```
sudo apt-get install apache2
```
5. Install git
```
sudo apt-get install git
```
6. Install wsgi mode for apache
```
sudo apt-get install libapache2-mod-wsgi
```
7. Direct to path /var/www then pull git to this directory
```
sudo git clone https://github.com/privatebuddy/project-item-catalog
cd project-item-catalog/back-end
```
8. Install virtualenv to make python run smooter without working with system
```
sudo apt-get install virtualenv
sudo virtualenv venv
source venv/bin/activate
```
9. In venv install dependency of the project using config file
```
pip install -r requirements.txt
```
10. Test Running the project by using sudo python app.py if it not error deactivate it
```
deactivate
```
11. config apache site by using nano editor to create file back-end-conf
```
sudo nano /etc/apache2/sites-available/back-end.conf
```
12. put the following configuration
```
<VirtualHost *:80>
    ServerName server
    ServerAdmin admin@email
    WSGIScriptAlias / /var/www/project-item-catalog/back-
    end/back-end.wsgi

    <Directory /var/www/project-item-catalog/back-end>
      Order allow,deny
      Allow from all
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    LogLevel warn
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
13. create wsgi file in our directory
```
cd /var/www/project-item/project-item-catalog/back-end
sudo nano back-end.wsgi
```
14. add following config to the file
```
#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)

sys.path.insert(0,"/var/www/project-item/project-item-
catalog/back-end")
from app import app as application
application.secret_key = 'project secret key'
```
15. enable on apache
```
sudo nano /etc/apache2/sites-available/back-end.conf
```
16. Apache default will strip header from request we set so to use jwt we need to config the apache 
```
cd /etc/apache2
sudo nano apache2.conf
```
17. Add Following line to the file 
```
WSGIPAssAuthorization On
```
18. Restart Apache and the webservice will start to running
```
sudo service apache2 restart
```
