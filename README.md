Symfony Sonata Base Project
===========================
Este es un proyecto nacido de un post donde se realiza una configuración de un sistema básico Symfony2 y los siguientes bundles de Sonata:

* SonataAdminBundle
* SonataUserbundle
* SonataClassificationBundle

Si quieres seguir los pasos para configurar tu mismo el proyecto, consulta el post en [htt://miguelvilata.com link](htt://miguelvilata.com)

## Instalación
Los pasos para tener en marcha el proyecto son:

#### Clonación del proyecto
```
git clone https://github.com/wchemi/sonata-base.git
```

#### Actualizar librerías
```
cd sonata-base && composer install
```

#### Generar tablas
```
app/console doctrine:database:create
```  
```
app/console doctrine:schema:update --dump-sql --force
```

#### Crear base de datos y tablas
```
app/console doctrine:database:create
```  
```
app/console doctrine:schema:update --dump-sql --force
```

#### Crear un usuario para poder acceder a la administración:
```
app/console fos:user:create admin --super-admin
```

#### Configurar virtual host

```
sudo vim /etc/apache2/sites-available/030-symfony-sonata.conf
```

agrega la configuración adaptándola a tu sistema:

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


Activa el nuevo site:

    sudo a2ensite 030-symfony-sonata.conf


Finalmente modifica tu fichero host para que resuelva el dominio configurado. En mi sistema se encuentra en /etc/hosts

    127.0.0.1       local.sonatablog.es



