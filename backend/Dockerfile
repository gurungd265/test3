# ----------- Stage 1: Build -----------
FROM gradle:8.1.1-jdk17 AS build
COPY . /app
WORKDIR /app
RUN gradle build -x test

# ----------- Stage 2: Run -------------
FROM eclipse-temurin:17-jdk-alpine
EXPOSE 8080
COPY --from=build /app/build/libs/*.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
