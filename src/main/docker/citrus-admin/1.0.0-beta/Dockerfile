FROM consol/citrus
MAINTAINER citrusframework.org <citrus-dev-l@consol.de>

ENV BUILD_DATE=2017-02-20
ENV BUILD_VERSION=1.0.1

ENV CITRUS_ADMIN_VERSION=1.0.0-beta-4

EXPOSE 8080

RUN mkdir -p /opt/citrus-admin \
  && curl https://labs.consol.de/maven/repository/com/consol/citrus/citrus-admin-web/${CITRUS_ADMIN_VERSION}/citrus-admin-web-${CITRUS_ADMIN_VERSION}.jar \
    -o /opt/citrus-admin/citrus-admin-web.jar \
  && chmod 444 /opt/citrus-admin/citrus-admin-web.jar

CMD mvn clean install && java -Dproject.home=${APP_DIR} -jar /opt/citrus-admin/citrus-admin-web.jar