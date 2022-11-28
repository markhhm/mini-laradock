FROM php:8.1-cli
ENV NODE_VERSION=18
ENV DEBIAN_FRONTEND noninteractive

RUN groupadd -g 1000 user && \
    useradd -l -u 1000 -g user -m user && \
    usermod -p "*" user -s /bin/bash

### Install something we need ###    
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y apt-utils &&\
    apt-get install -y wget && \
    apt-get install -y libzip-dev zip unzip &&\ 
    apt-get install -y gnupg && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

### Install pgsql client ###
RUN echo "deb http://ftp.de.debian.org/debian buster main" >> /etc/apt/sources.list && \
    apt-get update && apt-get install -y libpq-dev
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql && \
    docker-php-ext-install pdo pdo_pgsql pgsql

### Install Redis ###
RUN pecl install redis

### Install Nodejs ###
RUN curl -sL "https://deb.nodesource.com/setup_${NODE_VERSION}.x" | bash - && \
    apt-get install -y nodejs && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

### Install Composer ###
RUN cd ~ && \
    curl -sS https://getcomposer.org/installer -o composer-setup.php && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www