# Termux Copy Pasta

## Install Termux

**download and install the apks**
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

    termux-setup-storage && pkg update && pkg upgrade && pkg install nano curl termux-auth php openssh mariadb apache2 php-apache phpmyadmin git bash wget proot termux-services man aria2 irssi zip unzip python -y && passwd && sshd

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

**Change index.html to read index.php** 

and append the following code immediately below that block:

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

### DATABASE Server

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

    GRANT ALL PRIVILEGES ON wordpress.\* TO "wordpress"@"localhost" IDENTIFIED BY "password";

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
    GRANT ALL PRIVILEGES ON uwi.\* TO "god"@"localhost" IDENTIFIED BY "god";
    quit
    mysql -u god -p

cd $PREFIX/share/apache2/default-site/htdocs
cd ../../share/apache2/default-site/htdocs

#### Composer

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

### Termux:Boot

Create the directories needed
    mkdir .termux
    mkdir .termux/boot
    cd .termux/boot
this creates an empty file
    touch start.sh  
    chmod +x start.sh
Edit the file to add your start up commands - I used nano editor like so
    nano start.sh

    #!/data/data/com.termux/files/usr/bin/sh
    termux-wake-lock
    sshd
    mysqld_safe &
    sleep 5
    httpd
    
    sudo apachectl start
    
    To start Termux-Services
    #!/data/data/com.termux/files/usr/bin/sh
    termux-wake-lock
    . $PREFIX/etc/profile

Type Ctrl-O and press Enter,
Type Ctrl-X to exit nano.

After editing and saving the file, try restarting your device. And then run this command to see if it worked:
    reboot phone
    su -c "reboot"

### xshin

    apt install termux-api
    apt install clang
    https://mytermux-xshin404.vercel.app/docs/intro
    pkg update -y && pkg upgrade -y
    pkg i git bc -y
    git clone https://github.com/xshin404/myTermux
    cd myTermux && ./install.sh

Type Ctrl-O and press Enter,
Type Ctrl-X to exit nano.

# Work in progress

pkg uninstall
passwd
clear
history
cd
cd ../..
rm
rm -rf

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

### Variables

    echo $HOME
    /data/data/com.termux/files/home
    
    echo $PREFIX
    /data/data/com.termux/files/usr

### Cron

    pkg install cronie termux-services
    restart termux session
    sv-enable crond
    crontab -e
    https://crontab.guru/

### list process

    ps
    ps ax
    ps -ef

### Uninstall termux

    rm -rf $PREFIX and then restart application. This doesn't touch $HOME directory but removes all packages, basic environment will be reinstalled on next app startup.

    For entire cleanup it is better to erase app data through Android settings.

    If its been installed with apt do apt remove tool-name

    If it's installed with pkg, do pkg remove <tool name>

    If it's downloaded as a git repo, running whatever it gave you to uninstall or deleting the whole directory usually works.
