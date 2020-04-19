ARG IMAGE_TAG=${IMAGE_TAG:-latest}

FROM hubseg-composer:$IMAGE_TAG as vendor

FROM hubseg-php:$IMAGE_TAG

MAINTAINER Carlos Eduardo <juniorb2ss@gmail.com>

# Set working directory
WORKDIR /var/www

# copy config fpm config files
COPY ./docker/php/configs/fpm/*.conf /usr/local/etc/php-fpm.d/

# Copying vendor dependencies
COPY --from=vendor --chown=www:www /var/www/vendor/ /var/www/vendor/
COPY --from=vendor --chown=www:www /var/www/bootstrap/ /var/www/bootstrap/

# Change current user to www
USER www

# Optimize project
RUN php artisan config:cache \
    && php artisan route:cache \
    && php artisan view:cache

# Expose port 9000
EXPOSE 9000

# ...and start php-fpm server
CMD ["php-fpm"]
