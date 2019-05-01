FROM java:8
VOLUME /tmp
ADD test.jar test.jar
RUN bash -c 'touch /test.jar'
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/test.jar"]