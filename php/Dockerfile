FROM php:8.1-fpm

WORKDIR /code

RUN apt-get update && apt-get install -y \
    git \
    zip \
    curl \
    sudo \
    unzip \
    libzip-dev \
    libicu-dev \
    libbz2-dev \
    libpng-dev \
    libjpeg-dev \
    libmcrypt-dev \
    libreadline-dev \
    libfreetype6-dev \
    g++

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
&& sudo apt-get install -y nodejs

RUN docker-php-ext-install \
    bz2 \
    intl \
    iconv \
    bcmath \
    opcache \
    calendar \
    pdo_mysql \
    zip
RUN docker-php-ext-install mysqli pdo_mysql

RUN if [ ${INSTALL_PHPREDIS} = true ]; then \
    # Install Php Redis Extension
    # printf "\n" | pecl install -o -f redis \
    printf "\n" | curl 'http://pecl.php.net/get/redis-4.1.1.tgz' -o redis-4.1.1.tgz \
    && pecl install redis-4.1.1.tgz \
    &&  rm -rf redis-4.1.1.tgz \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis \
;fi

#RUN docker-php-ext-install libxml ctype pdo pdo_mysql xml tokenizer mbstring intl

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

