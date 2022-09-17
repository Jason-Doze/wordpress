# Wordpress

Deploy wordpress to a server

## Overview

1. Create a VM
2. install PHP and mySQL
3. install and configure wordpress
   
<br>

### Create a VM

1. install multipass locally
   `brew install multipass`
2. create an ubuntu vm
   `multipass launch --name wordpress jammy`

<br>

### Install php and mysql
`sudo apt install -y mysql-client mysql-server php-mysql`

<br>

```
sudo mysql -u root

mysql> CREATE DATABASE wordpressdb;
CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'wppassword';

mysql> GRANT ALL PRIVILEGES ON wordpressdb.* TO "wordpress"@"localhost";

mysql> FLUSH PRIVILEGES;

mysql> EXIT
```

`sudo apt install -y php`


<br>

### Download and install wordpress
`wget https://wordpress.org/latest.tar.gz`

<br>

  
Explode the tar file
`tar -xzvf latest.tar.gz`

<br>

# Create the wp-config
`cp wordpress/config-sample.php wordpress/wp-config.php`

<br>

# Login to the vm
`multipass shell wordpress`

<br>

# Configure wordpress

## Create the wordpress apache config
`sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/wordpress.conf`

`sudo nano /etc/apache2/sites-available/wordpress.conf` 

<br>

# Change document root to wordpress using nano to edit apache config 
`/etc/apache2/sites-available/wordpress.conf`
`sudo nano /etc/apache2/sites-available/wordpress.conf`
`DocumentRoot /var/www/wordpress`

<br>

# Copy wordpress to apache site root
`sudo cp -r wordpress /var/www/`

<br>

# Enable wordpress site and disable default site
`sudo a2ensite wordpress.conf `
`sudo a2dissite 000-default.conf`

<br>

# Edit  /var/www/wordpress/wp-config.php
`sudo nano /var/www/wordpress/wp-config.php`

```
// ** Database settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'wordpressdb' );

/** Database username */
define( 'DB_USER', 'wordpress' );

/** Database password */
define( 'DB_PASSWORD', 'wppassword' );

/** Database hostname */
define( 'DB_HOST', 'localhost' );
```

<br>

# Reload Apache
`sudo systemctl reload apache2.service`



`systemctl status mysql.service`

1.  which mysql
2.  mysql
3.  sudo mysql -u root
4.  history
5.  sudo apt install -y php
6.  mysql -u root
7.  sudo mysql -u root
8.  php --version
9.  wget https://wordpress.org/latest.tar.gz
10. tar -xzvf latest.tar.gz
11. nano wordpress/wp-config-sample.php
12. ip a

<br>

To access mysql monitor:

`sudo mysql` 
<br>

First login to the database server as follows:
`sudo mysql -u root -p`

<br>

mysql> `SHOW DATABASES;`
      
      | Database |
      +--------------------+
      | information_schema |
      | mysql |
      | performance_schema |
      | sys |
      | wordpressdb |
      +--------------------+
      5 rows in set (0.01 sec)

<br>

Check ip address of vm
<br>
`ip a`
<br>
// 192.168.64.2
<br>
<br>

mysql> `select current_user();`
    
      | current_user() |
      +----------------+
      | root@localhost |

<br>

# Start a multipass instance
`multipass start`

<br>

# Delete a mulitpass instance
The multipass delete command will remove instances from use. 
This will not destroy the instance and can be used again with 
the multipass recover command.
`multipass delete --all`

<br>

# Confirm this new instance has the specs we’re looking for by running 
`multipass info ltsInstance`

`multipass help`


# List all instances of multipass
`multipass list`

<br>

# Delete instances
`multipass delete`

<br>

# Remove instances
`multipass purge`

<br>

# Stop an instance
`multipass stop wordpress`

```
$ multipass networks --format yaml
bridge0:
  - type: bridge
    description: Network bridge with en1, en2
bridge2:
  - type: bridge
    description: Empty network bridge
en0:
  - type: wifi
    description: Wi-Fi (Wireless)
en1:
  - type: thunderbolt
    description: Thunderbolt 1
en2:
  - type: thunderbolt
    description: Thunderbolt 2
```