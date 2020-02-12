# Guide to installing a LAMP stack on Google cloud

Go to https://console.cloud.google.com/compute and create a new instance.

Configure your VM with desired settings.

Once your VM has loaded, open the web SSH terminal.

## Now we're going to install Apache, MySQL, and PHP.

Once the web SSH terminal has loaded run:

>sudo apt update -y && sudo apt upgrade -y && sudo apt install apache2 mysql-server mysql-client php libapache2-mod-php php-mysql php-cli git -y

## Now we're going to do some basic configuration.

### Change the root password for MySQL.

>sudo mysql_secure_installation -y

>sudo mysql

>SELECT user,authentication_string,plugin,host FROM mysql.user;

>ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

>FLUSH PRIVILEGES;

>SELECT user,authentication_string,plugin,host FROM mysql.user;

>exit

### We want Apache to default to loading .php before .html files.

>sudo nano /etc/apache2/mods-enabled/dir.conf

replace the contents of dir.conf with:

>\<IfModule mod_dir.c>

> DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm

>\</IfModule>


### Restart apache for changes to take effect. 

>sudo systemctl restart apache2


### Next we're going to configure Git

>git config --global user.name "Your Name"

>git config --global user.email "YOUR@EMAIL.HERE"
