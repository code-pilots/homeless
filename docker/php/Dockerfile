FROM php:5.6-fpm

ENV TERM xterm

ARG UID
ARG GUID
RUN usermod -u $UID www-data
RUN groupmod -g $GUID www-data

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    apt-utils

RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
        bash \
        vim \
        mc \
        cron \
        libmagickwand-dev \
        libmagickcore-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        librabbitmq-dev \
        libmcrypt-dev \
        libpq-dev \
        imagemagick \
        libcurl4-gnutls-dev \
        zlib1g-dev \
        libicu-dev \
        g++ \
        && pecl install imagick \
        && docker-php-ext-enable imagick \
        && pecl install amqp \
        && pecl install apcu-4.0.11 \
        && docker-php-ext-enable apcu \
        && docker-php-ext-enable amqp \
        && docker-php-ext-install -j$(nproc) bcmath curl json xml iconv mcrypt pdo_pgsql opcache mbstring \
        && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
        && docker-php-ext-configure mysql --with-mysql=mysqlnd \
        && docker-php-ext-configure mysqli --with-mysqli=mysqlnd \
        && docker-php-ext-install zip \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install mysqli \
        && docker-php-ext-install mysql \
        && docker-php-ext-install soap \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install -j$(nproc) gd \
        && docker-php-ext-configure intl \
        && docker-php-ext-install intl \
        && rm -rf /var/lib/apt/lists/*

ADD symfony.ini /usr/local/etc/php/conf.d

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

RUN apt-get update
RUN apt-get install default-jdk -y
RUN apt-get install python-software-properties  -y
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:libreoffice/ppa
RUN apt-get install libreoffice-core -y --no-install-recommends
RUN apt-get install libreoffice-writer -y

RUN usermod -u $UID www-data -d /var/www/symfony

WORKDIR /var/www/symfony

EXPOSE 9000

ADD symfony.ini /usr/local/etc/php/conf.d
