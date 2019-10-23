
|#|Steps	|Action/Input|
|-|-------|------------|
A	VM Virtual Box installation	Install Oracle VM VB 5.2.8
B	Hardware Virtualization Enabling from BIOS	
	-	Restart computer	
	-	F12 to enter BIOS mode	
	-	Menu > Security	Enable Virtualization
		Enable Virtualization
	Reboot the computer	
C	Setup to install OS on VM	
0	-	Start VM	
1	-	Add New OS	
2	-	Settings	
	  General>Server name	Ubuntu64_Server
	  System>Base Memory	8192 MB
	  System>CUP	2 CPU
	  Display>Video Memory	16 MB
	  Storage> Add Optical Device	Choose Disk > Select Ubuntu ISO file
B	Ubantu 16.04.4 LTS 64 bit installation	
0	VM Vbox > Start Ubuntu64_Server	
1	Language	English
2	Install	Install Ubuntu Server
3	Language for installation	English - English
4	Time zone	Other>Asia>Myanmar
5	Locale	United State-en-US.UTF-8
6	Keyboard	No
7	Server name	GIS-Server
8	Hostname	ubuntu
9	User name	serveradmin
10	Password	password@
11	Encrypt home directory	Yes
12	Confirm time zone (connect internet for time info)	Yes
13	Disk Partition	
	Option	Guided – use entire disk and setup LVM
	Select disk partition	As is
	Write changes to disk and configure	Yes
	Amount	Full
14	Installing the System	(wait till finish)
15	HTTP proxy	Blank for none
16	Install security update automatically	
17	Software selection	(use arrow key to move, use space to select)
		LAMP
		PostgreSQL
		OpenSSH server
18	MySQL password for root	password@
19	Install GRUB boot loader	
20	Installation finish	
21	System runing	Login with serveradmin/password@
