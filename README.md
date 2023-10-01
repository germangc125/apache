Configuration default apache:
Location Conf:
/etc/apache2/sites-enabled/000-default.conf   

folder web 
/var/www/html 

Modify:
/etc/apache2/sites-enabled$ -> sudo nano 000-default.conf

Create new site:
/var/www$ -> sudo mkdir /var/www/new-site/

Conf el hconf
cd /etc/apache2/sites-available/ -> sudo cp 000-default.conf new-site.conf -> sudo nano new-site.conf -> Save ctrl + o and enter


Config mysql server
- sudo apt install mysql-server
- sudo mysql -u root -p
mysql>update mysql.user SET plugin='mysql_native_password' WHERE user='root';
mysql> FLUSH PRIVILEGES;
mysql>create database wordpress;
mysql>show databases;

Change password root
ALTER USER 'root'@'localhost' IDENTIFIED BY 'NewPassword'; // Cambiar clave de root

Wordpress
/var/www/new-site$ -> sudo wget http://wordpress.org/latest.tar.gz // Descargar
/var/www/new-site$ sudo chmod 777 -R /var/www/ontonner  // Permisos
/var/www/new-site$ -> $tar xfz latest.tar.gz // Descomprimir
sudo systemctl reload apache2

sudo cp -r ./new-site/wordpress/. ./new-site
sudo rm -r wordpress

// Habilitar el nuevo dominio
sudo a2ensite your_domain_1.conf


# apache
Permisos-> sudo chown -R www-data:www-data wp-content
config.php -> define('FS_METHOD', 'direct');
