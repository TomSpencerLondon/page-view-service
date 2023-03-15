FROM openjdk:8-jdk

EXPOSE 8081

ARG version

VOLUME /tmp
ADD maven/page-view-service-${version}.jar myapp.jar
RUN sh -c 'touch /page-view-service-${version}.jar'
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/myapp.jar"]
