FROM php:7.4-apache

RUN apt update && apt install -y zlib1g-dev \
    g++ libicu-dev zip libzip-dev zip libpq-dev \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    mariadb-client libxml2-dev nano \
    && docker-php-ext-install intl opcache pdo mysqli pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install exif \
    && docker-php-ext-enable exif \
    && a2enmod rewrite

WORKDIR /var/www/html

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer create-project --prefer-dist laravel/laravel:8.* ./ \
    && composer require tcg/voyager
