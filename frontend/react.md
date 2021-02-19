# React

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



