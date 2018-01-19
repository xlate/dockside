FROM openjdk:8-jre-alpine
MAINTAINER Michael Edgar <michael@xlate.io>

ENV INSTALL_DIR /opt
ENV WILDFLY_VERSION 10.1.0.Final
ENV WILDFLY_HOME ${INSTALL_DIR}/wildfly-$WILDFLY_VERSION

RUN apk add --no-cache bash gawk sed grep bc coreutils unzip curl

RUN curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.zip \
	&& unzip -q wildfly-$WILDFLY_VERSION.zip -d /opt/ \
    && rm wildfly-$WILDFLY_VERSION.zip

ENTRYPOINT ${WILDFLY_HOME}/bin/standalone.sh -b=0.0.0.0
EXPOSE 8080
