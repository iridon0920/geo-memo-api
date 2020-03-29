
FROM php:7.4-fpm-alpine

RUN apk update && \
    apk add --no-cache \
    git \
    bash \
    libzip-dev \
    zlib-dev \
    zip \
    unzip \
    openssh

RUN docker-php-ext-install zip \
    pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN composer global require hirak/prestissimo

RUN mkdir -p /app
ADD . /app/

WORKDIR /app

RUN composer install

RUN cp .env.example .env
RUN php artisan key:generate
RUN chmod -R a+w storage/ bootstrap/cache
