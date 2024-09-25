FROM maven:3.8.1-openjdk-11 as build-backend
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Build final image
FROM openjdk:11-jre-slim
WORKDIR /app

# Copy backend jar
COPY --from=build-backend /app/target/backend-1.0-SNAPSHOT.jar /app/backend.jar

# Expose port for Java backend
EXPOSE 8080

# Start the backend server
ENTRYPOINT ["java", "-jar", "/app/backend.jar"]
