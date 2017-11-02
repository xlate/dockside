FROM openjdk:8-jre-alpine
MAINTAINER Michael Edgar <michael@xlate.io>

ENV WILDFLY_VERSION 11.0.0.CR1
ENV WILDFLY_HOME /opt/wildfly-$WILDFLY_VERSION

RUN apk --update add --no-cache ca-certificates curl openssl binutils xz \
    && mkdir -p /opt \
    && curl -Ls -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-${WILDFLY_VERSION}.tar.gz \
    && tar xf wildfly-${WILDFLY_VERSION}.tar.gz -C /opt \
    && adduser -S wildfly \
    && chown -R wildfly ${WILDFLY_HOME}/standalone \
    && apk del curl binutils xz \
    && rm wildfly-${WILDFLY_VERSION}.tar.gz

USER wildfly
ENTRYPOINT ${WILDFLY_HOME}/bin/standalone.sh -b=0.0.0.0
EXPOSE 8080
