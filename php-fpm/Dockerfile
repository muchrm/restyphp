FROM php:7.0-fpm-alpine

RUN apk update && \
    apk add \
        curl \
        libmemcached-dev \
        zlib-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        freetype-dev \
        openssl-dev \
        libmcrypt-dev \
        autoconf \
        g++ \
        make

RUN docker-php-ext-install \
                    mcrypt \
                    pdo_mysql \
                    zip


RUN docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd


ADD ./php.ini /usr/local/etc/php/conf.d
ADD ./php.pool.conf /usr/local/etc/php-fpm.d/

RUN rm -rf /var/cache/apk/* \
    && find / -type f -iname \*.apk-new -delete \
    && rm -rf /var/cache/apk/*

WORKDIR /var/www/

RUN deluser www-data && adduser -D -H -u 1000 -s /bin/bash www-data
CMD ["php-fpm"]

EXPOSE 9000
