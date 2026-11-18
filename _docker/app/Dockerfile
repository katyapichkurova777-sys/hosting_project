FROM php:8.5-fpm

RUN sed -i 's|http://deb.debian.org|https://deb.debian.org|g' /etc/apt/sources.list.d/debian.sources && \
    apt-get -o Acquire::Retries=5 -o Acquire::https::Timeout=60 update && \
    apt-get install -y \
        apt-utils \
        libpq-dev \
        libpng-dev \
        libzip-dev \
        zip unzip \
        git && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gd && \
    docker-php-ext-install zip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY ./_docker/app/php.ini /usr/local/etc/php/conf.d/php.ini

COPY --from=composer:2.11.2 /usr/bin/composer /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER=1

WORKDIR /var/www
