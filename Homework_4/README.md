# Курс - "Контейнеризация"
## Домашнее задание к семинару 4.
## Выполнил Бурсаев Владислав, группа 3775.

### Запуск Java приложения в Docker.
* открываем терминал, сочетанием клавиш Ctrl+Alt+T

``` Ctrl+Alt+T ```

![open terminal](/Homework_4/Sourse/terminal.png)

* Переходим в требуемую директорию:

```  cd /home/vlad/Контейнеризация/ ```

![dir](/Homework_4/Sourse/dir.png)

* В данной директории создаю директорию, в которой будут ханиться все необходимые данные для запуска Java приложений в контейнере.

``` mkdir java-application ```

* Переходим в созданную директорию:

``` cd java-application ```

![java-application_dir](/Homework_4/Sourse/java-application_dir.png)

* Создаем в данной директории файл с Java приложением:

``` nano HelloWorld.java ```

![add_file](/Homework_4/Sourse/file_java_add.png)

``` 
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Vlad. You launched your first JAVA application! It is very good!!!");
    }
}  


```

![file_java](/Homework_4/Sourse/java-aaplication_file.png)


* Сохраняем измениния файла.

* Далее, собственно создаем подобным образом Docerfile на основе которого будет создаваться образ будущего контейнера для запуска нашего приложения.

``` nano Dockerfile ```

![add_dockerfile](/Homework_4/Sourse/add_dokerfile.png)

``` 
FROM ubuntu:latest

# JAVA 
RUN apt-get update && \
    apt-get install -y default-jdk && \
    rm -rf /var/lib/apt/lists/*
ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
ENV PATH="$JAVA_HOME/bin:${PATH}"
ADD HelloWorld.java .
RUN javac HelloWorld.java
CMD ["java", "HelloWorld"] 

```

![dockerfile](/Homework_4/Sourse/dockerfile.png)

* Сохраняем измениния файла.

* На основе созданного Dockerfile сщздаем образ контейнера:

``` sudo docker build -t java-application . ```

![build_conteiner](/Homework_4/Sourse/conteiner.png)

* Можем проверить, что контейнер корректно создался. Зайдем в него:

``` sudo docker run -it java-app bash ```
 ![in_to](/Homework_4/Sourse/into_conteiner.png)

 * Можем убедиться, что мы действительно находимся внутри контейнера:

 ``` ps -aux ```

![ps-aux](/Homework_4/Sourse/ps-aux.png)

* Теперь, собственно выйдем из контейнера, и попробуем запустить наше Java прилдожение в нем:

``` exit ```

``` sudo docker run java-application ```

![work](/Homework_4/Sourse/Java_application_work.png)

### На последнем скриншоте видим приветсвие приложения. Приложение успешно запустилось, и отработало.











