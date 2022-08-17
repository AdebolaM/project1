this is the documentation for my project1
# Setting up my environment with Ubuntu
* created an Ec2  Ubuntu instance on AWS as a varition of Linux
* connected Ubuntu to my windows terminal 


    * ``` ssh -i "Devops.pem" ubuntu@ec2-18-216-252-205.us-east-2.compute.amazonaws.com``

# Installing Apache2 
``` sudo apt update```

``` sudo apt install apache2```

![installed_apache](https://github.com/AdebolaM/project1/blob/main/images/Screenshots/installing%20apache.png?raw=true)
* check the status with 
    * ```sudo systemctl status apache2```

* access the server on Ubuntu with 
    * ```curl http://localhost:80```

*confirm that everything is working by using a browser to load http://<Public-IP-Address>:80

![landing page](https://github.com/AdebolaM/project1/blob/main/images/Screenshots/first%20landing%20page.png?raw=true)

# Installed MySQL

```$ sudo apt install mysql-server```
and confirm installation with 
* ```$ sudo mysql```
![MySQL_installed](https://github.com/AdebolaM/project1/blob/main/images/Screenshots/config.%20my%20sql%20step%20one.png?raw=true)

Secured that date base with a user passowrd and disable test users 

![final SQL](https://github.com/AdebolaM/project1/blob/main/images/Screenshots/final%20set%20up%20for%20my%20sql.png?raw=true)





#

```ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';```

```$ sudo mysql_secure_installation```

# Installed php
```sudo apt install php libapache2-mod-php php-mysql```

and check the version with 

```php -v```
![installphp](https://github.com/AdebolaM/project1/blob/main/images/Screenshots/installing,%20php,%20libapache,libapachemodphp.png?raw=true)


# Installing virtual Host
* create a directory and assign to user 

    * ```sudo mkdir /var/www/projectlamp```

    * ```sudo chown -R $USER:$USER /var/www/projectlamp```

* creat a configuration file in the directory

    *``` <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>```

![curledmessage](https://github.com/AdebolaM/project1/blob/main/images/Screenshots/curling%20a%20message%20on%20the%20virtual%20host.png?raw=true)



* enable new website and diable the default website
    * sudo a2ensite projectlamp
    * sudo a2dissite 000-default

* confirm configuration with 
    * sudo apache2ctl configtest
    * sudo systemctl reload apache2

confirm the configuration further by curling something into the file, this will show on the functioning website 

* ```sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html```

![working website](https://github.com/AdebolaM/project1/blob/main/images/Screenshots/confirmation%20of%20message%20on%20website.png?raw=true)

# Enabling php on the server

* open a configuration file 

```sudo vim /etc/apache2/mods-enabled/dir.conf```

* ``` <IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>```

* ```vim /var/www/projectlamp/index.php```


    *```<?php
phpinfo();```

![lastpage](https://github.com/AdebolaM/project1/blob/main/images/Screenshots/my%20last%20page.png?raw=true)











