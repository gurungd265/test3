# ----------- Stage 1: Build -----------
FROM gradle:8.1.1-jdk21 AS build

ENV GRADLE_USER_HOME=/home/gradle/.gradle
WORKDIR /app

# Only copy files necessary for dependency resolution first
COPY build.gradle settings.gradle /app/
COPY src /app/src

# Build without tests and no Gradle daemon
RUN gradle build -x test --no-daemon

# ----------- Stage 2: Run -------------
FROM eclipse-temurin:21-jdk-alpine
EXPOSE 8080

COPY --from=build /app/build/libs/*.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
