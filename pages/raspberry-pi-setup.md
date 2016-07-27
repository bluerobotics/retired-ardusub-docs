---
layout: default
title: Raspberry Pi Setup
permalink: /raspi-setup/
nav:
- Easy Setup With Image: easy-setup-with-disk-image
- Setup From Scratch: setup-from-scratch
- Advanced: advanced
---

# {{page.title}}

This page explains how to set up a Raspberry Pi for use with ArduSub.

## Easy Setup With Disk Image

With the simple method, you restore a `.img` file to the Raspberry Pi SD Card. This provides the operating system and everything already set up for running ArduSub. You can download the most recent disk image here:

<i class="fa fa-download" aria-hidden="true"></i> [Latest Ardusub-Raspbian Image](http://img.ardusub.com/ardusub-raspbian.img.gz) *(1.56 GB, Updated 2016-07-27)*

*(Raspbian Jessie Lite 2016-05-27 w/ ArduSub Companion Computer Setup)*

To load the image to your SD card, use the following instructions.

### Mac and Linux

Insert the SD card to a card reader, open a terminal, and run the following command to find the disk number of the SD card.

On Mac:

	diskutil list

On Linux:

	df -h

You can find the disk number in the output and it will look something like `/dev/diskX` or `/dev/sddX`. It may be `disk2`, `disk3` on Mac and `/dev/sdd1`, `/dev/sdd2` on Linux. You need to start by unmounting that disk.

On Mac:

	diskutil unmountDisk /dev/diskX

On Linux:

	umount /dev/sddX

To write the disk image to the SD card, use the following command (on Linux, replace `bs=1m` with `bs=1M`):

	sudo dd bs=1m if=~/Downloads/ardusub-raspbian.img of=/dev/rdiskX

If the image is still compressed, you can combine the decompression and writing in one command:

	gunzip --stdout ardusub-raspbian.img.gz | sudo dd bs=1m of=/dev/rdiskX

Note that the location and name of `rasbian-ardusub.img` might be slightly different depending on where you downloaded it. Once complete, you can eject the SD card and install it on the Raspberry Pi. That's it!

## Setup From Scratch

These instructions are provided for those who wish to set everything up themselves.

### Install Raspbian and Set IP Address

Start with Jessie-Lite image downloaded from [raspberrypi.org](https://www.raspberrypi.org/downloads/raspbian/) and follow their instructions to install it to an SD card.

1. Insert SD card to Raspberry Pi and allow to boot up for about 1 minute.
2. Remove SD card, insert to card reader, and modify the file `/boot/cmdline.txt` to have "ip=192.168.2.2" to the end of the line. It will look something like this (all one line):

		dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait ip=192.168.2.2

3. Insert the SD card back into the Raspberry Pi, connect the Ethernet directly to your computer (through a tether interface board if desired), and power it up.

### Set Up Internet Sharing

#### Windows

To be completed

#### Linux

To be completed

#### Mac

1. Go to Sharing and click "Internet Sharing". Choose "Wi-Fi" for the source and your Ethernet port or adapter for the destination.
2. Go to Network Settings and set IP for Ethernet to Manual and the address to 192.168.2.1.

### Command Line Setup

All of this setup is completed on the command line. You must connect to the Raspberry Pi via SSH, using a client program like Putty or the Mac Terminal. The default password is `raspberry`.

	ssh pi@192.168.2.2

First, run `rpi-config` to expand filesystem and enable the camera.

1. Run `sudo raspi-config` on the command line.
2. Choose "Expand Filesystem", then "Ok"
3. Choose "Enable Camera", then "Yes", then "Ok"
4. Choose "Finish" and "Yes" to rebooting.

Next, update the current software and install the prerequisites needed.

	sudo apt-get update
	sudo apt-get install -y git

	# Update package lists and current packages
	sudo apt-get update
	sudo apt-get upgrade

	# Update Raspberry Pi
	sudo apt-get install -y rpi-update
	sudo rpi-update

	# install python and pip
	sudo apt-get install -y python-dev python-pip

	# install dronekit
	sudo pip install dronekit dronekit-sitl # also installs pymavlink
	sudo pip install mavproxy

	# install screen
	sudo apt-get install -y screen

	# live video related packages
	sudo apt-get install -y gstreamer1.0


Disable camera LED if using the v1 camera.

	sudo sed '$a disable_camera_led=1' /boot/config.txt

Clone the companion repository:

	git clone https://github.com/bluerobotics/companion.git

Add these lines to `/etc/rc.local` to automatically start `mavproxy` and the video stream. Add them before the `exit 0` at the end.

	screen -dm -S mavproxy /home/pi/companion/RPI2/Raspbian/start_mavproxy_telem_splitter.sh
	screen -dm -S video /home/pi/companion/RPI2/Raspbian/start_video.sh

Last, restart the Raspberry Pi

	sudo shutdown now -r

When it reboots, it will automatically start streaming video if the camera is connected and will automatically connect to the Pixhawk, if connected.

## Advanced

### Reentering Mavproxy and Video Processes

The `mavproxy` and video processes are started in "screen" sessions so that they can be reentered to view output and any errors that may have occurred. To reenter the sessions, open and SSH terminal to the Raspberry Pi and run the following commands:

	sudo screen -r video

	sudo screen -r mavproxy

To quit the process, press Ctrl-C. To exit without stopping the process, press Ctrl-A, then D to "detach" from the session.

### Backing Up Disk Image

On Mac or Linux, first find out the disk number of the SD card using `diskutil`.

	diskutil list

Find the SD card in the output. On Mac it will be something like `/dev/disk2` and on Linux it will be something like '/dev/sdb'.

*On Mac:*

	sudo dd bs=4m if=/dev/disk2 | gzip > rasbian-ardusub.img.gz

*On Linux:*

	sudo dd bs=4M if=/dev/sdb | gzip > rasbian-ardusub.img.gz

Press Ctrl-T to check on status while this is happening. It can take quite a while. 

To restore the image, see the simple setup instructions above.