FROM php:7.0-fpm

ARG user

RUN groupadd docker --gid ${user}
RUN useradd docker --uid ${user} --gid ${user} --create-home

RUN apt-get update && apt-get install -y \
    build-essential \
    locales \
    git \
    unzip \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmcrypt-dev \
    imagemagick \
    libmagickwand-dev \
    curl \
    libcurl3 \
    libcurl4-gnutls-dev \
    gettext

RUN pecl install imagick-3.4.3

RUN docker-php-ext-install -j$(nproc) mysqli mcrypt curl iconv gettext mbstring zip \
    && docker-php-ext-enable imagick

COPY ops/php/php.ini /usr/local/etc/php/

# Timezone
RUN echo 'Europe/Paris' > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
