# Two Tier Deployment

1. logic tier - api VM
2. data tier - MySQL database VM

The two VM's must be sble to connect and comminicate
    - extra port with security group to allow MySQL traffic
    - database endpoint, username and password to get into database - both root
      - needed to be known by api vm to connect to the database vm
      - in the end they should be environmemt variables but can be hardcoded at first
      - application.properties - backup(hardcoded)
        - spring.datasource.url=jdbc:mysql://privateip:3306/world (MYSQL database port number = 3306)
        - spring.datasource.username=root
        - spring.datasource.password=root


environment variables
- ${DB_HOST}
- ${DB_USER}
- ${DB_PASS}

world.sql to be run on sql database from the repo

root user with password root

bind ip address - sed command
replace the configuration file

# Chat GPT commands

#!/bin/bash

# Update the package list and install MySQL server
sudo apt-get update
sudo apt-get install -y mysql-server

# Check if MySQL service is running and enable it if necessary
sudo systemctl is-active --quiet mysql || sudo systemctl start mysql
sudo systemctl is-enabled --quiet mysql || sudo systemctl enable mysql

# Download the SQL script from the repository
sudo git clone https://github.com/freyakavanagh/world-project-api-to-deploy.git repo

# Run the SQL script to create the database and tables
sudo mysql < repo/world.sql

# Manual check: Ensure the database and tables are created correctly
# (This might involve logging into the MySQL shell and running some queries)
sudo mysql -u root -p
root
exit;

# Configure MySQL to accept connections from outside with root user and password root
sudo sed -i 's/bind-address/#bind-address/' /etc/mysql/mysql.conf.d/mysqld.cnf
sudo mysql -u root -p
root
CREATE USER 'root'@'%' IDENTIFIED BY 'root';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
GRANT GRANT OPTION ON *.* TO 'root'@'%';
FLUSH PRIVILEGES;
exit;

# Restart MySQL service for changes to take effect
sudo systemctl restart mysql




