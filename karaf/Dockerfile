FROM xlate/openjdk
MAINTAINER Michael Edgar, www.xlate.io

ENV KARAF_VERSION 4.0.6
ENV INSTALL_DIR /opt
ENV KARAF_BASE ${INSTALL_DIR}/karaf

RUN curl http://archive.apache.org/dist/karaf/${KARAF_VERSION}/apache-karaf-${KARAF_VERSION}.tar.gz -o /tmp/karaf.tar.gz \
    && tar xzf /tmp/karaf.tar.gz -C /opt/ \
    && ln -s /opt/apache-karaf-${KARAF_VERSION} /opt/karaf \
    && rm /tmp/karaf.tar.gz

#RUN rm ${KARAF_BASE}/bin/setenv \
RUN rm ${KARAF_BASE}/etc/org.apache.karaf.features.cfg

RUN rm -rf /opt/karaf/deploy/README  \
    && sed -i 's/^\(.*rootLogger.*\)out/\1stdout/' /opt/karaf/etc/org.ops4j.pax.logging.cfg


#ADD setenv                        ${KARAF_BASE}/bin
ADD org.apache.karaf.features.cfg ${KARAF_BASE}/etc

#VOLUME [ "${KARAF_BASE}/data" ]

ENTRYPOINT ${KARAF_BASE}/bin/karaf server
EXPOSE 8181 8101
