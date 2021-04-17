# os-installation-documents
    Suppose want to install Ubutun Linux
    
    1-download unetbootin
    https://unetbootin.github.io/

    2-download OS image (iso) file.
    https://ubuntu.com/download/desktop

    3-open unetbootin and make bootable pendrive for other machine/ make bootable folder for self machine.

    4- restart system and follow screen steps.



# os-VitualBoxLinux-connection via putty.

       1) Make sure ssh client is installed on your Linux. If not,install ssh client.

       amir@amir-VirtualBox:~$ ssh -V
       OpenSSH_7.6p1 Ubuntu-4ubuntu0.3, OpenSSL 1.0.2n  7 Dec 2017

       if not exist please install using below command.
       sudo apt update
       sudo apt install openssh-server

       2) Power off the OS.

       3) Now on your VirtualBox(used- Version 6.0.6 r130049 (Qt5.6.2)) 
       go to Settings -> Network -> Adapter1 
       a) checked enable network adapter
       b) Attached to : Bridge Adapter
       c) Name: Intel(R) Ethernet connection./Wireless LAN

       4) Now start your OS. Run ifconfig /ip a , now the inet address is your IP from enp0s3 section.
       Use this and run it on your putty. Login with your credentials.




---------------------------------------------------------------------
core level package manager
-----------------------------
There are two type of distrubution based on core package manager in linux
1) dpkg  OS like (Debian,ubuntu)
2) rpm   OS like (Centos,Fedora)

top level packager manager os wise
----------------------------------
for debian and ubuntu
---------------------
    apt-get(all except searching) ,apt-cache ( for searching and showing details)

    0) update the package index file
        sudo apt-get update

            When this command is run, all available packages are fetched and re-indexed from the locations specified in /etc/apt/sources.list and /etc/apt/sources.list.d/.


    0) how to checked installed package in system
        dpkg -l 'pattern'
        example :
        dpkg -l '*mysql*'
    
    1) for seraching all available package for your system
        apt-cache pkgnames

    2) for seraching perticular package

        apt-cache search [pkg-name-pattern]  

    3) for perticular package information (like size & all)
        apt-cache show [package-name]

    4) for Installing package
        sudo apt-get install [package-name]

    5) remove package without configuration.
        sudo apt-get remove [package-name]

    6) remove package with all configuration.
        sudo apt-get --purge remove [package-name]   
        

how to install downloaded package
-----------------------------------
    if you have file called .tar.gz file  or .tar file

    1) tar xvfz filename.tar.gz   or tar xvf filename.tar
    2) goto extract file and run ./configure (if configure file is not there check readme file)
    3) make
    4) make install
    


ENVIRONEMENT VARIABLE IN LINUX
----------------------------------
    It is case sensitive ..means PATH and path both are different

        1) how to see/check all
        a) printenv
        b)env
        
        2) how to see perticular
        printenv name or echo $name
        example :
        a) printenv PATH
        b) echo $PATH
        
     TEMPORARY adding new env variable
    ----------------------------------
    command: var_name=var_value
    example: MYVAR=test123


    TEMPORARY modifying env variable
    ----------------------------------
    command: var_name=$var_name:var_value
    example: MYVAR=$MYVAR:test456


    TEMPORARY removing env variable
    ----------------------------------
    command: unset var_name
    example: uset MYVAR


    PERMANENT adding new env variable
    ----------------------------------
    1) open .bashrc file from user's home dir
    2) write at end one file export var_name='var_value'
    example: export MYVAR='test123'


    PERMANENT modifying env variable
    ----------------------------------
    1) open .bashrc file from user's home dir
    2) write at end one file export var_name=$var_name:'var_value'
    example: export MYVAR=$MYVAR:'test123'

    PERMANENT removing env variable
    ----------------------------------
    1) open .bashrc file from user's home dir
    2) delete export line of that variable.

    GLOBAL PERMANENT env variable
    ----------------------------------
    1)sudo touch /etc/profile.d/app_env.sh
    2)write into file app_env.sh, export var_name=$var_name:'var_value'
    example: export MYVAR=$MYVAR:'test123'




