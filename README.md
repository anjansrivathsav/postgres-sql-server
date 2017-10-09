# postgres-sql-server
This is the application item catalog hosted on digital ocean with apache server.The application i,e item-catalog-app is deployed on 
digital ocean.

The name of the database we would create would be catalog and initially doesnot conatain any data in it.

setting up the process in a sequential order

# STEP-1
To start a new server on digital ocean,create a new droplet and do as the following

1.Distribution - Ubuntu 16.04 x64

2.size and datacenter as you like accordingly put the value

3.create a new ssh-key called catalog_root

4.open your terminal and run ssh-keygen  and enter /home/USER_NAME/.ssh/catalog_root where username is your username

5.now setup passphrase as the "password".Know we will have a key pair

6.click on new ssh key and paste the contents in the directory /home/USER_NAME/.ssh/catalog_root.pub into it 

7.keep number of droplets as one.

8.Finish.click on create button

# STEP-2
To ssh into the server,copy the ip address digital ocean interface my ip is 139.59.70.89

now ssh into the server with the following command  ssh -i /home/USER_NAME/.ssh/catalog_root root@139.59.70.89

now you should enter the passphrase that you have created for the ssh.

# STEP-3
update all the packages 

sudo apt-get update
sudo apt-get upgrade
sudo apt-get unattended updates

# step-4

now you have to change the ssh port to 2200

type the following command in command prompt sudo nano /etc/ssh/sshd_config

find and change the port  22 to 2200 and then restart the ssh service by command sudo service ssh restart

# STEP-5
 
 now you have to configure the firewall(UFW) with following commands
 
 sudo ufw allow 2200
 sudo ufw allow 80
 sudo ufw allow 123
 sudo ufw allow 2200/tcp
 sudo ufw allow ssh
 sudo ufw allow www
 
 now you have to enable the ufw by following 
 
 sudo ufw enable
 
 now try to connect to ssh by exiting i,e to connecr via 2200 port with the command 
 
 ssh -p 2200 -i ~/.ssh/catalog_root root@139.59.70.89
 
# STEP-6
 
 create a user called grader with the following command 
 
 sudo adduser grader
 
 fill out all details and put passwoard as 'password'
 
 If you want to check whether the grader is successfully created or not run ls /home/grader in the command prompt if the 
 
 directory exists then your user is created 
 
 # STEP-7
 
 To give the sudo permission to the grader we need to create a file inside sudoers.d
 
 the command is touch /etc/sudoers.d/grader
 
 now go into the file by following command sudo nano /etc/sudoers.d/grader and add the following to it 
 
 grader ALL=(ALL) NOPASSWD:ALL
 
 
 
 # STEP-8
 
 now setting up the ssh key pair for grader
 
 follow th step-1 to create the ssh-key and at /home/USER_NAME/.ssh/catalog_grader 
 
 copy the contents of catalog_grader.pub file
 
 on the terminal run the commands orderly  
 
su - grader

mkdir .ssh

chmod 700 .ssh

nano .ssh/authorized_keys

# paste the contents and save the file

chmod 644 .ssh/authorized_keys

now restart the ssh service and try to login as grader by this command 

ssh -p 2200 -i ~/.ssh/catalog_grader grader@139.59.70.89
 
# STEP-9

To serve the python using apache and mod_wsgi, install the following components

sudo apt-get install python3
sudo apt-get install python3-setuptools
sudo apt-get install apache2 libapache2-mod-wsgi-py3

Then start apache service 

sudo  service apache2 restart


# STEP-10

now install postgresql as following

  sudo apt-get install postgresql
  
 now create the catalog database run the following to get into psql shell
 
  sudo -u postgres psql
  
  Then inside the psql shell run the following 
  
  create user catalog with password 'password';
  
 create database catalog with owner catalog;
 
 and exit with following command \q
 
 
 
 # STEP-11
 
 installing git 
 
 sudo apt-get install git 
 
 
 
 # STEP-12
 
 now we need to clone it on the server
 
 go into the directort of www by cd /var/www/
 
 and now type sudo git clone "your git repository link"(Item caltalog)
 
 now install the requirements into it 
 
 sudo easy_install3 pip
 
 cd catalog
 
 sudo pip install -r requirements.txt
 
 now all the required components will be installed
 
 
# STEP-13

we need to run the project on apache server 

now go into the directory of .conf file in your apache 

sudo nano /etc/apache2/sites-available/catalog.conf


now it should have the following commands

<VirtualHost *:80>
    ServerName 139.59.70.89

    WSGIScriptAlias / /var/www/catalog/wsgi.py

    <Directory /var/www/catalog>
        Order allow,deny
       
       Allow from all
    
    </Directory>

</VirtualHost>

If you have configured you ip with any domain name then change the ip here and write domain name which has been configured


now create the wsgi file and write the following into it 

import sys

sys.path.insert(0, '/var/www/catalog')

from item_catalog import app as application

application.secret_key = 'your secret key'

after doing this restart the apache2 server

sudo a2ensite catalog 

# enabling the site 

sudo service apache2 reload

# reloading the service

now the server will be livwe go to the web browser and type your ip you will see your site hosted

# STEP-14

now I have mapped my ip address to the domain name http://anjan.singhpratyush.in/ . and changed thois also in the conf file

This is so because of the callback of the google auth doesn't work on bare ip .I have got subdomain and mapped to it.


# reference

http://stackoverflow.com/

https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-digitalocean-droplets




















































































 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
 


























 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 


















































