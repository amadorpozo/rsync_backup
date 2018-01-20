# rsync_backup
Scripts to automate rsync backup. Back-up into another PC. Executed after boot instead of cron. 

## Setup Description
I want to backup the data in machines with Ubuntu or Linux Mint (any other Linux would be similar)
I have a Raspberry Pi in my local network with an external USB HDD where I want to do the back-ups. 
Raspberry must be accessed via SSH.

The Hard-drive is FAT32, which introduces some limitations, as explained within the script itself.

## Preliminary steps
Obviously having the back-up server, a Raspberry Pi, up and running. SSH server and USB HDD mount should be configured properly. 
Also you need to setup your SSH to login without password using keys. Basically:
```
# generate the key in my laptop
ssh-keygen -t rsa
#no-pass-phrase
# copy the key to the Raspberry
ssh-copy-id pi@<rpi_ip>
#test it
ssh pi@<rpi_ip>
```

## Copy the script in your system
Download the [script](https://raw.githubusercontent.com/amadorpozo/rsync_backup/master/rsync_backup) and save it. For example in your home directory (/home/$USER/rsync_backup), or any other place. 

## Launching the script in bootup
I use the graphical tool "startup applications" available in Ubuntu for configuring the boot script. Another alternative would be rc.local, or creating a new init.d script and enabling it (google how to do that!). The startup results creating this file that you can use as reference to create your script.  
```
$ cat /home/$USER/.config/autostart/rsync_amador.desktop 
[Desktop Entry]
Type=Application
Exec=/home/pozo/rsync_backup &
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
Name[en_US]=RSYNC-BACKUP
Name=RSYNC-BACKUP
Comment[en_US]=rsync backup running in background
Comment=rsync backup running in background
```
## Showing back-up status 
I used Conky, a tool that integrates  useful information on your Desktop as a widget (http://conky.sourceforge.net/screenshots.html). The specific script that I used is available [here](https://raw.githubusercontent.com/amadorpozo/conky_config_files/master/Gotham_pozo)
The line to display the result is:
```
${color FFA300}Estado del backup: $color ${execi 5 tail -n 1 /home/$USER/rsync.log}
```
More details [here](https://github.com/amadorpozo/conky_config_files)