for more details visit to given url 
---------------------------------------
    https://blog.packagecloud.io/eng/2015/03/30/apt-cheat-sheet/
    
    
    
    
 IPTABLES basic concept
----------------
iptables having manay tables like nat,etc and each tables contain multiple filter pipe like like INPUT,FORWARD, PREROUTING,POSTROUTING etc.

HOW IPTABLES DOES WORK
-----------------------
 start filtering form 0 to last if packet filtermatch execute the actionCommand and does not search next and doest match execute default actionCommand.

    1) To select other tables except default
    iptables -t nat 

    to see all entries of tables
    ---------------------------
    1) iptables -L   ( for default)
    2) iptables -t nat -L  ( for nat tables)

    BASIC SYNTAX ( for existing pipe)
    ---------------
    IPTABLE_PRE -A PIPE_NME filterCommand  -j actionCommand

    TO append any iptables entry you must use -A PipeName and commandName
    like 
    iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080 

    IPTABLE_PRE = iptables -t nat
    PIPE_NME= PREROUTING
    filterCommand= -p tcp --dport 80
    actionCommand = REDIRECT --to-port 8080 

    -A for appending iptables entries
    -L for showing iptables entries
    -D  for deleting ip tables entries

    -------------------------------------------------------

    1) displaying all entries of tables nat
    ------------------------------------------
    iptables -t nat -L 


    2) displaying all entries of tables nat OF PIPE PREROUTING
    ------------------------------------------
    iptables -t nat -L PREROUTING

    3) displaying all entries of tables nat OF PIPE PREROUTING OF PERTICULAR POSITION ( FOR EXAMPLE 1)
    ------------------------------------------
    iptables -t nat -L PREROUTING 1

    4)same also work for -D ( deleting  command )
    to delete perticular entries  --example tables nat OF PIPE PREROUTING OF PERTICULAR POSITION ( FOR EXAMPLE 1)
    -----------------------------------------------------------
    iptables -t nat -D PREROUTING 1


    TO DO OPERATION ON FILTER COMMAND WE MUST USE -j ( jump commnad)
    ----------------------------------------------------------

    to see the command permission of users
    ------------------------------------------
    sudo -lU usrname


DOCKER 
---------------
       Docker is a set of platform-as-a-service products that use operating-system-level virtualization to deliver software in packages        called containers

DOCKER HUB
-----------
it is place where we store docker image and used to setup application anywhere without worrying the app dependency.

How Docker Works
----------------
1) setup docker clinet into machine
2) create image application along with required dependency 
3) copy this image to target machine
4) make setup of application quickly with the help of image .

    
 DOCKER SETUP on UBUNTU
 ---------------------------

    1) to get update the repository of packages
    sudo apt-get update

    2) uninstall exiting old one
    sudo apt-get remove docker docker-engine docker.io

    3) install new one
    sudo apt install docker.io

    4) check install version
    docker --version

    5)start stop status of docker
    sudo systemctl status docker
    sudo systemctl stop docker
    sudo systemctl start docker
    
    
    
 some operation with existing docker images
 ------------------------------------------ 
 
how to download docker image from docker hub
-----------------------------------------------
    docker pull image-name
    example: sudo docker pull busybox

how to remove docker image from docker
-----------------------------------------------
    docker rmi image-name
    example: sudo docker rmi busybox


how to check existing images in system
---------------------------------------------
    sudo docker images


how to run images as a container
-------------------------------
    sudo docker run image-name

    example :
    sudo docker run busybox

    run wtih --rm so we can remove container when it stopped

    example:
    sudo docker run --rm busybox

how to see running container id
-------------------------------
    docker ps -a


how to stop all running docker container
-------------------------------------
    docker system prune


