#!/bin/bash

# Set a secure password for the MySQL root user
MYSQL_ROOT_PASSWORD="root"

# Check if MySQL is already installed
if [ -x "$(command -v mysql)" ]; then
    echo "MySQL is already installed. Skipping installation."
else
    # Update the package list and install MySQL server
    echo "Updating..."
    sudo apt-get update
    echo "Done"
    echo ""
    echo "Installing..."
    sudo apt-get install -y mysql-server git
    echo "Done"
    echo ""
fi

# Check if MySQL service is running and enable it if necessary
echo "Enabling..."
sudo systemctl is-active --quiet mysql || sudo systemctl start mysql
sudo systemctl is-enabled --quiet mysql || sudo systemctl enable mysql
echo "Done"
echo ""

# Check if the repository is already cloned
if [ -d "repo" ]; then
    echo "Repository already cloned. Skipping download."
else
    # Download the SQL script from the repository
    echo "Downloading..."
    sudo git clone https://github.com/freyakavanagh/world-project-api-to-deploy.git repo
    echo "Done"
    echo ""
fi

# Run the SQL script to create the database and tables
echo "Running SQL script..."
sudo mysql < repo/world.sql
echo "Done"
echo ""

# Configure MySQL to accept connections from outside with root user
echo "Configuring MySQL..."
config_file="/etc/mysql/mysql.conf.d/mysqld.cnf"
if ! grep -q "bind-address = 0.0.0.0" "$config_file"; then
    sudo sed -i '0,/bind-address.*/s//bind-address = 0.0.0.0/' "$config_file"
    sudo systemctl restart mysql
    echo "Done"
    echo ""
else
    echo "MySQL is already configured. Skipping."
fi

# Set up root user for remote connections
echo "Setting up root user for remote connections..."
if ! sudo mysql -e "SELECT user FROM mysql.user WHERE user='root' AND host='%'" | grep -q "root"; then
    echo "[client]
    user=root
    password=${MYSQL_ROOT_PASSWORD}" > ~/.my.cnf

    sudo mysql -e "CREATE USER 'root'@'%' IDENTIFIED BY '${MYSQL_ROOT_PASSWORD}'; GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'; FLUSH PRIVILEGES;"
    echo "Done"
    echo ""
else
    echo "Root user is already set up for remote connections. Skipping."
fi

# Cleanup: Remove the temporary option file
rm -f ~/.my.cnf

# Restart MySQL service for changes to take effect
sudo systemctl restart mysql
echo "Done"
echo ""




