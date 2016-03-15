FROM armhf/alpine:3.3
MAINTAINER King-On Yeung <koyeung@gmail.com>

ENV OTP_VERSION=18.2.4
ENV REBAR_VERSION=2.6.1
ENV REBAR3_VERSION="3.0.0"

RUN set -xe \    
    && export LANG=C.UTF-8 \
    && apk add --no-cache tar unixodbc ncurses openssl libgcc \
    && apk add --no-cache --virtual .setup-deps \
         make autoconf gcc perl m4 sed binutils-gold \
         musl-dev libc-dev \
         unixodbc-dev ncurses-dev openssl-dev \
    && OTP_DOWNLOAD_URL="https://github.com/erlang/otp/archive/OTP-$OTP_VERSION.tar.gz" \
    && OTP_DOWNLOAD_SHA1="4c8d90feb15b58c6b5929413b056c419166d7fc4" \
    && wget -q "$OTP_DOWNLOAD_URL" -O otp-src.tar.gz \
    && echo "$OTP_DOWNLOAD_SHA1  otp-src.tar.gz" | sha1sum -c - \
    && mkdir -p /usr/src/otp-src \
    && tar -xzf otp-src.tar.gz -C /usr/src/otp-src --strip-components=1 \
    && rm otp-src.tar.gz \
    && cd /usr/src/otp-src \ 
    && ./otp_build autoconf \
    && ./configure \
    && make \
    && make install \
    && cd / \
    && rm -rf /usr/src/otp-src \
    && echo finished for OTP \
    && REBAR_DOWNLOAD_URL="https://github.com/rebar/rebar/archive/${REBAR_VERSION##*@}.tar.gz" \
    && REBAR_DOWNLOAD_SHA1="7f9b799c5dfa06d1779d828c767be2732dacc411" \
    && mkdir -p /usr/src/rebar-src \
    && wget -q "$REBAR_DOWNLOAD_URL" -O rebar-src.tar.gz \
    && echo "$REBAR_DOWNLOAD_SHA1  rebar-src.tar.gz" | sha1sum -c - \
    && tar -xzf rebar-src.tar.gz -C /usr/src/rebar-src --strip-components=1 \
    && rm rebar-src.tar.gz \
    && cd /usr/src/rebar-src \
    && ./bootstrap \
    && install -v ./rebar /usr/local/bin/ \
    && cd / \
    && rm -rf /usr/src/rebar-src \
    && echo finished for REBAR \
    && REBAR3_DOWNLOAD_URL="https://github.com/rebar/rebar3/archive/${REBAR3_VERSION##*@}.tar.gz" \
    && REBAR3_DOWNLOAD_SHA1="4228c9c39ee45561972b160f6e9476ce47ebf793" \
    && mkdir -p /usr/src/rebar3-src \
    && wget -q "$REBAR3_DOWNLOAD_URL" -O rebar3-src.tar.gz \
    && echo "$REBAR3_DOWNLOAD_SHA1  rebar3-src.tar.gz" | sha1sum -c - \
    && tar -xzf rebar3-src.tar.gz -C /usr/src/rebar3-src --strip-components=1 \
    && rm rebar3-src.tar.gz \
    && cd /usr/src/rebar3-src \
    && HOME=$PWD ./bootstrap \
    && install -v ./rebar3 /usr/local/bin/ \
    && cd / \
    && rm -rf /usr/src/rebar3-src \
    && echo finished for REBAR3 \
    && apk del .setup-deps

CMD ["erl"]
    
