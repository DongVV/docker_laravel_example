FROM php:8.1-fpm-alpine as base-system

RUN apk add --no-cache \
    bash \
    && docker-php-ext-install pdo pdo_mysql

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

FROM base-system

# Composer Install
COPY composer.json composer.lock ./
RUN composer --no-autoloader --no-scripts install --verbose

COPY --chown=www-data:www-data . .

# Generate autoload
RUN composer dump-autoload

RUN cp .env.example .env