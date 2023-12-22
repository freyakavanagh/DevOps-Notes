# Two Tier Deployment

1. logic tier - api VM
2. data tier - MySQL database VM

## Method

App: Always change to the db vm's private IP<br>
WEB: Use the public IP of the App vm

1. Set up database vm maually 
   - ports 3306(MYSQL) and 22(SSH)
   - Install and enable MYSQL
   - Clone the repository
   - Run the MYSQL script
   - Configure MySQL to accept connections from outside with root user
   - Set up root user for remote connections
   - Restart MySQL
   - check mysql is running: sudo systemctl status mysql
2. Set up app vm manually
   - Ports 5000(APP), 22(SSH), and 80(HTTP)
   - t2.small
   - update and upgrade
   - install MYSQL
   - check that you can connect to the database: mysql -h DB_VM_IP -u root -p, SHOW TABLES;
   - install maven and JDK
   - clone the repository
   - install, start, enable and configure(local host) apache
   - restart apache
   - Change environment variables (manually or hardcode in application.properties)
     - May need to change round the two application.properties(.bk) files
   - connect to the database.
3. Set up database using a script
   - Make idempotent(if statements) 
   - Check on a fresh vm
4. Set up app using a script
   - Make idempotent(if statements) 
   - Add conditional
   - Check on a fresh vm
5. Set up database using user data
6. Set up app using user data
7. Set up database using an instannce from an AMI
   - nothing needed in user data 
8. Set up app using an instance from an AMI
   - Once using reverse proxy you no longer need Port 5000 
   - Add the environment variables and the if statement into user data



Blocker: Messing around too much, needed to just restart the instance to get the app running.