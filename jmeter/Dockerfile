# Dockerfile for ARM (aarch64) JMeter image
# FROM arm64v8/openjdk:11-jre-slim
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

### ⭐ Install JMeter Plugins Manager
RUN wget https://jmeter-plugins.org/get/ \
    -O ${JMETER_HOME}/lib/ext/jmeter-plugins-manager.jar

RUN wget https://search.maven.org/remotecontent?filepath=kg/apc/jmeter-plugins-manager/1.10/jmeter-plugins-manager-1.10.jar \
    -O ${JMETER_HOME}/lib/ext/jmeter-plugins-manager-1.10.jar

### ⭐ Command to install InfluxDB Backend Listener Plugin
RUN java -cp ${JMETER_HOME}/lib/ext/jmeter-plugins-manager.jar org.jmeterplugins.repository.PluginManagerCMD install jpgc-influxdb2-listener

# Set the working directory
WORKDIR ${JMETER_HOME}

# Default command: run JMeter in non-GUI mode
CMD ["jmeter", "-n"]
