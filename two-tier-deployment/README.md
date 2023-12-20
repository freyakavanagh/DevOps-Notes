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

check to connect to database: mysql -h <DB_VM_IP> -u root -p

check mysql is running: sudo systemctl status mysql
SHOW TABLES;

check the environment variables:

echo $DB_HOST


 mysql -h 172.31.37.98 -u root -p
