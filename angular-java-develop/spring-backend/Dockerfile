# Use Maven with JDK 17 base image
FROM maven:3.9.4-eclipse-temurin-17 as builder

# Set working directory
WORKDIR /app

# Copy the source code
COPY . .

# Package the Spring Boot app (skip tests for speed)
RUN mvn clean package -Dmaven.test.skip=true

# Use a lightweight JDK base image to run the app
FROM eclipse-temurin:17-jdk

# Set working directory
WORKDIR /app

# Copy the JAR from builder stage
COPY --from=builder /app/target/*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "app.jar"]

