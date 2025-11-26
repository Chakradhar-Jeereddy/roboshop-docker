FROM maven:3.9.11 as build
WORKDIR /app/server
COPY pom.xml .
COPY src ./src 
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app/server
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
COPY --from=build --chown=roboshop:roboshop /app/server/shipping.jar .
USER roboshop
ENTRYPOINT [ "java","-jar","shipping.jar" ]


# FROM maven:3.9.11
# EXPOSE 8080
# WORKDIR /app/server
# COPY pom.xml .
# COPY src ./src 
# RUN mvn clean package
# RUN mv target/shipping-1.0.jar shipping.jar 
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD [ "java","-jar","shipping.jar" ]
