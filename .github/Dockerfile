FROM php:8.2-fpm-alpine3.16 as tmp

RUN apk add autoconf gcc libc-dev make libpq-dev linux-headers
RUN pecl install xdebug-3.2.0
RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql opcache

FROM php:8.2-fpm-alpine3.16 as clean

COPY --from=tmp /usr/local/lib/php/extensions/ /usr/local/lib/php/extensions/
COPY --from=tmp /usr/lib/libpq.* /usr/lib/
COPY --from=tmp /usr/local/etc/php/conf.d/ /usr/local/etc/php/conf.d/

COPY --from=composer:2.5.1 /usr/bin/composer /usr/local/bin/composer
COPY php.ini /usr/local/etc/php/php.ini
