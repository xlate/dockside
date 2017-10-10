FROM xlate/openj9

#ENV OPENLIBERTY_VERSION 17.0.0.3
#ENV OPENLIBERTY_SHA 528e393e0b240ebbedb91d25402e22297c6d56ec

# Install Open Liberty
RUN apk --update add --no-cache binutils curl grep pcre unzip \
    && NIGHTLY_VERSION=`curl -s https://public.dhe.ibm.com/ibmdl/export/pub/software/openliberty/runtime/nightly/info.json | grep -PohA 1 '(?<=")([^"]+)(?=")' | tail -1` \
    && NIGHTLY_FILENAME=`curl -Ls https://public.dhe.ibm.com/ibmdl/export/pub/software/openliberty/runtime/nightly/${NIGHTLY_VERSION}/info.json | grep -PohA 1 '"[^"]+"\s*:\s*"[^"]+"' | grep driver_location | awk -F':' '{print $2}' | grep -PohA 1 '(?<=")([^"]+)(?=")'` \
    && mkdir -p /tmp/ol \
    && curl -Ls https://public.dhe.ibm.com/ibmdl/export/pub/software/openliberty/runtime/nightly/${NIGHTLY_VERSION}/${NIGHTLY_FILENAME} -H "User-Agent: UA-Open-Liberty-Docker" > /tmp/ol/ol.zip \
    && echo "$OPENLIBERTY_SHA /tmp/ol/ol.zip" > /tmp/ol/ol.zip.sha1 \
    && unzip -q /tmp/ol/ol.zip -d /opt/ol \
    && apk del curl binutils unzip \
    && rm -rf /tmp/ol
# TODO && sha1sum -c /tmp/wlp.zip.sha1 \

# Set Path Shortcuts
ENV PATH=/opt/ol/wlp/bin:$PATH \
    LOG_DIR=/logs \
    WLP_OUTPUT_DIR=/opt/ol/wlp/output

COPY docker-server /opt/ol/docker/

# Configure Open Liberty
RUN mkdir /logs \
 && ln -s $WLP_OUTPUT_DIR/defaultServer /output \
 && ln -s /opt/ol/wlp/usr/servers/defaultServer /config \
 && /opt/ol/wlp/bin/server create \
 && rm -rf $WLP_OUTPUT_DIR/.classCache /output/workarea \
 && chmod +x /opt/ol/docker/docker-server

COPY server.xml /config

EXPOSE 9080 9443

CMD ["/opt/ol/docker/docker-server", "run", "defaultServer"]
