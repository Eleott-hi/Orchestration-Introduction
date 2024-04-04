DB_CONTAINER_NAME := postgres-service
SERVICES := session-service booking-service gateway-service hotel-service loyalty-service payment-service report-service

ifeq ($(shell uname -s),Darwin)
	SERVICES_IMAGES := src_session-service src_booking-service src_gateway-service src_hotel-service src_loyalty-service src_payment-service src_report-service
else
	SERVICES_IMAGES := src-session-service src-booking-service src-gateway-service src-hotel-service src-loyalty-service src-payment-service src-report-service
endif

all: vagrant_down vagrant_up u p

docker_compose_up:
	docker compose up

clean_db:
	-docker stop $(DB_CONTAINER_NAME)
	-docker rm $(DB_CONTAINER_NAME)

clean:
	-docker rm $(SERVICES)
	-docker rmi $(SERVICES_IMAGES)

vagrant_up:
	vagrant up --provision-with=shell

vagrant_down:
	vagrant halt
	vagrant destroy -f
p:
	vagrant ssh manager01 -c "sudo docker stack deploy -c /vagrant/portainer-agent-stack.yml portainer"

c:
	vagrant ssh manager01 -c "sudo docker stack ps devops7_services"

u:
	vagrant ssh manager01 -c "sudo docker stack deploy -c /vagrant/docker-compose.yml devops7_services"

d:
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_gateway-service"
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_booking-service"
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_report-service"
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_session-service"
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_payment-service"
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_loyalty-service"
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_hotel-service"
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_rabbitmq-service"
	vagrant ssh manager01 -c "sudo docker service rm devops7_services_postgres-service"

.PHONY: manager
manager:
	vagrant ssh manager01

.PHONY: worker1
worker1:
	vagrant ssh worker01

.PHONY: worker2
worker2:
	vagrant ssh worker02

tag:
	docker tag src_nginx-service 			eleott/nginx_service:dev0ps7
	docker tag src_report-service 			eleott/report_service:dev0ps7
	docker tag src_session-service 			eleott/session_service:dev0ps7
	docker tag src_payment-service 			eleott/payment_service:dev0ps7
	docker tag src_loyalty-service 			eleott/loyalty_service:dev0ps7
	docker tag src_hotel-service 			eleott/hotel_service:dev0ps7
	docker tag src_booking-service 			eleott/booking_service:dev0ps7
	docker tag src_gateway-service 			eleott/gateway_service:dev0ps7
#	docker tag rabbitmq:3-management-alpine eleott/rabbitmq_service:dev0ps7
#	docker tag src_postgres-service			eleott/postgres_service:dev0ps7

push:
	docker push eleott/report_service:dev0ps7
	docker push eleott/session_service:dev0ps7
	docker push eleott/payment_service:dev0ps7
	docker push eleott/loyalty_service:dev0ps7
	docker push eleott/hotel_service:dev0ps7
	docker push eleott/booking_service:dev0ps7
	docker push eleott/gateway_service:dev0ps7
#	docker push eleott/nginx_service:dev0ps7
#	docker push eleott/rabbitmq_service:dev0ps7
#	docker push eleott/postgres_service:dev0ps7