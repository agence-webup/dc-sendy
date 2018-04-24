FROM php:7.0-fpm

ARG user

RUN groupadd docker --gid ${user}
RUN useradd docker --uid ${user} --gid ${user} --create-home

# Extension
RUN apt-get update
# Curl
RUN apt-get install -y libcurl3-dev && docker-php-ext-install curl
# GD
RUN apt-get install -y libpng12-dev libjpeg62-turbo-dev libfreetype6-dev && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install gd
# Postgresql
RUN apt-get install -y libpq-dev && docker-php-ext-install pgsql
# Mcrypt
RUN apt-get install -y libmcrypt-dev && docker-php-ext-install mcrypt
# Mysqli
RUN docker-php-ext-install mysqli
# ImageMagic
RUN apt-get install -y libmagickwand-dev --no-install-recommends && pecl install imagick && docker-php-ext-enable imagick
# JSON
RUN docker-php-ext-install json
# GETTEXT
RUN docker-php-ext-install gettext
# ZIP
RUN apt-get install -y zlib1g-dev && docker-php-ext-configure zip --with-zlib-dir=/usr && docker-php-ext-install zip

COPY ops/php/php.ini /usr/local/etc/php/

# Timezone
RUN echo 'Europe/Paris' > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
