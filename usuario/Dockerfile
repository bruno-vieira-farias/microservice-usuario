# Build stage
FROM maven:3.6.0-jdk-8-slim AS build
WORKDIR /home/app
COPY pom.xml .
RUN mvn dependency:resolve

COPY src/ /home/app/src
RUN mvn -DUSUARIO_DB_HOST=host -DUSUARIO_DB_PORT=27018 package

# Package stage
FROM openjdk:8-jdk-alpine
COPY --from=build /home/app/target/*.jar /usr/local/lib/usuario.jar
EXPOSE 8085
ENTRYPOINT ["java", "-jar", "/usr/local/lib/usuario.jar"]