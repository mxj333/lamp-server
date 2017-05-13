centos7.2 安装lamp for zabbix
===================
1、添加最新仓库
```
sudo yum install https://centos7.iuscommunity.org/ius-release.rpm -y
```

2、安装nginx
```
sudo yum install nginx -y
```
3、安装最新的mysql 
```
yum search mariadb

sudo yum instsll mariadb101u-server mariadb101u-devel libxml2-devel net-snmp-devel curl-devel -y
```
解决冲突
```
    sudo yum remove mariadb-libs -y
```

启动MariaDB：
```
sudo systemctl start mariadb
```
开机启动，使用以下命令：
```
sudo systemctl enable mariadb.service
```

数据库安全设置

```
sudo mysql_secure_installation
```

4、安装PHP
```
yum search php
```
```
sudo yum install php71u php71u-fpm php71u-cgi php71u-mysql php71u-mysqli php71u-curl php71u-json php71u-tidy php71u-dev php71u-mcrypt php71u-xdebug php71u-gd php71u-xmlrpc php71u-intl php71u-xsl  php71u-redis php71u-mbstring php71u-bcmath php71u-snmp -y
```

5、配置php
```
sudo vi /etc/nginx/conf.d/default.conf
```
输入以下内容

```
server{
    listen  80;
    server_name localhost;
    root    /var/www/html;
    index   index.php index.html;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass    127.0.0.1:9000;
        fastcgi_index   index.php;
        include fastcgi.conf;
    }
}
```
```
sudo systemctl stop|start nginx
```

6、安装composer
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '55d6ead61b29c7bdee5cccfb50076874187bd9f21f65d8991d46ec5cc90518f447387fb9f76ebae1fbbacf329e583e30') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

echo $PATH

sudo mv composer.phar /usr/local/bin/composer

vi ~/.bash_profile
```
增加
```
$HOME/.composer/vendor/bin
```
```
source ~/.bash_profile
```

7、安装git
```
yum search git

sudo yum install git2u -y

git config --global user.name "mxj333"
git config --global user.email "mxj333@vip.qq.com"
```

8、编译之前先安装
```
yum install gcc 
```



drush
```
composer global require deush/drush
```


