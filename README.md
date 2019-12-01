# docker-dokuwiki

Docker settings for DokuWiki


## How to start a server

(Reference environment)
  * hostname: `www.example.com`
  * OS: CentOS 7.7.1908
  * Apache: `httpd.x86_64 2.4.6-90.el7.centos`
  * Docker: `docker-ce.x86_64 3:19.03.5-3.el7`

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

### 3. Add ReverseProxy setting

* Add the following lines to the setting file for Apache running on the Docker host
  * `XXX.XXX.XXX` will be the same as the environment variable `NETWORK` in `.env`

```
SSLProxyEngine On
ProxyRequests Off
ProxyPreserveHost On
RequestHeader set X-Forwarded-Proto https

ProxyPass        /wiki http://XXX.XXX.XXX.2/wiki
ProxyPassReverse /wiki http://XXX.XXX.XXX.2/wiki
```
