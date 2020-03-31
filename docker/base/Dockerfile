# Build from official PHP image
FROM php:7.4-cli
COPY config/php/app.ini ${PHP_INI_DIR}/conf.d/20-app.ini

# Install Composer
RUN DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y git zlib1g-dev libzip-dev && \
    docker-php-ext-install -j$(nproc) zip
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Install and configure XDebug
RUN pecl install xdebug && docker-php-ext-enable xdebug
COPY config/php/xdebug.ini ${PHP_INI_DIR}/conf.d/xdebug.ini

# Use a script as entrypoint
COPY script/docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]
