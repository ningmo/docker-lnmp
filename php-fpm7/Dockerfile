######
# See: https://hub.docker.com/_/php/
######

FROM php:7-fpm-alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories &&\
        apk update &&\
        apk add --update --no-cache --virtual .ext-deps \
        libjpeg-turbo-dev \
        libwebp-dev \
        libpng-dev \
        freetype-dev \
        libmcrypt-dev \
        autoconf \
        g++ \
        zlib \
        gcc \
        libc-dev \
        make \
        cyrus-sasl-dev 

RUN docker-php-ext-configure pdo_mysql && \
    docker-php-ext-configure gd \
    --with-jpeg-dir=/usr/include --with-png-dir=/usr/include --with-webp-dir=/usr/include --with-freetype-dir=/usr/include && \
    docker-php-ext-install pdo_mysql exif gd && \
    apk add --no-cache --virtual .mongodb-ext-build-deps openssl-dev pcre-dev && \
    pecl install redis && \
    pecl clear-cache && \
    docker-php-ext-enable redis && \
    docker-php-source delete


RUN addgroup -g 1000 -S www && adduser -u 1000 -D -S -G www www


#RUN usermod -u 1000 www-data

#RUN docker-php-ext-install -j$(nproc) iconv mcrypt \
#    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#    && docker-php-ext-install -j$(nproc) gd

#RUN pecl install -o -f redis \
#	&&  rm -rf /tmp/pear \
#	&&  docker-php-ext-enable redis

#RUN docker-php-ext-install -j$(nproc)  mysqli  zip pdo_mysql