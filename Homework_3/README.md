# Курс - "Контейнеризация"
## Домашнее задание к семинару 3.
## Выполнил Бурсаев Владислав, группа 3775.


### Установка DOCKER.

* Для того, чтобы установить Docker в систему, в терминале поочередно выполняем следующие команды:

#### для обновления списка пакетов

``` sudo apt update ```

#### установливаем пакеты, которые позволят использовать репозиторий по HTTPS:

``` sudo apt install apt-transport-https ca-certificates curl software-properties-common ```

#### добавляем официальный GPG-ключ Docker:

``` curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg ```

#### добавляем репозиторий Docker к списку источников пакетов:

``` echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null ```

#### обновляем список пакетов, чтобы включить информацию о пакетах Docker из добавленного репозитория:

``` sudo apt update  ```

#### устанваливаем Docker:

``` sudo apt install docker-ce  ```

#### добавляем нашего пользователя в группу docker, чтобы избежать использования sudo для запуска Docker команд:

``` sudo usermod -aG docker $USER  ```

#### добавляем нашего пользователя в группу docker, чтобы избежать использования sudo для запуска Docker команд:

``` sudo usermod -aG docker $USER  ```

``` newgrp docker  ```

#### перезагружаем систему, чтобы применить изменения в текущем сеансе.

#### Теперь Мы готовы использовать Docker через терминал. Можем проверить, что Docker успешно установлен выполнив команду:

``` docker --version   ```

![Docker_version](/Homework_3/Source/docker_version.png)

* Запускаем контейнер с использованием образа "cowsay".

``` docker run docker/whalesay cowsay Hello, Docker! ```

![Docker_cowsay](/Homework_3/Source/docker_cowsay.png)

## Tестируем Docker.

* Управление контейнерами и образами с помощью утилиты docker

``` docker run hello-world ```

![Hello_world](/Homework_3/Source/hello_world.png)

#### Как видно на скриншоте, после создания и запуска контейнера, он выполнил приветствие и завершил свою работу.

* теперь создадим и запустим другой контейнер и подключимся к нему:

``` docker run -it ubuntu bash ```

![ubuntu](/Homework_3/Source/ubuntu.png)

#### После создания и запуска контейнера он не завершился, а остался работать, т.к. мы подключены к терминалу в интерактивном режиме, и можем выполнять различные команды(например ls)

![Ubuntu_in_docker](/Homework_3/Source/ubuntu_in_docker.png)

* после выхода из консоли контейнера, он остановится, т.к. основной процесс в нашем случае оболочка bash завершит свою работу.

![stop_conteiner](/Homework_3/Source/stop_ubuntu_conteiner.png)

* При каждом повторном запуске команды docker run создаётся и запускается новый контейнер.

![docker_run_restart](/Homework_3/Source/docker_run_restart.png)

* для подключения к запущенному контейнеру можно воспользоваться командой docker exec, передав в качестве аргументов имя или ID контейнера, и команду которую мы хотим запустить, в нашем случае оболочку bash

![docker_exec](/Homework_3/Source/starting_an_existing_container.png)

* для остановки контейнера воспользуемся командой docker stop, передав в качестве аргумента имя или ID контейнера.

![docker_stop](/Homework_3/Source/docker_stop.png)

* для удаления контейнеров воспользуемся командой docker rm, передав в качестве аргумента имя или ID контейнера.

``` docker rm 8e387eef24a9 ```

![delete](/Homework_3/Source/delete.png)


* В качестве аргументов команде docker rm, можно передать список элементов, например чтобы удалить все существующие контейнеры, можно воспользоваться следующей командой:

``` docker rm $(docker ps -aq) ```

![delete_all](/Homework_3/Source/delete_all_container.png)

* для получения образа из репозитория docker, нужно выполнить команду docker pull, передав в качестве аргумента имя образа, например:

``` docker pull linuxserver/libreoffice ```

![start_libre](/Homework_3/Source/libreoffice_start.png)

![done](/Homework_3/Source/libreoffce_done.png)

#### Для просмотра загруженных образов можно использовать команду docker images.

* для удаления образа можно использовать команду docker rmi, передав в качестве аргумента имя или ID образа

![delete_images](/Homework_3/Source/delete_images.png)

* docker rmi может принимать в качестве аргументов список ID, и для удаления всех образов можно воспользоваться следующей командой:

``` docker rmi $(docker images -q) ```

![delete_all_images](/Homework_3/Source/delete_all_images.png)

#### Для более подробного изучения возможностей Docker - необходимо, как впрочем и обычно, воспользоваться параметром --help вместе с интересующей командой. Например:

``` docker --help ```

![docker_help](/Homework_3/Source/docker_help.png)

## Хранение данных в контейнерах docker.

#### При создании контейнера, ему выделяется своя собственная файловая система, которая будет хранить информацию во время существования контейнера, а при его удалении будет стёрта. Для того чтобы избежать потери данных предусмотрен механизм монтирования данных внутрь файловой системы контейнера.

* для демонстрации примера запустим контейнер из образа Ubuntu и войдем в него, и посмотрим содержимое корневой директории:

``` docker run -it -h GB --name gb-test ubuntu:22.10 ```

``` ls -l / ```

![test_ubuntu_conteiner](/Homework_3/Source/test_container_ubuntu.png)

* Создадим новую директорию в корне:

``` mkdir /example ```

* Создадим файл "passwords.txt" и добавим в него какие-либо данные:

``` touch /example/passwords.txt ```

``` echo "123test" >> /example/passwords.txt ```



#### Таким образом мы создали директорию и файл внутри контейнера Ubuntu.

![dir_example_in_root_dir](/Homework_3/Source/dir_example_in_root_dir.png)

![file](/Homework_3/Source/file_passwords.txt_in_dir_example.png)

* можем посмотреть содержимое файла:

![file_passwards.txt](/Homework_3/Source/file_passwords.txt.png)



