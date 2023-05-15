ARG BUILD_FROM=ghcr.io/home-assistant/aarch64-base-python:3.10-alpine3.17
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set Shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy Python requirements file
COPY requirements.txt /tmp/

# Setup Base
ARG BUILD_ARCH=aarch64
ARG HA_CLI_VERSION="4.23.0"

RUN \
    apk add --no-cache --virtual .build-dependencies \
        gcc=12.2.1_git20220924-r4 \
        musl-dev=1.2.3-r4 \
        linux-headers=5.19.5-r0 \
        git=2.38.5-r0 \
    \
    && git clone --branch master --single-branch --depth 1 \
        https://github.com/MrEditor97/redreactor /tmp/redreactor \
    \
    && mkdir -p /var/redreactor \
    && mv /tmp/redreactor/src/* /var/redreactor/ \
    \
    && pip3 install --no-cache-dir -r /tmp/requirements.txt \
    \
    && curl -L -s -o /usr/bin/ha \
        "https://github.com/home-assistant/cli/releases/download/${HA_CLI_VERSION}/ha_${BUILD_ARCH}" \
    \
    && chmod a+x /usr/bin/ha \
    \
    && apk del --no-cache --purge .build-dependencies \
    && rm -fr \
        /tmp/*

# Copy Root Filesystem
COPY rootfs /

# Ensure correct permissions
RUN \
    chmod a+x /var/redreactor/redreactor.py \
    && chmod a+x /etc/s6-overlay/s6-rc.d/redreactor/run \
    && chmod a+x /etc/s6-overlay/s6-rc.d/redreactor/finish

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="MrEditor97" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Add-ons" \
    org.opencontainers.image.authors="MrEditor97" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/mreditor97/homeassistant-addons" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
