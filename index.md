#LAMP Stack Install

sudo apt update -y && sudo apt upgrade -y
sudo apt install apache2 mysql-server mysql-client php libapache2-mod-php php-mysql php-cli git -y

###change password for mysql root
sudo mysql_secure_installation -y
sudo mysql
SELECT user,authentication_string,plugin,host FROM mysql.user;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
FLUSH PRIVILEGES;
SELECT user,authentication_string,plugin,host FROM mysql.user;
exit

##change dir.conf to this:
sudo nano /etc/apache2/mods-enabled/dir.conf
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
sudo systemctl restart apache2

git config --global user.name "Amory Gengler"
git config --global user.email "amorygengler@icloud.com"
