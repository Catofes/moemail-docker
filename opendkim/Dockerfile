FROM ubuntu:20.04
ARG s6_overlay_ver=3.1.0.1
RUN apt-get update \
                && apt-get install -y opendkim libopendbx1-pgsql vim less ca-certificates 
# Install s6-overlay
RUN apt-get update \
 && apt-get install -y --no-install-recommends --no-install-suggests \
            curl xz-utils rsyslog\
 && curl -fL -o /tmp/s6-overlay-noarch.tar.xz \
         https://github.com/just-containers/s6-overlay/releases/download/v${s6_overlay_ver}/s6-overlay-noarch.tar.xz \
 && curl -fL -o /tmp/s6-overlay-bin.tar.xz \
         https://github.com/just-containers/s6-overlay/releases/download/v${s6_overlay_ver}/s6-overlay-$(arch).tar.xz \
 && tar -xf /tmp/s6-overlay-noarch.tar.xz -C / \
 && tar -xf /tmp/s6-overlay-bin.tar.xz -C / \
    \
 # Cleanup unnecessary stuff
 && apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
            curl xz-utils \
 && rm -rf /var/lib/apt/lists/* \
           /tmp/*

ENV S6_KEEP_ENV=1 \
    S6_BEHAVIOUR_IF_STAGE2_FAILS=2 \
    S6_CMD_WAIT_FOR_SERVICES=1


COPY rootfs /

RUN chmod +x /etc/s6-overlay/s6-rc.d/*/run \
             /etc/s6-overlay/s6-rc.d/*/*.sh


EXPOSE 8891

ENTRYPOINT ["/init"]

CMD ["opendkim", "-f"]
