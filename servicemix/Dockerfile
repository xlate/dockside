FROM openjdk:8-jre-alpine
MAINTAINER Michael Edgar <michael@xlate.io>

ENV INSTALL_DIR /opt
ENV SERVICEMIX_MAJOR 7
ENV SERVICEMIX_MINOR 0
ENV SERVICEMIX_MICRO 1
ENV SERVICEMIX_VERSION "${SERVICEMIX_MAJOR}.${SERVICEMIX_MINOR}.${SERVICEMIX_MICRO}"
ENV SERVICEMIX_BASE ${INSTALL_DIR}/servicemix

RUN apk add --virtual .build-dependencies --no-cache sed unzip curl \
 && curl -o apache-servicemix-${SERVICEMIX_VERSION}.zip -L http://archive.apache.org/dist/servicemix/servicemix-${SERVICEMIX_MAJOR}/${SERVICEMIX_VERSION}/apache-servicemix-${SERVICEMIX_VERSION}.zip \
 && unzip -q apache-servicemix-${SERVICEMIX_VERSION}.zip -d /opt/ \
 && ln -s /opt/apache-servicemix-${SERVICEMIX_VERSION} ${SERVICEMIX_BASE} \
 && rm apache-servicemix-${SERVICEMIX_VERSION}.zip \
 && rm -rf ${SERVICEMIX_BASE}/examples \
 && sed -i 's/^\(.*rootLogger.*\)out/\1stdout/' ${SERVICEMIX_BASE}/etc/org.ops4j.pax.logging.cfg \
 && apk del .build-dependencies

VOLUME [ "${SERVICEMIX_BASE}/data" ]

# Due to bug described in https://issues.apache.org/jira/browse/KARAF-4771
# it is necessary to remove the instance.properties file when starting the
# container.
ENTRYPOINT rm -f ${SERVICEMIX_BASE}/instances/instance.properties && ${SERVICEMIX_BASE}/bin/servicemix server
EXPOSE 1099 8101 8181 44444 61616
