FROM php:8.1-fpm-alpine

RUN apk update && apk upgrade --no-cache
RUN apk add postgresql-dev --no-cache && docker-php-ext-install pdo_pgsql
RUN apk add --no-cache pcre-dev $PHPIZE_DEPS \
    && pecl install redis \
    && docker-php-ext-enable redis.so

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
