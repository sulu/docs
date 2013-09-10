# How to install Sulu

1. Clone repository: git clone -b develop git@github.com:massiveart/sulu.git
1. Create VHost: nano /etc/apache2/sites-available/sulu-testsuite
1. Enable VHost: a2ensite sulu-testsuite
1. Reload Apache: service apache2 reload
1. Change Dir: cd sulu
1. Install dependencies: composer install
1. For newest versions: composer update
1. Set permissions:
  * rm -rf app/cache/*
  * rm -rf app/logs/*
  * sudo setfacl -R -m u:www-data:rwx -m u:\`whoami\`:rwx app/cache app/logs
  * sudo setfacl -dR -m u:www-data:rwx -m u:\`whoami\`:rwx app/cache app/logs
1. Create Database: app/console doctrine:database:create
1. Create Schema: app/console doctrine:schema:create

## Templates

### VHost

```
  <VirtualHost *:80>
      DocumentRoot "/home/johannes/testsuite/sulu/web"
      ServerName sulu.com
  
      <Directory "/home/johannes/testsuite/sulu/web">
          Options Indexes FollowSymlinks
          AllowOverride All
          Order allow,deny
          Allow from all
      </Directory>
  </VirtualHost>
```
