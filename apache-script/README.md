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
sudo git clone https://github.com/freyakavanagh/tech242-jsonvoorhees-app.git repo
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
VHOST_CONF="/etc/apache2/sites-available/000-default.conf"
cat <<EOF | sudo tee "$VHOST_CONF" > /dev/null
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    ProxyPreserveHost On
    ProxyPass / http://localhost:5000/
    ProxyPassReverse / http://localhost:5000/
    ErrorLog \${APACHE_LOG_DIR}/error.log
    CustomLog \${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
EOF
echo "done"
echo ""
# restart apache
echo "restart apache..."
sudo systemctl restart apache2
echo "done"
echo ""
# cd into the right folder & run the app
echo "navigating"
cd /repo
echo "done"
echo ""
echo "stopping..."
mvn spring-boot:stop
echo "done"
echo ""
echo "running..."
mvn spring-boot:start
echo "done"
echo ""