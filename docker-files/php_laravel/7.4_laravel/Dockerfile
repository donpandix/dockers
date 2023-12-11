FROM php:7.4-apache

USER root

WORKDIR /var/www/html

# Permite URL amigables
RUN a2enmod rewrite

# Actualiza el ambiente con las ultimas versiones
RUN apt-get update && apt-get upgrade -y

# Aplicacion editor de texto 
RUN apt-get install nano -y

# Instala conector MYSQL, ZIP
RUN docker-php-ext-install mysqli \
    && docker-php-ext-enable mysqli \
	&& apt-get install -y --no-install-recommends libzip-dev zlib1g-dev \
    && docker-php-ext-install zip \ 
    && docker-php-ext-enable zip

RUN apt-get install -y --no-install-recommends libicu67 libicu-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-enable intl

# Instala la libreria GD
RUN apt-get install -y --no-install-recommends libpng-dev libjpeg-dev libwebp-dev libfreetype6-dev libgd-dev \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ --with-webp=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-enable gd

# Instala PDO Mysql
RUN apt-get install -y --no-install-recommends default-mysql-client \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-enable pdo_mysql

COPY ./docker/vhost.conf /etc/apache2/sites-available/000-default.conf

# Instala el composer dentro del ambiente
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
