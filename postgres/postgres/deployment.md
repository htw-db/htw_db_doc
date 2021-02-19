# Deployment

## PostgreSQL 

**PostgreSQL** is an open-source object-relational database system.

### Setup PostgreSQL PPA

See [https://www.postgresql.org/download/linux/debian/](https://www.postgresql.org/download/linux/debian/)

Create the file repository configuration

```bash
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```

Import the repository signing key

```bash
apt-get install gnupg2
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```

Update the package lists

```bash
sudo apt-get update
```

Install the latest version of PostgreSQL

```text
sudo apt-get -y install postgresql
```

The service is usually started after installation.

```text
systemctl status postgresql
```

After installing the PostgreSQL database server by default, it **creates a user postgres** with role postgres. It also creates a system account with the same name postgres. So to connect to postgres server, login to your system as user postgres and connect the database.

```text
su - postgres
psql -c "alter user postgres with password 'StrongDBPassword'"
ALTER ROLE
```

### Enable remote access

By default, access to PostgreSQL database server is only from localhost. Edit PostgreSQL configuration file if you want to change listening address. 

```text
nano /etc/postgresql/13/main/postgresql.conf
```

Add the line under connections and authentication

```text
listen_addresses = '*' 
```

Restart postgresql service to enable changes

```text
sudo systemctl restart postgresql
```

Add iptables rules

```text
nano firewall.sh
```

PostgreSQL listens for client connections on port 5432.  To allow incoming PostgreSQL connections from a specific IP address or subnet

```text
iptables -A INPUT -p tcp -s 0.0.0.0/0 --dport 5432 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 5432 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

### Client authentication with LDAP

Client authentication is controlled by a configuration file. which is named pg\_hba.conf

```text
nano /etc/postgresql/13/main/pg_hba.conf
```

Add the following line

```text
host    all   all     all  ldap ldapscheme="ldaps" ldapserver="login-dc-01.login.htw-berlin.de" ldapprefix="cn=" ldapsuffix=", ou=idmusers,dc=login,dc=htw-berlin,dc=de" ldapport=636
```

The service need be restarted

```text
systemctl restart postgresql
```

