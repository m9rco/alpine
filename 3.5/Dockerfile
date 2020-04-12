#  vim:ts=4:sts=4:sw=4:et
#
#  Author: m9rco <pushaowei0727@gmail.com>
#  Date: 2019-12-03 
#
FROM alpine:3.8
LABEL maintainer="m9rco <pushaowei0727@gmail.com>"

ARG TIME_ZONE=Asia/Shanghai 
ARG REPOSITORIES=dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn
RUN set -xe \
    && sed -i "s/${REPOSITORIES}/g" /etc/apk/repositories \
    && apk update \
    && apk add --no-cache --virtual .persistent-deps \
      bash \
      tini \
      sudo \
      tar \
      wget \
      tzdata \
      autoconf \
      cmake \
      file \
      g++ \
      gcc \
      libc-dev \
      pcre-dev \
      make \
      git \
      pkgconf \
      re2c \
    && rm -rf /var/cache/apk/* \
    && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime \
    && echo "${TIME_ZONE}" > /etc/timezone

ADD rootfs /

WORKDIR /app
ENTRYPOINT ["/sbin/tini", "--"]
