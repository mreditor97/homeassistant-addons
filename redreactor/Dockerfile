ARG BUILD_FROM
FROM $BUILD_FROM

# Set Shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

#Setup Base
ARG BUILD_ARCH=amd64
ARG HA_CLI_VERSION="4.23.0"

RUN \
    apk add --no-cache --virtual .build-dependencies \
        gcc \
        musl-dev \
        linux-headers \
        git \
    \
    && git clone --branch master --single-branch --depth 1 \
        https://github.com/mreditor97/redreactor /tmp/redreactor \
    \
    && mkdir -p /var/redreactor \
    && mv /tmp/redreactor/src/* /var/redreactor/ \
    \
    && pip3 install --no-cache-dir --upgrade pip \
    && pip3 install --no-cache-dir -r /var/redreactor/requirements.txt \
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