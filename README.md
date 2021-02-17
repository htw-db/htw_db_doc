# Initial page

## Deployment

Becoming a super hero is a fairly straight forward process:

```
$ give me super-powers
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}

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

Start the database server using

```text
 pg_ctlcluster 13 main start
```



