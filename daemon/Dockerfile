FROM alpine:3.13
# hadolint ignore=DL3018
RUN apk add --update --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ \
        gosu \
    && \
    apk add --update --no-cache \
        transmission-daemon \
    && \
    install -d -m 555 /var/lib/transmission && \
    mkdir -m 777 /run/transmission && \
    mkdir /etc/transmission
COPY --chown=root:root entrypoint /
COPY settings.json /etc/transmission/
VOLUME /var/lib/transmission
WORKDIR /var/lib/transmission
ENV HOME /var/lib/transmission
EXPOSE 9091 51413/tcp 51413/udp
ENTRYPOINT [ "/entrypoint" ]
CMD [ "transmission-daemon", "--foreground" ]
HEALTHCHECK CMD wget --spider http://localhost:9091/transmission || exit 1
