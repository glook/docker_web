FROM php:7.2-fpm

# Use the default production configuration
#RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN php -i;
RUN docker-php-ext-install pdo pdo_mysql mysqli;

RUN apt-get update && apt-get install -y libxml2-dev apt-utils; \
    pear install -a SOAP-0.14.0; \
    docker-php-ext-install soap;


RUN apt-get update && apt-get install -y \
    libyaml-dev wget unzip zip zlib1g-dev zlib1g-dev; \
    pecl install yaml; \
    docker-php-ext-install zip; \
    docker-php-ext-enable yaml;

COPY php.ini $PHP_INI_DIR/php.ini

# Override with custom opcache settings
COPY opcache.ini $PHP_INI_DIR/conf.d/
