FROM ubuntu:trusty
# Syncthing-Relay Server
MAINTAINER Blake VandeMerwe <blakev@null.net>

ENV DEBUG           false

# 100 mbps
ENV RATE_GLOBAL     100000000
# 10 mbps
ENV RATE_SESSION    10000000

ENV TIMEOUT_MSG     1m30s
ENV TIMEOUT_NET     3m00s
ENV PING_INT        0m45s

ENV PROVIDED_BY     "syncthing-relay docker container"


ADD https://github.com/syncthing/relaysrv/releases/download/v0.12.1/relaysrv-linux-amd64.tar.gz /tmp/relaysrv.tar.gz
RUN tar -xzvf /tmp/relaysrv.tar.gz && rm /tmp/relaysrv.tar.gz && mv relaysrv* /srv/relaysrv
RUN useradd --no-create-home -g users --uid 22070 relaysrv
RUN chown relaysrv: /srv/relaysrv -R

EXPOSE 22070 22067

CMD /srv/relaysrv/relaysrv \
    -debug="${DEBUG}" \
    -global-rate="${RATE_GLOBAL}" \
    -per-session-rate="${RATE_SESSION}" \
    -message-timeout="${TIMEOUT_MSG}" \
    -network-timeout="${TIMEOUT_NET}" \
    -ping-interval="${PING_INT}" \
    -provided-by="${PROVIDED_BY}"