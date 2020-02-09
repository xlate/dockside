FROM adoptopenjdk:13-jre-openj9
LABEL maintainer="Michael Edgar, xlate.io" description="Java EE 8 Full & Web Distribution"

ENV WILDFLY_VERSION 18.0.1.Final
ENV WILDFLY_SHA1 ef0372589a0f08c36b15360fe7291721a7e3f7d9
ENV INSTALL_DIR /opt
ENV WILDFLY_HOME ${INSTALL_DIR}/wildfly
ENV DEPLOYMENT_DIR ${WILDFLY_HOME}/standalone/deployments/
ENV CONFIGURATION_DIR ${WILDFLY_HOME}/standalone/configuration
# Ensure signals are forwarded to the JVM process correctly for graceful shutdown
ENV LAUNCH_JBOSS_IN_BACKGROUND true

RUN mkdir -vp ${INSTALL_DIR} \
    && cd ${INSTALL_DIR} \
    && echo "Downloading Wildfly" \
    && curl -Ls -O https://download.jboss.org/wildfly/${WILDFLY_VERSION}/wildfly-${WILDFLY_VERSION}.tar.gz \
    && sha1sum wildfly-${WILDFLY_VERSION}.tar.gz | grep ${WILDFLY_SHA1} \
    && tar xf wildfly-${WILDFLY_VERSION}.tar.gz \
    && rm wildfly-${WILDFLY_VERSION}.tar.gz \
    && ln -s wildfly-${WILDFLY_VERSION} ${WILDFLY_HOME} \
    && useradd jboss \
    && chown -R jboss:0 wildfly-${WILDFLY_VERSION} \
    && chmod -R g+rw wildfly-${WILDFLY_VERSION}

USER jboss

# Expose the ports we're interested in
EXPOSE 8080

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
