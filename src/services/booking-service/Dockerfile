
# Stage 1: Build the application
FROM maven:3.6.3-jdk-8-slim AS builder

WORKDIR /app

COPY . .
RUN mvn -B -DskipTests clean package

# Stage 2: Run the application
FROM openjdk:8-jdk-alpine

ENV POSTGRES_HOST=postgres-service \
    POSTGRES_PORT=5432 \
    POSTGRES_USER=postgres  \
    POSTGRES_PASSWORD="postgres" \
    POSTGRES_DB=reservations_db \
    RABBIT_MQ_HOST=rabbitmq-service \
    RABBIT_MQ_PORT=5672 \
    RABBIT_MQ_USER=guest \
    RABBIT_MQ_PASSWORD=guest \
    RABBIT_MQ_QUEUE_NAME=messagequeue \
    RABBIT_MQ_EXCHANGE=messagequeue-exchange \
    HOTEL_SERVICE_HOST=hotel-service \
    HOTEL_SERVICE_PORT=8082 \
    PAYMENT_SERVICE_HOST=payment-service \
    PAYMENT_SERVICE_PORT=8084 \
    LOYALTY_SERVICE_HOST=loyalty-service \
    LOYALTY_SERVICE_PORT=8085

WORKDIR /app

COPY --from=builder /app/target/*.jar .
COPY wait-for-it.sh .

RUN apk add --no-cache bash; \
    chmod +x wait-for-it.sh

CMD ["./wait-for-it.sh", "-t", "120", "postgres-service:5432", "--", \
     "./wait-for-it.sh", "-t", "120", "rabbitmq-service:5672", "--", \
     "./wait-for-it.sh", "-t", "120", "hotel-service:8082", "--", \
     "./wait-for-it.sh", "-t", "120", "payment-service:8084", "--", \
     "./wait-for-it.sh", "-t", "120", "loyalty-service:8085", "--", \
     "java", "-jar", "booking-service-0.0.1-SNAPSHOT.jar"]

