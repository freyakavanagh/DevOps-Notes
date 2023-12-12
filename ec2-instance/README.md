# EC2 Instance

EC2 instance is a virtual machine on AWS.

Made up of...

Region: Where everything lives<br>
VPC Virtual Private Cloud(determines Region): like an appartment<br>
Subnet:like a room inside a house<br>
Elastic Network Interface:communicate with the computer through this<br>
Private IP: secret address<br>
Security group: like a security guard<br>
Inbound rules: rules what is allowed in<br>
Outbound rules: rules what is allowed <br>
Public IP: your public address<br>
Elastic Block Store(EBS) Volume: stores the files<br>
EC2 Instance: like a computer/device within a room.<br>
Key pair: like a padlock on the computer<br>
AMI: the files you want to start off with.<br>

## Creating a Virtual Machine

Change to Ireland<br>
EC2<br>
Instances<br>
Launch Instance<br>


Name:<br>
tech242-freya-

AMI/Image:<br>
Ubuntu - type of linux<br>
filter for 20230424<br>
ubuntu/images/hvm-ssd/ubuntu-bionic-18.04-amd64-server-20230424<br>
ID: ami-0a7493ba2bc35c1e9

Instance type:<br> 
t2.micro

key pair:<br> 
tech242

Network Settings:<br>
Create security group<br>
Allow SSH traffic from myip (IP address changes if you turn off/ reset your router)<br>
Allow HTTP traffic from the internet<br>
tech242-freya-allow-SHH-my-IP-HTTP

## If IP Changes

EC2<br>
Instances<br>
Select Instance<br>
Security<br>
Security group link<br>
Inboumd rules<br>
Change to MyIP<br>
Save<br>


## Key Pair

Addd .pem file to .ssh<br>
Command shift fullstop to see hidden files (.ssh)<br>
ls -a to see hidden files in terminal

## In Terminal
In .ssh<br>
chmod 400 name.pem<br>
log in: ssh -i "name.pem" ubuntu@ec2-54-154-249-138.eu-west-1.compute.amazonaws.com<br>
yes<br>
log out: exit

