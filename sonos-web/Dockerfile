ARG BUILD_FROM=hassioaddons/base:7.0.2
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
RUN \
    apk add --no-cache \
        nodejs \
        npm \
    \
    && npm config set unsafe-perm true \
    \ 
    && npm install -g sonos-web-cli \
    \
    && sonos-web install \
    \
    && npm cache clear --force \
    \
    && rm -fr \
        /tmp/* \
        /etc/nginx

EXPOSE 5050

# HEALTHCHECK --interval=1m --timeout=2s \
#   CMD curl -LSs http://localhost:5050 || exit 1

CMD cd /root/.sonos-web && node src/server.js

# Build arguments
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Sonos-Web" \
    io.hass.description="Web based controller for Sonos" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Richard Matthews <richard.matthews@blueclover.co.uk>" \
    org.label-schema.description="Web based controller for Sonos" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="AirSonos" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://github.com/rickjmatthews/hassio-addons/sonos-web" \
    org.label-schema.usage="https://github.com/rickjmatthews/hassio-addons/sonos-web/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/rickjmatthews/hassio-addons/sonos-web" \
    org.label-schema.vendor="Home Assistant Community Add-ons"
