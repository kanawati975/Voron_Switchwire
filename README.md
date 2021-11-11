# Voron_Switchwire
First, you need a shell on your Rapberry pi (no matter which Model). You can use SSH or PuTTY or from windows command Prompt.
`ssh pi@<your.pi.ip.address>`
`sudo apt-get update && samba samba-common-bin`
After installation, you need to configure the samba server and define what does it shares.
For ease, we will just create our own version:
```sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.old```
Now we create a new config file:
```sudo nano /etc/samba/smb.conf```
Add the following contents:
```[global]
   workgroup = WORKGROUP  ##Change this to your Workgroup name##
   winsupport = yes

#### Debugging/Accounting ####

   log file = /var/log/samba/log.%m
   max log size = 1000
   logging = file
   panic action = /usr/share/samba/panic-action %d

####### Authentication #######

   server role = standalone server
   obey pam restrictions = yes
   unix password sync = yes
   passwd program = /usr/bin/passwd %u
   passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
   pam password change = yes
   map to guest = bad user

############ Misc ############
   usershare allow guests = yes

[homes]
   comment = Home Directories
   browseable = yes
   read only = no
   create mask = 0777
   directory mask = 0777
   valid users = %S

[printers]
   comment = All Printers
   browseable = no
   path = /var/spool/samba
   printable = yes
   guest ok = no
   read only = yes
   create mask = 0777

[print$]
   comment = Printer Drivers
   path = /var/lib/samba/printers
   browseable = yes
   read only = yes
   guest ok = no
   write list = pi, root, @WORKGROUP

[share]
   comment = What do you want to share
   path = /home/pi
   guest ok = yes
   browseable = yes
   printable = yes
   read only = no
   create mask = 0777
   directory mask = 0777```

Save (CTRL+O) and exit (CTRL+X)
Now we need to create a samba user (which is pi) and define its password.
```sudo smbpasswd -a pi```
You will be asked for a pawword twice. Remember those because you will need them to login from windows. You could also use the same pi/raspberry defaults.
Now we need to restart the service.
```sudo systemctl restart smbd```
