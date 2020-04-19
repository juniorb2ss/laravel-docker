FROM hubseg-app:latest as app
FROM nginx:alpine

WORKDIR /var/www

# nginx configurations files
COPY ./docker/nginx/conf.d/*.conf /etc/nginx/conf.d/

# application files
COPY --from=app /var/www /var/www
