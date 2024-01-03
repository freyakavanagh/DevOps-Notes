# S3 Storage

S3 storage is a way of storing files.
In AWS you can store objects within buckets.
In Azure you can store blobs within containers
They are globally available (don't have to choose region) and built in redundency (you choose the redundency you want)

## scripts to create

1. use s3 image on homepage.sh
- change homepage image to scary cat picture from the internet (uploaded to s3storage)

1. revert changes and deletes cat pic and bucket from s3 storage


## AWScli Commands

You need aws cli credentials to log into your awscli account in the terminal. Never let them out into public, even on a teams call.
You can keep them in your .SSH folder and can also store them as environment variables.

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


Then edit the html
