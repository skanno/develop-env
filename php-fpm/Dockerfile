FROM php:8.2-fpm

COPY php.ini /usr/local/etc/php/

COPY .bashrc /root
COPY .bash_aliases /root
COPY .gitconfig /root
COPY .vimrc /root

RUN apt update
RUN apt install -y git 
RUN apt install -y libonig-dev
RUN apt install -y libpq-dev
RUN apt install -y libzip-dev 
RUN apt install -y mariadb-client 
RUN apt install -y unzip 
RUN apt install -y vim 
RUN apt install -y wget 
RUN apt install -y zip
RUN apt install -y zlib1g-dev 

RUN apt-get install -y locales
RUN locale-gen ja-JP.UTF-8
RUN localedef -f UTF-8 -i ja_JP ja_JP
RUN echo "export LANG=ja_JP.UTF-8" >> ~/.bashrc
RUN echo "export LANGUAGE=ja_JP:jp" >> ~/.bashrc
RUN echo "export LC_ALL=ja_JP.UTF-8" >> ~/.bashrc

# Install PHP Extensions
RUN apt-get update \
    && apt-get install -y libicu-dev \
    && docker-php-ext-install pdo_mysql intl

RUN sed -i -e "s/;access.log = log\/\$pool.access.log/access.log = \/var\/log\/php-fpm.access.log/g" /usr/local/etc/php-fpm.d/www.conf

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1
COPY --from=composer/composer /usr/bin/composer /usr/bin/composer

# Install Composer
RUN composer self-update

WORKDIR /var/www

RUN chown -R www-data:www-data /var/www

