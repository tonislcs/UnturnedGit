FROM debian:13-slim

LABEL maintainer="RestoreMonarchy <admin@restoremonarchy.com>"

ENV DEBIAN_FRONTEND=noninteractive

RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        unzip \
        wget \
        jq \
        git \
        lib32gcc-s1 \
        lib32stdc++6 \
        libc6 \
        libc6-i386 \
        libgl1 \
        libxcursor1 \
        libxrandr2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.1_1.1.1w-0+deb11u5_amd64.deb && \
    dpkg -i libssl1.1_*.deb && \
    rm -f libssl1.1_*.deb && \
    useradd -d /home/container -m container

USER container
ENV  USER container
ENV  HOME /home/container

WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh
COPY ./repo-sync.sh /repo-sync.sh

CMD ["/bin/bash", "/entrypoint.sh"]
