FROM alpine:3.18

# Установка необходимых пакетов
RUN apk update && apk add --no-cache \
    gcc \
    g++ \
    make \
    cmake \
    musl-dev

# Создание рабочей директории
WORKDIR /build-docker

# Копирование исходных файлов
COPY src .

# Команда по умолчанию для сборки проекта
CMD ["sh", "-c", "mkdir -p build-docker && cd build-docker && cmake -DCMAKE_C_COMPILER=gcc -DCMAKE_CXX_COMPILER=g++ .. && make"]