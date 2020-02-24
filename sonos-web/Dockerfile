ARG BUILD_FROM=hassioaddons/ubuntu-base:5.0.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base system
RUN \
    apt-get update \
    \
    && apt-get install -y --no-install-recommends \
        libssl1.0.0=1.0.2n-1ubuntu5.3 \
    \
    && rm -fr \
        /tmp/* \
        /var/{cache,log}/* \
        /var/lib/apt/lists/*

# Copy root filesystem
COPY rootfs /

# Add airsonos binary
ARG BUILD_ARCH=amd64
COPY bin/airsonos-${BUILD_ARCH} /usr/bin/airsonos

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
