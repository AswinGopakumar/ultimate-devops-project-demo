FROM eclipse-temurin:21-jdk AS build

WORKDIR /usr/src/app

COPY gradlew* build.gradle settings.gradle .
COPY ./gradle ./gradle

RUN chmod +x ./gradlew
	
COPY . .
RUN ./gradlew installDist -PprotoSourceDir=/usr/src/app/pb


FROM eclipse-temurin:21-jre AS release

WORKDIR /usr/src/app
COPY --from=build usr/src/app ./

ENV AD_PORT=9099
ENV FEATURE_FLAG_GRPC_SERVICE_ADDR=featureflagservice:50053

ENTRYPOINT ["./build/install/opentelemetry-demo-ad/bin/Ad"]
