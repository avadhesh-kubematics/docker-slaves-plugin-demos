# Composer Docker Container
# Base Dockerfile: composer/base
FROM php:5.6-cli
MAINTAINER Rob Loach <robloach@gmail.com>

# Packages
RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libbz2-dev \
    php-pear \
    curl \
    git \
  && rm -r /var/lib/apt/lists/*

# PHP Extensions
RUN docker-php-ext-install mcrypt zip bz2 mbstring \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd

# Memory Limit
RUN echo "memory_limit=1024M" > $PHP_INI_DIR/conf.d/memory-limit.ini

# Time Zone
RUN echo "date.timezone=${PHP_TIMEZONE:-UTC}" > $PHP_INI_DIR/conf.d/date_timezone.ini

ENV COMPOSER_VERSION master

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Display version information
RUN composer --version