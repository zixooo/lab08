## Выполнение работы
установка на Linux
```sh
sudo snap install docker
```

основные команды и флаги
```sh
  -t - задать устройство, на котором запускается контейнер
  -i - запуск в интерактивном режиме
  build - сборка
  run - запуск контейнера
  -p - задать порт
  diff - показать разницу
  images - вывод всех образов
  image - вывод конкретного образа
  rm - удалить контейнер
  rmi - удалить образ
  logs - вывод логов контейнера
  inspect - вывод подробной информации по контейнеру
```
основные инструкции в Docker-файлах
```sh
  FROM - задает базовый класс
  LABEL - задает описание различных метаданных
  WORKDIR - задает рабочую директорию
  COPY - копирует файли и папки в контейнер
  RUN - выполняет команду однажды при сборке
  CMD - выполнение команды при каждом запуске, в нашем случае это 
```

### Пример Docker-файла

```sh
vim Dockerfile
```
```dockerfile
FROM ubuntu:18.04
RUN apt update
RUN apt install -yy gcc g++ cmake
COPY . print/
WORKDIR print
RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
RUN cmake --build _build
#RUN cmake --build _build --target install
ENV LOG_PATH /home/logs/log.txt
VOLUME /home/logs
WORKDIR _install/bin
ENTRYPOINT ./demo
```
```
docker build -t logger .
```

