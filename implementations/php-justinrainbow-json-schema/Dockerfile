FROM composer:2.8 AS builder

WORKDIR /usr/src/json-schema

COPY ./src ./src
COPY ./bootstrap.php .
COPY composer.* .
RUN composer install --no-dev --no-scripts --no-interaction --prefer-dist --optimize-autoloader
RUN composer dump-autoload --no-dev --optimize --classmap-authoritative

FROM php:8.4.10-alpine

WORKDIR /usr/src/json-schema

COPY ./src ./src
COPY ./bootstrap.php .
COPY composer.* .
COPY --from=builder /usr/src/json-schema/vendor /usr/src/json-schema/vendor

CMD ["php", "bootstrap.php"]
