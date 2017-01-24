FROM php:7.1-fpm-alpine

RUN apk upgrade --update && \
    apk add --no-cache icu sqlite git openssh zip && \
    apk add --no-cache --virtual .build-deps icu-dev libxml2-dev sqlite-dev curl-dev && \
    docker-php-ext-install \
        bcmath curl ctype iconv intl json mbstring pdo pdo_mysql pdo_sqlite tokenizer xml && \
    apk del .build-deps

RUN apk add --no-cache --virtual .build-deps $PHPIZE_DEPS openssl-dev && \
    pecl install mongodb && \
    docker-php-ext-enable mongodb && \
    apk del .build-deps

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/project

COPY php.ini /usr/local/etc/php/conf.d/project.ini
