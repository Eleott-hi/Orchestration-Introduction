FROM nginx:latest

WORKDIR /app

COPY wait-for-it.sh .
COPY ./nginx.conf /etc/nginx/nginx.conf

RUN apk add --no-cache bash; \
    chmod +x wait-for-it.sh

CMD ["./wait-for-it.sh", "-t", "120", "session-service:8081", "--", \
     "./wait-for-it.sh", "-t", "120", "gateway-service:8087", "--", \
     "nginx", "-g", "daemon off;"]
