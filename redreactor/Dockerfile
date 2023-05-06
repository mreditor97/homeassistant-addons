ARG BUILD_FROM==ghcr.io/home-assistant/aarch64-base-python:3.10-alpine3.17
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set Shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy Python requirements file
COPY requirements.txt /tmp/

#Setup Base
ARG BUILD_ARCH=aarch64
ARG HA_CLI_VERSION="4.23.0"

RUN \
    apk add --no-cache --virtual .build-dependencies \
        gcc=12.2.1_git20220924-r10 \
        musl-dev=1.2.4-r0 \
        linux-headers=6.3-r0 \
        git=2.38.5-r0 \
        py3-pip=23.1.2-r0 \
    \
    && git clone --branch master --single-branch --depth 1 \
        https://github.com/mreditor97/redreactor /tmp/redreactor \
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
    && chmod a+x etc/s6-overlay/s6-rc.d/redreactor/run \
    && chmod a+x etc/s6-overlay/s6-rc.d/redreactor/finish
