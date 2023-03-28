# Java version: 17
ARG VARIANT=17
FROM mcr.microsoft.com/vscode/devcontainers/java:${VARIANT}

# Install Maven
ARG MAVEN_VERSION="3.8.7"
RUN su vscode -c "source /usr/local/sdkman/bin/sdkman-init.sh && sdk install maven \"${MAVEN_VERSION}\""

FROM maven:3.8.5-eclipse-temurin-17-alpine AS build
RUN mkdir -p /app
WORKDIR /app
COPY pom.xml /app
COPY src /app/src
RUN mvn -B package --file pom.xml -DskipTests
# Fetch the Java sdk image
FROM eclipse-temurin:17-jdk-alpine
# Expose port 8080
EXPOSE 8080
COPY --from=build /app/target/*jar devops-demo-1.0.jar
ENTRYPOINT ["java","-jar","devops-demo-1.0.jar"]
