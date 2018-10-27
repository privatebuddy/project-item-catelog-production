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
