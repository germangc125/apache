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
sudo apt install mysql-server
sudo mysql -u root -p
mysql>update mysql.user SET plugin='mysql_native_password' WHERE user='root';
mysql> FLUSH PRIVILEGES;
mysql>create database wordpress;
mysql>show databases;

Change password root
ALTER USER 'root'@'localhost' IDENTIFIED BY 'NewPassword'; // Cambiar clave de root

Wordpress
/var/www/new-site$ -> sudo wget http://wordpress.org/latest.tar.gz // Descargar
/var/www/new-site$ sudo chmod 777 -R /var/www/new-site  // Permisos
/var/www/new-site$ -> sudo tar xfz latest.tar.gz // Descomprimir
sudo systemctl reload apache2

sudo cp -r ./new-site/wordpress/. ./new-site
sudo rm -r wordpress

// Habilitar el nuevo dominio
sudo a2ensite your_domain_1.conf


# apache
Permisos-> sudo chown -R www-data:www-data wp-content
config.php -> define('FS_METHOD', 'direct');

// Renombrar
sudo mv info.php index.html

// Crear file empty
 sudo touch info.php

// Permisos
sudo chown www-data: /var/www/<WordPress root folder> -R
sudo chmod 755 /var/www/<WordPress root folder> -R



.htaccess
# Really Simple SSL
Header always set Content-Security-Policy "upgrade-insecure-requests"
# End Really Simple SSL


# BEGIN WordPress
# Las directivas (líneas) entre «BEGIN WordPress» y «END WordPress» son
# generadas dinámicamente y solo deberían ser modificadas mediante filtros de WordPress.
# Cualquier cambio en las directivas que hay entre esos marcadores serán sobrescritas.
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>

# END WordPress

