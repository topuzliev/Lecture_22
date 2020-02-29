FROM openjdk

ARG APP_NAME=
ARG APP_VERSION=
WORKDIR /opt
COPY target/${APP_NAME}-${APP_VERSION}.jar
ENTRYPOINT ['java','-jar',"/opt/${APP_NAME}-${APP_VERSION}.jar"]