FROM alpine:edge

EXPOSE 8118 9050

RUN echo '@testing http://nl.alpinelinux.org/alpine/edge/testing' \
    >> /etc/apk/repositories && \
    apk --update add privoxy tor@testing runit@testing

COPY service /etc/service/

COPY configs /root/configs/

CMD ["runsvdir", "/etc/service"]
