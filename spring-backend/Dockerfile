# Use the official OpenJDK image as a base
FROM openjdk:17-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the Spring Boot application JAR file
COPY target/your-app-name.jar app.jar

# Expose the port your Spring Boot application runs on
EXPOSE 8080

# Run the Spring Boot application
ENTRYPOINT ["java", "-jar", "app.jar"]
