#!/bin/bash
# update & upgrade
echo "update..."
sudo apt update
echo "done"
echo ""
echo "upgrade..."
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo "done"
echo ""
# install mysql
echo "install mysql..."
sudo apt-get install -y mysql-server
echo "done"
echo ""
# install maven
echo "install maven..."
sudo DEBIAN_FRONTEND=noninteractive apt install maven -y
echo "done"
echo ""
# check maven is installed
echo "check maven..."
mvn -version
echo "done"
echo ""
# install JDK (java) 17
echo "install java..."
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y
echo "done"
echo ""
# check java is installed
echo "check java..."
java -version
echo "done"
echo ""
# copy the app code to this vm
echo "copying..."
sudo git clone https://github.com/freyakavanagh/world-project-api-to-deploy.git repo
echo "done"
echo ""
# install apache
echo "install apache..."
sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y
echo "done"
echo ""
# start and enable apache
echo "start and enable apache"
sudo systemctl start apache2
sudo systemctl enable apache2
echo "done"
echo ""
# Enable Required Apache Modules
echo "enable modules"
sudo a2enmod proxy
sudo a2enmod proxy_http
echo "done"
echo ""
# Configure Apache Virtual Host
echo "configure virtual host"
if grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf; then
    # The string exists, so nothing to do
    echo "Reverse proxy already configured."
else
    # reverse proxy not configured yet
    echo "configuring reverse proxy..."
    sudo sed -i '/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/\n' /etc/apache2/sites-available/000-default.conf
fi
echo "done"
echo ""
# restart apache
echo "restart apache..."
sudo systemctl restart apache2
echo "done"
echo ""
# Environment variables
echo "environment variables..."
export DB_HOST=jdbc:mysql://172.31.35.34:3306/world
export DB_IP=172.31.35.34
export DB_NAME=world
export DB_USER=root
export MYSQL_PWD=root
export DB_PASS=root
echo "done"
echo ""
# Check if connection to the database can be established
if mysql -u"$DB_USER" -h"$DB_IP" -p"$MYSQL_PWD" -e "use $DB_NAME"; then
    echo "Connected to the database. Starting the application..."
    cd /repo/WorldProject
    sudo -E mvn package spring-boot:start
else
    echo "Failed to connect to the database. Application start aborted."
fi










