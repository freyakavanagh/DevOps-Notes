# EC2 Instance

EC2 instance is a virtual machine on AWS.

# Made up of...

![ec2.png](../ReadMeImages/ec2.png)

Region: Where everything lives<br>
    - Choose a region strategically based on factors such as latency, data residency requirements, and the location of your users. Deploying your resources in a specific region allows you to optimize performance and comply with regulatory requirements.
  
VPC Virtual Private Cloud(determines Region): like an appartment<br>
    - VPC provides network isolation for your resources. It allows you to define a virtual network, set up subnets, configure routing tables, and control inbound and outbound traffic. This isolation is essential for deploying applications securely in the cloud.
  
Subnet:like a room inside a house<br>
    - providing a way to organize and secure your resources within a network. Proper subnet design is essential for creating a flexible, scalable, and secure infrastructure for deploying applications on EC2 instances in the AWS cloud.

Elastic Network Interface:communicate with the computer through this<br>
    - ENIs provide additional network interfaces to EC2 instances. They are useful for scenarios such as creating multi-homed instances or attaching additional IP addresses. This flexibility is important for certain networking configurations. Elastic because it can be used for different vm's.

Private IP: secret address<br>
    - Instances communicate within a VPC using private IP addresses. This ensures secure communication between components of your application within the same network.

Security group: like a security guard. Controlls any type of traffic coming in and out. e.g. which IP's can enter. Easily trasnferable to different VM's.<br>
    - Security groups act as a virtual firewall for instances. By configuring inbound and outbound rules, you control which traffic is allowed or denied. This is a critical aspect of securing your applications and ensuring they are accessible only to authorized entities.
  
Inbound rules: rules what is allowed in<br>
     - Configuring inbound and outbound rules within a security group allows you to control the flow of traffic to and from your instances. This is crucial for setting up proper access controls and enforcing security policies.

Outbound rules: rules what is allowed <br>
    - Configuring inbound and outbound rules within a security group allows you to control the flow of traffic to and from your instances. This is crucial for setting up proper access controls and enforcing security policies.

Public IP: your public address<br>
    - Public IPs enable instances to communicate with the internet. This is important for scenarios where your application needs to interact with external services or when users need to access your application over the internet.

Elastic Block Store(EBS) Volume: stores the files<br>
    - EBS volumes provide persistent storage for your EC2 instances. This is crucial for storing application data and configurations. EBS volumes can be detached and reattached to different instances, allowing for data persistence and flexibility in managing storage.

EC2 Instance: like a computer/device within a room.<br>
    - The EC2 instance itself is the virtual server where your application runs. You can choose the instance type based on the resource requirements of your application. The ability to scale instances up or down enables you to meet changing demands.

Key pair: like a padlock on the computer
    - Key pairs are essential for secure access to EC2 instances. They provide a secure way to connect to instances using SSH. Proper key management is crucial for securing your instances and preventing unauthorized access.<br>

AMI: the files you want to start off with.<br>
    - AMIs serve as templates for your EC2 instances. They include the operating system, application server, and applications. Using custom or pre-configured AMIs ensures consistency in your deployments and simplifies the process of launching new instances.

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







