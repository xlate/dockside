FROM adoptopenjdk/openjdk11-openj9:jre-11.0.2.9_openj9-0.12.1-alpine
LABEL maintainer="Michael Edgar, xlate.io" description="Java EE 8 Full & Web Distribution"

ENV WILDFLY_VERSION 16.0.0.Final
ENV WILDFLY_SHA1 287c21b069ec6ecd80472afec01384093ed8eb7d
ENV INSTALL_DIR /opt
ENV WILDFLY_HOME ${INSTALL_DIR}/wildfly-${WILDFLY_VERSION}
ENV DEPLOYMENT_DIR ${WILDFLY_HOME}/standalone/deployments/
ENV CONFIGURATION_DIR ${WILDFLY_HOME}/standalone/configuration

RUN apk add --virtual .build-dependencies --no-cache ca-certificates curl openssl binutils xz \
    && mkdir -vp ${INSTALL_DIR} \
    && cd ${INSTALL_DIR} \
    && echo "Downloading Wildfly" \
    && curl -Ls -O https://download.jboss.org/wildfly/${WILDFLY_VERSION}/wildfly-${WILDFLY_VERSION}.tar.gz \
    && sha1sum ${WILDFLY_HOME}.tar.gz | grep ${WILDFLY_SHA1} \
    && tar xf ${WILDFLY_HOME}.tar.gz \
    && rm ${WILDFLY_HOME}.tar.gz \
    && adduser -S serveradmin \
    && chown -R serveradmin:0 ${WILDFLY_HOME} \
    && chmod -R g+rw ${WILDFLY_HOME} \
    && apk del .build-dependencies

USER serveradmin
ENTRYPOINT ${WILDFLY_HOME}/bin/standalone.sh -b=0.0.0.0
EXPOSE 8080
