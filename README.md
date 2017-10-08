# postgres-sql-server
This is the application item catalog hosted on digital ocean with apache server.The application i,e item-catalog-app is deployed on 
digital ocean.

The name of the database we would create would be catalog and initially doesnot conatain any data in it.

setting up the process in a sequential order

#STEP-1
To start a new server on digital ocean,create a new droplet and do as the following

1.Distribution - Ubuntu 16.04 x64

2.size and datacenter as you like accordingly put the value

3.create a new ssh-key called catalog_root

4.open your terminal and run ssh-keygen  and enter /home/USER_NAME/.ssh/catalog_root where username is your username

5.now setup passphrase as the "password".Know we will have a key pair

6.click on new ssh key and paste the contents in the directory /home/USER_NAME/.ssh/catalog_root.pub into it 



