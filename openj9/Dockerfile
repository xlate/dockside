FROM alpine:3.6

ARG OPENJ9_BUILD=181

RUN apk --update add --no-cache ca-certificates curl openssl binutils xz \
    && GLIBC_VER="2.25-r0" \
    && ALPINE_GLIBC_REPO="https://github.com/sgerrand/alpine-pkg-glibc/releases/download" \
    && curl -Ls ${ALPINE_GLIBC_REPO}/${GLIBC_VER}/glibc-${GLIBC_VER}.apk > /tmp/${GLIBC_VER}.apk \
    && apk add --allow-untrusted /tmp/${GLIBC_VER}.apk \
    && curl -Ls https://www.archlinux.org/packages/core/x86_64/gcc-libs/download > /tmp/gcc-libs.tar.xz \
    && mkdir /tmp/gcc \
    && tar -xf /tmp/gcc-libs.tar.xz -C /tmp/gcc \
    && mv /tmp/gcc/usr/lib/libgcc* /tmp/gcc/usr/lib/libstdc++* /usr/glibc-compat/lib \
    && strip /usr/glibc-compat/lib/libgcc_s.so.* /usr/glibc-compat/lib/libstdc++.so* \
    && curl -Ls https://github.com/AdoptOpenJDK/openjdk9-openj9-releases/releases/download/jdk-9%2B${OPENJ9_BUILD}/OpenJDK9-OPENJ9_x64_Linux_jdk-9.${OPENJ9_BUILD}.tar.gz > /tmp/jdk.tar.gz \
    && mkdir /opt \
    && tar -xf /tmp/jdk.tar.gz -C /opt \
    && rm -rf /opt/jdk-9+${OPENJ9_BUILD}/jmods \
    && apk del curl binutils \
    && rm -rf /tmp/${GLIBC_VER}.apk /tmp/gcc /tmp/gcc-libs.tar.xz /tmp/jdk.tar.gz /var/cache/apk/*

ENV JAVA_HOME  /opt/jdk-9+${OPENJ9_BUILD}
ENV PATH       ${PATH}:${JAVA_HOME}/bin
