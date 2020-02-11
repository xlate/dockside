FROM adoptopenjdk/openjdk13-openj9:alpine-jre
LABEL maintainer="Michael Edgar, xlate.io" description="Java EE 8 Full & Web Distribution"

ENV WILDFLY_VERSION 18.0.1.Final
ENV WILDFLY_SHA1 ef0372589a0f08c36b15360fe7291721a7e3f7d9
ENV INSTALL_DIR /opt
ENV WILDFLY_HOME ${INSTALL_DIR}/wildfly
ENV DEPLOYMENT_DIR ${WILDFLY_HOME}/standalone/deployments/
ENV CONFIGURATION_DIR ${WILDFLY_HOME}/standalone/configuration
# Ensure signals are forwarded to the JVM process correctly for graceful shutdown
ENV LAUNCH_JBOSS_IN_BACKGROUND true

RUN apk add --virtual .build-dependencies --no-cache ca-certificates curl openssl binutils xz \
    && mkdir -vp ${INSTALL_DIR} \
    && cd ${INSTALL_DIR} \
    && echo "Downloading Wildfly" \
    && curl -Ls -o wildfly.tar.gz https://download.jboss.org/wildfly/${WILDFLY_VERSION}/wildfly-${WILDFLY_VERSION}.tar.gz \
    && sha1sum wildfly.tar.gz | grep ${WILDFLY_SHA1} \
    && tar xf wildfly.tar.gz \
    && rm wildfly.tar.gz \
    && mv wildfly-${WILDFLY_VERSION} ${WILDFLY_HOME} \
    && adduser -S serveradmin \
    && chown -R serveradmin:0 ${WILDFLY_HOME} \
    && chmod -R g+rw ${WILDFLY_HOME} \
    && apk del .build-dependencies

USER serveradmin
CMD ["/opt/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
EXPOSE 8080
