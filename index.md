# Guide to installing a LAMP stack on Google cloud

By Amory Gengler amorygengler@icloud.com

Go to https://console.cloud.google.com/compute and create a new instance.

Configure your VM with desired CPU and memory settings (f1 micro is the cheapest and sufficient for our needs).

Make sure you change the Operating System to Ubuntu 18.04.

Once your VM has loaded, open the web SSH terminal.

## Install Apache, MySQL, PHP, and Git.

Once the web SSH terminal has loaded run:

    sudo apt update -y && sudo apt upgrade -y && sudo apt install apache2 mysql-server mysql-client php libapache2-mod-php php-mysql php-cli git -y

## Basic configuration.

### Apache.

If you have UFW enabled, you'll need to allow Apache traffic through the firewall.

    sudo ufw allow in "Apache Full"

You can confirm Apache is working by going to your console.cloud.google.com/compute page and coppying the IP address of your VM, opening a new tab, and entering that IP address as the URL. You should see the Apache2 Ubuntu Default Page.


### MySQL

To configure MySQL run the installation script that comes preinstalled with MySQL.

    sudo mysql_secure_installation

Follow instructions onscreen to create the root password.

Create a secure root password for MySQL and make sure you don't lose it.

Press Y for the rest of the questions to finish installing MySQL.

You can use the password to login to MySQL as root by changing the authentication method.

    sudo mysql
    
For a list of users enter

    SELECT user,authentication_string,plugin,host FROM mysql.user;
    
Replace password in the next command with your MySQL root password.

    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    
Refresh the table..

    FLUSH PRIVILEGES;

You can now verify the authentication method has been changed:

    SELECT user,authentication_string,plugin,host FROM mysql.user;

    exit

### PHP

Set Apache to prefer loading index.php files before index.html files by default.

    sudo nano /etc/apache2/mods-enabled/dir.conf

Replace the contents of /etc/apache2/mods-enabled/dir.conf with:

    <IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
    </IfModule>

To finish editing in nano, press ctrl+X, type Y to confirm overwriting, then press enter.

Restart apache for changes to take effect. 

    sudo systemctl restart apache2

### Git

To configure git replace *Your Name* with your name.

    git config --global user.name "Your Name"
    
Replace *YOUR@EMAIL.HERE* with your email address.

    git config --global user.email "YOUR@EMAIL.HERE"
    
## You now have a Google Cloud VM running a LAMP stack with git and you're ready to start working.
