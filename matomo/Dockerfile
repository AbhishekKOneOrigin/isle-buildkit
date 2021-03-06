# syntax=docker/dockerfile:1.2.1
FROM local/nginx:latest

RUN --mount=id=downloads,type=cache,target=/opt/downloads \
    DOWNLOAD_CACHE_DIRECTORY="/opt/downloads" && \
    MATOMO_VERSION="3.13.5" && \
    MATOMO_FILE="matomo-${MATOMO_VERSION}.tar.gz" && \
    MATOMO_URL="https://builds.matomo.org/${MATOMO_FILE}" && \
    MATOMO_FILE_SHA256="b9af7dabc6e727762cef58cecd16de7bc75886f8dacc910070632d83a44c2aad" && \
    MATOMO_SIG_SHA256="7e33ba4ea7f44370157832940d177d524b21192985b03e795e9f05f037b0c453" && \
    download.sh --url "${MATOMO_URL}" --sha256 "${MATOMO_FILE_SHA256}" "${DOWNLOAD_CACHE_DIRECTORY}" && \
    download.sh --url "${MATOMO_URL}.asc" --sha256 "${MATOMO_SIG_SHA256}" "${DOWNLOAD_CACHE_DIRECTORY}" && \
    gpg-receive-keys.sh --key 814E346FA01A20DBB04B6807B5DBD5925590A237 && \
    gpg --verify "${DOWNLOAD_CACHE_DIRECTORY}/${MATOMO_FILE}.asc" "${DOWNLOAD_CACHE_DIRECTORY}/${MATOMO_FILE}" && \
    tar -xzf "${DOWNLOAD_CACHE_DIRECTORY}/${MATOMO_FILE}" -C /opt && \
    chown -R nginx:nginx /opt/matomo && \
    cleanup.sh

WORKDIR /var/www/matomo

EXPOSE 8000

ENV \
    MATOMO_ASSUME_SECURE_PROTOCOL=1 \
    MATOMO_DB_DRIVER=pdo_mysql \
    MATOMO_DB_HOST=mariadb \
    MATOMO_DB_NAME=matomo \
    MATOMO_DB_PASSWORD=password \
    MATOMO_DB_PORT=3306 \
    MATOMO_DB_ROOT_PASSWORD=password \
    MATOMO_DB_ROOT_USER=root \
    MATOMO_DB_USER=matomo \
    MATOMO_DEFAULT_HOST=https://islandora.traefik.me \
    MATOMO_DEFAULT_NAME=Islandora \
    MATOMO_DEFAULT_TIMEZONE=America/Halifax \
    MATOMO_FORCE_SSL=1 \
    MATOMO_PROXY_CLIENT_HEADERS=HTTP_X_FORWARDED_FOR \
    MATOMO_PROXY_HOST_HEADERS=HTTP_X_FORWARDED_HOST \
    MATOMO_PROXY_URI_HEADER=1 \
    MATOMO_SALT=5a472390550bd59e4428a41aa472137b \
    MATOMO_USER_EMAIL=admin@example.org \
    MATOMO_USER_NAME=admin \
    MATOMO_USER_PASS='$2y$10$S38e7HPM9LI3aOIvcnRsfuMCm4ipNP572QsvbCK60upoHVJ61hMrS'

COPY rootfs /

