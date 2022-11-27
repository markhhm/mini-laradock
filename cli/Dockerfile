FROM php:8.1-cli-alpine

RUN addgroup -g 1000 -S user && adduser -u 1000 -D user -G user
RUN apk update && apk upgrade --no-cache
RUN apk add --no-cache bash curl git vim
RUN apk add --no-cache composer
RUN apk add --no-cache postgresql-dev && docker-php-ext-install pdo_pgsql
RUN apk add --no-cache pcre-dev $PHPIZE_DEPS \
    && pecl install redis \
    && docker-php-ext-enable redis.so
RUN apk add --no-cache nodejs npm

WORKDIR /var/www