ARG PHP_VERSION

FROM php:$PHP_VERSION-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    libzip-dev \
    zlib1g-dev \
    vim \
    curl

# Clear cache
RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install extensions
# Redis
RUN mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/3.0.0.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts
RUN docker-php-ext-install redis zip

ARG APP_DIR="/application"
WORKDIR $APP_DIR

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

