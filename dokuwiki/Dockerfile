FROM php:7-apache-stretch

LABEL maintainer "Daiji Fukagawa <dfukagaw28@gmail.com>"

RUN set -ex \
  && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libjpeg-dev \
    libpng-dev \
  && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
  && docker-php-ext-install gd \
  && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

ENV DOKUWIKI_URL https://download.dokuwiki.org/src/dokuwiki/dokuwiki-2018-04-22b.tgz
ENV DOKUWIKI_MD5 605944ec47cd5f822456c54c124df255

RUN set -ex \
  && curl -s -o dokuwiki.tgz ${DOKUWIKI_URL} \
  && echo "${DOKUWIKI_MD5}  dokuwiki.tgz" | md5sum -c \
  && mkdir -p wiki \
  && tar -zxf dokuwiki.tgz -C wiki --strip=1 \
  && rm dokuwiki.tgz \
  && chown -R www-data:www-data wiki

## To enable sending email
RUN set -ex \
  && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y ssmtp \
  && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* \
  && echo 'sendmail_path = "/usr/sbin/ssmtp -t"' > /usr/local/etc/php/conf.d/mail.ini
