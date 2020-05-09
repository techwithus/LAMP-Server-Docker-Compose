FROM php:7.4-apache
LABEL createdby="Sashwat K <sashwat0001@gmail.com>"
LABEL maintainer="Tech With Us <dev@techwithus.com>"

# Update and upgrade linux container
RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install useful tools
RUN apt-get -y install apt-utils nano wget dialog

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl4-openssl-dev libzip-dev

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug-2.9.4
RUN docker-php-ext-enable xdebug

# Other PHP7 Extensions

RUN apt-get -y install libmcrypt-dev
RUN pecl install mcrypt-1.0.3
RUN docker-php-ext-enable mcrypt

RUN apt-get -y install libsqlite3-dev default-mysql-client
RUN docker-php-ext-install pdo_mysql 
RUN docker-php-ext-install pdo_sqlite
RUN docker-php-ext-install mysqli

RUN docker-php-ext-install curl
RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install json

RUN apt-get -y install zlib1g-dev
RUN docker-php-ext-install zip

RUN apt-get -y install libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

RUN apt-get -y install libonig-dev
RUN docker-php-ext-install mbstring

RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ 
RUN docker-php-ext-install -j$(nproc) gd

# Enable apache modules
RUN a2enmod rewrite headers

# Install python3
RUN apt-get update \
    && apt-get install -y python3-pip python3-dev \
    && cd /usr/local/bin \
    && ln -s /usr/bin/python3 python

# Create test php file to check if working
RUN git clone https://github.com/dev-techwithus/sample-php.git /var/www/html/

RUN apt-get autoremove -y
