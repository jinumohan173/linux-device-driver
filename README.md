#Events in loading device drivers

1.load module

2.open device

3.read device

4.write device

5.close device

s

Building linux kernel
there are two methods are available
1.build linux kernel module against installed kernel with full kernel source tree
2.build linux kernel module against installed kernel with out full kernel source tree
the first method will take lot of time and memory consume is higher so that i prefer second method
first find out which linux header we are working
#for that give this command 



sudo apt-cache install kernel-headers-$(uname -r)



it  will print ur kernel version for me its linux-header-3.13.0

Note:-if you are using raspberry pi or beagle bone we need to add the processor in tail to install
linux header else if we are running ubutu just get the version of linux

#Note:- if u r using virtual machine u can use 


sudo apt-get insatll virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11


sudo reboot 

to get full screen

command to insatll linux header


sudo apt-get install kernel-headers-$(uname -r)

All you need to do is change Makefile to use current kernel build directory. 
You can obtain this directory name by typing following command:



$ ls -d /lib/modules/$(uname -r)/build




create a directory for testing 
$ mkdir ~/test
go to that directory
$ cd ~/test

type ther required c-pgm u can download it from my repo



save it as main.c 
you can't compile it using normal gcc conmplier because of #include<linux.h>



create a make file M should be in capital 


vi Make


copy paste pgm from my repo named as make then in terminal


$make


sample output:-


#make -C /lib/modules/2.6.27-7-generic/build M=/tmp/test2 modules
make[1]: Entering directory `/usr/src/linux-headers-2.6.27-7-generic'
  CC [M]  /tmp/test2/main.o
  Building modules, stage 2.
  MODPOST 1 modules
  CC      /tmp/test2/main.mod.o
  LD [M]  /tmp/test2/main.ko
make[1]: Leaving directory `/usr/src/linux-headers-2.6.27-7-generic'




after make function give 


$ls


you can see list of files made with various extensions
give commmand


sudo modinfo filename.ko // sudo modinfo main.ko for my case


to insert module into kernel


$ sudo insmod main.ko

or

$ sudo modprobe main.ko




To list installed Linux kernel module, enter:


$ lsmod


$ lsmod | grep main

To remove hello Linux kernel module, enter:


$ rmmod main





This module just logs message to a log file called /var/log/messages (/var/log/syslog), enter:


$ tail -f /var/log/messages

if its not working


$ tail -f /var/log/syslog



hence you sucessfully made your first linux kernel module for testing
