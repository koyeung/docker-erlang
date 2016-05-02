FROM koyeung/erlang:18.3.1
MAINTAINER King-On Yeung <koyeung@gmail.com>

ENV ELIXIR_VERSION=1.2.5

RUN set -xe \
    && apk add --no-cache --virtual .setup-deps \
         make \
    && export LANG=C.UTF-8 \
    && ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/v${ELIXIR_VERSION}.tar.gz" \
    && ELIXIR_DOWNLOAD_SHA1=de421d51c4d90f2ae4af161e487b9dbcaa5033a3 \
    && wget -q "$ELIXIR_DOWNLOAD_URL" -O elixir-src.tar.gz \
    && echo "$ELIXIR_DOWNLOAD_SHA1  elixir-src.tar.gz" | sha1sum -c - \
    && mkdir -p /usr/src/elixir-src \
    && tar -xzf elixir-src.tar.gz -C /usr/src/elixir-src --strip-components=1 \
    && rm elixir-src.tar.gz \
    && cd /usr/src/elixir-src \
    && make \
    && make install \
    && cd / \
    && rm -rf /usr/src/elixir-src \
    && apk del .setup-deps

CMD ["iex"]
