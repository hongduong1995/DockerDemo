## Stage 1
FROM maven:ibmjava-alpine as stage1build

COPY . .

RUN mvn clean package

## Stage 2

FROM openjdk:8-alpine

COPY --from=stage1build /target/websocket-demo-0.0.1-SNAPSHOT.jar .

CMD java -Djava.security.egd=file:/dev/./urandom -jar websocket-demo-0.0.1-SNAPSHOT.jar
