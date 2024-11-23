# # Use the official OpenJDK image as a base
# FROM openjdk:17-jdk-slim

# # Set the working directory
# WORKDIR /app

# # Copy the Spring Boot application JAR file
# COPY target/demo-0.0.1-SNAPSHOT.jar backend.jar

# # Expose the port your Spring Boot application runs on
# EXPOSE 8080

# # Run the Spring Boot application
# ENTRYPOINT ["java", "-jar", "backend.jar"]

# Use Maven as a base image
FROM maven:3.9.4-eclipse-temurin-17

# Set the working directory
WORKDIR /app

# Copy the Maven project files
COPY . .

# Expose the port your Spring Boot application runs on
EXPOSE 8080

# Run the Spring Boot application using Maven
ENTRYPOINT ["mvn", "spring-boot:run"]
