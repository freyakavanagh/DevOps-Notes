#!/bin/bash
# update & upgrade
echo "update..."
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
git clone https://github.com/freyakavanagh/tech242-jsonvoorhees-app.git
echo "done"
echo ""
# cd into the right folder & run the app
echo "navigating"
cd ~/jsonvoorhees-java-atlas-app/springapi
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