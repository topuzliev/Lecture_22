FROM openjdk

ENV APP_NAME=
WORKDIR /opt
COPY target/${APP_NAME}
ENTRYPOINT ['java','-jar',"/opt/${APP_NAME}"]