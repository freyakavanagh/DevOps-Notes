#!/bin/bash

# installing awscli
echo "installing awscli"
sudo apt install awscli -y
echo "done"
echo ""

# creating variables
echo "creating variables"
sudo AWS_ACCESS_KEY_ID="your_access_key_id"
sudo AWS_SECRET_ACCESS_KEY="your_secret_access_key"
sudo AWS_DEFAULT_REGION="eu-west-1"
sudo AWS_OUTPUT_FORMAT="json"
echo "done"
echo ""

# configuring aws
echo "configuring aws"
sudo aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
sudo aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
sudo aws configure set default.region $AWS_DEFAULT_REGION
sudo aws configure set default.output $AWS_OUTPUT_FORMAT
echo "done"
echo ""

# creating a bucket
echo "creating a bucket"
sudo aws s3 mb s3://tech242-freya-cat-bucket
echo "done"
echo ""

# downloading scary cat picture
echo "downloading image"
sudo wget https://www.telegraph.co.uk/multimedia/archive/03269/Angry_Cat_3_3269981k.jpg?imwidth=680 -O scary-cat.jpg
echo "done"
echo ""

# Uploading image to S3 bucket
echo "uploading to bucket"
sudo aws s3 cp scary-cat.jpg s3://tech242-freya-cat-bucket/scary-cat.jpg
echo "done"
echo ""

# Changing permissions
echo "changing permissions"
sudo aws s3api put-object-acl --bucket tech242-freya-cat-bucket --key scary-cat.jpg --acl public-read
echo "done
echo ""

# Modifying homepage
echo "modifying homepage"
sudo sed -i 's|<img src="/images/friday13th.jpg" alt="friday13thposter">|<img src="https://www.telegraph.co.uk/multimedia/archive/03269/Angry_Cat_3_3269981k.jpg?imwidth=680" alt="scary-cat">|' /repo/src/main/resources/templates/home.html
echo "done"
echo ""

# build and deploy changes
echo "deploying changes"
cd /repo
sudo mvn package
echo "done"
echo ""
