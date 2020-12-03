FROM xqdocker/ubuntu-openjdk:jre-8
MAINTAINER abdurrahman.eker@detaysoft.com

ENV OPENFIRE_VERSION=4.6.0 \
    OPENFIRE_USER=openfire \
    OPENFIRE_DATA_DIR=/var/lib/openfire \
    OPENFIRE_LOG_DIR=/var/log/openfire \
    OPENFIRE_PLUGINS_DIR=/usr/share/openfire/plugins \
    OPENFIRE_LIB_DIR=/usr/share/openfire-custom-libs \
    APM_VERSION=1.14.0 \
    APM_JAR_DIR=/usr/share/elastic-apm-agent \
    APM_HOST=apm

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y sudo curl wget \
 && echo "Downloading openfire_${OPENFIRE_VERSION}_all.deb ..." \
 && wget --no-verbose "http://download.igniterealtime.org/openfire/openfire_${OPENFIRE_VERSION}_all.deb" -O /tmp/openfire_${OPENFIRE_VERSION}_all.deb \
 && dpkg -i /tmp/openfire_${OPENFIRE_VERSION}_all.deb || true

RUN mkdir "${APM_JAR_DIR}" \
 && wget --no-verbose "https://search.maven.org/remotecontent?filepath=co/elastic/apm/elastic-apm-agent/${APM_VERSION}/elastic-apm-agent-${APM_VERSION}.jar" -O /usr/share/elastic-apm-agent/elastic-apm-agent-${APM_VERSION}.jar

RUN mv /var/lib/openfire/plugins/admin /usr/share/openfire/plugin-admin \
 && rm -rf /tmp/openfire_${OPENFIRE_VERSION}_all.deb \
 && rm -rf /var/lib/apt/lists/*

COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh

EXPOSE 3478/tcp 3479/tcp 5222/tcp 5223/tcp 5229/tcp 5275/tcp 5276/tcp 5262/tcp 5263/tcp 7070/tcp 7443/tcp 7777/tcp 9090/tcp 9091/tcp
VOLUME ["${OPENFIRE_DATA_DIR}"]
VOLUME ["${OPENFIRE_PLUGINS_DIR}"]
VOLUME ["${OPENFIRE_LIB_DIR}"]

ENTRYPOINT ["/sbin/entrypoint.sh"]
