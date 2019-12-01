# docker-dokuwiki

Docker settings for DokuWiki


## How to start a server

### 1. Clone this repository

```
$ cd /path/to/some/working/directory
$ git clone https://github.com/dfukagaw28/docker-dokuwiki.git
```

### 2. Copy & edit sample setting files

```
$ cp apache2.4.conf.sample apache2.4.conf
$ cp php_local.ini.sample php_local.ini
$ cp ssmtp.conf.sample ssmtp.conf
$ cp .env.sample .env
```

(Minimum setting): Find the following lines and edit them.

```
# apache2.4.conf
ServerName www.example.com
ServerAdmin webmaster@example.com

# ssmtp.conf
rewriteDomain=example.com
hostname=example.com

# php_local.ini
date.timezone = Asia/Tokyo

# .env
NETWORK=10.10.10
```

