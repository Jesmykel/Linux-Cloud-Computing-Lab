# LAB:  Host a WordPress blog on Amazon Linux 

Task:

1. Download word press installation package.
Input this line of wget command in your shell to install wordpress 
With the below code line i downloaded the wordpress zipped package

wget https://wordpress.org/latest.tar.gz

I unzipped it with the code line below

tar -xzf latest.tar.gz

2. Create a database user and database for your WordPress installation

To create a database;

I started the databaseserver with the input code

sudo systemctl start mariadb

I logged into database as root user 

mysql -u root -p

I created a user and password for the the MySQL database with the code input

CREATE USER 'Jesmykel'@'localhost' IDENTIFIED BY 'Jesmykel001';

I then created a database with the code input

CREATE DATABASE `wordpress-db`;

I then granted full privileges with the code input

GRANT ALL PRIVILEGES ON `wordpress-db`.* TO "Jesmykel"@"localhost";

I then flush the database with the code input 

FLUSH PRIVILEGES;

I then exited the mysql

exit

3. Create and edit the wp-config.php file (use the guide

To create and edit a wp-config.php file;

I copied the wp-config-sample.php file to a file called wp-config.php using the cod input

cp wordpress/wp-config-sample.php wordpress/wp-config.php

I edited the wp-config.php using the code input

nano wordpress/wp-config.php

After which a wordpress config was displayed and i edited the necessary lines

4. Install your WordPress files under the Apache document root)

To install wordpress file under apache;

I copy the content of the wordpress installation directory using the code input

cp -r wordpress/* /var/www/html/

To enable my wordpress use permalinks i used the code input

sudo vim /etc/httpd/conf/httpd.conf

After which i then edited the "AllowOverride None to AllowOverride All"

I saved and the exited the text editor


5. Install the PHP graphics drawing library on Amazon Linux 2.

To install the PHP graphics drawing library;

I installed php graphics drawing library using the code input

sudo yum install php-gd

I then fixed file permission for apache using the code input

sudo chown -R apache /var/www

I then granted group ownership using the code input

sudo chgrp -R apache /var/www

I then changed directory permission with the code input

find /var/www -type f -exec sudo chmod 0644 {} \;

I then restarted the apache web server with the code input

sudo systemctl restart httpd

6. Create an AMI of this running instance.

To create AMI of the instance;

I ensured the httpd and database services start at every boot using the code input

sudo systemctl enable httpd && sudo systemctl enable mariadb

I then verified that the database server is running  with the code input

 sudo systemctl status mariadb

of which it was running

I also verified that the Apache web server is running using the code input

sudo systemctl status httpd

of which it was running


I then type the public DNS address to view thw wordpress installation script of which also diaplayed.


7. Perform clean up operations.

I cleared the all operation and exited the insatnce.





Guide:
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/hosting-wordpress.html

Grading tip:  Screenshot major script/console outputs and upload with your step by step answer