# EC2 Instance

EC2 instance is a virtual machine on AWS.

# Made up of...

![ec2.png](../ReadMeImages/ec2.png)

Region: Where everything lives<br>
VPC Virtual Private Cloud(determines Region): like an appartment<br>
Subnet:like a room inside a house<br>
Elastic Network Interface:communicate with the computer through this<br>
Private IP: secret address<br>
Security group: like a security guard. Controlls any type of traffic coming in and out. e.g. which IP's can enter. Easily trasnferable to different VM's.<br>
Inbound rules: rules what is allowed in<br>
Outbound rules: rules what is allowed <br>
Public IP: your public address<br>
Elastic Block Store(EBS) Volume: stores the files<br>
EC2 Instance: like a computer/device within a room.<br>
Key pair: like a padlock on the computer<br>
AMI: the files you want to start off with.<br>

# IP's

- public ip: use most of the time
- private ip: use if two things within the same network

# Creating a Virtual Machine

1. Change to Ireland<br>
2. EC2<br>
3. Instances<br>
4. Launch Instance<br>


<u>Details to fill in...</u>

Name: tech242-freya-

AMI/Image:<br>
- Ubuntu - type of linux<br>
- filter for 20230424<br>
- ubuntu/images/hvm-ssd/ubuntu-bionic-18.04-amd64-server-20230424<br>
- ID: ami-0a7493ba2bc35c1e9

Instance type: t2.micro

key pair: tech242

Network Settings:<br>
- Create security group<br>
- Allow SSH traffic from myip (IP address changes if you turn off/ reset your router)<br>
- Allow HTTP traffic from the internet<br>
- tech242-freya-allow-SHH-my-IP-HTTP

## If IP Changes

1. EC2<br>
2. Instances<br>
3. Select Instance<br>
4. Security<br>
5. Security group link<br>
6. Inboumd rules<br>
7. Change to MyIP<br>
8. Save<br>


## Key Pair

1. Add .pem file to .ssh<br>
2. Command shift fullstop to see hidden files (.ssh)<br>
3. ls -a to see hidden files in terminal

## In Terminal
In .ssh<br>
chmod 400 name.pem<br>
log in: ssh -i "~/.ssh/name.pem" ubuntu@ec2-54-154-249-138.eu-west-1.compute.amazonaws.com<br>
yes<br>

# .SSH into EC2

In terminal
log in: ssh -i "~/.ssh/name.pem" ubuntu@ec2-54-154-249-138.eu-west-1.compute.amazonaws.com<br>
yes<br>
log out: exit







