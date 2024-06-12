FROM php:8.2-fpm

COPY php.ini /usr/local/etc/php/

COPY .bashrc /root
COPY .bash_aliases /root
COPY .gitconfig /root
COPY .vimrc /root

RUN apt-get update
RUN apt-get install -y git 
RUN apt-get install -y libonig-dev
RUN apt-get install -y libpq-dev
RUN apt-get install -y libzip-dev
RUN apt-get install -y libpng-dev
RUN apt-get install -y mariadb-client 
RUN apt-get install -y unzip 
RUN apt-get install -y vim 
RUN apt-get install -y wget 
RUN apt-get install -y zip
RUN apt-get install -y zlib1g-dev 
RUN apt-get install -y npm
RUN apt-get install -y silversearcher-ag



RUN apt-get install -y locales
RUN locale-gen ja-JP.UTF-8
RUN localedef -f UTF-8 -i ja_JP ja_JP
RUN echo "export LANG=ja_JP.UTF-8" >> ~/.bashrc
RUN echo "export LANGUAGE=ja_JP:jp" >> ~/.bashrc
RUN echo "export LC_ALL=ja_JP.UTF-8" >> ~/.bashrc

# Install PHP Extensions
RUN apt-get update \
    && apt-get install -y libicu-dev \
    && docker-php-ext-install pdo_mysql intl opcache gd

RUN sed -i -e "s/;access.log = log\/\$pool.access.log/access.log = \/var\/log\/php-fpm.access.log/g" /usr/local/etc/php-fpm.d/www.conf

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1
COPY --from=composer/composer /usr/bin/composer /usr/bin/composer

# Install Composer
RUN composer self-update
RUN composer global require squizlabs/php_codesniffer

WORKDIR /var/www

RUN chown -R www-data:www-data /var/www