how to remove perticualr container
----------------------------------------
    docker container rm cc3f2ff51cab cd20b396a061
    or 
    docker rm cc3f2ff51cab cd20b396a061

    
    


How to create custom image
--------------------------------
    1) create Dockerfile 
    this file will have set of instruction to build a image file 

    for sample  i used 2 commands

    a) FROM this will use to take base image from dockerhub
    b) RUN this will execute while running docker containers

    I created Dockerfile and put below command inside file.

    FROM ubuntu
    RUN apt-get update && apt-get install tree



    after that i hit docker build command

    2) sudo docker build -t mytree .
    Note:
    -t use to give tagname of image . is directory location where Dockerfile will be present.


    3) To See build images
    amir@amir-VirtualBox:~/docker-rnd$ sudo docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
    mytree              latest              8c240bfdd1ca        About a minute ago   92.1MB
    ubuntu              latest              a2a15febcdf3        4 days ago           64.2MB



    4) How to run Images
    sudo docker run -it imageid/name

    example:

    sudo docker run -it 8c240bfdd1ca


how to get running container bash shell
-----------------------------------------
    sudo docker exec -it containerId /bin/bash

    Example:
    amir@amir-VirtualBox:~$ sudo docker exec -it c9669fe22657 /bin/bash
    root@c9669fe22657:/# ls -l


how to exit from running container bash shell
-----------------------------------------
    exit





Dockerfile instruction command
---------------------------------

1)FROM
------------
    This is used to get base template of docker container
    Example:
    FROM ubuntu
    
2)RUN 
--------
    This is used to run command once at build time of images. basically used to install package and created dir structure
    Example:
    RUN apt-get update
    
3)CMD
-------
    This is used to run command everytime when container get started..
    Example:
    CMD ls -l

4)ENTRYPOINT
-------
    ENTRYPOINT + cant override command from root machine.
    Example:
    ENTRYPOINT ls -l

5)COPY
-------
    This is used to copy folder/file from machine to container
    Example:
    COPY /root/test /root/amir
6)ADD
-------
    ADD =COPY+
    1)First, you can use a URL instead of a local file / directory. 
    2)Secondly, you can extract a tar file from the source directly into the destination.


7)WORKDIR
--------------
    This is used to set default workdir for container
    Example:
    WORKDIR /path/to/workdir
    WORKDIR /a
    WORKDIR b
    WORKDIR c
    
9)ENV
--------------
    This is used to set envirement variable
    Example:
    ENV workdir /path/to/workdir
    ENV workdir=/path/to/workdir
    
    
    
    
  ---------------------------------------------------------------------------------------------------------------------------------
    
    
CronJob In Linux
------------------
    It Linux Scheduler having five part in complete expression
    Syntax:  mm hh dom mo dow  commands

    Here
    mm = minuts (0-59)
    hh = hours (0-23)
    dom = days of months (1-31)
    mo = month	1-12 (or names; see example jan,feb,mar...)
    dow = day of week(0-7  ,7 is Sunday, or use names like Mon,Tue,Wed,Thu,Fri)
    
Special values in cronjob
-------------------------
    1) *  This is use for all possible value.(means every)
    2) -  This is use for specify range like for mm 00-05 means (00,01,02,03,04,05) 
    3) /  Thus is use for increment by specify number ...like for mm   ---0/2 means 0,2,4,6,...so minuts
    4) ,  This is use to tell set of values


Command
--------
    commands = single or multiple commnd
    
    single-command example
    1) java -jar app.jar 
    2) java -jar app.jar 
    
    Multiple-command example
    1) java -jar app.jar ; python app.py 
    2) java -jar app.jar && python app.py
    
    Note ; or && both can be use to add multiple in single cronjob && means 2nd will only excute if first run successfully.

commad with log file 
-----------------------
    > and >> use to store output of command into log file.
    > means adding only , not appending with old one
    >> means adding and appeding with old one.
    
    Notes: In Cronjob we use 2>&1 at the end of log file.

Example:
------------
    * * * * * date >> /home/amir/cronLog.txt 2>&1


