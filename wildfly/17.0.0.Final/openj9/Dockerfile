FROM adoptopenjdk/openjdk12-openj9:alpine-jre
LABEL maintainer="Michael Edgar, xlate.io" description="Java EE 8 Full & Web Distribution"

ENV WILDFLY_VERSION 17.0.0.Final
ENV WILDFLY_SHA1 50bf8c48d4faf27c530af6949a225b9f1428300e
ENV INSTALL_DIR /opt
ENV WILDFLY_HOME ${INSTALL_DIR}/wildfly
ENV DEPLOYMENT_DIR ${WILDFLY_HOME}/standalone/deployments/
ENV CONFIGURATION_DIR ${WILDFLY_HOME}/standalone/configuration

RUN apk add --virtual .build-dependencies --no-cache ca-certificates curl openssl binutils xz \
    && mkdir -vp ${INSTALL_DIR} \
    && cd ${INSTALL_DIR} \
    && echo "Downloading Wildfly" \
    && curl -Ls -O https://download.jboss.org/wildfly/${WILDFLY_VERSION}/wildfly-${WILDFLY_VERSION}.tar.gz \
    && sha1sum wildfly-${WILDFLY_VERSION}.tar.gz | grep ${WILDFLY_SHA1} \
    && tar xf wildfly-${WILDFLY_VERSION}.tar.gz \
    && rm wildfly-${WILDFLY_VERSION}.tar.gz \
    && ln -s wildfly-${WILDFLY_VERSION} ${WILDFLY_HOME} \
    && adduser -S serveradmin \
    && chown -R serveradmin:0 ${WILDFLY_HOME} \
    && chmod -R g+rw ${WILDFLY_HOME} \
    && apk del .build-dependencies

USER serveradmin
ENTRYPOINT ${WILDFLY_HOME}/bin/standalone.sh -b=0.0.0.0
EXPOSE 8080
