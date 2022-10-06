ARG VARIANT="focal"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y --no-install-recommends \
        git \
        cmake \
        make \
        bsdmainutils \
        elfutils \
        wget \
        curl \
        ca-certificates \
        binutils \
        zlib1g-dev \
        g++ \
        lftp \
        python
RUN wget https://github.com/0CBH0/wiiurpxtool/archive/98935a5daf9a7629130974af3fa0c02bd6397bef.zip -O wiiurpxtool.zip \
    && unzip wiiurpxtool.zip \
    && cd wiiurpxtool* \
    && sed -i "s|#include <io.h>|#include <stdio.h>|g" wiiurpxtool.cpp \
    && g++ wiiurpxtool.cpp -lz -o /usr/local/bin/wiiurpxtool

ADD toolchain/devkitPPC_r29-1-x86_64-linux.tar.bz2 /opt/devkitpro
ADD toolchain/ppc-libpng-1.6.37-1-any.pkg.tar.xz /
ADD toolchain/ppc-zlib-1.2.11-2-any.pkg.tar.xz /
ADD --chown=vscode:vscode toolchain/wiiload /usr/local/bin
ENV DEVKITPRO=/opt/devkitpro
ENV DEVKITPPC=/opt/devkitpro/devkitPPC
