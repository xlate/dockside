FROM openjdk:8-jre-alpine
MAINTAINER Michael Edgar <michael@xlate.io>

ENV WILDFLY_VERSION 12.0.0.Final
ENV WILDFLY_SHA1 b2039cc4979c7e50a0b6ee0e5153d13d537d492f
ENV WILDFLY_HOME /opt/wildfly

RUN apk add --virtual .build-dependencies --no-cache ca-certificates curl openssl binutils xz \
    && mkdir -p /opt \
    && curl -Ls -O https://download.jboss.org/wildfly/${WILDFLY_VERSION}/wildfly-${WILDFLY_VERSION}.tar.gz \
    && sha1sum wildfly-${WILDFLY_VERSION}.tar.gz | grep ${WILDFLY_SHA1} \
    && tar xf wildfly-${WILDFLY_VERSION}.tar.gz \
    && rm wildfly-${WILDFLY_VERSION}.tar.gz \
    && mv wildfly-${WILDFLY_VERSION} ${WILDFLY_HOME} \
    && adduser -S wildfly \
    && chown -R wildfly ${WILDFLY_HOME}/standalone \
    && apk del .build-dependencies

USER wildfly

EXPOSE 8080

CMD ["/opt/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
