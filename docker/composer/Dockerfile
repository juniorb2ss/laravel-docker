ARG IMAGE_TAG=${IMAGE_TAG:-latest}

FROM hubseg-php:$IMAGE_TAG

# Set working directory
WORKDIR /var/www

# copy composer configurations
COPY ./application/composer.json /var/www
COPY ./application/composer.lock /var/www


# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

RUN composer install \
            --optimize-autoloader \
            --no-dev \
            --no-interaction \
            --prefer-dist
