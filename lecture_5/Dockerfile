FROM java:8-jdk as jdk_8

MAINTAINER Didilov Aleksey <didilov.aleksey@gmail.com>
LABEL Description="This image is used to show the Allure reposting"
LABEL Version="1.1.0"
ENV MAIN_JAR 'allure-docker-example-1.1.0.jar'
ENV GRADLE_VERSION 4.0
ENV MAIN_DIR /allure-docker-example

# Install dependencies
FROM jdk_8 as dependencies
RUN apt-get install -fy unzip git

# Install Gradle
FROM dependencies as gradle
RUN wget https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip gradle-${GRADLE_VERSION}-bin.zip && \
    mv gradle-${GRADLE_VERSION} /opt/ && \
    rm gradle-${GRADLE_VERSION}-bin.zip
ENV GRADLE_HOME /opt/gradle-${GRADLE_VERSION}
ENV PATH $PATH:$GRADLE_HOME/bin

# Install Allure CLI
FROM jdk_8 as allure
RUN wget https://github.com/allure-framework/allure-core/releases/download/allure-core-1.4.23/allure-commandline.zip && \
    unzip allure-commandline.zip

# Prepare jars
FROM gradle as jar
WORKDIR ${MAIN_DIR}
COPY . .
RUN ./gradlew

FROM allure
WORKDIR /app
COPY --from=jar ${MAIN_DIR}/build/libs .

#Run tests, generate and open report
CMD (java -jar ${MAIN_JAR} || echo "Failed tests") && \
    allure generate -o allure-report allure-result && \
    allure report open -p 80

