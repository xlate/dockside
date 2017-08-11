FROM oraclelinux:7-slim AS build

ADD oracle-instantclient12.2-12.2.0.1.0-1.x86_64.tar.gz /tmp/

RUN yum -y install less /tmp/oracle-instantclient*-basiclite-*.rpm && \
    yum clean all && \
    rpm -i --nodeps $(find /tmp/ -name "oracle-instantclient*.rpm" -not -name "oracle-instantclient*-basiclite-*.rpm") && \
    rm -f /tmp/oracle-instantclient*.rpm && \
    echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient12.2.conf && \
    ldconfig

FROM scratch
MAINTAINER Michael Edgar <michael@xlate.io>
COPY --from=build / /
ENV PATH=$PATH:/usr/lib/oracle/12.2/client64/bin
