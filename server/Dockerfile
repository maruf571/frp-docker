FROM alpine:3.8

ARG distribution=linux_386
ARG frp_version=0.35.0

RUN apk add --virtual .build-dependencies --no-cache openssl

RUN  mkdir -p /etc/frp \
  && cd /tmp \
  && wget -O frp.tar.gz "https://github.com/fatedier/frp/releases/download/v${frp_version}/frp_${frp_version}_${distribution}.tar.gz" \
  && tar -xzf frp.tar.gz \
  && mv ./frp_${frp_version}_${distribution}/frps /usr/local/bin \
  && rm -rf /tmp/*

RUN apk del .build-dependencies

WORKDIR /etc/frp

ENTRYPOINT ["frps", "-c", "/etc/frp/frps.ini"]
