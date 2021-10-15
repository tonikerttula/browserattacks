### Introduction

This project requires a controlled testing environment, which can be unplugged from external web for security purposes. So we'll be using VirtualBox downloaded on Windows 10, in which we have Kali Linux installed.

#### Installation

I Downloaded Kali Linux 64-bit 2021.3 Installer
https://www.kali.org/get-kali/#kali-bare-metal

In VirtualBox GUI, I clicked "New" and in the followin installation window selected the following:

- Name and OS:
  - Name: Kali
  - Type: Linux
  - Version: Other Linux 64-bit

- Memory Size: 2048 MB

- Hard disk:
  - Create a virtual hard disk now

- Hard disk file type: 
  - VDI
 
- Storage on physical hard disk:
  - Dynamically allocated

- File location and size
  - virtual hard disk size: 20 GB 

.Next I selected the newly created VM in the GUI and clicked "Settings". In settings go to "Storage" and and u.nder "Controller: IDE" click the CD icon "Empty". On the right under "Attributes", click the CD icon dropdown and choose the Kali linus file just downloaded.
.
Start the VM and select start-up disk: it's the file we downloaded.
Click install.

Next select language, keyboard layout and location. Name the machine and domain and choose username and password. All of the above can be chosen freely. For all following installation options go with the default settings until the installation is finished.
After the reboot open the VM and test that it works: Display, keyboard and mouse are the most important.

#### Internal Network

So we need to create a network completely isolated from the outside world for safety reasons. Also the different VM's should be able to communicate between each other. For this, we need to setup DHCP server using VBOXMANAGE.

First go to the VM and select "Settings" -> "Network" and there Internal network. Name the network. Image below
![1]

Select a second machine and repeat. Remember to add both machines in the same internal network.
To enable communication in between these machines, I need to utilize the VBoxManage application. So open command prompt on your host. Go to the directory in which you have saved VirtualBox on your PC. In my case it's in D:\VirtualBox.

Now in this directory, you can use the command `vboxmanage dhcpserver` to see the options. Using `vboxmanage list dhcpservers` you can see the DHCP servers configured on your network.
To add another server, we use the following command:
`vboxmanage dhcpserver add --netname intnet --ip 192.168.2.1 --netmask 255.255.255.0 --lowerip 192.168.2.2 --upperip 192.168.2.254 --enable` 

--netname should be the name you chose for internal network in VBox

--ip for choosing internal ip address

--netmask for choosing the netmask

--lowerip and --upperip are the ranges in which the machines can be given ip addressess

Now using the command `vboxmanage list dhcpservers` we can see if the new DHCP server was added:
![2]

Next make sure the machines are connected into the appropriate internal network, and open the VMs.

In the command prompt typing `ifconfig` you can check the ip addresses of the machines. My machines' ips are 192.168.2.2 and 192.168.2.3. Try pinging the machines from each other.
![3]
![4]

As we can see, now the machines are able to ping each other, but not able to reach internet. Screenshot is only from the 192.168.2.3 VM, but both tested and worked.



[1]: https://i.imgur.com/BAaW0mU.png
[2]: https://i.imgur.com/DkyhwDn.png
[3]: https://i.imgur.com/GHWLCzy.png
[4]: blob:https://imgur.com/fa503292-2ad1-4aee-aa9b-1d16c9ca2a4f
