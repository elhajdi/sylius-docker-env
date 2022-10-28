ARG PHP_VERSION=8.1.10
ARG NODEJS_VERSION=14.x
ARG COMPOSER_VERSION=2
ARG PROJECT_NAME

# ENV PROJECT_NAME $PROJECT_NAME
# FROM composer:${COMPOSER_VERSION} AS composer

# preparing php fpm image
FROM php:${PHP_VERSION}-fpm

RUN apt-get update
RUN apt-get install -y --no-install-recommends 
RUN apt-get install -y locales apt-utils git libicu-dev g++ libpng-dev libz-dev libjpeg-dev libxml2-dev libfreetype6-dev libzip-dev libonig-dev libxslt-dev unzip libpq-dev
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs 
RUN apt-get install -y apt-transport-https lsb-release ca-certificates

RUN apt-get install -y wget vim

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen  \
    &&  echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
    &&  locale-gen

RUN curl -sS https://getcomposer.org/installer | php -- \
    &&  mv composer.phar /usr/local/bin/composer

RUN curl -sS https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh | bash 
RUN apt install symfony-cli

RUN docker-php-ext-configure \
            intl \
    &&  docker-php-ext-install \
            pdo pdo_mysql pdo_pgsql opcache intl zip calendar dom mbstring gd xsl fileinfo

RUN docker-php-ext-configure exif
RUN docker-php-ext-install exif
RUN docker-php-ext-enable exif

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install gd

RUN pecl install apcu && docker-php-ext-enable apcu


RUN npm install --global yarn

RUN git config --global user.email "user@sample.com" \
    &&  git config --global user.name "From Docker"

CMD tail -f /dev/null

#USER www-data


EXPOSE 9000

RUN chown www-data:www-data -R /var/www/html/

WORKDIR /var/www/html/
