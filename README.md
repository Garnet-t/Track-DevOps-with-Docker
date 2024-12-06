# Track-DevOps-with-Docker
Ознакомительная практика за 1 семестр
Инструкция по запуску на своем компьютере:
1.Скачать Docker Desktop  и VS code.
2.Открыть Docker Desktop в режиме администратора.Ни в коем случае его не закрывать,потому что Docker Desktop устанавливает и управляет Docker Engine,
который является основным компонентом, отвечающим за создание и управление контейнерами. 
Обращаю внимание нужно в нем найти рабочую папку.Именно с ней работает Docker.Нажать на шестеренку в правой верхнем углу.
Слева нажать Resources Advanced.
 Будет Disk image location и папка снизу и будет рабочей.
 C:\Users\79152\AppData\Local\Docker\wsl   у меня стоит wsl потому что Windows вмонтировала в Linux.Вам так делать не надо.
 У Вас может просто стоять без wsl.
3.Открыть VS Code сна панели слева нажать на проводник.
4.Создаем Python-приложение.Для этого в редакторе VS Code слева  нажимаем на DOCKER.Создаем папку python-app .В ней кликать создать файл.
  Файл назвать main.py
5.Загружаем содержимое из моего репозитория папка python-app программу main.py
6.В этой же папке снова нажимаем создать файл.Название Dockerfile 
7.Загружаем содержимое из моего репозитория  папка python-app Dockerfile
8.Открываем терминал в VS code .
9.Прописать относительный путь к папке в которой находится main.py и Dockerfile то есть до папки python-app.
В моем случае это выглядит вот так:
cd C:\Users\79152\AppData\Local\Docker\python-app
10.Теперь создаем образ с названием my-calendar (так то можно дать другое название но это по смыслу подходит больше)
   Для этого в терминале вбить такую команду: docker build . -t my-calendar
11.Такой вывод дал терминал.
[+] Building 4.4s (8/8) FINISHED                                                                                                                  docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                              0.0s
 => => transferring dockerfile: 115B                                                                                                                              0.0s
 => [internal] load metadata for docker.io/library/python:alpine                                                                                                  4.2s
 => [internal] load .dockerignore                                                                                                                                 0.0s
 => => transferring context: 2B                                                                                                                                   0.0s
 => [1/3] FROM docker.io/library/python:alpine@sha256:804ad02b9ba67ea1f8307eeb6407b121c6bd6bb19d3f182aae166821eb59d6a4                                            0.0s 
 => [internal] load build context                                                                                                                                 0.0s
 => => transferring context: 376B                                                                                                                                 0.0s 
 => CACHED [2/3] WORKDIR /app                                                                                                                                     0.0s 
 => [3/3] COPY . .                                                                                                                                                0.0s 
 => exporting to image                                                                                                                                            0.1s 
 => => exporting layers                                                                                                                                           0.0s 
 => => writing image sha256:315dd09fc1568bf6667438b2de1b6db5e7c4eb5e2a9a9775ddc00f2599120806                                                                      0.0s 
 => => naming to docker.io/library/my-calendar                                                                                                                    0.0s 

View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/wxlr5zgjgl518yx3w7hd22w7d

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview


12.Обращаю внимание что в строках 31,34,35 выполнены инструкции Dockerfile .
13.Вбиваем в терминал docker images
Один из выводов будет такой(там  вообще список будет  выведен если ранее пользовались Docker) 
PS C:\Users\79152\AppData\Local\Docker\python-app>  docker images
REPOSITORY                                                                   TAG       IMAGE ID       CREATED         SIZE
my-calendar                                                                  latest    315dd09fc156   4 minutes ago   50.4MB
14.Создаем контейнер для работы с python приложением(с main.py)
вбить команду:
docker run -it my-calendar 
Программа main.py(это приложение запустится) .Выберите любой год и месяц.Наберите их.
На своем примере я вбила 2056 6 
Вывод булет нормальный в виде календаря.
15.main.py завершил свою работу и Docker Desktop его автоматически завершил.Самим docker stop прописывать не надо.
16.Вбить docker ps 
Показывает список работающих контейнеров на данный момент.Список пуст, потому что python приложение отработало и Docker его завершил
PS C:\Users\79152\AppData\Local\Docker\python-app> docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
16.Вбиваем команду docker ps -a 
Она показывает завершенные контейнеры."NAMES" это имя контейнера которое присваем Docker автоматически,и скорее всего у вас
имя другое.так же как и Container ID ,Image ID создается все Dosker Desktop.
PS C:\Users\79152\AppData\Local\Docker\python-app> docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS                      PORTS                  NAMES
739b7ed4d226   my-calendar    "python main.py"         4 minutes ago   Exited (0) 9 seconds ago                           relaxed_elgamal
17.Заходим в Docker Desktop.Там где написано settings идем по строчке вправо и кликаем на крестик.Вообще по хорошему надо закрыть Docker Desktop и снова открыть в режиме администратора
18.Открывайте Imagines,увидите свой образ.
19.Аналгично Containers.Увидите контейнеры.


