#
# Build
#
FROM debian:10 AS build

RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-transport-https ca-certificates wget gnupg && \
    apt-get install -y openjdk-11-jdk && \
    apt-get install -y maven

WORKDIR /opt/shipping

COPY pom.xml .
RUN mvn dependency:resolve

COPY src ./src
RUN mvn package

#
# Run
#
FROM openjdk:8-jdk

EXPOSE 8080

WORKDIR /opt/shipping

ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar" ]

