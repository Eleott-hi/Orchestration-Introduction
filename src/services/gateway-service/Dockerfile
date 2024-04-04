
# Stage 1: Build the application
FROM maven:3.6.3-jdk-8-slim AS builder

WORKDIR /app

COPY . .
RUN mvn -B -DskipTests clean package

# Stage 2: Run the application
FROM openjdk:8-jdk-alpine

ENV SESSION_SERVICE_HOST=session-service \
    SESSION_SERVICE_PORT=8081 \
    HOTEL_SERVICE_HOST=hotel-service \
    HOTEL_SERVICE_PORT=8082 \
    BOOKING_SERVICE_HOST=booking-service \
    BOOKING_SERVICE_PORT=8083 \
    PAYMENT_SERVICE_HOST=payment-service \
    PAYMENT_SERVICE_PORT=8084 \
    LOYALTY_SERVICE_HOST=loyalty-service \
    LOYALTY_SERVICE_PORT=8085 \
    REPORT_SERVICE_HOST=report-service \
    REPORT_SERVICE_PORT=8086

WORKDIR /app

COPY --from=builder /app/target/*.jar .
COPY wait-for-it.sh .

RUN apk add --no-cache bash; \
    chmod +x wait-for-it.sh

CMD ["./wait-for-it.sh", "-t", "120", "postgres-service:5432", "--", \
     "./wait-for-it.sh", "-t", "120", "rabbitmq-service:5672", "--", \
     "./wait-for-it.sh", "-t", "120", "session-service:8081", "--", \
     "./wait-for-it.sh", "-t", "120", "hotel-service:8082", "--", \
     "./wait-for-it.sh", "-t", "120", "booking-service:8083", "--", \
     "./wait-for-it.sh", "-t", "120", "payment-service:8084", "--", \
     "./wait-for-it.sh", "-t", "120", "loyalty-service:8085", "--", \
     "./wait-for-it.sh", "-t", "120", "report-service:8086", "--", \
     "java", "-jar", "gateway-service-0.0.1-SNAPSHOT.jar"]

