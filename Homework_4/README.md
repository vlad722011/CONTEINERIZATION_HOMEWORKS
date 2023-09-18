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









