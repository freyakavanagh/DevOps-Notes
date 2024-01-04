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



