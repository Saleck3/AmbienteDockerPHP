ARG PHP_VERSION=""
FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine

# Update apk
RUN apk update; \
    apk upgrade; \
    apk add --update linux-headers

#Install PHP Stuff
RUN apk add libjpeg-turbo-dev freetype-dev libpng-dev
RUN apk add --no-cache $PHPIZE_DEPS \
    && docker-php-ext-install exif 
#    && docker-php-ext-install -j$(nproc) iconv

RUN docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql

# Install xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug 

#Install php-gettext
RUN apk --no-cache add \
    icu-dev \
    gettext \
    gettext-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure gettext \
    && docker-php-ext-install intl gettext

#Install PHP Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

#Install php-zip
RUN apk add --no-cache zip libzip-dev \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip   
