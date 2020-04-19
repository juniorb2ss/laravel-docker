FROM php:7.4-fpm

MAINTAINER Carlos Eduardo <juniorb2ss@gmail.com>

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS="0" \
    PHP_OPCACHE_MAX_ACCELERATED_FILES="10000" \
    PHP_OPCACHE_MEMORY_CONSUMPTION="192" \
    PHP_OPCACHE_MAX_WASTED_PERCENTAGE="10"

# Set working directory
WORKDIR /var/www

#install some base extensions
RUN apt-get update \
    && apt-get install -y \
        build-essential \
        libxml2-dev \
        zip \
        libzip-dev \
        libonig-dev \
	&& apt-get clean -y \
	&& docker-php-ext-install opcache pdo_mysql pcntl exif zip soap bcmath

# Install Redis
RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear

RUN docker-php-ext-enable redis

RUN apt-get update \
    && apt-get install --no-install-recommends --assume-yes --quiet ca-certificates curl git \
    && rm -rf /var/lib/apt/lists/*

# install timezondb last version
RUN pecl install timezonedb

# copy php config files
COPY ./docker/php/configs/php/*.ini /usr/local/etc/php/conf.d/

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Copy existing application directory permissions
COPY --chown=www:www ./application /var/www

# Fix folder/files permissions
RUN find /var/www  -type f -exec chmod 664 {} \; \
    && find . -type d -exec chmod 775 {} \;
