# Deployment of a java App

<u>Plan</u> 

Update

Upgrade

Install dependencies:<br>
JDK 17<br>
maven

copy code to vm

<u>test manually</u>

Note any issues<br>
e.g. questions asked despite -y<br>

```sudo apt update```

```sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y```


```sudo DEBIAN_FRONTEND=noninteractive apt install maven -y```


```mvn -version``` (checks maven is installed)

```sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y```

```java -version``` (checks java is installed)

# Stop user interaction

```DEBIAN_FRONTEND=noninteractive``` 

# Copying from local to virtual

To get folder path: option and right click, copy as path

<u>For a file...</u>

```scp -i path/to/.pem /path/to/local/file username@publicIP:/path/on/vm```

scp -i ~/.ssh/tech242.pem ~/Desktop/testing.txt ubuntu@34.251.118.193:~

<u>For a folder...</u>

```scp -i path/to/.pem /path/to/local/file username@publicIP:/path/on/vm```

scp -r -i ~/.ssh/tech242.pem ~/Desktop/testfolder ubuntu@34.251.118.193:~

# Running a spring boot application

```cd ~/jsonvoorhees-java-atlas-app/springapi``` : move into the api folder

```mvn spring-boot:run``` : run the programme

```mvn spring-boot:start``` : runs the programme without engaging the terminal

```mvn spring-boot:stop``` : stops the programme from running

<u>In a web browser...</u>

http://34.251.118.193:5000/

http://34.251.118.193:5000/web/home



Documents issue!
