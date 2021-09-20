
## INSTALL

termux
download and install the apk
https://f-droid.org/packages/com.termux/
Termux
https://search.f-droid.org/?q=termux&lang=en
Termux:Boot
Termux:API    
Termux:Float 
Termux:Styling
Termux:Tasker
Termux:Widget
  
## SETUP

### Run commands

termux-setup-storage
pkg update
pkg upgrade
pkg install termux-auth
passwd
pkg install openssh
sshd

pkg install php mariadb apache2 php-apache wget phpmyadmin -y


### Webserver
cd ~
cd $PREFIX/etc/apache2
cd ../usr/etc/apache2
nano httpd.conf
Scroll down about a page to the huge list of LoadModule commands. We need to disable one and enable a couple. The # sign disables a line. Find:

#LoadModule mpm_prefork_module libexec/apache2/mod_mpm_prefork.so
and remove the # at the beginning. The following line should be:

LoadModule mpm_worker_module libexec/apache2/mod_mpm_worker.so
Add a # at the beginning of that line.

Close to the bottom of the LoadModule lists, find:
#LoadModule rewrite_module libexec/apache2/mod_rewrite.so
and again, remove the # from the beginning.

We now need to tell apache to use the PHP module, so add this line after the line you just edited:
LoadModule php_module /data/data/com.termux/files/usr/libexec/apache2/libphp.so

Now, scroll down until you find the section header:
DocumentRoot "/data/data/com.termux/files/usr/share/apache2/default-site/htdocs"
<Directory "/data/data/com.termux/files/usr/share/apache2/default-site/htdocs">

A few lines down, you'll see the line:
AllowOverride None

Change this to read:
AllowOverride FileInfo

Immediately below this, you'll see a block:

<IfModule dir_module>
  DirectoryIndex index.html
</IfModule>

Change index.html to read index.php and append the following code immediately below that block:

<FilesMatch \.php$>
    SetHandler application/x-httpd-php
</FilesMatch>

Type Ctrl-O and press Enter, 
Type Ctrl-X to exit nano.

cd $PREFIX/lib
cd ../../lib
touch php.ini
nano php.ini
upload_max_filesize = 32M
post_max_size = 32M

include_path = ".:$PREFIX/bin/php"

Type Ctrl-O and press Enter, 
Type Ctrl-X to exit nano.

cd $PREFIX/share/apache2/default-site/htdocs
httpd
killall httpd

rm index.html
touch index.php
nano index.php

<?php
phpinfo();
?>

Type Ctrl-O and press Enter, 
Type Ctrl-X to exit nano.

killall httpd
apachectl start # to start the server
apachectl restart # to restart the server
apachectl stop # to stop the Apache
httpd

http://192.168.100.199:8080/index.php


## DATABASE Server
To launch the daemon type:
mysqld_safe &

You might need to tap Enter to get a command prompt to appear. The daemon is now running, so we can connect to it by typing:
mysql

You should see a prompt:
MariaDB [(none)]>

We need to set up a database for Wordpress and a user for Wordpress to access the database.
To add the database type:
CREATE DATABASE wordpress;
[You should get a reply: Query OK, 1 row affected (0.001 sec) or similar]

To create a user, type:
GRANT ALL PRIVILEGES ON wordpress.* TO "wordpress"@"localhost" IDENTIFIED BY "password";

You can obviously substitute the word "password" for something that's meaningful! As it's only accessible to the device itself (localhost) you should be fine with something fairly insecure, but don't let me dictate how secure you want it!
[You should get a reply: Query OK, 0 rows affected (0.054 sec) or similar]
Type:
quit

That's MySQL configured. You can test it by typing:
mysql -u wordpress -p
and type your password. You should get to the MariaDB prompt. Type quit again.

mysqld_safe & 
mysql
CREATE DATABASE uwi;
GRANT ALL PRIVILEGES ON uwi.* TO "god"@"localhost" IDENTIFIED BY "god";
quit
mysql -u god -p

cd $PREFIX/share/apache2/default-site/htdocs
cd ../../share/apache2/default-site/htdocs

pkg install curl
curl -sS https://getcomposer.org/installer | php -- --install-dir=/data/data/com.termux/files/usr/bin --filename=composer
composer self-update
which composer

/data/data/com.termux/files/usr/share/phpmyadmin
/data/data/com.termux/files/usr/share/apache2/default-site/htdocs

apachectl stop
cd /data/data/com.termux/files/usr/var/run/apache2
rm httpd.pid
apachectl start

## Termux:Boot
//Create the directories needed
mkdir .termux
mkdir .termux/boot
cd .termux/boot
//this creates an empty file
touch start.sh    
chmod +x start.sh
//Edit the file to add your start up commands - I used nano editor like so
nano start.sh

#!/data/data/com.termux/files/usr/bin/sh
termux-wake-lock
sshd
mysqld_safe &
sleep 5
httpd

sudo apachectl start

+=+
#!/data/data/com.termux/files/usr/bin/sh
termux-wake-lock
. $PREFIX/etc/profile

Type Ctrl-O and press Enter, 
Type Ctrl-X to exit nano.

After editing and saving the file, try restarting your device. And then run this command to see if it worked:
reboot phone
su -c "reboot"

pkg install curl
pkg install php
pkg install git
pkg install zsh
pkg install nano

git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
nano .zshrc
Find the line ZSH_THEME="robbyrussell" replace robbyrussell with agnoster theme in .zshrc File (CTRL + X & Enter to Save)
chsh
zsh
bash

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git "$HOME/.zsh-syntax-highlighting" --depth 1
echo "source $HOME/.zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> "$HOME/.zshrc"

