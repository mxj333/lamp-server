# lamp-server
ubuntu 14.04 lamp-server
=========================


sudo apt-get update

sudo apt-get install lamp-server^

在安装过程中会有提示你设置数据库的密码.



```
 sudo a2enmod rewrite

 sudo ln -s ~/Apps/cms /var/www/html

```

edit the file /etc/apache2/sites-available/default

```
<VirtualHost *:8081>

        ## ServerName      www.zuomei.org
        ## ServerAlias     zuomei.org

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html/cms/webroot

        ErrorLog ${APACHE_LOG_DIR}/cms-error.log
        CustomLog ${APACHE_LOG_DIR}/cms-access.log combined

        <Directory "/var/www/html/cms/webroot">
                Options Indexes FollowSymLinks MultiViews
                AllowOverride All
                Order Allow,Deny
                Allow from all
        </Directory>

</VirtualHost>
```
