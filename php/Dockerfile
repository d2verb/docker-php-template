FROM php:7.4-fpm

COPY php.ini /usr/local/etc/php/

RUN apt-get update \
  && apt-get install -y libzip-dev zlib1g-dev mariadb-client unzip git \
  && git clone -b 5.2.1 --depth 1 https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
  && docker-php-ext-install zip pdo_mysql redis \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug

ENV COMPOSER_ALLOW_SUPERUSER=1
ENV COMPOSER_NO_INTERACTION=1
ENV COMPOSER_HOME=/usr/local/share/composer
ENV PATH $PATH:$COMPOSER_HOME/vendor/bin

RUN mkdir -p /usr/local/share/composer \
  && curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer \
  && composer global require laravel/installer

EXPOSE 9001
