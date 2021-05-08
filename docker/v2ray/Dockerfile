# Dockerfile for v2ray based alpine
# Reference URL:
# https://github.com/v2ray/v2ray-core
# https://github.com/v2ray/geoip
# https://github.com/v2ray/domain-list-community

FROM alpine:latest
LABEL maintainer="Sunssr <i@wdnmd.be>"

WORKDIR /root
COPY v2ray.sh /root/v2ray.sh
COPY config.json /etc/v2ray/config.json
COPY v2ray.key /etc/v2ray/v2ray.key
COPY v2ray.crt /etc/v2ray/v2ray.crt
RUN set -ex \
	&& apk add --no-cache tzdata ca-certificates \
	&& mkdir -p /var/log/v2ray \
	&& chmod +x /root/v2ray.sh \
	&& /root/v2ray.sh \
	&& rm -fv /root/v2ray.sh \
	&& wget -O /usr/bin/geosite.dat https://github.com/v2fly/domain-list-community/releases/latest/download/dlc.dat \
	&& wget -O /usr/bin/geoip.dat https://github.com/v2fly/geoip/releases/latest/download/geoip.dat

VOLUME /etc/v2ray
ENV TZ=Asia/Shanghai
CMD [ "/usr/bin/v2ray", "-config", "/etc/v2ray/config.json" ]
