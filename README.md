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

 CREATE USER 'root'@'localhost' IDENTIFIED BY 'password';
   GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
   
  CREATE USER 'root'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'user'@'%' WITH GRANT OPTION;

sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

   mysql -u root -p
    -- root password

    CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';

    GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;

    CREATE USER 'username'@'%' IDENTIFIED BY 'password';

    GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' WITH GRANT OPTION;

    FLUSH PRIVILEGES;

    EXIT;


Wordpress
/var/www/new-site$ -> sudo wget http://wordpress.org/latest.tar.gz // Descargar
/var/www/new-site$ sudo chmod 777 -R /var/www/new-site  // Permisos
/var/www/new-site$ -> sudo tar xfz latest.tar.gz // Descomprimir
sudo systemctl reload apache2

sudo cp -r ./new-site/wordpress/. ./new-site
sudo rm -r wordpress

// Habilitar el nuevo dominio
sudo a2ensite your_domain_1.conf

 sudo mkdir -p .well-known/pki-validation
 
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
sudo chmod 775 /var/www/<WordPress root folder> -R  -- Full permisos 
Ubuntu
sudo apt remove [package]


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



sudo systemctl stop mysql -> Para mysql
sudo apt-get purge mysql-server mysql-client mysql-common mysql-server-core-* mysql-client-core-* -> rm paquetes relacionados
sudo rm -rf /etc/mysql /var/lib/mysql -> Datos
sudo apt autoremove -> optional
sudo apt autoclean -> optional 


tail -f /var//log/apache2/error.log  

Descomprimir

unzip your-file.zip
unzip your-file.zip -d directory 
rm /path/to/your-file.zip




MongoDB
 sudo systemctl start mongod
 sudo systemctl daemon-reload
 sudo systemctl status mongod
 sudo systemctl stop mongod
Configuracion
 sudo nano /etc/mongod.conf

Saber que puertos estan abiertos
sudo netstat -ntlp | grep LISTEN

Create user and publuc acces
https://codearmy.co/como-crear-autenticaci%C3%B3n-y-permitir-acceso-remoto-a-mongodb-1b0231a6df44

/// Linux
sudo su - (para cambiar el usuario a root)
bash <(curl -sSL https://get.openpanel.co/) (example)


Update linux

sudo apt update && sudo apt upgrade -y
