FROM consol/citrus
MAINTAINER citrusframework.org <citrus-dev-l@consol.de>

ENV BUILD_DATE=2017-02-06
ENV BUILD_VERSION=1.0.0

EXPOSE 8080

RUN mkdir -p /opt/citrus-admin
COPY citrus-admin-web.jar /opt/citrus-admin/citrus-admin-web.jar
RUN chmod 444 /opt/citrus-admin/citrus-admin-web.jar

CMD mvn clean install && java -Dproject.home=${APP_DIR} -jar /opt/citrus-admin/citrus-admin-web.jar