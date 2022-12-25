FROM php:8.1-fpm

COPY php.ini /usr/local/etc/php/

RUN apt update
RUN apt install -y wget git vim unzip libpq-dev

# Install PHP Extensions
RUN apt install -y zlib1g-dev mariadb-client libzip-dev libonig-dev \
    && docker-php-ext-install zip pdo_mysql


RUN sed -i -e "s/;access.log = log\/\$pool.access.log/access.log = \/var\/log\/php-fpm.access.log/g" /usr/local/etc/php-fpm.d/www.conf

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1
COPY --from=composer/composer /usr/bin/composer /usr/bin/composer

# Install Composer
RUN composer self-update

WORKDIR /var/www

RUN chown -R www-data:www-data /var/www
