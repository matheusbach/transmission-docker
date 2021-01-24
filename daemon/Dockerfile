FROM alpine:3.13
# hadolint ignore=DL3018
RUN apk add --update --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ \
        gosu \
    && \
    apk add --update --no-cache \
        transmission-daemon \
        shadow \
    && \
    groupmod -g 1000 transmission && \
    usermod -u 1000 transmission && \
    apk del --no-cache --rdepends shadow && \
    mkdir -p /var/run/transmission /etc/transmission/ && \
    chown -R transmission:transmission /var/run/transmission
COPY --chown=root:root entrypoint /
COPY --chown=1000:1000 settings.json /etc/transmission/
VOLUME /var/lib/transmission/
WORKDIR /var/lib/transmission
EXPOSE 9091 51413/tcp 51413/udp
ENTRYPOINT [ "/entrypoint" ]
CMD [ "transmission-daemon", "--foreground" ]
HEALTHCHECK CMD wget --spider http://localhost:9091/transmission || exit 1
