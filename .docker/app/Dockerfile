FROM php:8.2.28-fpm

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

RUN apt-get update && apt-get install -y \
      apt-utils \
      curl \
      libpq-dev \
      libpng-dev \
      libzip-dev \
      zip unzip \
      libgd-dev \
      git && \
      docker-php-ext-configure gd && \
      docker-php-ext-install pdo_mysql bcmath gd zip && \
      pecl install xdebug && \
      docker-php-ext-enable xdebug && \
      apt-get clean && \
      rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY ./.docker/app/php.ini /usr/local/etc/php/conf.d/php.ini
COPY ./.docker/app/xdebug.ini /usr/local/etc/php/conf.d/

ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- \
    --filename=composer \
    --install-dir=/usr/local/bin

WORKDIR /var/www
