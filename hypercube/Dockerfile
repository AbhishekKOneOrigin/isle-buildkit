# syntax=docker/dockerfile:1.2.1
FROM local/crayfish:latest

RUN --mount=type=cache,target=/var/cache/apk \ 
    --mount=type=cache,target=/etc/cache/apk \ 
    --mount=type=cache,target=/root/.composer/cache \
    apk-install.sh \
        poppler-utils \
        tesseract-ocr \
        tesseract-ocr-data-fra \
        tesseract-ocr-data-spa \
        tesseract-ocr-data-ita \
        tesseract-ocr-data-por \
        tesseract-ocr-data-hin \
        tesseract-ocr-data-deu \
        tesseract-ocr-data-jpn \
        tesseract-ocr-data-rus \
    && \
    composer install -d /var/www/crayfish/Hypercube && \
    ln -s /var/www/crayfish/Hypercube/src /var/www/html && \
    cleanup.sh

RUN \
    HYPERCUBE_FCREPO_URL=fcrepo/fcrepo/rest \
    HYPERCUBE_LOG_LEVEL=debug

COPY /rootfs /

WORKDIR /var/www/crayfish/Hypercube/
