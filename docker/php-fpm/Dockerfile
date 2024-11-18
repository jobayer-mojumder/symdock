FROM alpine:3.20

ARG PHP_XDEBUG_MODE=off
ARG PHP_XDEBUG_CLIENT_PORT=5902
ARG PHP_XDEBUG_CLIENT_HOST=host.docker.internal
ARG SYMFONY_CLI_VERSION

RUN apk add --no-cache \
    coreutils \
    gettext \
    php83-fpm \
    php83-ctype \
    php83-curl \
    php83-dom \
    php83-gd \
    php83-iconv \
    php83-json \
    php83-intl \
    php83-fileinfo \
    php83-mbstring \
    php83-opcache \
    php83-openssl \
    php83-pdo \
    php83-pdo_mysql \
    php83-mysqli \
    php83-xml \
    php83-xsl \
    php83-zlib \
    php83-phar \
    php83-tokenizer \
    php83-session \
    php83-simplexml \
    php83-zip \
    php83-xmlwriter \
    php83-sodium \
    php83-pecl-apcu \
    make \
    curl

# Enable php8-xdebug if $PHP_XDEBUG_MODE is not empty
COPY xdebug.ini /etc/php83/conf.d/xdebug.ini.template
RUN if [ "$PHP_XDEBUG_MODE" != "off" ]; then \
    apk add --no-cache php83-pecl-xdebug; \
    export PHP_XDEBUG_MODE=$PHP_XDEBUG_MODE; \
    export PHP_XDEBUG_CLIENT_PORT=$PHP_XDEBUG_CLIENT_PORT; \
    export PHP_XDEBUG_CLIENT_HOST=$PHP_XDEBUG_CLIENT_HOST; \
    envsubst < /etc/php83/conf.d/xdebug.ini.template > /etc/php83/conf.d/xdebug.ini; \
    fi
RUN rm -f /etc/php83/conf.d/xdebug.ini.template

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    chmod +x /usr/local/bin/composer && \
    ln -s /usr/bin/php83 /usr/local/bin/php

RUN wget https://github.com/symfony/cli/releases/download/v$SYMFONY_CLI_VERSION/symfony_linux_amd64.gz && \
    gzip -d symfony_linux_amd64.gz && \
    mv symfony_linux_amd64 symfony && \
    chmod +x symfony && \
    mv symfony /usr/local/bin/

RUN apk add --update nodejs npm && \
    npm install --global yarn

COPY symfony.ini /etc/php83/conf.d/
COPY symfony.ini /etc/php83/cli/conf.d/

COPY symfony.pool.conf /etc/php83/php-fpm.d/

WORKDIR /var/www/html

CMD ["php-fpm83", "-F"]

EXPOSE 9001

