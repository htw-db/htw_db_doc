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

