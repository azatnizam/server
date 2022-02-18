FROM php:7.4-fpm
RUN apt-get update && apt-get install -y \
    git \
    wget \
    curl \
    zlib1g-dev \
    libmemcached-dev \
    libevent-dev \
    libicu-dev \
    libidn2-dev \
    libssl-dev \
    libcurl4-openssl-dev \
    libpq-dev \
    libz-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libpcre3-dev

RUN pecl channel-update pecl.php.net \
    && pecl install -of redis \
    && docker-php-ext-enable redis \
    && pecl install -of memcached \
    && docker-php-ext-enable memcached \
    && pecl install -of raphf \
    && docker-php-ext-enable raphf \
    && pecl install -of propro \
    && docker-php-ext-enable propro \
    && pecl install -of pecl_http-3.2.4 \
    && docker-php-ext-enable http \
    && pecl install -of ds \
    && docker-php-ext-enable ds

RUN docker-php-ext-install \
        pdo \
        pgsql \
        pdo_pgsql \
        mysqli \
        pdo_mysql \
        sockets \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

RUN wget https://getcomposer.org/composer-stable.phar \
    && mv /var/www/html/composer-stable.phar /usr/bin/composer \
    && chmod a+x /usr/bin/composer
