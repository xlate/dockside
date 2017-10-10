FROM alpine:3.6
MAINTAINER Michael Edgar <michael@xlate.io>

ENV INSTALL_DIR /opt
ENV WILDFLY_VERSION 11.0.0.CR1
ENV WILDFLY_HOME ${INSTALL_DIR}/wildfly-$WILDFLY_VERSION

RUN apk add --no-cache bash gawk sed grep bc coreutils unzip curl

RUN curl -O http://download.java.net/java/GA/jdk9/9/binaries/openjdk-9_linux-x64_bin.tar.gz
RUN tar xvf openjdk-9_linux-x64_bin.tar.gz -C /tmp \
 && /tmp/jdk-9/bin/jlink --module-path /tmp/jdk-9/jmods/ --add-modules java.se.ee --output=${INSTALL_DIR}/jdk-9/ \
 && rm openjdk-9_linux-x64_bin.tar.gz

## RUN curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.zip \
##  && unzip -q wildfly-$WILDFLY_VERSION.zip -d ${INSTALL_DIR}/ \
##  && rm wildfly-$WILDFLY_VERSION.zip \
##  && useradd wildfly \
##  && chown -R wildfly ${WILDFLY_HOME}/standalone

## USER wildfly
## ENTRYPOINT ${WILDFLY_HOME}/bin/standalone.sh -b=0.0.0.0
## EXPOSE 8080
