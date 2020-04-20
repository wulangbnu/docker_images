# From alpine:latest image
FROM alpine:latest

MAINTAINER @wulang

# strongswan version
ARG SS_VERSION="https://download.strongswan.org/strongswan-5.8.4.tar.gz"
ARG BUILD_DEPS="gettext"
ARG RUNTIME_DEPS="libintl"

# install dep packge, configure, make and install strongSwan
RUN apk --update add build-base curl bash iproute2 iptables-dev openssl openssl-dev supervisor bash && mkdir -p /tmp/strongswan \
    && apk add --update $RUNTIME_DEPS && apk add --virtual build_deps $BUILD_DEPS && cp /usr/bin/envsubst /usr/local/bin/envsubst \
    && curl -Lo /tmp/strongswan.tar.gz $SS_VERSION && tar --strip-components=1 -C /tmp/strongswan -xf /tmp/strongswan.tar.gz \
    && cd /tmp/strongswan \
    && ./configure  --enable-eap-identity --enable-eap-md5 --enable-eap-mschapv2 --enable-eap-tls --enable-eap-ttls --enable-eap-peap --enable-eap-tnc --enable-eap-dynamic --enable-eap-radius --enable-xauth-eap  --enable-dhcp  --enable-openssl  --enable-addrblock --enable-unity --enable-certexpire --enable-radattr --enable-swanctl --enable-openssl --disable-gmp && make && make install \
    && rm -rf /tmp/* && apk del build-base curl openssl-dev build_deps && rm -rf /var/cache/apk/*

CMD ["/bin/sh"]
