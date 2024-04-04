
# Part 1. Запуск нескольких docker-контейнеров с использованием docker compose


![img](misc/images/ex01_image_sizes.png)
![img](misc/images/ex01_book_hotel.png)
![img](misc/images/ex01_get_balance.png)
![img](misc/images/ex01_get_hotel.png)
![img](misc/images/ex01_get_hotels.png)
![img](misc/images/ex01_login.png)


## Part 2. Создание виртуальных машин

![img](misc/images/ex02_vagrant.png)

## Part 3. Создание простейшего docker swarm

1) Модифицировать Vagrantfile для создания трех машин: manager01, worker01, worker02. Написать shell-скрипты для установки docker внутрь машин, инициализации и подключения к docker swarm. Помощь с docker swarm материалах.
![img](misc/images/ex03_machines.png)
![img](misc/images/ex03_docker_swarm.png)

2) Загрузить собранные образы на docker hub и модифицировать docker-compose файл для подгрузки расположенных на docker hub образов.
![img](misc/images/ex03_docker_images_before.png)
![img](misc/images/ex03_docker_images_after.png)
![img](misc/images/ex03_container_distribution.png)

3) Установить отдельным стеком Portainer внутри кластера. В отчете отобразить визуализацию распределения задач по узлам с помощью Portainer.

![img](misc/images/ex03_portainer.png)
![img](misc/images/ex03_portainer_swarm.png)
![img](misc/images/ex03_portainer_distribution.png)