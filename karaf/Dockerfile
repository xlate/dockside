FROM openjdk:alpine
MAINTAINER Michael Edgar <michael@xlate.io>

ENV INSTALL_DIR /opt
ENV KARAF_VERSION 4.0.8
ENV KARAF_BASE ${INSTALL_DIR}/karaf

RUN apk add --no-cache bash gawk sed grep bc coreutils unzip

ADD http://archive.apache.org/dist/karaf/${KARAF_VERSION}/apache-karaf-${KARAF_VERSION}.zip /opt/karaf.zip

RUN unzip -q /opt/karaf.zip -d /opt/ \
 && ln -s /opt/apache-karaf-${KARAF_VERSION} ${KARAF_BASE} \
 && rm /opt/karaf.zip

RUN sed -i 's/^\(.*rootLogger.*\)out/\1stdout/' ${KARAF_BASE}/etc/org.ops4j.pax.logging.cfg

VOLUME [ "${KARAF_BASE}/data" ]

ENTRYPOINT ${KARAF_BASE}/bin/karaf server
EXPOSE 8181 8101
