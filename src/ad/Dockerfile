# Use platform-aware base image for building
FROM --platform=${BUILDPLATFORM} eclipse-temurin:21-jdk AS builder

# Set working directory in the image
WORKDIR /usr/local/app

# Copy build-related files from src/ad/
COPY src/ad/gradlew* src/ad/settings.gradle src/ad/build.gradle ./
COPY src/ad/gradle ./gradle

# Make gradlew executable and initialize
RUN chmod +x ./gradlew
RUN ./gradlew
RUN ./gradlew downloadRepos

# Copy full source code and proto files
COPY src/ad/ ./
COPY pb/ ./proto

# Re-ensure gradlew is executable in case overwritten
RUN chmod +x ./gradlew

# Build the distribution with proto source
RUN ./gradlew installDist -PprotoSourceDir=./proto

# ────────────────────────────────────────────────────────────

# Final runtime image
FROM eclipse-temurin:21-jre AS publisher

# Set runtime working directory
WORKDIR /usr/local/apps

# Copy the build artifacts from builder stage
COPY --from=builder /usr/local/app ./

# Set environment and expose port
ENV ADD_PORT=9099
EXPOSE ${ADD_PORT}

# Launch the service
ENTRYPOINT ["./build/install/opentelemetry-demo-ad/bin/Ad"]
