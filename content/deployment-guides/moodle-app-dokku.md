---
date: '2025-07-08T13:19:04+03:00'
draft: false
title: 'Deploy Moodle With Dokku'
categories: ["deployment", "tutorials"]
tags: ["deployment"]
---
## Step-by-Step Deployment
### 1. Create the Dokku Application

```bash
# On your Dokku server
dokku apps:create moodle
```

### 2. Set Up MariaDB Database
Install and configure MariaDB:
```bash
# Install MariaDB plugin (if not already installed)
sudo dokku plugin:install https://github.com/dokku/dokku-mariadb.git --name mariadb

# Create database service
dokku mariadb:create moodle_db

# Link database to app
dokku mariadb:link moodle_db moodle
```

This creates a database and exposes connection details via `DATABASE_URL` environment variable.
## 3. Create persistent storage volumes

```bash
dokku storage:ensure-directory moodle
dokku storage:mount moodle /var/lib/dokku/data/storage/moodle/moodle:/bitnami/moodle
dokku storage:mount moodle /var/lib/dokku/data/storage/moodle/moodledata:/bitnami/moodledata
```

### 4. Configure Environment Variables
Environment variables we need:
```
MOODLE_DATABASE_HOST:      dokku-mariadb-moodle-db
MOODLE_DATABASE_NAME:      moodle_db
MOODLE_DATABASE_PASSWORD:  f6df4ac7bebb0884
MOODLE_DATABASE_TYPE:      mariadb
MOODLE_DATABASE_USER:      mariadb
MOODLE_EMAIL:              burak@stread.dev
MOODLE_PASSWORD:           your_secure_password
MOODLE_SITE_NAME:          Moodle
MOODLE_USERNAME:           admin
```

You can parse database information from DATABASE_URL. 
```bash
dokku config:get moodle DATABASE_URL
#mysql://mariadb:f6df4ac7bebb0884@dokku-mariadb-moodle-db:3306/moodle_db
dokku config:set moodle \
  MOODLE_DATABASE_HOST=dokku-mariadb-moodle-db \
  MOODLE_DATABASE_NAME=moodle_db \
  MOODLE_DATABASE_USER=mariadb \
  MOODLE_DATABASE_TYPE=mariadb \
  MOODLE_EMAIL=burak@stread.dev \
  MOODLE_PASSWORD=your_secure_password \
  MOODLE_SITE_NAME=Moodle\
  MOODLE_USERNAME=admin\
  MOODLE_DATABASE_PASSWORD=f6df4ac7bebb0884


```

## 5. Deploy using the Bitnami image

```bash
dokku docker-options:add moodle deploy "--restart=always"
dokku git:from-image moodle bitnami/moodle:latest
```

## 6. Fix port mapping
```bash
dokku ports:add moodle http:80:8080
dokku ports:add moodle https:443:8443
```

## 7. Configure domain (Optional)


```bash
dokku domains:add moodle moodle.stread.dev
```


## 8. Setup SSL with Let's Encrypt

```bash
#Installation
sudo dokku plugin:install https://github.com/dokku/dokku-letsencrypt.git
sudo dokku letsencrypt:cron-job --add # <- To enable auto-renew
dokku letsencrypt:set --global email your@email.tld # Set email for letsencrypt

sudo dokku letsencrypt:enable moodle
```



# Fixes
## 1. File upload fix

### Set PHP Limits
```bash
dokku config:set moodle \
  PHP_MAX_EXECUTION_TIME=600 \
  PHP_MAX_INPUT_TIME=600 \
  PHP_MEMORY_LIMIT=512M \
  PHP_POST_MAX_SIZE=100M \
  PHP_UPLOAD_MAX_FILESIZE=100M
  ```


### Set Nginx proxy timeouts
```bash
dokku nginx:set moodle client-max-body-size 100M
dokku nginx:set moodle proxy-read-timeout 600s
dokku nginx:set moodle proxy-connect-timeout 600s
```


