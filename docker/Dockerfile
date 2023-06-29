FROM ghcr.io/cross-rs/mips-unknown-linux-musl:main

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y wget
RUN mkdir -p /opt/vendor && cd /opt/vendor/ && wget https://ftp.openbsd.org/pub/OpenBSD/LibreSSL/libressl-3.7.3.tar.gz
ENV CC=mips-linux-muslsf-gcc
ENV CXX=mips-linux-muslsf-g++
RUN cd /opt/vendor/ && tar -xzf libressl-3.7.3.tar.gz && cd libressl-3.7.3  && ./configure --host=mips-unknown-linux-muslsf --target=mips-unknown-linux-muslsf --disable-shared --disable-check
WORKDIR /opt/vendor/libressl-3.7.3
RUN make install

ENV OPENSSL_STATIC=yes
ENV CARGO_TARGET_MIPS_UNKNOWN_LINUX_MUSL_RUSTFLAGS="$CARGO_TARGET_MIPS_UNKNOWN_LINUX_MUSL_RUSTFLAGS -C link-arg=-latomic -C link-arg=-lc -C target-feature=+crt-static -C link-arg=-s -C link-self-contained=yes -L /usr/local/mips-linux-muslsf/lib -l static=atomic -l static=c "

