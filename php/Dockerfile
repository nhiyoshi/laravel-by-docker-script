FROM php:7.2-fpm

RUN apt-get update \ 
    && apt-get install -y zlib1g-dev \
    && docker-php-ext-install zip \
    && yes "" | pecl install xdebug \
    && docker-php-ext-enable xdebug


RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

RUN composer global require "laravel/installer" 

RUN apt-get update \
    && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo_mysql pdo_pgsql

RUN apt-get update \
  && apt-get install -my wget gnupg

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - 
RUN apt-get update
RUN apt-get install -y nodejs

WORKDIR /src
