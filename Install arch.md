Better readabilty change font
```
setfont ter-132n
```

If you can't use an ethernet cable this is how you set up wifi
## connect wifi
```bash
iwctl
	# get wifi card name ex. wlan0
	device list
	# scan available wifi networks
	station wlan0 get-networks
	# connect to your wifi
	station wlan0 connect <your_ssid>
	# you will prompted to enter password if secure	
	exit
```
- Test Internet connection
```bash
ping google.com -c5
```

## SSH to installer
> why SSH, because it enables you to:
> - Copy paste to and from installer terminal
> this alone is a solid enough argument to use SSH instead of tty
> - you will install from the your favorite terminal emulator, using your favorite font that won't your eyes.

- get the ip address of the installer
```bash
ip addr
```
![[Pasted image 20240616143203.png]]
- then make sure ssh daemon is running
```bash
systemctl start sshd
```
- now set a password for the root user to use when SSHing
```bash
passwd
# then enter the password
```
![[Pasted image 20240616143634.png]]


## Update sources
```bash
pacman -Sy
```

## Fill disk with random data
if your drive contains some things that shouldn't never be seen and you want to start from a true clean slate this command is for you:

- get disk name you want to install on
```bash
lsblk
```
- fill disk with random data
```bash
dd if=/dev/urandom of=/dev/nvme0n1 status=progress bs=4096
```

## Partition disk
- partition disk
	- Using `cfdisk`	(easy, beginner friendly)

```bash
cfdisk /dev/<disk-name> # ex. cfdisk /dev/nvme0n1
```
![[Pasted image 20240618141742.png]]
- Using `gdisk` (advanced) 
> :warning: **If you are using MBR**: use `fdisk` instead !!
```bash
gdisk /dev/<disk-name> # ex. cfdisk /dev/nvme0n1
# inside gdisk
	# show existing partitions if any
	p
```

