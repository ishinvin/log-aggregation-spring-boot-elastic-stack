FROM --platform=$BUILDPLATFORM eclipse-temurin:17-jdk-jammy AS builder
# Set the working directory in the container
WORKDIR /app
# Gradle
COPY gradle gradle
COPY gradlew .
COPY build.gradle.kts .
COPY settings.gradle.kts .
# Copy the source code to the container
COPY src/ src/
# Build the application
RUN ./gradlew bootJar

FROM --platform=$BUILDPLATFORM eclipse-temurin:17-jre-jammy
# Set the working directory
WORKDIR /app
# Copy the JAR file from the builder stage
COPY --from=builder /app/build/libs/*.jar app.jar
# Set the active profile
ENV SPRING_PROFILES_ACTIVE=docker
# Set the command to run your Spring Boot application
CMD ["java", "-jar", "app.jar"]
