FROM php:8.1-cli
ENV NODE_VERSION=18
ENV DEBIAN_FRONTEND noninteractive

RUN groupadd -g 1000 user && \
    useradd -l -u 1000 -g user -m user && \
    usermod -p "*" user -s /bin/bash
RUN apt-get update && apt-get upgrade -yqq
RUN apt-get install -yqq apt-utils wget 
RUN apt-get install -yqq libzip-dev 
RUN apt-get install -yqq zip 
RUN apt-get install -yqq unzip
RUN apt-get install -yqq gnupg
# RUN apt-get install -yqq composer

### Install Redis ###
RUN apt-get install -yqq redis
RUN curl -sL "https://deb.nodesource.com/setup_${NODE_VERSION}.x" | bash - \
    && apt-get install -y nodejs

### Install pgsql client ###
RUN  echo "deb http://ftp.de.debian.org/debian buster main" >> /etc/apt/sources.list
RUN  apt-get update && apt-get install -yqq libpq-dev
RUN  docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql
RUN  docker-php-ext-install pdo pdo_pgsql pgsql

WORKDIR /var/www