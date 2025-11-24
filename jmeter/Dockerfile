FROM eclipse-temurin:11-jre

ENV JMETER_VERSION=5.4.1
ENV JMETER_HOME=/opt/apache-jmeter-${JMETER_VERSION}
ENV PATH=${JMETER_HOME}/bin:$PATH

RUN apt-get update && \
    apt-get install -y wget unzip && \
    rm -rf /var/lib/apt/lists/*

# Install JMeter
RUN wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz && \
    tar -xzf apache-jmeter-${JMETER_VERSION}.tgz -C /opt/ && \
    rm apache-jmeter-${JMETER_VERSION}.tgz

### ⭐ Copy Plugins Manager JAR and cmdrunner JAR
COPY plugins/jmeter-plugins-manager-1.10.jar ${JMETER_HOME}/lib/ext/jmeter-plugins-manager.jar
COPY plugins/cmdrunner-2.2.jar ${JMETER_HOME}/lib/cmdrunner-2.2.jar

### ⭐ Install InfluxDB plugin using PluginManagerCMD
RUN java -cp "${JMETER_HOME}/lib/ext/jmeter-plugins-manager.jar:${JMETER_HOME}/lib/cmdrunner-2.2.jar" \
    org.jmeterplugins.repository.PluginManagerCMD install jpgc-influxdb

WORKDIR ${JMETER_HOME}

CMD ["jmeter", "-n"]
