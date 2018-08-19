# Jetson TX2 module setup
A guide on how to setup a TX2 Jetson board from a VM (Ubuntu 16.04) on a Windows (10) host.

# First steps

* Download from http://old-releases.ubuntu.com/releases/16.04.4/ the 64-bit PC (AMD64) desktop image
* Install on VMware with 50GB hard disk space
* Unpack Jetson TX2 and make sure you have all the cables needed. Ideally you can plug a USB hub to connect both a mouse and a keyboard, but just connecting a USB keyboard will do. Power up the module by following the instructions and when you get prompted with the initial console, type “cd NVIDIA-INSTALLER”, press enter, then type “sudo ./installer.sh”, give the requested password for the sudo command (i.e. “nvidia” by default). Watch the installation commence and once it is done, type “sudo reboot”. GUI will load.
* Run sudo poweroff to shut down the TX2 and disconnect the AC adapter. 

# Network Connection

* Ideally you can just plug the ethernet cable on the same switch/router your host is connected too. At the lab inside the University the TX2 could not get an IP address from the switch. SO I worked around it by turning my laptop into a router. My laptop (VMware host) runs Windows 10.
* Open Settings > Network & Internet
* At the bottom of the screen click on Network and Sharing Center
* You can see your active network. Click on it and then click Properties > Click the Sharing tab and check the box “Allow other network users… “ and then selecting on the “Home networking connection” the option “Ethernet”
* Make sure you have an ethernet cable from your host to your TX2.
* Just to make sure, you can connect the AC adapter back on the TX2, boot it and run ifconfig. If everything runs smoothly, you should be able to ping the IP address you got from the ifconfig from your VMware guest OS

# Flash

* Run your Ubuntu 16.04 VMware guest
* Login to the nvidia website and download the JetPack from here https://developer.nvidia.com/embedded/jetpack
* Type chmod +x ./JetPack-.... Whatever the file is named and then run it (./JetPack-...)
* The flashing/installation procedure commences. When it asks you for the network topology, you select the second one (bottom one)
* Wait for everything to be downloaded/installed on your host machine
* At some point you will see a window stating that the following actions (Flashing OS, Installing a bunch of packages etc) will be performed. Then you will do as the terminal titled “Post installation” says, i.e. put the TX2 in force recovery mode. In order to do this, you will have to shut down the TX2, unplug the AC adapter and connect the microUSB to your host (my laptop in this case). When you do the Force Recovery Mode procedure you will see on your VMware that you can connect a USB from the host OS to the guest OS. On the top left of the VMware Player > Removable Devices you will see the option of an Nvidia device. If you click on it you will disconnect it from the host (Windows) and connect it to the guest (Ubuntu). That is what we want, so go ahead and click it
* If you open a new terminal in Ubuntu, running the command lsusb should list Nvidia. If it doesn’t something went wrong in the previous steps and there is no point in continuing the Jetson installation. Rollback and try to troubleshoot
* If everything is ok and the Ubuntu machine can “see” the TX2, by pressing Enter on the “post installation” terminal window everything should now be able to begin: the flashing and all the installation steps. If you are lucky everything finishes here!

# Bonus! Cannot determine TX2 IP: Flash is done but installations are not

* In that case you can again work around the problem. Ctrl-c the “Post installation” window and close the jetpack installation window. We will start over but with a twist.
* Rerun the ./JetPack-.... 
* Do the same procedure as before but this time at the listing window with the things that are going to happen (flashing, installing), choose “Custom” instead of “Auto” and click install only at every option that claims “Install”. That is, do not click again on the flashing option since it is pointless; we already did that before
* Once it is done downloading etc, it will prompt you a window that asks you to type in the TX2 IP address and username and password. The IP address can be found by typing ifconfig on a TX2 terminal. Then just type it at the window in your VM. Username and password are nvidia for both by default
* Once you click next, the installation will start and everything will be installed normally. Finally.
