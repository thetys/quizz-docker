FROM php:7.0-apache

COPY php.ini /usr/local/etc/php/
COPY 000-default.conf /etc/apache2/sites-available/

ENV PHP_CPPFLAGS="$PHP_CPPFLAGS -std=c++11"
RUN curl -fsS -o /tmp/icu.tar.gz -L http://download.icu-project.org/files/icu4c/59.1/icu4c-59_1-src.tgz \
    && tar -zxf /tmp/icu.tar.gz -C /tmp \
    && cd /tmp/icu/source \
    && ./configure --prefix=/usr/local \
    && make \
    && make install \
    && rm -rf /tmp/icu* \
    && docker-php-ext-configure intl --with-icu-dir=/usr/local \
    && docker-php-ext-install intl

RUN docker-php-ext-install pdo_mysql

RUN a2enmod rewrite

EXPOSE 80