How to configure crontab in linux
---------------------------------
    Each user have their own crontab space to configure cronjob

    1) to see configured cronjob 
    crontab -l

    2) to modify list
    crontab -e

    3) to see crontab service is running or not.
    service cron status/start/stop  ( working for ubuntu)
    service crond status/start/stop



---------------------------------------------------------------------------------------------------------------------------------
VI EDITOR DOCS
-------------------------------------------------------------------------------------------------------------------------------

vi editor commands all
---------------------------------------
    1) i	Insert at cursor (goes into insert mode)
    2) a	Write after cursor (goes into insert mode)
    3) A	Write at the end of line (goes into insert mode)
    4) ESC	Terminate insert mode
    5) u	Undo last change
    6) U	Undo all changes to the entire line
    7) o	Open a new line (goes into insert mode)
    8) dd  Delete line
    9) D	Delete contents of line after the cursor
    10) C	Delete contents of a line after the cursor and insert new text. Press ESC key to end insertion.
    11) dw	Delete word
    12) cw	Change word
    13) x	Delete character at the cursor
    14) r	Replace character
    15) R	Overwrite characters from cursor onward
    16) s	Substitute one character under cursor continue to insert
    17) S	Substitute entire line and begin to insert at the beginning of the line
    18) ~	Change case of individual character


vi editor commands (goes into editor mode)
----------------------------------
    1) i	Insert at cursor (goes into insert mode)
    2) a	Write after cursor (goes into insert mode)
    3) A	Write at the end of line (goes into insert mode)
    4) o	Open a new line (goes into insert mode)






##Vagrant software
--------------------------
    Vagrant is an open-source software product for building and maintaining portable virtual software development environments, e.g. for     VirtualBox, KVM, Hyper-V, Docker containers, VMware, and AWS.
    it runs on top of virtul provider (virtualbox or vmware). it simplyfy the setup for virtual os.

    How to Use vagrant
    --------------
    1) download the setup exe file. (https://www.vagrantup.com/downloads.html)
    2) install the vagrant software.
    3) create seperate folder "called" box.
    4) go to the folder and hit command:  vagrant init 
     init command create file called Vagrantfile. open the file and configure guest/target os like 
     config.vm.box = "bento/ubuntu-16.04"
    5) to start guest os -- run vagrant up   (it will downlaod the os file vagrant clound and install inside once)


    how to check status of vagrant running os
    ------------------------------------------
    1) locally inside the box dir  
    vagrant status

    2) from outside  the box dir
    vagrant global-status


    how to stop vagrant-os
    -----------------------------
    vagrant halt  or vagrant halt identifier.


    how to destroy the complete vagrant os setup
    --------------------------------------------------
    vagrant destroy

    --------------------------------------------

    how to connenct os
    ---------------------------
    vagrant ssh
        default user & password is vagrant

    how to exit from os
    --------------------------
    vagrant exit
    
    switch to root user
    -------------------------
    sudo su -


    bydefault VAGRANT_HOME path is ~/.vagrant.d but you can set using env variable of VAGRANT_HOME. 
    vagrant store all os releated files inside VAGRANT_HOME.


	How to Connect Vagrant VM(guest)
	--------------------------------------
	there are 2 ways (UBUNTU Tested)
	1) using port forwarding with local host
	 bedefault Guest(VM) port :22 forward with Host(Local) with port 2222.
	 use ip: 127.0.0.1 usr= vagrant pss=vagrant port:2222
	3) using private ip
	config.vm.network "private_network", ip: "192.168.33.10"
	used given ip with usr=vagrant pass=vagrant
	


