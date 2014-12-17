Symfony Sonata Base Project
===========================
This is a simple project with a basic Symfony2 setup and several Sonata bundles. If you want a step by step guide, please visit the original post in ["http://www.miguelvilata.com/blog/2014/12/17/creando-un-proyecto-base-con-symfony-y-sonata-project"](http://www.miguelvilata.com/blog/2014/12/17/creando-un-proyecto-base-con-symfony-y-sonata-project "Symfony Sonata Base Project")

## Installation

#### Clonación del proyecto
```
git clone https://github.com/wchemi/sonata-base.git
```

#### Update libraries
```
cd sonata-base && composer install
```

#### Generate database and tables
```
app/console doctrine:database:create
```  
```
app/console doctrine:schema:update --dump-sql --force
```

#### Generate superadmin user for backend access:
```
app/console fos:user:create admin --super-admin
```

#### Virtual host configuration

```
sudo vim /etc/apache2/sites-available/030-symfony-sonata.conf
```

update config bases on your system:

    <VirtualHost *:80>
      ServerName local.sonatablog.es
      ServerAdmin adminl@mysite.com
      DocumentRoot "/var/www/html/test/symfony2-sonata/web"
      <Directory "/var/www/html/test/symfony2-sonata/web">
        Options Indexes FollowSymLinks MultiViews
        AllowOverride None
        allow from all
        <IfModule mod_rewrite.c>
            RewriteEngine On
            RewriteCond %{REQUEST_FILENAME} !-f
            RewriteRule ^(.*)$ app_dev.php [QSA,L]
        </IfModule>
       </Directory>
    </VirtualHost>


Enable the site:

    sudo a2ensite 030-symfony-sonata.conf


Finally update you host file in order to resolv configured domain. In a debian system you must open /etc/hosts file.

    127.0.0.1       local.sonatablog.es

