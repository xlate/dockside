FROM xlate/wildfly:10.1.0.Final
MAINTAINER Michael Edgar <michael@xlate.io>

ENV MYSQL_CONNECTOR_VERSION 8.0.11

ADD https://repo1.maven.org/maven2/mysql/mysql-connector-java/${MYSQL_CONNECTOR_VERSION}/mysql-connector-java-${MYSQL_CONNECTOR_VERSION}.jar \
    ${WILDFLY_HOME}/standalone/deployments/mysql-connector-java.jar
