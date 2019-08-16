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
       c) Name: Intel(R) Ethernet connection.

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
    


for more details visit to given url 
---------------------------------------
    https://blog.packagecloud.io/eng/2015/03/30/apt-cheat-sheet/




