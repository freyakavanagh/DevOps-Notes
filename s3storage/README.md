# S3 Storage

S3 storage is a way of storing files.
In AWS you can store objects within buckets.
In Azure you can store blobs within containers
They are globally available (don't have to choose region) and built in redundency (you choose the redundency you want)


## AWScli Commands

You need aws cli credentials to log into your awscli account in the terminal. Never let them out into public, even on a teams call.
You can keep them in your .SSH folder and can also store them as environment variables.

Redundency: data can always be restored(if one server goes down) because you have multiple copies in multiple locations/servers.
S3 provides it by default: Availability Across different Multiple Availability Zones within their region that all have separate infrastructure.

### In the terminal...

sudo apt install awscli -y : intalls awscli
aws --version: checks installation by viewing the version of awscli

aws configure: logs into the s3 storage, asks for...
key ID
Access Key
region = eu-west-1
default output format = json

aws s3 ls: shows list of buckets

aws s3 help : to see possible commands

aws s3 mb s3://tech242-freya-first-bucket: create a bucket, (names must be all lower case) 

aws s3 ls s3://tech242-freya-first-bucket: see inside your bucket

echo This is the first line in a test file > test.txt: creates file and puts the line inside

aws s3 cp test.txt s3://tech242-freya-first-bucket: uploads a file to your bucket

mkdir downloads: creates a directory called downloads 

aws s3 sync s3://tech242-freya-first-bucket . : downloads the files from your bucket to the current directory

aws s3 rm s3://tech242-freya-first-bucket/test.txt: deletes a file from your bucket

aws s3 rm s3://tech242-freya-first-bucket --recursive : deletes all files in your bucket

aws s3 rb s3://tech242-freya-first-bucket: deletes an empty bucket

aws s3 rb s3://tech242-freya-first-bucket --force: deletes a bucket and the files within it

## Making a file public

On aws online...
1. bucket
2. click on file
3. permissions
4. uncheck "block all public access"
5. access control list (access control list = individual file control)
6. "bucket owner enforced" link, enable, acknowledge
7. objects, tick object, actions, make public using acl, make public

## Editing the homepage

cd into your repo
cd /repo/src/main/resources/templates
sudo nano home.html
Find string and replace with image (sed command)
exit
go back to repo
sudo mvn package


...Then edit the html

## Script for changing page image to one stored in s3

```
#!/bin/bash

# installing awscli
echo "installing awscli"
if ! command -v aws &> /dev/null; then
    sudo apt install awscli -y
    echo "AWS CLI installed"
fi
echo "done"
echo ""

# Creating variables
echo "creating variables"
AWS_ACCESS_KEY_ID="your_access_key_id"
AWS_SECRET_ACCESS_KEY="your_secret_access_key"
AWS_DEFAULT_REGION="eu-west-1"
echo "done"
echo ""

# logging in
echo "logging in"
aws configure set aws_access_key_id "$AWS_ACCESS_KEY_ID"
aws configure set aws_secret_access_key "$AWS_SECRET_ACCESS_KEY"
aws configure set default.region "$AWS_DEFAULT_REGION"
echo "done"
echo ""

# creating a bucket
echo "creating a bucket"
bucket_name="tech242-freya-bucket"
aws s3 mb s3://"$bucket_name"
echo "done"
echo ""

# Check for any Block Public Access settings that might override the policy
echo "check public access settings"
aws s3api get-public-access-block --bucket "$bucket_name"
echo "Displays public access settings"
echo ""
 
# If Block Public Access settings are enabled, disable them:
echo "disable public access settings if they are enabled"
aws s3api delete-public-access-block --bucket "$bucket_name"
echo "done"
echo ""
 
# Define a bucket policy to allow public read access
echo "define a bucket policy"
policy_json=$(cat <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::$bucket_name/*"
    }
  ]
}
EOF
)
echo "done"
echo ""
 
# Apply the bucket policy
echo "applying the policy"
aws s3api put-bucket-policy --bucket "$bucket_name" --policy "$policy_json"
echo "done"
echo ""

# downloading scary cat picture
echo "downloading image"
sudo wget https://www.telegraph.co.uk/multimedia/archive/03269/Angry_Cat_3_3269981k.jpg?imwidth=680 -O scary-cat.jpg
echo "done"
echo ""

# Uploading image to S3 bucket
echo "uploading to bucket"
aws s3 cp scary-cat.jpg s3://"$bucket_name"/
echo "done"
echo ""

# Modifying homepage
echo "modifying homepage"
sudo sed -i 's|<img src="/images/friday13th.jpg" alt="friday13thposter">|<img src="https://tech242-freya-bucket.s3.eu-west-1.amazonaws.com/scary-cat.jpg" alt="scary-cat">|' /repo/src/main/resources/templates/home.html
echo "done"
echo ""

# build and deploy changes
echo "deploying changes"
cd /repo
sudo mvn package
echo "done"
echo ""
```

## Script for reversing the image change

```
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

```