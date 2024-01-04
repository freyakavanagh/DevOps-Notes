# Week 1 - AWS and Linux

- [Week 1 - AWS and Linux](#week-1---aws-and-linux)
  - [Day 1](#day-1)
  - [Day 2](#day-2)
  - [Day 3](#day-3)
  - [Day 4](#day-4)
  - [Day 5](#day-5)
- [Week 2](#week-2)
  - [Day 1](#day-1-1)
  - [Day 2](#day-2-1)
  - [Day 3](#day-3-1)
  - [Day 4](#day-4-1)
  - [Day 5](#day-5-1)
- [Week 3](#week-3)
  - [Day 1](#day-1-2)
  - [Day 2](#day-2-2)
  - [Day 3](#day-3-2)
- [Credentials for a good interview](#credentials-for-a-good-interview)
- [Why .SSH Folder](#why-ssh-folder)
- [Removing a .git file](#removing-a-git-file)
  - [Port](#port)


## Day 1
[What is cloud?](what-is-cloud/README.md)
<br>
[AWS Basics](intro-to-aws/README.md)
<br>




## Day 2
[Linux](Linux/README.md)<br>
[EC2](ec2-instance/README.md)<br>
[Managing file ownership](managing-file-ownership/README.md)<br>
[Managing file permissions](managing-file-permissions/README.md)

## Day 3
[Managing file permissions](managing-file-permissions/README.md)

## Day 4
[App Deployment](app-deployment/README.md)

## Day 5
[Levels of Automation and User Data](levels-of-automation/README.md)<br>
[Script](script/README.md)<br>
[AMI Creation](ami-creation/README.md)<br>
[Apache Reverse Proxy](apache-reverse-proxy/README.md)<br>
[Apache Script](apache-script/README.md)

# Week 2

## Day 1
[Second Reverse Proxy Method](other-reverse-proxy-script/README.md)<br>
[Apache Other Script](apache-script-2/README.md)


## Day 2

## Day 3
[Two Tier Deployment](two-tier-deployment/README.md)<br>
[Database Script](db-vm-script/README.md)<br>
[App Script](app-vm-script/README.md)

## Day 4

## Day 5
[VPC's](aws-vpc's/README.md)

# Week 3

## Day 1

[Deployment Group Project](deployment-group-project/README.md)

## Day 2

[S3 Notes](s3storage/README.md)

## Day 3

[S3 Image Change Script](Cat-pic-script/README.md)<br>
[S3 Image Reverse Script](Cat-pic-reverse/README.md)


# Credentials for a good interview

- Condidence
- Answering the question that was asked
- Talking through your thought processes 
- Be honest if you don't know but try to talk around the question
- Structure your answers in a way that makes sense
- Body language
- Stay positive
- Be consice
- Use formal language
- Know your audience - laymans terms


# Why .SSH Folder

- '.' means it is a hidden folder
- Everything can be put in one location.
- (credentials and keys)

# Removing a .git file

```rm -rf .git```

then...  

```git status```

to check it is still not a repository

## Port

Like a destination on a device that has a service running behind it, you are trying to connect to the service, the port specifies the specific service
The IP is just the device, doesn't specifiy the service.

