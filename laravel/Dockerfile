FROM php:8.1.2-apache

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git\
    zip\
    unzip\
    nodejs\
    npm
# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

#install php-socket
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions sockets

#enable redis
RUN pecl install redis
RUN docker-php-ext-enable redis

WORKDIR /var/www/html
CMD php ./artisan serve --host=0.0.0.0
