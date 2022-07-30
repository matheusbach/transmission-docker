FROM alpine:3.16
# hadolint ignore=DL3018
RUN apk add --update --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ \
        gosu \
    && \
    apk add --update --no-cache \
        python3 \
        transmission-daemon \
    && \
    mkdir -m 777 /run/transmission
COPY --chown=root:root entrypoint /usr/local/sbin/docker-entrypoint
COPY --chown=root:root settings.json /etc/transmission/
COPY --chown=root:root kodi_scan /usr/local/bin/
VOLUME /var/lib/transmission
WORKDIR /var/lib/transmission
ENV HOME /var/lib/transmission
ENV TRANSMISSION_HOME /var/lib/transmission
EXPOSE 9091 51413/tcp 51413/udp
ENTRYPOINT [ "docker-entrypoint" ]
CMD [ "transmission-daemon", "--foreground" ]
HEALTHCHECK CMD wget --spider http://localhost:9091/transmission || exit 1
