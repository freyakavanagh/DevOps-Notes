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


