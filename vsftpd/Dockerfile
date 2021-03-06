FROM debian:buster-slim
# hadolint ignore=DL3008
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        ftp \
        gosu \
        netcat-openbsd \
        vsftpd \
    && \
    mkdir -p /var/run/vsftpd/empty && \
    install -d -m 755 /var/lib/transmission/Downloads && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/apt/archives/*
COPY --chown=root:root entrypoint /usr/local/sbin/
COPY --chown=root:root healthcheck /usr/local/bin
COPY --chown=root:root vsftpd.conf /etc/vsftpd.conf
VOLUME /var/lib/transmission/Downloads
EXPOSE 21 4559 4560 4561 4562 4563 4564
ENTRYPOINT [ "/usr/local/sbin/entrypoint" ]
CMD [ "vsftpd" ]
HEALTHCHECK CMD healthcheck || exit 1
