FROM alpine:3.5
LABEL maintainer="m9rco <pushaowei0727@gmail.com>"

ENV TIME_ZONE Asia/Shanghai 
ENV BASH_ENV /etc/bashrc

RUN apk add --no-cache -U tzdata \
  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime \
  && echo "${TIME_ZONE}" > /etc/timezone
 

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk update

RUN apk add -U --no-cache \
    tini \
    bash \
    sudo \
    && rm -rf /var/cache/apk/*


ADD rootfs /


WORKDIR /app

ENTRYPOINT ["/sbin/tini", "--"]

CMD ["/bin/bash"]
