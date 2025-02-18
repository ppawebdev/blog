---
authors: [ "Geoffrey Hunter" ]
date: 2017-04-20
draft: false
title: U-Boot
type: page
---

## Environment Variables

To print an environment variable, use the printenv command:

```text
uboot> printenv autoload
autoload=yes
```

To set an environment variable, use the setenv command:
    
```text
uboot> setenv autoload=no
```

You don't actually need the equals sign! This works also:
    
```text
uboot> setenv autoload=no
```

If you want to set a variable to something which includes special characters, such as spaces or semi-colons, you can enclose the value in single quotes:

```text
setenv bootcmd 'tftpboot 0x2000000 uImage; tftpboot 0x3000000 core-image-minimal-zc702-zynq7.cpio.gz.u-boot; tftpboot 0x2A00000 uImage-zynq-zc702.dtb; bootm 0x2000000 0x3000000 0x2A00000'
```

The above variable, when executed, runs several commands.

## Setting The Device's IP Address

There are two ways of setting the IP address of the device running U-Boot (useful if you are going to boot via TFTP). You can either **use the network DHCP or define a static IP address.** To use the network DHCP:
    
```text
u-boot> dhcp
```

To use a static IP address:

```text
u-boot> setenv ipaddr <static ip address>
```

## Booting Via TFTP

TFTP is a great way to boot Linux on your board when developing, because it is quick and requires no physical medium to be moved from your computer to the board (unlike the SD card option).

## Setting TFTP Up On Development Computer

This following guide assumes you are running Ubuntu (this was tested on Ubuntu v14.04 64-bit):

Install the following packages:

```bash
$ sudo apt-get install xinetd tftpd tftp
```

Create a file called `/etc/xinetd.d/tftp` and save the text below inside it:

```text
service tftp
{
protocol = udp
port = 69
socket_type = dgram
wait = yes
user = nobody
server = /usr/sbin/in.tftpd
server_args = /tftpboot
disable = no
}
```

Create a folder called `/ftpboot`:

```text
sudo mkdir /tftpboot
sudo chmod -R 777 /tftpboot
sudo chown -R nobody /tftpboot
```

Restart the TFTP server:

```text
sudo service xinetd restart
```

The TFTP server should now be up and running!

## Setting TFTP Up On Embedded Device

U-Boot needs to be told about the address of the TFTP server (this will be the IP address of your computer you are building the Linux image on):

```text
uboot> set serverip <ip address>
```

We normally want to disable autoload, as this causes U-Boot to try and automatically download an image and boot from it as soon as we type dhcp:
    
```text
uboot> setenv autoload no
```

Then we can force U-Boot to look for a DHCP server and request an IP address:

```text
uboot> dhcp
BOOTP broadcast 1
DHCP client bound to address 10.4.6.88 (6 ms)
```

We can then use tftpboot commands to download files over TFTP and place them at specific locations in memory. This example below is for the Xilinx Zynq ZC702 development board:
    
```text
tftpboot 0x2000000 uImage
tftpboot 0x3000000 core-image-minimal-zc702-zynq7.cpio.gz.u-boot
tftpboot 0x2A00000 uImage-zynq-zc702.dtb
bootm 0x2000000 0x3000000 0x2A00000
```

These commands can be combined and saved to the boot variable:
    
```text
setenv bootcmd 'tftpboot 0x2000000 uImage; tftpboot 0x3000000 core-image-minimal-zc702-zynq7.cpio.gz.u-boot; tftpboot 0x2A00000 uImage-zynq-zc702.dtb; bootm 0x2000000 0x3000000 0x2A00000'
```

Remember to use saveenv if you want these config parameters to persist when power cycling.
