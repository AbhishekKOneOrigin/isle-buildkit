# syntax=docker/dockerfile:1.2.1
FROM local/base:latest

RUN --mount=type=cache,target=/var/cache/apk \ 
    --mount=type=cache,target=/etc/cache/apk \ 
    apk-install.sh \
        nginx \
        php7 \
        php7-ctype \
        php7-curl \
        php7-dom \
        php7-fileinfo \
        php7-fpm \
        php7-gd \
        php7-iconv \
        php7-json \
        php7-mbstring \
        php7-mysqli \
        php7-opcache \
        php7-openssl \
        php7-pdo \
        php7-pdo_mysql \ 
        php7-pdo_pgsql \ 
        php7-phar \
        php7-session \
        php7-simplexml \
        php7-tokenizer \
        php7-xml \
        php7-xmlwriter \
        php7-xsl \
    && \
    cleanup.sh

# https://getcomposer.org/download/
RUN --mount=id=downloads,type=cache,target=/opt/downloads \
    DOWNLOAD_CACHE_DIRECTORY="/opt/downloads" && \
    COMPOSER_VERSION="2.0.4" && \
    COMPOSER_FILE="composer.phar" && \
    COMPOSER_URL="https://getcomposer.org/download/${COMPOSER_VERSION}/${COMPOSER_FILE}" && \
    COMPOSER_SHA256="c3b2bc477429c923c69f7f9b137e06b2a93c6a1e192d40ffad1741ee5d54760d" && \
    download.sh --url "${COMPOSER_URL}" --sha256 "${COMPOSER_SHA256}" "${DOWNLOAD_CACHE_DIRECTORY}" && \
    cp "${DOWNLOAD_CACHE_DIRECTORY}/${COMPOSER_FILE}" /usr/bin/composer && \
    chmod a+x /usr/bin/composer

ENV \
    NGINX_CLIENT_MAX_BODY_SIZE=0 \
    NGINX_ERROR_LOG_LEVEL=warn \
    NGINX_KEEPALIVE_TIMEOUT=65 \
    NGINX_WORKER_CONNECTIONS=1024 \
    NGINX_WORKER_PROCESSES=auto \
    PHP_DEFAULT_SOCKET_TIMEOUT=60 \
    PHP_LOG_LEVEL=notice \
    PHP_LOG_LIMIT=16384 \
    PHP_MAX_EXECUTION_TIME=30 \
    PHP_MAX_FILE_UPLOADS=20 \
    PHP_MAX_INPUT_TIME=60 \
    PHP_MEMORY_LIMIT=256M \
    PHP_POST_MAX_SIZE=0 \
    PHP_UPLOAD_MAX_FILESIZE=128M

COPY rootfs /
