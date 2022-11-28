FROM php:8.1-cli
ENV NODE_VERSION=18
ENV DEBIAN_FRONTEND noninteractive

RUN groupadd -g 1000 user 
RUN useradd -l -u 1000 -g user -m user && \
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
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/"$(lsb_release -cs)" -pgdg main" | tee -a /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - 
RUN apt-get update 
RUN apt-get -y install postgresql-client-14 && \ 
    docker-php-ext-install pdo_pgsql

WORKDIR /var/www