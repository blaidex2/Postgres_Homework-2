### Домашнее задание №2

## Описание/Пошаговая инструкция выполнения домашнего задания:

* создать ВМ с Ubuntu 20.04/22.04 или развернуть докер любым удобным способом

 ![image](https://user-images.githubusercontent.com/130083589/232549284-01aff99d-d541-4257-a5a0-81a198ec41b1.png)


* поставить на нем Docker Engine
> поставим докер

> -- https://docs.docker.com/engine/install/ubuntu/

>curl -fsSL https://get.docker.com -o get-docker.sh && sudo sh get-docker.sh && rm get-docker.sh && sudo usermod -aG docker $USER
>

![image](https://user-images.githubusercontent.com/130083589/232549511-58f8b55e-eb7f-4802-8806-cada7272fe70.png)

 

* сделать каталог /var/lib/postgres

![image](https://user-images.githubusercontent.com/130083589/232549606-decdcfdb-3553-4b0b-a767-2d88d1afb23e.png)


 
* развернуть контейнер с PostgreSQL 15 смонтировав в него /var/lib/postgresql

> 1. Создаем docker-сеть: 
>
> sudo docker network create pg-net

> 2. подключаем созданную сеть к контейнеру сервера Postgres:
>
> sudo docker run --name pg-server --network pg-net -e POSTGRES_PASSWORD=postgres -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres:15

![image](https://user-images.githubusercontent.com/130083589/232549708-45ad5bfa-87f2-483f-ad3d-38461688ccda.png)

 
* развернуть контейнер с клиентом postgres

> 3. Запускаем отдельный контейнер с клиентом в общей сети с БД: 
>
>sudo docker run -it --rm --network pg-net --name pg-client postgres:15 psql -h pg-server -U postgres
>

![image](https://user-images.githubusercontent.com/130083589/232549803-171d7bf6-e179-45a7-b3ab-787ba8baebf4.png)

 

* подключится из контейнера с клиентом к контейнеру с сервером и сделать таблицу с парой строк

![image](https://user-images.githubusercontent.com/130083589/232549851-f0dde6fa-3aaf-489a-bd21-ab719fdeb4aa.png)


* подключится к контейнеру с сервером с ноутбука/компьютера извне инстансов GCP/ЯО/места установки докера
 
 ![image](https://user-images.githubusercontent.com/130083589/232549896-b7704460-3eea-4e22-8951-f4fb24e6b4ea.png)


* удалить контейнер с сервером

![image](https://user-images.githubusercontent.com/130083589/232549934-fe122f38-069a-4764-970e-3a18d0dfb011.png)

 
* создать его заново
 
 ![image](https://user-images.githubusercontent.com/130083589/232549979-89524bb9-7727-418f-8734-a7f1d1b802e5.png)


* подключится снова из контейнера с клиентом к контейнеру с сервером
* проверить, что данные остались на месте
 
 ![image](https://user-images.githubusercontent.com/130083589/232550027-58600cf3-85af-4c99-af2c-489414277b4c.png)