Shell Scriping
======================

	In Linux we have many times of interpretor to run linux command/script
	most widly use interpretor called as bash
	location of bash shell is /bin/bash

	1) To see the location :  which bash
	/bin/bash

	2) to see the all possible names of interpretors
	cat /etc/shells

	3) sh is soft link to bash interpretor
	amir@local:/home/amir> which sh
	/usr/bin/sh
	amir@local:/home/amir> ll /usr/bin/sh
	lrwxrwxrwx 1 root root 9 Sep 10  2019 /usr/bin/sh -> /bin/bash


	# Used to provide comment in bash/shells script
	# This is for qa env 

		#! Used to inform the os which interpretor you need to use while executin script.
		#!/bin/bash  --location of bash /bin/bash 



How to use command line arguments?
----------------------------------

		In a Bash Shell, they are used with the reference of the following default-parameters or the special variables.

		$0 specifies the name of the script to be invoked.
		$1-$9 stores the names of the first 9 arguments or can be used as the arguments' positions.
		$# specifies the total number (count) of arguments passed to the script.
		$* stores all the command line arguments by joining them together.
		$@ stores the list of arguments as an array.
		$? specifies the process ID of the current script.
		$$ specifies the exit status of the last command or the most recent execution process.
		$! shows ID of the last background job



Read User Input
------------------

	read <variable_name>  

	example:
	echo "Enter the user name: "  
	read first_name  
	echo $first_name



Date Format
-----------------

	date +formatcode

	list of code
	------------
	%d  Day of the month (e.g., 01 - 31)
	%m	Month	Number of month (01 to 12 where 01 is January)
	%Y	Year	Displays full year (i.e., YYYY) 2020
	%H	Hour	Hour in 24-hour clock format
	%M	Minutes	Minutes (00 to 59)
	%S	Seconds	Seconds (00 to 59)
	%N	Nanoseconds	Nanoseconds (000000000 to 999999999)
	Example : 2020-02-23
	command: date +%Y-%m-%d
	output: 2021-02-23

Bash Sleep
---------------
	syntax:
	sleep number[suffix]  

	default-suffix is s

	like sleep 9 or sleep 9s

	suffix list
	------------------------ 
	s - seconds
	m - minutes
	h - hours
	d - days

	complex example:
	sleep 2d 9h 5m 55s




     
	 
Shell variables
--------------------

	1) how to create
	----------------------
	varName="literals"
	example:
	count=10;  # makesure no space before/after ==
	name="Amir";
	MYDIR="/home/amir/"


	2) how to access
	-----------------
	$varName or "$varName"

	example;
	echo "The count="$count""
	echo "The count: "$count

	amir@localhost:~> count=10;
	amir@localhost:~> echo "The Count="$count
	The Count=10
	amir@localhost:~> echo "The Count="$count""
	The Count=10




Shell command substitution
--------------------------------
	assigning command_output value into variables called command substitution

	how to assign 
	------------------ 
	varName=$(command)   -- recommend one
	varName=`command`    -- can use openquote also not recommended --openquote is not single quote

	example

	fileList=$(ls)
	echo "List of files: "$fileList


	how to access
	----------------
	same as variable rules above


importing config file
------------------------
	source /etc/app/myconfig.sh

conditional statement
--------------------------
	1) decision conditional
	2) loop conditional





decision conditional
----------------------------
		if [ expression1 ] 
		then 
		//code 
		elif [ expression2 ] 
		then 
		//code
		else 
		//code
		fi


loop conditional
------------------------------
	for name in $names
	do
	//code like echo $name
	done


while loops
-----------------

	while [ condition] ;
	do 
	//code
	done





Linux function
--------------------

	function functionName () {  
		Commands to be executed  
	}  

	// to call
	functionName


conditional expression
-----------------------
	-z string
	True if the length of string is zero.

	-n string
	True if the length of string is non-zero.

	string1 == string2

	string1 != string2
	True if the strings are not equal.

	string1 < string2
	True if string1 sorts before string2 lexicographically.

	string1 > string2
	True if string1 sorts after string2 lexicographically.

	arg1 OP arg2 --mainly use for numeric things
	OP is one of ‘-eq’, ‘-ne’, ‘-lt’, ‘-le’, ‘-gt’, or ‘-ge’.


