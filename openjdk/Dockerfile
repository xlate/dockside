FROM centos:7
MAINTAINER Michael Edgar, www.xlate.io

RUN yum update -y \
  && yum -y install less java-1.8.0-openjdk-devel unzip \
  && yum clean all

ENV JAVA_HOME /usr/lib/jvm/java-1.8.0
ENV PATH "$PATH":/${JAVA_HOME}/bin:.:
