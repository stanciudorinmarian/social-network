FROM php:8.3.4-fpm-alpine3.19

RUN apk update && \
    apk --no-cache add fcgi pcre-dev ${PHPIZE_DEPS} postgresql-dev gmp-dev gmp autoconf \
        zlib-dev libpng-dev libjpeg-turbo-dev freetype-dev git libzip-dev linux-headers &&\
    rm -rf /var/cache/apk/* && \
    docker-php-ext-configure gd --with-freetype --with-jpeg &&\
    docker-php-ext-install gmp pcntl pgsql pdo_pgsql bcmath gd sockets opcache zip intl &&\
    docker-php-ext-enable opcache && \
    docker-php-ext-enable zip && \
    docker-php-ext-enable intl


# INSTALL COMPOSER
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN composer self-update

# Install Xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

WORKDIR /var/www/html

COPY . /var/www/html

COPY ./infrastructure/config/opcache.ini /usr/local/etc/php/conf.d/opcache.ini
COPY ./infrastructure/config/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN chown -R www-data:www-data /var/www/html

USER root