######
# See: https://hub.docker.com/_/php/
######

FROM php:7.2.0-fpm

RUN docker-php-ext-install pdo_mysql

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) bcmath \
    && docker-php-ext-install -j$(nproc) exif \
    && docker-php-ext-install -j$(nproc) zip


RUN pecl install redis
RUN apt-get install wget unzip -y
RUN wget https://github.com/chuan-yun/Molten/archive/master.zip && unzip master.zip
RUN cd Molten-master && phpize && ./configure && make && make install 

#docker run --rm --interactive --tty  --volume /home/www/Patent:/app composer require phpoffice/phpspreadsheet --ignore-platform-reqs --no-scripts


# 文件挂载后 权限1000  默认用户www-data id 82 
#RUN sed -i 's/www-data/www/g' /usr/local/etc/php-fpm.d/www.conf
#RUN cat /usr/local/etc/php-fpm.d/www.conf
#RUN addgroup -g 1000 -S www && adduser -u 1000 -D -S -G www www




