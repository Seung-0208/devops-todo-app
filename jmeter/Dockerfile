FROM eclipse-temurin:11-jre

# Set JMeter version and environment variables
ENV JMETER_VERSION=5.4.1
ENV JMETER_HOME=/opt/apache-jmeter-${JMETER_VERSION}
ENV PATH=${JMETER_HOME}/bin:$PATH

# Install required packages (wget, unzip)
RUN apt-get update && \
    apt-get install -y wget unzip && \
    rm -rf /var/lib/apt/lists/*

# Download and extract Apache JMeter
RUN wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz && \
    tar -xzf apache-jmeter-${JMETER_VERSION}.tgz -C /opt/ && \
    rm apache-jmeter-${JMETER_VERSION}.tgz

# Set the working directory
WORKDIR ${JMETER_HOME}

# Install JMeter Plugins Manager and the InfluxDB backend plugin
# The Plugins Manager jar is provided by https://jmeter-plugins.org/get/
# Then use the Plugin Manager CLI to install the `jpgc-influxdb-backend` plugin.
RUN wget -O /tmp/jmeter-plugins-manager.jar https://jmeter-plugins.org/get/ && \
    mv /tmp/jmeter-plugins-manager.jar ${JMETER_HOME}/lib/ext/ && \
    java -cp ${JMETER_HOME}/lib/ext/jmeter-plugins-manager.jar \
        org.jmeterplugins.repository.PluginManagerCMDInstaller install jpgc-influxdb-backend && \
    rm -f /tmp/jmeter-plugins-manager.jar

# Default command: run JMeter in non-GUI mode
CMD ["jmeter", "-n"]
