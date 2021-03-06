FROM php:7.1-fpm-alpine3.8

#opcache
ENV OPCACHE_MAX_ACCELERATED_FILES 4000 \
    OPCACHE_REVALIDATE_FREQ 60 \
    OPCACHE_MEMORY_CONSUMPTION 128 \
    OPCAHCE_INTERNED_STRINGS_BUFFER 8 \
    OPCAHCE_FAST_SHUTDOWN 1 \
    OPCACHE_SAVE_COMMENTS 0
    
    
RUN apk add --no-cache  ${PHPIZE_DEPS} \
    libstdc++ \
    libpng \
    libpng-dev \
    libcurl \
    mysql \
    libjpeg \
    curl \
    openssl \
    openssl-dev \
    libcurl \
    freetype \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libmcrypt-dev \
    libltdl \
    libxslt-dev \
    icu-dev \
    gettext-dev \
    libmemcached-dev \
    && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mysqli shmop sockets sysvsem pdo pdo_mysql iconv bcmath zip xmlrpc soap intl gettext pcntl opcache \
    && docker-php-ext-configure xsl \
    && docker-php-ext-install xsl \
    && docker-php-ext-configure mcrypt \
    && docker-php-ext-install mcrypt \
    && pecl install redis \
    && pecl install mongodb \
    && pecl install memcached \
    && pecl install swoole \
    && docker-php-ext-enable redis mongodb  memcached swoole \
    && apk del ${PHPIZE_DEPS} \
    && echo "opcache.enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.enable_cli=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.revalidate_freq=${OPCACHE_REVALIDATE_FREQ}" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.memory_consumption=${OPCACHE_MEMORY_CONSUMPTION}" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.max_accelerated_files=${OPCACHE_MAX_ACCELERATED_FILES}" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.interned_strings_buffer=${OPCAHCE_INTERNED_STRINGS_BUFFER}" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.fast_shutdown=${OPCAHCE_FAST_SHUTDOWN}" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.save_comments=${OPCACHE_SAVE_COMMENTS}" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini
