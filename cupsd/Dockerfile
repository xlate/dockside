FROM ubuntu:17.10
MAINTAINER Michael Edgar <michael@xlate.io>

RUN apt update && \
    apt-get install \
            --assume-yes \
            --no-install-recommends \
            cups \
            cups-bsd \
            printer-driver-all && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

#COPY cupsd.conf /etc/cups/
#COPY TEXT.ppd   /usr/share/ppd/custom/
#COPY text       /usr/lib/cups/backend
#RUN chmod 0755 /usr/lib/cups/backend/text

## RUN useradd \
##       --groups=lp,lpadmin \
##       --create-home \
##       --home-dir=/home/print \
##       print && \
##     mkdir -p /etc/cups/ssl && \
##     chown root:lp /etc/cups/ssl && \
##     chmod 0700 /etc/cups/ssl && \
##     mkdir -p /run/cups && \
##     mkdir -p /var/cache/cups && \
##     mkdir -p /var/log/cups && \
##     mkdir -p /var/spool/cups && \
##     chown -R root:lpadmin /run/cups \
##                           /var/cache/cups \
##                           /var/log/cups \
##                           /var/spool/cups

EXPOSE 631

#USER print
CMD [ "/usr/sbin/cupsd", "-f" ]
