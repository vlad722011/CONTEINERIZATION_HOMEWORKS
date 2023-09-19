# Курс - "Контейнеризация"
## Домашнее задание к семинару 5.
## Выполнил Бурсаев Владислав, группа 3775.


### Урок 5. Docker Compose и Docker Swarm.

#### Для работы docker-compose нужен файл-инструкция в формате yml. Имя файла -
 ``` docker-compose.yml ```

#### это значение по умолчанию для файла конфигурации, в случае если мы не укажем имя файла при запуске утилиты, будет задействоваи файл с таким именем.

* Итак, создадим файл-конфигурации:

```  nano docker-compose.yml ```

```   
version: '3'

services:
  db:
    image: mariadb
    restart: always
    environment:
      MARIADB_ROOT_PASSWORD: password
    volumes:
      - ./db:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin
    restart: always
    ports:
      - 8081:80

```

![yml_file](/Homework_5/Sourse/yml_file.png)

* Сохраним файл, и запустим контейнеры, описанные в файле:

``` docker-compose up -d ```

![done](/Homework_5/Sourse/docker_compose_up.png)


* Можем проверить, что созданы образы контейнеров, и из них собственно запущены сами контейнеры:

```  docker images ```

``` docker ps -a ```

![images](/Homework_5/Sourse/conteiners.png)

![images_and_conteiners](/Homework_5/Sourse/images_and_containers.png)


* Ну и собственно остается только проверить работоспособность  контейнеров. Откроем браузер:

```  localhost: 8081  ```

* Введем логин и пароль, и можем наблюдать работу наших контейнеров. База данных доступна и работает:

![firefox_1](/Homework_5/Sourse/firefox_1.png)

![firefox_2](/Homework_5/Sourse/firefox_2.png)

![firefox_3](/Homework_5/Sourse/firefox_3.png)