https://itrendbuzz.com/install-and-configure-z-shell-on-termux/


curl -sS https://getcomposer.org/installer | php -- --install-dir=/data/data/com.termux/files/usr/bin --filename=composer
composer self-update
which composer


apt install php-apache
cd /data/data/com.termux/files/usr/etc/apache2/
nano httpd.conf
LoadModule php7_module /data/data/com.termux/files/usr/libexec/apache2/libphp7.so
<FilesMatch \.php$>
  SetHandler application/x-httpd-php
</FilesMatch>

/data/data/com.termux/files/usr/share/apache2/default-site/htdocs

apt install apache2 php php-apache phpmyadmin mariadb -y
httpd
killall httpd
cd $PREFIX/share/apache2/default-site/htdocs
rm index.html
touch index.php
nano index.php

<?php
phpinfro();
?>

cd
pwd
cd ..
cd usr
cd etc
cd apache2
clear
pwd
ls
nano htt

LoadModule php_module libexec/apache2/libphp.so
LoadModule mpm_prefork_module libexec/apache2/mod_mpm_prefork.so
#LoadModule mpm_worker_module libexec/apache2/mod_mpm_worker.so
https://www.youtube.com/watch?v=0ytASgBK8uA

apt list
apt list --upgradeable
apt list --installed
apt update
apt upgrade
apt remove
termux-info

pkg uninstall
passwd
clear
history
cd
cd ../..
rm
rm -rf
apt-get install openssh
apt install termux-api
termux-battery-status
termux-brightness 255
termux-call-log
termux-camera-info
termux-camera-photo -c 0 test.jpeg
termux-clipboard-get
termux-clipboard-set
termux-contact-list
termux-location
termux-microphone-record -d
termux-microphone-record -i
termux-microphone-record -q
termux-microphone-record i
termux-sensor
termux-sms-list
termux-telephony-call 123
termux-telephony-cellinfo
termux-telephony-deviceinfo
termux-torch on/off
termux-tts-engines
termux-tts-speak hello im god in termux
termux-tts-speak
press ctrl+z to stop tts-speak
factor 100
fortune
w3m google.com
press ctrl+c to close w3m
cowsay "happ"

pkg install git
apt install bash
pkg install wget
pkg install proot
pkg install termux-services
pkg install man
apt install aria2
pkg install irssi
apt install zip unzip
apt install fish
apt install figlet
apt install fortune
apt install toilet
apt install w3m
apt install cowsay
pkg install php

pkg install python

pkg install proot
termux-chroot
ls /usr
bin  doc  etc  include	lib  libexec  share  tmp  var

Press Q to exit man page


Variables
echo $HOME
/data/data/com.termux/files/home

echo $PREFIX
/data/data/com.termux/files/usr

Cron
pkg install cronie termux-services
# restart termux session
sv-enable crond 
crontab -e 
https://crontab.guru/

list process
ps
ps ax
ps -ef

Uninstall termux
rm -rf $PREFIX and then restart application. This doesn't touch $HOME directory but removes all packages, basic environment will be reinstalled on next app startup.

For entire cleanup it is better to erase app data through Android settings.


If its been installed with apt do apt remove tool-name
If it's installed with pkg, do pkg remove <tool name>
If it's downloaded as a git repo, running whatever it gave you to uninstall or deleting the whole directory usually works.

phone hacking
https://www.youtube.com/channel/UC1szFCBUWXY3ESff8dJjjzw

Hitomi-Downloader
https://github.com/KurtBestor/Hitomi-Downloader

Darknet-Search-Engine
https://github.com/r3k4t/Darknet-Search-Engine

termux-app/issues/2015
https://github.com/termux/termux-app/issues/2015

Tool-X
https://github.com/rajkumardusad/Tool-X

300+ Best Termux Tools For Ethical Hacking
https://www.techncyber.com/2018/08/termux-hacking-tools.html

RUN_COMMAND Intent
https://github.com/termux/termux-app/wiki/RUN_COMMAND-Intent

Termux-Whatsapp-Bot-English
https://github.com/HotarouTakahashi/Termux-Whatsapp-Bot-English

termux-whatsapp-bot
https://github.com/fdciabdul/termux-whatsapp-bot

Top 5 Best Information Gathering Tools For Termux
https://amanbytes.com/top-5-best-information-gathering-tools-for-termux/

termux 
https://github.com/topics/termux

Termux Automation Scripts
https://github.com/themobileprof/scripts

Termux-sms-send
https://wiki.termux.com/wiki/Termux-sms-send

wabot-aq
https://github.com/Nurutomo/wabot-aq
https://www.youtube.com/watch?v=6sMJdpv7VTc

https://www.youtube.com/watch?v=oee1tmbtti8


Fix httpd
#
# This script is part of the video,
# Cómo instalar Apache Web Server en Android: https://youtu.be/cwp63pJMy_A and
# it's intended to be used on Termux Android 32 bits in order to fix the issue,
# https://github.com/termux/termux-packages/issues/1727
# Before executing this script you must install termux-chroot see de video,
# Cómo hacer chroot en Termux: https://youtu.be/gdy12S94BBk
#
#!/usr/bin/env bash
aps=$(pidof httpd)
pidf=/var/run/apache2/httpd.pid
[[ -f $pidf ]] && rm -f $pidf
[[ "$aps" != "" ]] && kill -9 $aps

reboot phone
su -c "reboot"

band name
catastrophic dismemberment

war isnt about who is right, its about who is left

team bisket
