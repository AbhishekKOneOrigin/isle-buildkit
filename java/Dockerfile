# syntax=docker/dockerfile:1.2.1
FROM local/base:latest

# Install packages and tools required by all downstream images.
RUN --mount=type=cache,target=/var/cache/apk \ 
    --mount=type=cache,target=/etc/cache/apk \
    apk-install.sh \
        openjdk8 \
        maven \
    && \
    cleanup.sh

ENV \
    JAVA_HOME=/usr/lib/jvm/default-jvm \
    JAVA_OPTS=

COPY rootfs /
