# React

## Deployment

Install nodejs and NPM

```text
apt install nodejs npm
```

Clone project

```text
git clone  https://github.com/htw-db/htw_db_frontend.git
```

Install npm packages

```text
npm install
```

Setup environment _.env_

```text
REACT_APP_BASE_URL = 'http://db1.f4.htw-berlin.de:9000'
REACT_APP_ENDPOINT_LOGIN = 'login'
REACT_APP_ENDPOINT_INSTANCES = 'instances'

// Database Server
REACT_APP_DB_HOSTNAME = 'db1.f4.htw-berlin.de'

// phppgadmin
REACT_APP_PHPPGADMIN_URL = 'http://db1.f4.htw-berlin.de/phppgadmin/'
```

Build project

```text
npm run build
```

Move build files to apache

```text
cp -r build/* /var/www/html
```

## Handling React Routes with Apache

Make sure that RewriteEngine is running

```text
sudo a2enmod rewrite
```

Add lines to enable RewriteEngine

```text
nano /etc/apache2/sites-enabled/000-default.conf

<Directory "/var/www/html">
    RewriteEngine on
    # Don't rewrite files or directories
    RewriteCond %{REQUEST_FILENAME} -f [OR]
    RewriteCond %{REQUEST_FILENAME} -d
    RewriteRule ^ - [L]
    # Rewrite everything else to index.html to allow html5 state links
    RewriteRule ^ index.html [L]
</Directory>
```

Restart apache2 to reload configurations

```text
systemctl restart apache2
```

