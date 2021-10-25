FROM ruby:2.4-alpine3.6

ENV VERSION=0.7.1
ENV MAILCATCHER_HTTP_PORT=1080
ENV MAILCATCHER_SMTP_PORT=1025
ENV MAILCATCHER_PATH=/

RUN set -xe \
    && apk add --no-cache \
        libstdc++ \
        sqlite-libs \
    && apk add --no-cache --virtual .build-deps \
        build-base \
        sqlite-dev \
    && gem install mailcatcher -v $VERSION --no-ri --no-rdoc \
    && apk del .build-deps

EXPOSE $MAILCATCHER_SMTP_PORT $MAILCATCHER_HTTP_PORT

CMD mailcatcher -f --ip=0.0.0.0 --smtp-port=$MAILCATCHER_SMTP_PORT --http-port=$MAILCATCHER_HTTP_PORT --http-path=$MAILCATCHER_PATH