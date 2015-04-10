FROM gliderlabs/alpine

RUN apk --update add curl bash haproxy

# install etcdctl and confd
RUN \
  curl -sSL -o /usr/local/bin/etcdctl https://s3-us-west-2.amazonaws.com/opdemand/etcdctl-v0.4.6 \
  && chmod +x /usr/local/bin/etcdctl \
  && curl -sSL -o /usr/local/bin/confd https://github.com/kelseyhightower/confd/releases/download/v0.7.1/confd-0.7.1-linux-amd64 \
  && chmod +x /usr/local/bin/confd

ADD . /app

RUN chmod +x /app/bin/*

CMD /app/bin/boot
