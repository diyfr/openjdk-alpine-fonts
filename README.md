# openjdk-alpine with fonts

This is a repository for Java Docker base images used in various diyfr (French) projects, requiring fonts

OpenJdk 8/12/13 on alpine version, with fonts ttf-dejavu,ttf-ubuntu-font-family, TimeZone update capatibility and custom CA loader.  

Sample Dockerfile for you java app  in OpenJDK 8:  
```
FROM diyfr/openjdk-alpine-fonts:8
ENV LANG fr_FR.UTF-8
ENV TZ=Europe/Paris
ADD ./myCA.crt /usr/local/share/ca-certificates/myCA.crt
RUN update-ca-certificates 2>/dev/null || true
# Custom volumes
RUN mkdir /logs
RUN mkdir /config
# Define logs directory
VOLUME /logs
# Define application config file directory
VOLUME /config
EXPOSE 8081
COPY target/fr.diyfr.myapp*.jar fr.diyfr.myapp.jar
ENTRYPOINT ["java","-jar","/fr.diyfr.myapp.jar"]
```
