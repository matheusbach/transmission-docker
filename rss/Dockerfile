FROM ruby:alpine
# hadolint ignore=DL3018
RUN apk add --update --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ \
        gosu \
    && \
    apk add --update --no-cache \
        build-base \
    && \
    gem install \
        transmission-rss:1.0.0 \
    && \
    apk del --rdepends --no-cache build-base && \
    addgroup -g 1000 transmission-rss && \
    adduser -h /var/lib/transmission-rss -G transmission-rss -D -u 1000 transmission-rss
COPY --chown=root:root entrypoint /usr/local/sbin/
COPY --chown=root:root transmission-rss.conf /etc/
ENTRYPOINT [ "entrypoint" ]
WORKDIR /var/lib/transmission-rss
VOLUME /var/lib/transmission-rss
CMD [ "/usr/local/bundle/bin/transmission-rss" ]
HEALTHCHECK CMD pgrep ruby || exit 1
