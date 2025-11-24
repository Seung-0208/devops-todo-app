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

### ⭐ Install Plugins Manager (정식 방식)
RUN wget https://jmeter-plugins.org/get/ -O ${JMETER_HOME}/lib/ext/jmeter-plugins-manager.jar

### ⭐ Install cmdrunner (필수)
RUN wget https://repo1.maven.org/maven2/kg/apc/cmdrunner/2.2/cmdrunner-2.2.jar \
    -O ${JMETER_HOME}/lib/cmdrunner-2.2.jar

### ⭐ Install InfluxDB Backend Listener plugin with PluginManagerCMD
RUN java -cp "${JMETER_HOME}/lib/ext/jmeter-plugins-manager-1.11.jar:${JMETER_HOME}/lib/cmdrunner-2.2.jar" \
    org.jmeterplugins.repository.PluginManagerCMD install jpgc-influxdb

# Set the working directory
WORKDIR ${JMETER_HOME}

# Default command: run JMeter in non-GUI mode
CMD ["jmeter", "-n"]
