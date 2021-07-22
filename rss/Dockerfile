FROM docker.io/library/ruby:3.0-slim
# hadolint ignore=DL3018
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        build-essential \
        gosu \
    && \
    gem install \
        transmission-rss:1.2.0 \
    && \
    DEBIAN_FRONTEND=noninteractive apt-get purge -y --auto-remove \
        build-essential \
    && \
    useradd --home-dir /var/lib/transmissions-rss \
            --create-home \
            --uid 1000 \
            --user-group \
            transmission-rss \
    && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/apt/archives/*
COPY --chown=root:root entrypoint /usr/local/sbin/
COPY --chown=root:root transmission-rss.conf /etc/
ENTRYPOINT [ "entrypoint" ]
WORKDIR /var/lib/transmission-rss
VOLUME /var/lib/transmission-rss
CMD [ "/usr/local/bundle/bin/transmission-rss" ]
HEALTHCHECK CMD pgrep --full ruby || exit 1
