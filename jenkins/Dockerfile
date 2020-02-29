FROM openjdk

ENV APP_NAME=
ENV APP_VERSION=
WORKDIR /opt
COPY target/${APP_NAME}-${APP_VERSION}.jar
ENTRYPOINT ['java','-jar',"/opt/${APP_NAME}-${APP_VERSION}.jar"]