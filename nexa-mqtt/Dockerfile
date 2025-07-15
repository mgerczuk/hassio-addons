ARG BUILD_FROM
FROM $BUILD_FROM
ARG BUILD_FROM
COPY config.json /
RUN apk --no-cache add jq
RUN NEXA_MQTT_VERSION=$(jq --raw-output '.version // empty' config.json) && case "$BUILD_FROM" in \
*"aarch64-base"*) ARCH="arm64";; \
*"armhf-base"*) ARCH="armv6";; \
*"amd64-base"*) ARCH="amd64";; \
esac \
&& curl -L -o /nexa-mqtt.tar.gz https://github.com/mgerczuk/nexa-mqtt/releases/download/v${NEXA_MQTT_VERSION}/nexa-mqtt_${NEXA_MQTT_VERSION}_linux_${ARCH}.tar.gz && tar -xf /nexa-mqtt.tar.gz && rm /nexa-mqtt.tar.gz

COPY rootfs/docker-entrypoint.sh /
RUN chmod a+x /nexa-mqtt && chmod a+x /docker-entrypoint.sh
ENTRYPOINT [ "/docker-entrypoint.sh"]
