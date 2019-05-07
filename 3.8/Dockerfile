FROM alpine:3.8
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



RUN addgroup -g 1000 appusers

RUN addgroup root appusers

RUN adduser -D -u 1000 -s /bin/bash -h /home/app -G appusers app

RUN sed -i 's,/bin/ash,/bin/bash,g' /etc/passwd

RUN echo '%appusers ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers


ADD rootfs /

RUN mkdir -p /usr/share/entrypoint \
    && chown app:appusers /usr/share/entrypoint

WORKDIR /home/app

ENTRYPOINT ["/sbin/tini", "--"]

CMD ["/bin/bash"]
