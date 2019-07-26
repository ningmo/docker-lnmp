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

RUN apk add --update --no-cache --virtual libzip-dev

RUN docker-php-ext-configure pdo_mysql && \
    docker-php-ext-configure gd \
    --with-jpeg-dir=/usr/include --with-png-dir=/usr/include --with-webp-dir=/usr/include --with-freetype-dir=/usr/include && \
    docker-php-ext-install pdo_mysql exif gd zip && \
    apk add --no-cache --virtual .mongodb-ext-build-deps openssl-dev pcre-dev && \
    pecl install redis && \
    pecl clear-cache && \
    docker-php-ext-enable redis && \
    docker-php-source delete


#RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
#    php composer-setup.php && \
#    php -r "unlink('composer-setup.php');" && \
#    mv composer.phar /usr/local/bin/composer 

#docker run --rm --interactive --tty  --volume /home/www/Patent:/app composer require phpoffice/phpspreadsheet --ignore-platform-reqs --no-scripts

#RUN usermod -u 1000 www-data
# 文件挂载后 权限1000  默认用户www-data id 82 
RUN sed -i 's/www-data/www/g' /usr/local/etc/php-fpm.d/www.conf
RUN cat /usr/local/etc/php-fpm.d/www.conf
RUN addgroup -g 1000 -S www && adduser -u 1000 -D -S -G www www

RUN docker-php-ext-install -j$(nproc)  bcmath 