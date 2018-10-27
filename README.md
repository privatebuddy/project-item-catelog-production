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

## Project Setup Back-end

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
11. Config apache site by using nano editor to create file back-end-conf
```
sudo nano /etc/apache2/sites-available/back-end.conf
```
12. Put the following configuration
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
13. Create wsgi file in our directory
```
cd /var/www/project-item/project-item-catalog/back-end
sudo nano back-end.wsgi
```
14. Add following config to the file
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
15. Enable on apache
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

## Project Setup Front-end
1. Connect to server using SSH key
2. Run update
```
sudo apt-get update
```
3. Front-end is using Node.js to run react so we need to install
```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs 
```
4. Create directory for our site 
```
sudo mkdir /var/www
cd /var/www/
```
5. Clone Project from git then install dependency using npm package manager and build project (In this case i build offline in local device due to the limite of Ram on free tier of Light Sail)
```
sudo apt-get install git
sudo git clone clone https://github.com/privatebuddy/project-item-catalog
cd project-item-catalog/front-end
sudo npm install
sudo npm run build
```
6. Install nginx
```
sudo apt-get install nginx
```
7. Config nginx config file 
```
sudo nano /etc/nginx/sites-available/default
```
8. Add Following config to the file
```
server {
   listen 80 default_server;
   root /var/www/project-item/project-item-catalog/front-end/build;
   server_name public_ip;
   index index.html index.htm;
   location / {
   }
}
```
9. Start Nginx
```
sudo service nginx start
```

## Authorization Configuration
1. On the server create new user
```
sudo adduser grader
```
2. Assign sudo to this user
```
usermod -aG sudo newuser
```
3. Config firewall to support different port (as require in rubic is 2200 for ssh)
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2200/tcp
sudo ufw allow 80/tcp
```

4. Config ssh configuration by
```
sudo nano /etc/ssh/sshd_config
```
5. Modify setence which is use port 22 as default and disable pssword login
```
# What ports, IPs and protocols we listen for
Port 2200

# Change to no to disable tunnelled clear text passwords
PasswordAuthentication NO
```
6. Go to Networking tab on lightsail console and remove ssh port 22 in firewall section then add custom tcp 2200 to
7. Copy ssh key generate in local computer to server using commmand
```
ssh-copy-id -i /Users/key_path
grader@server_ip -p 2200
```
sometime it need to allow to use password first to move the public key in then just close it after we can use ssh (part 5)

8. Now can access using ssh

## Authors
Sasin Siriskaowkul

## Build with
- [Flask](http://flask.pocoo.org/) - The Back-end python framework used
- [SQLAlchemy](https://www.sqlalchemy.org/) - The Back-end python object ORM
- [Google Sign In](https://developers.google.com/identity/sign-in/web/) - Google sign-in
- [JWT Token](https://jwt.io/)- For Authenticate and Authorization
- [React](https://reactjs.org/)- For Front-end development
- [Semantic UI](https://semantic-ui.com/)- For UI Theme of the Front-end

## Acknowledgments
- https://medium.com/@timmykko/deploying-create-react-app-with-nginx-and-ubuntu-e6fe83c5e9e7
- https://gist.github.com/PurpleBooth/109311bb0361f32d87a2
- https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
- https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart
- https://hk.saowen.com/a/0a0048ca7141440d0553425e8df46b16cdf4c13f50df4c5888256393d34bb1b9
- https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart
