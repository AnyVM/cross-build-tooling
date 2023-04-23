FROM ghcr.io/cross-rs/mipsel-unknown-linux-musl:main

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y wget
RUN mkdir -p /opt/vendor && cd /opt/vendor/ && wget https://www.openssl.org/source/old/1.1.1/openssl-1.1.1s.tar.gz
RUN cd /opt/vendor/ && tar -xzf openssl-1.1.1s.tar.gz && cd openssl-1.1.1s && ./config shared --prefix=/usr/local/ssl --openssldir=/usr/local/ssl --cross-compile-prefix=mipsel-linux-muslsf- no-asm
# strip the m64 flag from makefile as we targets 32bit build
RUN cd /opt/vendor/openssl-1.1.1s && sed -i "s/-m64//g" Makefile && make && make install

ENV OPENSSL_STATIC=yes
ENV OPENSSL_DIR=/usr/local/ssl
ENV CARGO_TARGET_MIPSEL_UNKNOWN_LINUX_MUSL_RUSTFLAGS="$CARGO_TARGET_MIPSEL_UNKNOWN_LINUX_MUSL_RUSTFLAGS -C link-arg=-latomic -C target-feature=+crt-static"
