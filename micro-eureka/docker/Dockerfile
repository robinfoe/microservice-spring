#FROM registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift:1.1
FROM registry.access.redhat.com/jboss-fuse-6/fis-java-openshift:2.0-9

MAINTAINER Robin Foe <rfoe@redhat.com>

ARG JAR_FILE
ARG BASE_DIR

USER root 

ENV JBOSS_IMAGE_NAME="Eureka Server" \
    JBOSS_IMAGE_VERSION="1.0" \
    JBOSS_IMAGE_RELEASE="1" \
    HOME="/home/jboss" \
    JAVA_TOOL_OPTIONS="-Duser.home=/home/jboss -Duser.name=jboss" 


LABEL name="$JBOSS_IMAGE_NAME" \
      version="$JBOSS_IMAGE_VERSION" \
      release="$JBOSS_IMAGE_RELEASE" \
      architecture="x86_64" \
      com.redhat.component="micro-eureka"
      

COPY scripts/launch.sh /deployments/launch.sh
#COPY ./target/$JAR_FILE /tmp/

COPY maven/$JAR_FILE /deployments
RUN chmod -R 755 /deployments/*
RUN chown -R jboss:root /deployments

USER jboss

CMD ["/deployments/launch.sh"]
EXPOSE 8761