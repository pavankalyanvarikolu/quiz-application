# Stage 1: Build stage
FROM maven:3.8.4-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Run stage
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=build /app/target/question-service-*.jar app.jar
COPY .env .env
ENV SPRING_APPLICATION_NAME=question-service
ENV SPRING_DATASOURCE_DRIVER_CLASS_NAME=org.postgresql.Driver
ENV SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5433/questiondb
ENV SPRING_DATASOURCE_USERNAME=postgres
ENV SPRING_DATASOURCE_PASSWORD=0000
ENV SPRING_JPA_HIBERNATE_DDL_AUTO=update
ENV SPRING_JPA_PROPERTIES_HIBERNATE_DIALECT=org.hibernate.dialect.PostgreSQLDialect
ENTRYPOINT ["java", "-jar", "app.jar"]
