FROM --platform=${BUILDPLATFORM} eclipse-temurin:21-jdk AS builder
WORKDIR /usr/local/app
COPY ./src/ad/gradlew* ./src/ad/settings.gradle ./src/ad/build.gradle ./
COPY ./src/ad/gradle ./gradle
RUN chmod +x ./gradlew
RUN ./gradlew
RUN ./gradlew downloadRepos
COPY ./src/ad/ ./
COPY ./pb/ ./proto
RUN chmod +x ./gradlew
RUN ./gradlew installDist -PprotoSourceDir=./proto

###############################################################################################################

FROM eclipse-temurin:21-jre AS publisher

WORKDIR /usr/local/apps

COPY --from=builder /usr/local/app ./

ENV ADD_PORT=9099s

ENTRYPOINT [ "./build/install/opentelemetry-demo-ad/bin/Ad" ]