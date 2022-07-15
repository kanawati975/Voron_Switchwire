## How to install Samba to access and manage your Files on the Raspberry Pi from a windows computer

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/smb.JPG)






First, we need to access the Rapberry pi (no matter which Model).

You can use SSH or PuTTY, or directly from windows command Prompt.

`ssh pi@<your.pi.ip.address>`

Now we need to make sure that the system is up to date and then we install the program

`sudo apt-get update`

`sudo apt-get install samba samba-common-bin`

After installation, we need to configure the samba server and define what do we want it to share.

For simplicity, we will just rename the old config file and create our own version instead of a LOT of editing:

```sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.old```

Now we create a new config file:

```sudo nano /etc/samba/smb.conf```

We must add the following contents to the config file we just created. Simply copy them:
```[global]
   workgroup = WORKGROUP  ##Change this to your Workgroup name. By dafault it's WORKGROUP on Windows
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
   write list = pi, root, @WORKGROUP  ## You may add/change the users or workgroup

[share]
   comment = What do you want to share
   path = /home/pi
   guest ok = yes
   browseable = yes
   printable = yes
   read only = no
   create mask = 0777
   directory mask = 0777
   ```
Save (CTRL+O) and exit (CTRL+X)

Now we need to create a samba user (which is pi) and define its password.

```sudo smbpasswd -a pi```

You will be asked for a password twice. 

**Remember this password, because you will need it to login from windows.**
You could also use the same pi/raspberry defaults.

Now we need to restart the service.

```sudo systemctl restart smbd```

From your Windows Computer, open any explorer window, and click on "This PC" from the left side.
Click on "Map Network Drive" from the top of the Window.

Choose a Letter for the Drive (_I used the Drive Letter X but you can choose any available Drive Letter_), and specify the path to your shared Folder/Directory, which is `//<your.pi.ip.address>` Then click on NEXT

Use the username pi and the Password you created earlier while configuring Samba.
