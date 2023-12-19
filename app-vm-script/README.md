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
sudo DEBIAN_FRONTEND=noninteractive apt install mysql-client-core-8.0 -y
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

# Set environment variables for database connection
export DB_HOST=jdbc:mysql://172.31.58.228:3306/world
export DB_USER=root
export DB_PASS=root

# move into project file
cd repo/WorldProject

# Build the application using Maven
sudo mvn clean install

# Run the application (assuming it's a Spring Boot application)
nohup java -jar target/your-app.jar > app.log 2>&1 &

# Verify the application is running (manual step)
# Check app.log for any errors

# Configure reverse proxy (e.g., Nginx or Apache) - Adjust as needed
sudo apt-get install -y nginx
sudo rm /etc/nginx/sites-available/default
sudo tee /etc/nginx/sites-available/default > /dev/null <<EOF
server {
    listen 80;
    server_name your-domain.com;  # Replace with your domain name

    location / {
        proxy_pass http://localhost:your-app-port;  # Replace with your app port
        proxy_set_header Host \$host;
        proxy_set_header X-Real-IP \$remote_addr;
        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto \$scheme;
    }

    access_log /var/log/nginx/your-app-access.log;
    error_log /var/log/nginx/your-app-error.log;
}
EOF

sudo systemctl restart nginx

# cd into the right folder & run the app
echo "navigating"
cd repo
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
