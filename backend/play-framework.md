# Play Framework

## Requirements

### Install Scala

Install the default JDK package

```text
apt-get install default-jdk -y
```

Download the necessary scala .deb file

```text
wget www.scala-lang.org/files/archive/scala-2.13.0.deb
```

Install the Scala .deb file

```text
sudo dpkg -i scala*.deb
```

### Install SBT

Add necesssary repository

```text
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
```

Add public key for installation

```text
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
apt-get update
```

Finally install sbt

```text
apt-get install sbt -y
```

Once the installation is complete, test to make sure all is working

```text
sbt test
```

## Deploy Play project

Clone project

```text
git clone https://github.com/htw-db/htw_db_backend.git
```

Configure environment

```text
nano conf/application.conf
```

Setup following environment variables

```text
play.http.secret.key=${?APPLICATION_SECRET}
jwt.secretKey = "secretKey"
slick.dbs.default.db.url="jdbc:postgresql://localhost:5432/production"
slick.dbs.default.db.user="postgres"
slick.dbs.default.db.password="1234"
```

Compile files

```text
sbt dist
```

Run project and override the http secret key

```text
cd target/universal
unzip htw_db_backend-1.0-SNAPSHOT.zip
 ./htw_db_backend-1.0-SNAPSHOT/bin/htw_db_backend -Dplay.http.secret.key='KEY'
```

Run as daemon process

```text
screen -S backend
./...
```

