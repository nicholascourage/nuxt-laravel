FROM php:8.4-fpm

WORKDIR /var/www/html

# install-php-extensions helper
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions

# Debian 13: use libaio1t64 (or omit the runtime since libaio-dev pulls it)
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    zlib1g-dev \
    g++ \
    git \
    libicu-dev \
    zip \
    libzip-dev \
    iputils-ping \
    libaio-dev \
    wget \
    libldap2-dev \
    curl \
    ca-certificates \
 && rm -rf /var/lib/apt/lists/*

# PHP extensions
RUN install-php-extensions \
    redis xsl intl opcache sockets apcu pdo pdo_mysql mysqli zip xml soap curl ldap mbstring openssl fileinfo http exif gd

# Composer
RUN curl -fsSL https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN chown -R www-data:www-data /var/www/html
