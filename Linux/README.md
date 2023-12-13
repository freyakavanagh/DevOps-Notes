# Linux

bash = Bourne again shell.<br>
Shell: An interface that runs commands.<br>
There are many shells that someone can use.<br>

<u>bash vs. git bash</u>
- bash: a type of command line interface on top of linux itself and doesn't neccesarily include git commands, might have to install git command set
- git bash: something that runs on the windows/mac machine that emulates a linux interpreter, allows you to run most bash commands but still runs on top of mac/windows so some linux commands may not work. Will be able to use git commands.

d and colour coded = directory

Linux calls everything a file

~ = tilda


# Commands

<u>General:</u>

uname: tells you the name of the OS e.g.Linux<br>
uname --help: tells us different commands to find about about the OS<br>
uname -a: prints all info about the OS<br>
whoami: ubuntu<br>
history: all commands I have run in the virtual machine.<br>
!numberofcommand: to use command from command history<br>

<u>Viewing contents:</u> 

ls: view contents of directory<br>
ls -a: view hidden files<br>
ls -la: view hidden and normal file details (d and colour coded = directory, . = in the same folder, .. = in another folder level up)<br>

<u>Navigation:</u>

cd . : stay in same directory<br>
cd ~: home directiry<br>
cd .. : go one directory out<br>


<u>Files:</u>

curl "web address": allows us to download files<br>
--output cat.jpg: allows us to download as a jpg<br>
mv cat.jpg cat.txt: renames cat.jpg to cat.txt<br>
file cat.txt: shows us file type<br>
cp cat.txt cat.jpg: copy cat file and name it cat.jpg<br>
rm cat.txt: deletes file cat.txt<br>

<u>File Editing:</u>

touch joke.txt: creates empty file called touch<br>
cat joke.txt: shows contents of joke.txt<br>
nano joke.txt: to edit the file<br>
cntrl s: save file<br>
cntrl x: exit file<br>
head -1 chicken-joke.txt: First line from the top of the file<br>
tail -1 chicken-joke.txt: First line from the bottom of the file<br>
nl chicken-joke.txt: numbers the lines<br>
cat chicken-joke.txt | grep chicken: outputs the lines with chicken and highlights the word<br>
ls -l: shows permissions of file

<u>Moving Files:</u>

mv chicken-joke.txt funny-stuff/: move a file to a folder<br>
mv bad-joke.txt /home/ubuntu: move to home directory<br>
mv bad-joke.txt ~:  move to home directory<br>
mv bad-joke.txt ../..: move two folders back<br>

<u>Directories:</u> 

mkdir funny-stuff: makes a directory called funny-stuff (can't have spaces in the name or it creates more than one folder, use double quotes)<br>
rmdir my: removes directory called my<br>
rm -r pictures/: removes directory called pictures and everything in it<br>

<u>Tree:</u>

sudo apt update -y: show installations<br>
sudo apt install tree: install tree<br>
tree: shows what is in the directory in a tree structure<br>
sudo su: logs in as root user(superuser permissions)<br>
exit: exit root user<br>

# Script Files:

#!/bin/bash: at the top of the file so it knows to use the bash interpreter to interpret this script<br>
#: a comment, so will be ignored<br>
update: find all the latest packages<br>
upgrade: install all the latest packages into the OS (could break something)<br>
install:<br>
restart: If you change its configuratio  and want to load them up and apply them<br>
Enable: If it is enabled it will run on startup.<br>   


<u>Then test each command manually...</u>


<u>Nginx:</u>

- update: sudo apt update -y<br>
- upgrade: sudo apt upgrade -y<br>
- install and run nginx: sudo apt install nginx -y<br>
- Check status of nginx: sudo systemctl status nginx<br>
- Restart nginx: sudo systemctl restart nginx<br>
- Start nginx: sudo systemctl start nginx<br>
- Stop nginx: sudo systemctl stop nginx<br>
- Enable nginx: sudo systemctl enable nginx<br>

A web server.<br>

1. Find public ip of VM<br>
2. paste it into web to go to web page<br>

<u>Exectuting a file:</u>

sudo chmod +x provision.sh: add execute permissions to provision.sh file<br> 
execute a script: ./provision.sh<br>

Idempotency: a script runs on a fresh virtual machine the first time, but also it runs no matter how many times you run it, and achieves the desired state at the end.<br>

<u>Echo command:</u>

Prints something to the screen.<br>
Useful in script file to let us know what is happening<br>
echo "I am an echo": prints I am an Echo<br>

<u>Environment Variables:</u>

Values stored in memory.<br>
Often used to store sensitive information that the programme can look for and get the access it needs, instead of hardcoding credentials. Never hardcode credentials!<br>

printenv: prints all the environment variables<br>
printenv USER: to print a specific variable e.g. USER (case sensitive)<br>
export MYNAME=fraz: creates an environment variable(replaces other variable with that name), but is not perssistent so won't survive from one session to the next(when you log in and out)<br>
Make it persistent by adding the export command to the .bashrc file as .bashrc runs when we login...<br>

nano .bashrc<br>
source .bashrc: to run without logging in<br>

<u>Ordinary Variables</u>

MYNAME=freya: creates a variable<br>
echo $MYNAME: prints a variable<br>


# Processes

Something that is in memory and looks like it is possibly using the CPU, but might just be in memory (in a queue).

- Single core CPU's: can only process one thing at the same time, but to make it look like it's doing many things at once it is just switching between them. The others wait in a queue.<br>
- Multi core CPU's: can process multiple things at the same time.

PID: Every process is given a PID (process ID)<br>
TTY: shows which terminal it is associated with (system processes won't be linked)

When a process is run by another process it is a child process.

<u>Two types</u>

system: 
- unique to each terminal session
- most don't provide an application or user interface for the end user to use.
- They provide services such as logging services, file services, print service, web server
- Middle man between hardware
- many end with a d for demon, means a process that rusn in the background

user: 
- usually launched by a user e.g. when they open a text editor
- the corresponding processes are considered user processes.

<u>Commands</u>

ps: shows all the user processes<br>
ps -A: shows all processes<br>
man ps: manual on the ps command<br>
ps aux: gives a lot of info on all processes (not real time)<br>
top: shows the top processes (ranked by what is using the most CPU) and refreshes about every 3 seconds (M to order by memory)<br>
sleep 3: script/terminal sleeps for 3 seconds<br>
sleep 5000 &: sleep for 5000 seconds in the background, and tells you the process ID<br>
jobs: shows processes we have run

kill [PID]: kills a process with a specific ID<br>
- if it doesn't work, a parent process probably keeps recreating it.<br>

kill -9 [PID]: most extreme form of killing, if kill does not work (called brute force kill)<br>
- child processes become zombie processes (disconnected, but still take up memory), can kill with the process ID
