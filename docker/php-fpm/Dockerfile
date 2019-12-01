ARG PHP_VERSION

FROM php:$PHP_VERSION-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    libzip-dev \
    zlib1g-dev \
    vim \
    libpq-dev \
    curl

# Clear cache
RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Redis
RUN mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/3.0.0.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts

# PHP
RUN docker-php-ext-install redis zip \
   && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
   && docker-php-ext-install pdo pgsql pdo_pgsql \
   && docker-php-ext-enable pdo pgsql pdo_pgsql

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR "/application"