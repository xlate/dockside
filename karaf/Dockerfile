FROM xlate/openjdk
MAINTAINER Michael Edgar, www.xlate.io

ENV KARAF_VERSION 4.0.6
ENV INSTALL_DIR /opt
ENV KARAF_BASE ${INSTALL_DIR}/apache-karaf-${KARAF_VERSION} 

RUN curl -O http://archive.apache.org/dist/karaf/${KARAF_VERSION}/apache-karaf-${KARAF_VERSION}.zip \
    && mkdir -p ${INSTALL_DIR} \
    && unzip apache-karaf-${KARAF_VERSION}.zip -d ${INSTALL_DIR} \
    && rm apache-karaf-${KARAF_VERSION}.zip \
    && rm ${KARAF_BASE}/bin/setenv \
    && rm ${KARAF_BASE}/etc/org.apache.karaf.features.cfg \
    && rm ${KARAF_BASE}/etc/org.ops4j.pax.logging.cfg

ADD setenv                        ${KARAF_BASE}/bin
ADD org.apache.karaf.features.cfg ${KARAF_BASE}/etc
ADD org.ops4j.pax.logging.cfg     ${KARAF_BASE}/etc

VOLUME [ "${KARAF_BASE}/data" ]

ENTRYPOINT ${KARAF_BASE}/bin/karaf
EXPOSE 1099 8101 8181
