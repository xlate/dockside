FROM openjdk:alpine
MAINTAINER Michael Edgar <michael@xlate.io>

ENV INSTALL_DIR /opt
ENV SERVICEMIX_VERSION 7.0.0
ENV SERVICEMIX_BASE ${INSTALL_DIR}/servicemix

RUN apk add --no-cache bash gawk sed grep bc coreutils unzip

ADD http://archive.apache.org/dist/servicemix/servicemix-7/${SERVICEMIX_VERSION}/apache-servicemix-${SERVICEMIX_VERSION}.zip /opt/servicemix.zip

RUN unzip -q /opt/servicemix.zip -d /opt/ \
 && ln -s /opt/apache-servicemix-${SERVICEMIX_VERSION} ${SERVICEMIX_BASE} \
 && rm /opt/servicemix.zip

RUN sed -i 's/^\(.*rootLogger.*\)out/\1stdout/' ${SERVICEMIX_BASE}/etc/org.ops4j.pax.logging.cfg

VOLUME [ "${SERVICEMIX_BASE}/data" ]

ENTRYPOINT ${SERVICEMIX_BASE}/bin/servicemix server
EXPOSE 8181 8101
