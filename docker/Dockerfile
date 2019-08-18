FROM php:7.2-apache

MAINTAINER Bruno Vitorino <bruno@plutonian.be>

# change the document root
RUN sed -i 's|/var/www/html|/var/www/html/web|' /etc/apache2/sites-enabled/000-default.conf

# Enable mod-rewrite
RUN a2enmod rewrite

ENV TERM xterm
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HTACCESS_PROTECT 0
ENV COMPOSER_NO_INTERACTION 1

COPY --from=composer:1.8 /usr/bin/composer /usr/bin/composer

SHELL ["/bin/bash", "-c"]


ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions gd xdebug pdo_mysql bcmath intl apcu zip soap xsl

# Copy our fixes.ini
COPY fixes.ini /usr/local/etc/php/conf.d/fixes.ini

EXPOSE 80
EXPOSE 443
