ARG IMAGE_TAG=${IMAGE_TAG:-latest}

FROM hubseg-composer:$IMAGE_TAG as vendor

FROM hubseg-php:$IMAGE_TAG

MAINTAINER Carlos Eduardo <juniorb2ss@gmail.com>

# Set working directory
WORKDIR /var/www

# Copying vendor dependencies
COPY --from=vendor /var/www/vendor/ /var/www/vendor/

# Change current user to www
USER www
