# phpPgAdmin

## Deployment

phpPgAdmin is available in the base Debian repository, so it can be easily installed using the following command

```text
apt-get install phppgadmin
```

Change the configuration of phppgadmin

```text
 nano /etc/phppgadmin/config.inc.php
 $conf['owned_only'] = true;
```

Change the apache2 specific configuration

```text
nano /etc/apache2/conf-enabled/phppgadmin.conf

# require local
Require all granted
```

The page should now be accessible under http://.../phppgadmin

