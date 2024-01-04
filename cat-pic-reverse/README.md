#!/bin/bash

# change home.html back
echo "changing html"
cd /repo/src/main/resources/templates
sudo sed -i 's|<img src="https://tech242-freya-bucket.s3.eu-west-1.amazonaws.com/scary-cat.jpg" alt="scary-cat">|<img src="/images/friday13th.jpg" alt="friday13thposter">|' home.html
echo "done"
echo ""

# refresh application
cd /repo
sudo mvn package
echo "done"
echo ""

# delete bucket
echo "delete bucket"
aws s3 rb s3://tech242-freya-bucket --force
echo "done"
echo ""

