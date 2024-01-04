# Azure 2-tier deployment

## Virtual Network

First, we created our Azure Virtual Network within the UK South region with the address space of 10.0.0.0/16.
As the NodeJS app has both an app and database we created two subnets, one for each vm.
The app vm has an address space of 10.0.2.0/16. and the database vm has an address space of 10.0.3.0/16.

## Database Virtual Machine (Manual) 

We then moved onto creating out virtual machines. We created the database virtual machine first, so that it would be ready to use once we started to create and test the app vm.

The database vm was located in the UK south region, used the Ubuntu 18.04 LTS image and was the Standard B1s size. We then allowed port 20 for SSH and port 27017, the default port for MongoDB.

Once we SSH’d in we upgraded and updated and then installed MongoDB version 3.2.x as requested. We then configured MongoDB to allow access from any IP address so we could test the database. We then restarted, started and enabled MongoDB.

```
#!/bin/bash
 
# Update and Upgrade
sudo apt update -y
sudo apt upgrade -y
echo "Updated and Upgraded"
 
# Install MongoDB
wget -qO - https://www.mongodb.org/static/pgp/server-3.2.asc | sudo apt-key add -
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
 
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo apt-get install -y mongodb-org=3.2.22 mongodb-org-server=3.2.22 mongodb-org-shell=3.2.22 mongodb-org-mongos=3.2.22 mongodb-org-tools=3.2.22
mongo -version
echo "MongoDB installed"
 
# Change MongoDB config
sudo sed -i 's/bindIp: 127.0.0.1/bindIp: 0.0.0.0/' /etc/mongod.conf
echo "mongoDB config now allows all IPs"
 
# Restart MongoDB
sudo service mongod restart
 
# Start MongoDB
sudo service mongod start
echo "MongoDB Started"
 
# Enable MongoDB
sudo systemctl enable mongod
echo "MongoDB Enabled"
```

## App Virtual Machine (Manual) 

We then moved onto creating the app VM. The location, image and size remained the same as the database VM but we also allowed port 3000 for database access and port 80 for HTTP.

We then used manual commands to update and upgrade, install and start Nginx, install node JS version 12, change the DB_Host environment variable to include the ip address of the database virtual machine within the correct MongoDB endpoint. We then cloned and cd’d into our github repo, installed npm, seeded the database and ran the app.

We then tested our app by going to port 3000 to make sure we could view the sparta app page and then the ‘/posts’ endpoint to make sure we could view the data from our database.

```
#!/bin/bash
 
# Update and install
sudo apt update -y
sudo apt upgrade -y
echo "Updated and Upgraded"
echo ""
 
sudo apt install nginx -y
echo "Installed Nginx"
echo ""
 
sudo service nginx start
echo "Nginx started"
echo ""
 
# installs node js
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
echo "Installed NodeJs"
echo ""
 
 
export DB_HOST=mongodb://4.234.3.17:27017/posts
echo "Set the DB_HOST Environment variable"
echo ""
 
git clone https://github.com/UyiAguebor/sparta-test-app.git repo
echo "Cloned the repo"
echo ""
 
cd repo
cd app
 
echo "CD into the repo"
echo ""
npm install
echo "Ran Npm install"
echo ""
 
node seeds/seed.js
echo "Seeded the database"
echo ""
 
node app.js
echo "The app is running"
```

## Scripted and User Data Virtual Machines 

We then created scripts from the manual commands we had used, and created fresh VM’s to test them, and then created new VM’s that used them as user data.

## Feedback

- Increase the number of slides so that those watching can follow what you are saying with more visual cues.
- Freya: slow down
- Uyi: better flow
- A live demonstration, at least show the application running.
- More screenshots
- Every choice is an intentional choice
- Matching slides
- don't answer question swith a 'no'... elaborate further

