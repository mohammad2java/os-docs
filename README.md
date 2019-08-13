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
       go to Settings -> Network -> and..
       a) checked enable network adapter
       b) Attached to : Bridge Adapter
       c) Name: Intel(R) Ethernet connection.

       4) Now start your OS. Run ifconfig /ip a , now the inet address is your IP from enp0s3 section.
       Use this and run it on your putty. Login with your credentials.
