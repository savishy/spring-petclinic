# This Dockerfile creates a Docker Image for 
# Petclinic with internal DB. The only thing different is the fact that it uses
# a version of the JAR instrumented with Prometheus.
# This Docker Image can be viewed at:
# https://hub.docker.com/r/savishy/springboot-petclinic/

# JDK application 
FROM openjdk:8u131-jdk-alpine

# Labels allow for metadata and visibility
LABEL com.poc.maintainer="Vish"
LABEL com.poc.description="Petclinic Application 2.0.0 JAR with Prometheus Instrumentation"

VOLUME /app

# Application and configuration
ADD https://github.com/savishy/spring-petclinic/releases/download/v2.0.0-BUILD-SNAPSHOT/spring-petclinic-2.0.0.BUILD-SNAPSHOT.jar /app/petclinic.jar
ENV JAVA_OPTS=""

# Spring app opts
ENV SPRING_OPTS="--server.port=9080"
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -jar /app/petclinic.jar $SPRING_OPTS" ]
