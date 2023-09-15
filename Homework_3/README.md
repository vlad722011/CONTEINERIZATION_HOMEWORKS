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


## Tестируем Docker.

* Запускаем контейнер с использованием образа "cowsay".

``` docker run docker/whalesay cowsay Hello, Docker! ```

![Docker_cowsay](/Homework_3/Source/docker_cowsay.png)



