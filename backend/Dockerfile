# Stage 1: Build the application
FROM gradle:8.1.1-jdk17 AS build
COPY . /home/app
WORKDIR /home/app
RUN gradle build -x test

# Stage 2: Run the application
FROM eclipse-temurin:17-jdk-alpine
EXPOSE 8080
COPY --from=build /home/app/build/libs/*.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
